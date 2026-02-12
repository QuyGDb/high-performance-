# Chương 3: CPU Execution, ISA & Programming Languages

> **Mục tiêu chương:** Hiểu cách CPU thực thi mã máy từng bước, tại sao Pipeline và Branch Prediction ảnh hưởng trực tiếp đến game performance, và con đường đầy đủ từ C# source code → mã máy native trong Unity.

## 2. Stack & Function Calls — Cái giá của mỗi lần gọi hàm

### 2.1. Call Stack — Cách CPU quản lý hàm

```
C# code:
  void GameLoop() {
      float dmg = CalculateDamage(10, 5);
      ApplyDamage(enemy, dmg);
  }
  float CalculateDamage(int baseDmg, int level) {
      return baseDmg * (1 + level * 0.1f);
  }


Assembly flow (đơn giản hóa):

  GameLoop:
      PUSH  RBP                    ; Lưu Base Pointer cũ lên Stack
      MOV   RBP, RSP               ; Set Base Pointer mới = đỉnh Stack
      SUB   RSP, 16                ; Dành chỗ cho local variables

      MOV   ECX, 10                ; Arg 1: baseDmg = 10
      MOV   EDX, 5                 ; Arg 2: level = 5
      CALL  CalculateDamage        ; ← Push Return Address + Jump

      ; ... khi CalculateDamage return, kết quả nằm trong XMM0 ...
      
      MOV   RSP, RBP               ; Khôi phục Stack
      POP   RBP                    ; Khôi phục Base Pointer
      RET                          ; Pop Return Address + Jump back


Stack Memory khi đang trong CalculateDamage():

  Địa chỉ cao  ┌──────────────────────────┐
               │  ... (GameLoop caller)    │
               ├──────────────────────────┤
               │  Return Address (RIP cũ) │ ← CPU tự push khi CALL
               ├──────────────────────────┤
       RBP ──► │  Old RBP (GameLoop)      │ ← Nơi quay lại
               ├──────────────────────────┤
               │  local var: baseDmg = 10 │
               ├──────────────────────────┤
       RSP ──► │  local var: level = 5    │ ← Đỉnh Stack hiện tại
               ├──────────────────────────┤
               │  (Space trống — grow ↓)  │
  Địa chỉ thấp └──────────────────────────┘

  Khi RET:
  1. Pop return address
  2. Jump về GameLoop
  3. Khôi phục RBP/RSP
  → Stack Frame bị "hủy" (chỉ di chuyển pointer, KHÔNG xóa data)
```

### 2.2. Inlining — Loại bỏ chi phí gọi hàm

```
Chi phí mỗi CALL:
  1. PUSH return address        (~1 cycle)
  2. Push/Pop registers to save (~2-4 cycles)
  3. Pipeline flush (partial)   (~5-10 cycles)
  4. Return bookkeeping         (~1-2 cycles)
  ───────────────────────────────────────────
  Tổng: ~10-15 cycles overhead MỖI LẦN gọi hàm

Với 10,000 entities × 5 hàm/entity = 50,000 calls
→ 50,000 × 12 = 600,000 cycles wasted = ~0.12ms ở 5GHz


═══ Giải pháp: Inlining ═══

Compiler thay thế CALL bằng cách COPY code của hàm vào caller:

  Trước Inline:                    Sau Inline:
  ──────────────                   ────────────
  void Update() {                  void Update() {
      float d = CalcDmg(10, 5);       // CalcDmg "paste" trực tiếp:
      Apply(enemy, d);                 float d = 10 * (1 + 5 * 0.1f);
  }                                    Apply(enemy, d);
                                   }
  float CalcDmg(int b, int l) {
      return b * (1 + l * 0.1f);   → Không có CALL/RET overhead
  }                                → Burst/IL2CPP có thể tối ưu thêm
                                     (constant folding: d = 15.0f)


Unity & Inlining:
  ┌──────────────────────────────────────────────────────────────┐
  │  Mono JIT:   Inline rất hạn chế (hàm <32 bytes IL)          │
  │  IL2CPP:     Inline tốt hơn (C++ compiler quyết định)       │
  │  Burst:      Inline CỰC KỲ aggressive                       │
  │              + Tự vectorize sau khi inline                   │
  │              → Đây là lý do Burst nhanh hơn Mono 5-20×      │
  │                                                              │
  │  Tip: Đánh dấu [MethodImpl(MethodImplOptions.AggressiveInlining)] │
  │  để gợi ý compiler inline (không bắt buộc, compiler quyết)  │
  └──────────────────────────────────────────────────────────────┘
```

---

## 3. Từ C# đến Mã máy — Ba con đường trong Unity

### 3.1. Con đường Mono (JIT — Just-In-Time)

```
┌─────────────────────────────────────────────────────────────────┐
│  CON ĐƯỜNG MONO — Dùng trong Unity Editor & Development        │
│                                                                 │
│  1. Viết code C# (.cs files)                                    │
│     │                                                           │
│     ▼                                                           │
│  2. Roslyn Compiler biên dịch → IL bytecode (.dll files)        │
│     │    (Xảy ra khi bạn nhấn Ctrl+S hoặc Domain Reload)       │
│     │                                                           │
│     │    IL bytecode — Ví dụ:                                   │
│     │    .method void Update() {                                │
│     │        ldarg.0                  ; load "this"             │
│     │        ldfld float3 position    ; load position           │
│     │        ldarg.0                                            │
│     │        ldfld float3 velocity    ; load velocity           │
│     │        ldsfld float deltaTime   ; load Time.deltaTime     │
│     │        mul                      ; velocity * dt           │
│     │        add                      ; position + result       │
│     │        stfld float3 position    ; store back              │
│     │    }                                                      │
│     │                                                           │
│     ▼                                                           │
│  3. Mono Runtime JIT compile:                                    │
│     - Lần đầu gọi Update() → compile IL → x86-64 native        │
│     - Kết quả cache trong memory (không compile lại)             │
│     - Lần gọi sau: chạy native code trực tiếp                   │
│     │                                                           │
│     │  ⚠ Vấn đề JIT:                                           │
│     │  - Lần gọi đầu tiên CHẬM (JIT stutter / hiccup)          │
│     │  - JIT compiler phải NHANH → không đủ thời gian optimize  │
│     │  - Kết quả: native code CHƯA tối ưu bằng AOT             │
│     │                                                           │
│     ▼                                                           │
│  4. Native Code chạy trên CPU                                   │
│                                                                 │
│  ✅ Ưu điểm: Iterate nhanh (Save → Play ngay)                   │
│  ❌ Nhược điểm: Runtime performance kém hơn IL2CPP/Burst        │
└─────────────────────────────────────────────────────────────────┘
```

### 3.2. Con đường IL2CPP (AOT — Ahead-of-Time)

```
┌─────────────────────────────────────────────────────────────────┐
│  CON ĐƯỜNG IL2CPP — Dùng cho Production Builds                  │
│                                                                 │
│  1. C# → IL (giống Mono)                                        │
│     │                                                           │
│     ▼                                                           │
│  2. IL2CPP Transpiler:                                           │
│     Chuyển IL bytecode → C++ source code                         │
│     │                                                           │
│     │  Ví dụ output C++:                                        │
│     │  void Update_m1234(MyScript_t* __this) {                  │
│     │      float3 vel = __this->velocity;                       │
│     │      float dt = Time_get_deltaTime();                     │
│     │      float3 delta;                                        │
│     │      delta.x = vel.x * dt;                                │
│     │      delta.y = vel.y * dt;                                │
│     │      delta.z = vel.z * dt;                                │
│     │      __this->position.x += delta.x;                       │
│     │      __this->position.y += delta.y;                       │
│     │      __this->position.z += delta.z;                       │
│     │  }                                                        │
│     │                                                           │
│     ▼                                                           │
│  3. Platform C++ Compiler:                                       │
│     ┌─────────────────────────────────────────────────────┐     │
│     │  Windows: MSVC (cl.exe)     → x86-64 .exe          │     │
│     │  macOS:   Clang (Apple)     → ARM64 .app            │     │
│     │  Android: NDK Clang         → ARM64 .so             │     │
│     │  iOS:     Clang (Xcode)     → ARM64 .ipa            │     │
│     │  WebGL:   Emscripten        → WASM .wasm            │     │
│     └─────────────────────────────────────────────────────┘     │
│     │                                                           │
│     │  C++ compiler có HÀNG GIỜ để optimize:                    │
│     │  - Loop unrolling                                         │
│     │  - Dead code elimination                                  │
│     │  - Constant propagation                                   │
│     │  - Auto-vectorization (một phần)                          │
│     │  - Link-Time Optimization (LTO)                           │
│     │                                                           │
│     ▼                                                           │
│  4. Highly optimized native binary                               │
│                                                                 │
│  ✅ Performance gần C++ thuần                                    │
│  ✅ Code stripping giảm build size                               │
│  ❌ Build time lâu (phải compile C++)                            │
│  ❌ Debug khó hơn (native stack traces)                          │
│  📱 BẮT BUỘC cho iOS (Apple cấm JIT)                            │
└─────────────────────────────────────────────────────────────────┘
```

### 3.3. Con đường Burst (AOT + SIMD — Cao cấp nhất)

```
┌─────────────────────────────────────────────────────────────────┐
│  CON ĐƯỜNG BURST — Dành cho DOTS (ECS + Job System)             │
│                                                                 │
│  1. C# HPC# (High-Performance C#)                               │
│     │  Subset giới hạn của C#:                                  │
│     │  ✅ struct, NativeArray, math.*, fixed arrays              │
│     │  ❌ class, string, List<T>, LINQ, virtual, delegates       │
│     │  ❌ try/catch, reflection, GC allocations                  │
│     │                                                           │
│     ▼                                                           │
│  2. IL (giống Mono/IL2CPP)                                       │
│     │                                                           │
│     ▼                                                           │
│  3. Burst Compiler (LLVM Backend):                               │
│     │                                                           │
│     │  Burst = Custom LLVM frontend cho C#                      │
│     │  Sử dụng CÙNG backend optimizer như Clang/C++ compiler!   │
│     │                                                           │
│     │  Tối ưu hóa đặc biệt của Burst:                          │
│     │  ┌────────────────────────────────────────────────────┐   │
│     │  │ ✅ Auto-Vectorization (SIMD)                       │   │
│     │  │    → Tự chuyển scalar loop → SIMD instructions    │   │
│     │  │                                                    │   │
│     │  │ ✅ Loop Vectorization                              │   │
│     │  │    → for (i=0..N) → xử lý 4/8/16 phần tử/loop    │   │
│     │  │                                                    │   │
│     │  │ ✅ Bounds Check Elimination                        │   │
│     │  │    → Xóa [i] bounds check khi Burst chứng minh    │   │
│     │  │      index luôn hợp lệ                             │   │
│     │  │                                                    │   │
│     │  │ ✅ Alias Analysis                                  │   │
│     │  │    → Chứng minh 2 NativeArrays KHÔNG overlap      │   │
│     │  │    → Cho phép tối ưu mạnh hơn                     │   │
│     │  │                                                    │   │
│     │  │ ✅ Constant Folding                                │   │
│     │  │    → math.sin(0) → 0 tại compile time              │   │
│     │  │                                                    │   │
│     │  │ ✅ Aggressive Inlining                             │   │
│     │  │    → Inline GẦN NHƯ TẤT CẢ hàm nhỏ               │   │
│     │  └────────────────────────────────────────────────────┘   │
│     │                                                           │
│     ▼                                                           │
│  4. Platform-specific native code:                               │
│     - x86-64: SSE4.2 / AVX2 / AVX-512                           │
│     - ARM64:  NEON / SVE                                         │
│     - WASM:   SIMD128 (WebGL/WebGPU)                             │
│                                                                 │
│  ✅ Hiệu năng NGANG hoặc HƠN C++ hand-optimized                │
│  ✅ An toàn hơn C++ (safety checks ở Editor, remove ở Build)    │
│  ✅ Compile nhanh (vài giây cho Jobs)                            │
│  ❌ Chỉ dùng được HPC# subset                                   │
│  ❌ Không dùng được MonoBehaviour, strings, classes               │
└─────────────────────────────────────────────────────────────────┘
```

### 3.4. So sánh ba con đường — Benchmark thực tế

```
Bài test: Di chuyển 100,000 entities (position += velocity * dt)

┌───────────────┬──────────────┬────────┬──────────────────────────┐
│  Pipeline     │  Thời gian   │ So vs  │  Lý do                   │
│               │  (ms/frame)  │ Mono   │                          │
├───────────────┼──────────────┼────────┼──────────────────────────┤
│ Mono (JIT)    │  ~8.5 ms     │  1×    │ Scalar, bounds checks,   │
│               │              │        │ GC overhead, no SIMD     │
├───────────────┼──────────────┼────────┼──────────────────────────┤
│ IL2CPP (AOT)  │  ~3.2 ms     │  2.7×  │ C++ optimizer, inline,   │
│               │              │        │ minor auto-vectorize     │
├───────────────┼──────────────┼────────┼──────────────────────────┤
│ Burst (AOT    │  ~0.4 ms     │  21×   │ Full SIMD (AVX2),        │
│  + SIMD)      │              │        │ no bounds checks,        │
│               │              │        │ perfect cache (ECS),     │
│               │              │        │ ScheduleParallel (8 cores│
│               │              │        │ × 8-wide SIMD = 64×)     │
├───────────────┼──────────────┼────────┼──────────────────────────┤
│ Burst +       │  ~0.05 ms    │  170×  │ Burst + Job System       │
│ Parallel Jobs │              │        │ trên 8 cores             │
└───────────────┴──────────────┴────────┴──────────────────────────┘

Tại sao chênh lệch LỚN đến vậy?

  Mono:   scalar math (1 entity/lệnh) + bounds check + GC scan
  Burst:  SIMD math (8 entities/lệnh) + no checks + no GC
  + Jobs: chia 100K entities cho 8 cores
          = 100K ÷ 8 cores ÷ 8 SIMD = ~1,562 iterations/core
          thay vì 100,000 iterations trên 1 core
```

---

## 4. Garbage Collection — "Stop the World"

### 4.1. GC hoạt động như thế nào?

```
┌───────────────────────────────────────────────────────────────────┐
│              GARBAGE COLLECTOR (Boehm GC trong Unity)             │
│                                                                   │
│  Managed Heap:                                                    │
│  ┌─────┬─────┬█████┬─────┬█████┬─────┬─────┬█████┬─────┐        │
│  │ Obj │ Obj │DEAD │ Obj │DEAD │ Obj │ Obj │DEAD │ Obj │        │
│  │  A  │  B  │  C  │  D  │  E  │  F  │  G  │  H  │  I  │        │
│  └─────┴─────┴█████┴─────┴█████┴─────┴─────┴█████┴─────┘        │
│                                                                   │
│  GC Cycle:                                                        │
│  1. STOP THE WORLD — Tất cả C# code DỪNG LẠI                     │
│     (Game freeze! Player thấy "giật")                             │
│                                                                   │
│  2. MARK Phase:                                                   │
│     Bắt đầu từ "GC Roots" (static fields, stack variables)       │
│     Đi theo tất cả references → đánh dấu objects "sống"          │
│     Objects không được đánh dấu = "chết" (garbage)                │
│                                                                   │
│  3. SWEEP Phase:                                                  │
│     Giải phóng bộ nhớ của objects "chết"                           │
│     (Boehm GC KHÔNG di chuyển objects — không compact)            │
│                                                                   │
│  4. RESUME — Code tiếp tục chạy                                   │
│                                                                   │
│  Thời gian GC: 1-20ms tùy heap size                               │
│  Ở 60 FPS: 1 frame = 16.67ms                                      │
│  → GC 5ms = mất 30% thời gian frame → GIẬT!                      │
└───────────────────────────────────────────────────────────────────┘


Các "tội đồ" tạo GC trong Unity:

  ┌──────────────────────────────┬──────────────────────────────────┐
  │  Code thường gặp             │  Tạo GC bao nhiêu?              │
  ├──────────────────────────────┼──────────────────────────────────┤
  │  string name = "HP: " + hp;  │  ~100 bytes / frame (nối string)│
  │  new List<int>()             │  ~80 bytes (list object + array) │
  │  GetComponent<T>()           │  ~40 bytes (boxing/wrapper)      │
  │  LINQ (.Where, .Select)      │  ~200+ bytes (iterator objects)  │
  │  foreach (List<T>)           │  ~40 bytes (enumerator object)   │
  │  Closure / Lambda            │  ~60 bytes (delegate + captured) │
  │  params object[]             │  ~variable (boxing + array)      │
  │  ToString()                  │  ~40+ bytes (new string)         │
  ├──────────────────────────────┼──────────────────────────────────┤
  │  10 scripts × 5 allocs/frame │  ~2-5 KB / frame                │
  │  × 60 frames/second          │  ~120-300 KB / second            │
  │  → GC trigger mỗi ~10-30 giây│  → Giật định kỳ!                │
  └──────────────────────────────┴──────────────────────────────────┘


Giải pháp Zero-GC:

  ┌──────────────────────────────────────────────────────────────┐
  │  ❌ TRÁNH                     │  ✅ THAY BẰNG                 │
  ├──────────────────────────────┼───────────────────────────────┤
  │  string concat               │  StringBuilder (reuse)        │
  │  new List<T>() mỗi frame    │  Pool hoặc NativeList          │
  │  GetComponent<T>()           │  Cache reference ở Awake()    │
  │  LINQ                        │  for loop thủ công            │
  │  foreach trên List           │  for (int i=0; ...) loop      │
  │  Lambda / Closure            │  static method + struct data  │
  │  class (reference type)       │  struct (value type)          │
  │  Managed arrays              │  NativeArray<T>               │
  └──────────────────────────────┴───────────────────────────────┘
```

---

## 5. Tổng kết Chapter 3 — Con đường của một dòng code

```
Bạn viết:  position += velocity * deltaTime;

  ┌───────────────────────────────────────────────────────────────┐
  │                                                               │
  │  ① C# Source → Roslyn Compiler → IL Bytecode (.dll)          │
  │                                                               │
  │  ② IL → [Mono JIT | IL2CPP → C++ → Native | Burst → LLVM]   │
  │                                                               │
  │  ③ Native Code được CPU Fetch vào Pipeline (L1i Cache)        │
  │                                                               │
  │  ④ Decoder chuyển x86/ARM → μops                              │
  │                                                               │
  │  ⑤ Out-of-Order Engine dispatch μops tới ALU/FPU              │
  │     - Burst: SIMD registers (4-8 entities cùng lúc)           │
  │     - Jobs: ScheduleParallel → 8 cores × 8 SIMD = 64×        │
  │                                                               │
  │  ⑥ ALU/FPU thực thi phép tính                                 │
  │     (Transistors đóng/mở theo Chapter 1)                      │
  │                                                               │
  │  ⑦ Kết quả ghi vào Register → Cache → RAM                    │
  │     (Memory Hierarchy theo Chapter 2)                         │
  │                                                               │
  │  ⑧ Nếu có Branch (if/else):                                  │
  │     - Branch Predictor đoán nhánh                             │
  │     - Đoán đúng = 0 penalty                                  │
  │     - Đoán sai = 15-20 cycles flush pipeline                  │
  │                                                               │
  │  Toàn bộ: < 1 nanosecond cho 1 iteration                     │
  │  × 100,000 entities × 60 FPS = ~6 tỷ phép tính/giây          │
  └───────────────────────────────────────────────────────────────┘
```

> **Bài học thực tiễn:**
> 1. **Chọn đúng pipeline:** Mono cho Editor iteration, IL2CPP cho build, **Burst cho hot paths**.
> 2. **Tránh Branch** trong tight loops: dùng `math.select()`, `step()`, `lerp()`.
> 3. **Inline hàm nhỏ:** Burst làm tự động, nhưng Mono/IL2CPP cần hint.
> 4. **Zero-GC:** Mọi allocation trong Update() là "nợ" mà GC sẽ đòi lại (bằng frame drop).
> 5. **Profile trước khi tối ưu:** Unity Profiler + Burst Inspector cho biết CPU đang tốn thời gian ở đâu.

---

> **Chương tiếp theo:** [Chapter 4 — GPU Architecture & Rendering Pipeline]() — Cách GPU xử lý hàng triệu pixel song song, và tại sao shader code cần viết khác hoàn toàn CPU code.

---
*Chapter 3 — Nghiên cứu cho Unity High-Performance Agent*
