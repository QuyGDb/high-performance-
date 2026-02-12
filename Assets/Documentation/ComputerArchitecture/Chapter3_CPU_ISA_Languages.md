# Chương 3: CPU Execution, ISA & Programming Languages

> **Mục tiêu chương:** Hiểu cách CPU thực thi mã máy từng bước, tại sao Pipeline và Branch Prediction ảnh hưởng trực tiếp đến game performance, và con đường đầy đủ từ C# source code → mã máy native trong Unity.

---

## 1. Instruction Set Architecture (ISA) — Ngôn ngữ mẹ đẻ của CPU

### 1.1. ISA là gì?

ISA là **bản hợp đồng** giữa phần cứng (CPU) và phần mềm (Compiler/OS). Nó định nghĩa:
- Tập lệnh CPU hiểu được (ADD, MOV, JUMP, ...)
- Thanh ghi nào có sẵn (RAX, RSP, XMM0, ...)
- Cách đánh địa chỉ bộ nhớ (Addressing Modes)
- Kích thước dữ liệu (8/16/32/64-bit)

```
Tầng abstraction:

  ┌─────────────────────────────────────────────────┐
  │  C#:  health -= damage;                          │   ← Ngôn ngữ bậc cao
  ├─────────────────────────────────────────────────┤
  │  IL:  ldarg.0                                    │   ← Bytecode trung gian
  │       ldfld float Health::Value                  │
  │       ldarg.1                                    │
  │       sub                                        │
  │       stfld float Health::Value                  │
  ├─────────────────────────────────────────────────┤
  │  x86 ASM:                                        │   ← Assembly (1:1 với ISA)
  │       movss  xmm0, [rcx+0x10]   ; load health   │
  │       subss  xmm0, xmm1         ; health -= dmg │
  │       movss  [rcx+0x10], xmm0   ; store back    │
  ├─────────────────────────────────────────────────┤
  │  Machine Code:                                   │   ← Nhị phân thuần
  │       F3 0F 10 41 10                             │
  │       F3 0F 5C C1                                │
  │       F3 0F 11 41 10                             │
  └─────────────────────────────────────────────────┘
       ↑
  Mỗi byte → bộ giải mã → tín hiệu điều khiển ALU/FPU/Load-Store Unit.
```

#### > Anatomy of an Instruction (Giải phẫu lệnh):
Lệnh `ADD EAX, EBX` (01 03) trong x86:

```
  0000 0001   0000 0011
  └──┬────┘   └──┬────┘
    Opcode      ModR/M
    (ADD)      (EAX, EBX)

  CPU Decoder đọc 2 bytes này → Biết rằng:
  1. Cần dùng mạch ADDER (Chapter 1).
  2. Input 1 là Register EAX (Chapter 2).
  3. Input 2 là Register EBX (Chapter 2).
  4. Kết quả ghi lại vào EAX.
```

### 1.2. CISC vs RISC — Hai triết lý thiết kế ISA

```
┌─────────────────────────────────────────────────────────────────────┐
│                    CISC vs RISC                                     │
├─────────────────────────┬───────────────────────────────────────────┤
│        CISC             │            RISC                           │
│  (Complex Instruction   │    (Reduced Instruction                   │
│   Set Computer)         │     Set Computer)                         │
├─────────────────────────┼───────────────────────────────────────────┤
│ Đại diện: x86-64        │ Đại diện: ARM, RISC-V                    │
│ Intel, AMD              │ Apple Silicon, Qualcomm                   │
├─────────────────────────┼───────────────────────────────────────────┤
│ Lệnh PHỨC TẠP:          │ Lệnh ĐƠN GIẢN:                          │
│ 1 lệnh có thể làm      │ 1 lệnh chỉ làm 1 việc                   │
│ nhiều việc cùng lúc     │                                           │
│                         │                                           │
│ Ví dụ:                  │ Ví dụ:                                    │
│ ADD [mem], reg           │ LDR  R1, [mem]    ; Load                │
│ (Đọc RAM + Cộng +       │ ADD  R1, R1, R2   ; Cộng                │
│  Ghi lại RAM trong      │ STR  R1, [mem]    ; Ghi                 │
│  1 lệnh duy nhất)       │ (3 lệnh riêng biệt)                     │
├─────────────────────────┼───────────────────────────────────────────┤
│ Kích thước lệnh:        │ Kích thước lệnh:                         │
│ 1 → 15 bytes (biến đổi)│ 4 bytes CỐ ĐỊNH (ARM)                   │
│ → Bộ giải mã phức tạp  │ → Bộ giải mã đơn giản, nhanh             │
├─────────────────────────┼───────────────────────────────────────────┤
│ Ưu điểm:                │ Ưu điểm:                                  │
│ ✅ Code compact (ít byte)│ ✅ Pipeline hiệu quả hơn                 │
│ ✅ Tương thích ngược     │ ✅ Tiết kiệm năng lượng                  │
│    (chạy code từ 1978)  │ ✅ Dễ tối ưu cho compiler                 │
├─────────────────────────┼───────────────────────────────────────────┤
│ Nền tảng:                │ Nền tảng:                                 │
│ PC, PlayStation, Xbox    │ Mobile, Switch, Mac (M-series)           │
│ Server                   │ VR Headset (Quest)                       │
├─────────────────────────┼───────────────────────────────────────────┤
│ Unity build target:      │ Unity build target:                       │
│ Windows x64, Linux x64  │ Android ARM64, iOS ARM64                 │
│ macOS x64 (Intel Mac)   │ macOS ARM64 (Apple Silicon)              │
└─────────────────────────┴───────────────────────────────────────────┘
```

> **Thực tế hiện đại:** CPU x86 của Intel/AMD bên ngoài là CISC, nhưng bên trong giải mã thành **micro-ops** (μops) giống RISC rồi mới thực thi. Ranh giới CISC/RISC ngày nay đã mờ đi rất nhiều.

### 1.3. Một số lệnh Assembly quan trọng cho Unity Developer

```
┌──────────────────────────────────────────────────────────────────────────┐
│                  x86-64 ASSEMBLY — LỆNH THƯỜNG GẶP                      │
├──────────┬─────────────────────┬─────────────────────────────────────────┤
│  Lệnh    │  Ý nghĩa            │  Gặp ở đâu trong Unity?                │
├──────────┼─────────────────────┼─────────────────────────────────────────┤
│ MOV      │ Copy dữ liệu        │ Mọi nơi (gán biến, load field)        │
│ ADD/SUB  │ Cộng/Trừ            │ position += velocity                   │
│ MUL/IMUL │ Nhân                │ scale * direction                      │
│ CMP      │ So sánh             │ if (health <= 0)                       │
│ JE/JNE   │ Nhảy nếu bằng/khác │ Branching (if/else/switch)             │
│ CALL     │ Gọi hàm            │ Mỗi method call                        │
│ RET      │ Return từ hàm      │ Kết thúc method                        │
│ PUSH/POP │ Stack operations    │ Lưu/khôi phục registers khi gọi hàm   │
├──────────┼─────────────────────┼─────────────────────────────────────────┤
│          │   SIMD (Burst)       │                                        │
├──────────┼─────────────────────┼─────────────────────────────────────────┤
│ MOVAPS   │ Load 128-bit aligned│ Load float4 vào XMM register           │
│ ADDPS    │ Add Packed Singles  │ float4 a + b (4 phép cộng cùng lúc)   │
│ MULPS    │ Mul Packed Singles  │ float4 a * b (4 phép nhân cùng lúc)   │
│ SHUFPS   │ Shuffle floats     │ Swizzle (a.xyzw → a.wzyx)             │
│ DPPS     │ Dot Product         │ math.dot(a, b)                         │
│ RSQRTPS  │ Fast 1/sqrt        │ math.rsqrt() cho normalize             │
│ VFMADD   │ Fused Multiply-Add │ a * b + c trong 1 lệnh (AVX2)         │
└──────────┴─────────────────────┴─────────────────────────────────────────┘


Ví dụ thực tế — Burst biên dịch float3 addition:

  C# (trong IJobParallelFor):
  ──────────────────────────
  position.Value += velocity.Value * deltaTime;


  Burst output (x86-64 + AVX):
  ──────────────────────────────
  vbroadcastss  ymm2, [deltaTime]         ; Nhân rộng deltaTime sang 8 slots
  vmulps        ymm1, ymm0, ymm2          ; velocity * deltaTime (8 floats)
  vaddps        ymm3, ymm1, [positions]   ; position + result    (8 floats)
  vmovaps       [positions], ymm3         ; Store kết quả


  → 3 lệnh SIMD thay cho 24 lệnh scalar!
  → Burst tự phát hiện pattern và vectorize.
  → Đây là lý do [BurstCompile] nhanh hơn Mono 5-10×.
```

---

## 2. CPU Pipeline — Dây chuyền lắp ráp lệnh

### 2.1. Pipeline cơ bản (5 giai đoạn)

Nếu mỗi lệnh phải hoàn thành tất cả bước trước khi bắt đầu lệnh tiếp, CPU sẽ cực kỳ lãng phí. **Pipeline** giải quyết điều này bằng cách overlap các giai đoạn:

```
═══ KHÔNG có Pipeline (Sequential) ═══

  Lệnh 1: [Fetch][Decode][Execute][Memory][WriteBack]
  Lệnh 2:                                             [Fetch][Decode][Execute][Memory][WriteBack]
  Lệnh 3:                                                                                        [Fetch]...

  → 5 cycles/lệnh. Để xử lý 3 lệnh cần 15 cycles.
  → 4/5 bộ phận CPU NGỒI KHÔNG trong mỗi cycle!


═══ CÓ Pipeline (Overlapped) ═══

  Cycle:       1      2      3      4      5      6      7
  Lệnh 1: [Fetch][Decode][Exec ][Mem  ][Write]
  Lệnh 2:        [Fetch][Decode][Exec ][Mem  ][Write]
  Lệnh 3:               [Fetch][Decode][Exec ][Mem  ][Write]

  → Sau khi pipeline đầy (cycle 5), mỗi cycle hoàn thành 1 lệnh!
  → 3 lệnh chỉ cần 7 cycles thay vì 15.
  → Throughput: ~1 lệnh/cycle (IPC ≈ 1)

#### > Visualizing the Pipeline (Assembly View):
Giả sử ta có 3 lệnh Assembly liên tiếp:
1. `MOV EAX, 10`
2. `ADD EAX, 5`
3. `MOV [Ptr], EAX`

```
Time (Cycles) ──►
      1      2      3      4      5      6      7
   ┌────┐ ┌────┐ ┌────┐ ┌────┐ ┌────┐
1. │ IF │ │ ID │ │ EX │ │ MEM│ │ WB │  (MOV EAX, 10)
   └────┘ └────┘ └────┘ └────┘ └────┘
          ┌────┐ ┌────┐ ┌────┐ ┌────┐ ┌────┐
2.        │ IF │ │ ID │ │ EX │ │ MEM│ │ WB │  (ADD EAX, 5)
          └────┘ └────┘ └────┘ └────┘ └────┘
                 ┌────┐ ┌────┐ ┌────┐ ┌────┐ ┌────┐
3.               │ IF │ │ ID │ │ EX │ │ MEM│ │ WB │  (MOV [Ptr], EAX)
                 └────┘ └────┘ └────┘ └────┘ └────┘
```
**Tại cycle 3:**
*   Lệnh 1 đang Thực thi (EX).
*   Lệnh 2 đang Giải mã (ID).
*   Lệnh 3 đang được Tải về (IF).
*   → **3 phần của CPU đang làm việc CÙNG LÚC!**


Ẩn dụ — Giặt đồ:
  ┌────────────────────────────────────────────────────────────────┐
  │  Bạn có 3 bước: Giặt (30p) → Sấy (30p) → Gấp (30p)          │
  │                                                                │
  │  Không Pipeline: Cuộn 1 xong hết mới bắt đầu Cuộn 2           │
  │    → 3 cuộn × 90 phút = 270 phút                              │
  │                                                                │
  │  Có Pipeline: Cuộn 1 đang Sấy → bỏ Cuộn 2 vào Giặt           │
  │    → Cuộn 1: 90p, Cuộn 2: thêm 30p, Cuộn 3: thêm 30p        │
  │    → Tổng: 150 phút (tiết kiệm 44%!)                          │
  └────────────────────────────────────────────────────────────────┘
```

### 2.2. Pipeline hiện đại — Superscalar & Out-of-Order

CPU hiện đại (Zen 5, Intel Core Ultra) có pipeline **19-25 stages** và là **superscalar** (nhiều pipeline chạy song song):

```
CPU Pipeline hiện đại (đơn giản hóa):

  Instruction Stream (Dòng lệnh từ RAM/Cache):
  ────────────────────────────────────────────
  │ ADD │ SUB │ MUL │ LOAD │ CMP │ JNE │ ...
  ────────────────────────────────────────────
       │
       ▼
  ┌─────────────────────────────────────────────────────────────┐
  │  FRONT-END (Thu thập & Giải mã)                             │
  │                                                             │
  │  ① Fetch: Tải 16-32 bytes lệnh từ L1i Cache                │
  │     ↓                                                       │
  │  ② Pre-decode: Xác định ranh giới lệnh (x86 = biến đổi)   │
  │     ↓                                                       │
  │  ③ Decode: Chuyển x86 → μops (micro-operations)            │
  │     - 1 lệnh đơn giản → 1 μop                              │
  │     - 1 lệnh phức tạp → 2-4 μops                           │
  │     ↓                                                       │
  │  ④ μop Cache: Lưu μops đã decode (tránh decode lại)        │
  │     ↓                                                       │
  │  ⑤ Rename: Đổi tên registers ảo → vật lý (tránh hazards)   │
  │     ↓                                                       │
  │  ⑥ Allocate & Dispatch: Đưa μops vào Reservation Stations  │
  └────────────────────────────┬────────────────────────────────┘
                               │
                               ▼
  ┌─────────────────────────────────────────────────────────────┐
  │  BACK-END (Thực thi — Out-of-Order)                         │
  │                                                             │
  │  Reservation Station (Hàng đợi cho mỗi loại đơn vị):       │
  │                                                             │
  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐   │
  │  │  ALU #0  │  │  ALU #1  │  │  ALU #2  │  │  ALU #3  │   │  ← 4 ALU
  │  │ (Int Add)│  │ (Int Add)│  │(Int Mul) │  │(Bit ops) │   │     song song!
  │  └──────────┘  └──────────┘  └──────────┘  └──────────┘   │
  │                                                             │
  │  ┌──────────┐  ┌──────────┐                                │
  │  │  FPU #0  │  │  FPU #1  │                                │  ← 2 FPU
  │  │(FP Add)  │  │(FP Mul)  │                                │     (float math)
  │  └──────────┘  └──────────┘                                │
  │                                                             │
  │  ┌──────────┐  ┌──────────┐                                │
  │  │ Load #0  │  │ Load #1  │                                │  ← 2 Load Units
  │  │(Read mem)│  │(Read mem)│                                │
  │  └──────────┘  └──────────┘                                │
  │                                                             │
  │  ┌──────────┐                                              │
  │  │ Store #0 │                                              │  ← 1 Store Unit
  │  │(Write)   │                                              │
  │  └──────────┘                                              │
  │                                                             │
  │  → CPU có thể thực thi 6-8 μops CÙNG LÚC mỗi cycle!       │
  │  → Lệnh không cần chạy theo thứ tự (Out-of-Order)          │
  │    miễn là kết quả cuối cùng ĐÚNG thứ tự.                  │
  └────────────────────────────┬────────────────────────────────┘
                               │
                               ▼
  ┌─────────────────────────────────────────────────────────────┐
  │  RETIRE (Hoàn tất — In-Order)                               │
  │                                                             │
  │  Re-Order Buffer (ROB): Sắp xếp lại kết quả theo thứ tự   │
  │  gốc, rồi commit vào Register File / Cache.                │
  │                                                             │
  │  → Đảm bảo chương trình "nhìn" đúng thứ tự dù CPU         │
  │    thực thi xáo trộn bên trong.                             │
  └─────────────────────────────────────────────────────────────┘
```

> **IPC (Instructions Per Cycle):** CPU hiện đại đạt IPC = 4-6 (hoàn thành 4-6 lệnh mỗi clock cycle nhờ superscalar). Đây là lý do tốc độ GHz không phải tất cả — IPC quan trọng không kém.

---

## 3. Pipeline Hazards — Ba kẻ phá hoại Pipeline

### 3.1. Data Hazard — Phụ thuộc dữ liệu

```
Ví dụ:
  ADD  R1, R2, R3    ; R1 = R2 + R3
  SUB  R4, R1, R5    ; R4 = R1 - R5  ← CẦN R1 từ lệnh trên!

Vấn đề: SUB cần R1, nhưng ADD chưa ghi kết quả vào R1 xong.

  Cycle:      1      2      3      4      5
  ADD R1:  [Fetch][Decode][Exec ][Mem  ][Write] ← R1 có ở cycle 5
  SUB R4:         [Fetch][Decode][████ ][████ ] ← SUB cần R1 ở cycle 3!
                                  STALL!! (Đứng chờ 2 cycles)

Giải pháp — Forwarding (Bypass):
  CPU "chuyền" kết quả từ output của ALU TRỰC TIẾP sang input
  mà KHÔNG ĐỢI ghi vào Register File:

  Cycle:      1      2      3      4      5
  ADD R1:  [Fetch][Decode][Exec→][Mem  ][Write]
  SUB R4:         [Fetch][Decode][Exec ][Mem  ]
                              ↑
                    Forwarding! R1 sẵn sàng ngay sau Exec của ADD
                    → Không stall!
```

### 3.2. Control Hazard — Branch (Nhánh rẽ) — KẺ THÙ LỚN NHẤT

```
Ví dụ C#:
  if (enemy.health <= 0)
      DestroyEntity(enemy);
  else
      UpdateAI(enemy);


Assembly tương đương:
  CMP   [health], 0          ; So sánh health với 0
  JLE   destroy_label        ; Nhảy đến destroy NẾU health <= 0
  CALL  UpdateAI             ; Nhánh else
  JMP   done                 
  destroy_label:
  CALL  DestroyEntity        ; Nhánh if
  destroy_label:
  CALL  DestroyEntity        ; Nhánh if
  done:

#### > Branch Prediction: CPU "đoán" thế nào?
Khi CPU gặp lệnh `JLE` (cycle 2), nó **CHƯA BIẾT** kết quả so sánh `CMP` (phải đến cycle 3-4 mới tính xong).
*   Để không dừng lại (stall), CPU **ĐOÁN** luôn: "Chắc là sẽ nhảy (Taken)".
*   Nó bắt đầu nạp lệnh tại `destroy_label` (CALL DestroyEntity) vào Pipeline ngay lập tức.
*   **Nếu đoán đúng:** Pipeline chạy mượt mà (0 penalty).
*   **Nếu đoán sai:** (VD: health > 0), CPU phải **HỦY BỎ (Flush)** toàn bộ các lệnh `DestroyEntity` đang chạy dở và quay lại nạp `CALL UpdateAI`.
    → Mất trắng 15-20 cycles đã "cầm đèn chạy trước ô tô"!


Vấn đề Pipeline:
  Cycle:     1      2      3      4      5
  CMP:    [Fetch][Decode][Exec ]
  JLE:           [Fetch][Decode][Exec ] ← Kết quả nhảy biết ở cycle 4
  ???:                  [Fetch]         ← CPU KHÔNG BIẾT fetch lệnh nào!
                                          UpdateAI hay DestroyEntity?

  CPU phải ĐOÁN (Branch Prediction):
  - Đoán đúng:  Pipeline tiếp tục bình thường     → 0 penalty
  - Đoán sai:   Pipeline FLUSH — xóa sạch 15-20 lệnh đã fetch sai
                 → 15-20 cycles wasted!


Branch Prediction — CPU "đoán" nhánh nào:

  ┌────────────────────────────────────────────────────────────────┐
  │  Branch History Table (BHT):                                   │
  │                                                                │
  │  Địa chỉ lệnh JLE    │ Lịch sử (T=Taken, N=Not-Taken)        │
  │  ────────────────────┼───────────────────────────              │
  │  0x004010A0           │  T T T T T N T T → Predict: TAKEN      │
  │  0x004010B4           │  N N N N N T N N → Predict: NOT-TAKEN  │
  │  0x004010C8           │  T N T N T N T N → Predict: ???        │
  │                        │  ↑ Pattern không rõ → accuracy thấp    │
  │                                                                │
  │  CPU hiện đại: ~95-97% accuracy cho code thông thường          │
  │  Nhưng: Pattern ngẫu nhiên → accuracy ~50% → thảm họa!        │
  └────────────────────────────────────────────────────────────────┘
```

### 3.3. Ảnh hưởng thực tế trong Unity — Ví dụ Branching

```
═══ Kịch bản: Xử lý 10,000 entities, 50% alive, 50% dead ═══

--- Code có Branch ---
[BurstCompile]
public void Execute(int i)
{
    if (healths[i].Value > 0)        // Branch — CPU phải đoán!
    {
        positions[i] += velocities[i] * dt;
        healths[i] -= poisonDamage;
    }
    // else: skip (dead entity)
}

Phân tích:
  - 50% alive, 50% dead → Pattern NGẪU NHIÊN
  - Branch accuracy: ~50-60%
  - Mỗi miss-predict: ~15 cycles penalty
  - 10,000 × 40% miss × 15 = 60,000 cycles wasted


--- Code Branchless ---
[BurstCompile]
public void Execute(int i)
{
    float alive = math.select(0f, 1f, healths[i].Value > 0);
    // alive = 1.0 nếu sống, 0.0 nếu chết

    positions[i] += velocities[i] * dt * alive;
    // Dead entity: velocity × 0 = 0 → position không đổi
    
    healths[i] -= poisonDamage * alive;
    // Dead entity: -= 0 → health không đổi
}

Phân tích:
  - KHÔNG CÓ BRANCH → Không có prediction, không có miss
  - CPU + Burst vectorize toàn bộ bằng SIMD
  - Tính dư (dead entity vẫn nhân × 0) nhưng pipeline KHÔNG BỊ PHẪU
  - Nhanh hơn ~2-3× khi tỉ lệ alive/dead gần 50/50!


═══ Quy tắc: Khi nào dùng Branch vs Branchless? ═══

  ┌──────────────────────────────────────────────────────────┐
  │  Branch (if/else) TỐT KHI:                              │
  │    - Một nhánh chiếm >90% (CPU đoán đúng gần hết)      │
  │    - Nhánh đắt (skip heavy computation khi không cần)   │
  │    - Code clarity quan trọng hơn performance             │
  │                                                          │
  │  Branchless (select/step/lerp) TỐT KHI:                 │
  │    - Tỉ lệ hai nhánh gần 50/50 (CPU đoán sai nhiều)    │
  │    - Trong tight loop xử lý hàng nghìn phần tử          │
  │    - Trong Shader (GPU branch divergence còn tệ hơn!)   │
  │    - Code trong [BurstCompile] Job                       │
  └──────────────────────────────────────────────────────────┘
```

---

## 4. Stack & Function Calls — Cái giá của mỗi lần gọi hàm

### 4.1. Call Stack — Cách CPU quản lý hàm

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

### 4.2. Inlining — Loại bỏ chi phí gọi hàm

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

## 5. Từ C# đến Mã máy — Ba con đường trong Unity

### 5.1. Con đường Mono (JIT — Just-In-Time)

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

### 5.2. Con đường IL2CPP (AOT — Ahead-of-Time)

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

### 5.3. Con đường Burst (AOT + SIMD — Cao cấp nhất)

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

### 5.4. So sánh ba con đường — Benchmark thực tế

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

## 6. Garbage Collection — "Stop the World"

### 6.1. GC hoạt động như thế nào?

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

## 7. Tổng kết Chapter 3 — Con đường của một dòng code

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
