# Chương 4: GPU Architecture & Rendering Pipeline

> **Mục tiêu chương:** Hiểu kiến trúc phần cứng GPU khác CPU như thế nào, cách Rendering Pipeline biến dữ liệu 3D thành pixel, và tại sao mỗi quyết định trong Shader code ảnh hưởng trực tiếp đến hiệu năng game.

---

## 1. Tại sao cần GPU? — CPU không đủ cho đồ họa

### 1.1. Bài toán rendering

```
Render 1 frame Full HD (1920×1080) ở 60 FPS:

  Số pixel:        1920 × 1080 = 2,073,600 pixels
  Mỗi pixel cần:   ~50-200 phép tính (lighting, texturing, shadows, ...)
  Tổng phép tính:  2M × 100 = ~200 TRIỆU phép tính / frame
  Ở 60 FPS:        200M × 60 = ~12 TỶ phép tính / giây

  CPU 8 cores × 5 GHz × IPC 4 = ~160 tỷ ops/giây
  → CPU CÓ THỂ render, nhưng:
    - Hết sạch CPU cho graphics → không còn cho game logic
    - Mỗi pixel LÀ ĐỘC LẬP → song song hóa hoàn hảo
    - CPU chỉ có 8-16 cores → lãng phí tiềm năng song song

  GPU ~4000 cores × 1.5 GHz = không nhanh từng core, nhưng:
  → XỬ LÝ 4000 PIXELS CÙNG LÚC
  → Throughput (lượng công việc/giây) >> CPU gấp nhiều lần
```

### 1.2. Triết lý thiết kế: Latency vs Throughput

```
┌─────────────────────────────────────────────────────────────────────┐
│                CPU vs GPU — Hai triết lý đối lập                    │
├────────────────────────────┬────────────────────────────────────────┤
│         CPU                │              GPU                       │
│   "Làm 1 việc CỰC NHANH"  │   "Làm TRIỆU việc song song"         │
├────────────────────────────┼────────────────────────────────────────┤
│ ● 8-24 cores              │ ● 2,000-16,000 cores                  │
│ ● Clock cao: 4-6 GHz      │ ● Clock thấp hơn: 1.5-2.5 GHz        │
│ ● Out-of-Order execution  │ ● In-Order (đơn giản hơn)             │
│ ● Branch prediction       │ ● Branch = thảm họa                   │
│ ● Cache LỚN (32MB L3)     │ ● Cache NHỎ (6MB L2 shared)          │
│ ● Latency-oriented        │ ● Throughput-oriented                  │
├────────────────────────────┼────────────────────────────────────────┤
│                            │                                        │
│  Ẩn dụ:                    │  Ẩn dụ:                                │
│  1 giáo sư giải đề thi    │  10,000 học sinh lớp 1                 │
│  → CỰC NHANH từng bài     │  → Mỗi em giải 1 bài ĐƠN GIẢN       │
│  → Nhưng 1 người           │  → Tổng: xong 10,000 bài CÙNG LÚC    │
│                            │                                        │
├────────────────────────────┼────────────────────────────────────────┤
│ Phù hợp:                  │ Phù hợp:                               │
│ ✅ Game logic              │ ✅ Rendering (pixel processing)         │
│ ✅ AI phức tạp             │ ✅ Particle systems (100K particles)   │
│ ✅ Physics (broad phase)   │ ✅ Post-processing                     │
│ ✅ Networking              │ ✅ Compute Shaders (GPGPU)             │
│ ✅ File I/O                │ ✅ Machine Learning inference          │
└────────────────────────────┴────────────────────────────────────────┘
```

---

## 2. Kiến trúc phần cứng GPU

### 2.1. Cấu trúc phân cấp — SM (Streaming Multiprocessor)

```
GPU Die (ví dụ: NVIDIA RTX 4070 — AD104):

  ┌───────────────────────────────────────────────────────────────┐
  │                    GPU CHIP (AD104)                            │
  │                                                               │
  │  ┌──── GPC 0 ─────┐  ┌──── GPC 1 ─────┐  ┌──── GPC ... ──┐ │
  │  │                 │  │                 │  │                │ │
  │  │  ┌─SM 0─┐       │  │  ┌─SM 4─┐       │  │                │ │
  │  │  │      │       │  │  │      │       │  │                │ │
  │  │  └──────┘       │  │  └──────┘       │  │                │ │
  │  │  ┌─SM 1─┐       │  │  ┌─SM 5─┐       │  │                │ │
  │  │  │      │       │  │  │      │       │  │                │ │
  │  │  └──────┘       │  │  └──────┘       │  │                │ │
  │  │  ┌─SM 2─┐       │  │  ┌─SM 6─┐       │  │                │ │
  │  │  │      │       │  │  │      │       │  │                │ │
  │  │  └──────┘       │  │  └──────┘       │  │                │ │
  │  │  ┌─SM 3─┐       │  │  ┌─SM 7─┐       │  │                │ │
  │  │  │      │       │  │  │      │       │  │     ×5 GPC     │ │
  │  │  └──────┘       │  │  └──────┘       │  │     = 46 SM    │ │
  │  └─────────────────┘  └─────────────────┘  └────────────────┘ │
  │                                                               │
  │  ┌────────────────────────────────────────────────────┐       │
  │  │              L2 Cache (36 MB, Shared)              │       │
  │  └────────────────────────────────────────────────────┘       │
  │                         │                                     │
  │                    Memory Controllers                         │
  │                         │                                     │
  └─────────────────────────┼─────────────────────────────────────┘
                            │
                  ┌─────────┴──────────┐
                  │  VRAM (GDDR6X)     │
                  │  12 GB, 192-bit    │
                  │  Bandwidth: 504 GB/s│
                  └────────────────────┘


Bên trong 1 SM (Streaming Multiprocessor):

  ┌────────────────────────────────────────────────────────────┐
  │  SM (Streaming Multiprocessor)                             │
  │                                                            │
  │  ┌──────────────────────────────────────────────────┐      │
  │  │  Warp Scheduler ×4                                │      │
  │  │  (Mỗi scheduler quản lý nhiều Warps)              │      │
  │  └──────────────────────────────────────────────────┘      │
  │                                                            │
  │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐         │
  │  │ FP32 ×32│ │ FP32 ×32│ │ FP32 ×32│ │ FP32 ×32│         │
  │  │ (CUDA   │ │ (CUDA   │ │ (CUDA   │ │ (CUDA   │         │
  │  │  cores) │ │  cores) │ │  cores) │ │  cores) │         │
  │  └─────────┘ └─────────┘ └─────────┘ └─────────┘         │
  │  = 128 FP32 cores / SM                                     │
  │                                                            │
  │  ┌─────────┐ ┌─────────┐                                  │
  │  │ INT32×32│ │Tensor×4 │  ← Tensor Cores (AI/ML, DLSS)   │
  │  └─────────┘ └─────────┘                                  │
  │                                                            │
  │  ┌─────────┐ ┌─────────┐                                  │
  │  │  SFU ×4 │ │  RT ×1  │  ← RT Core (Ray Tracing)        │
  │  │(sin,cos)│ └─────────┘                                  │
  │  └─────────┘                                              │
  │                                                            │
  │  ┌──────────────────────────────────┐                      │
  │  │  Register File: 65,536 × 32-bit │  = 256 KB / SM       │
  │  └──────────────────────────────────┘                      │
  │                                                            │
  │  ┌──────────────────────────────────┐                      │
  │  │  Shared Memory / L1 Cache       │  = 128 KB / SM       │
  │  │  (Configurable: 64K shared +    │                      │
  │  │   64K L1, hoặc 128K shared)     │                      │
  │  └──────────────────────────────────┘                      │
  │                                                            │
  │  ┌──────────────────────────────────┐                      │
  │  │  Texture Units × 4              │                      │
  │  │  (Bilinear filter, mipmapping)  │                      │
  │  └──────────────────────────────────┘                      │
  └────────────────────────────────────────────────────────────┘

  Tổng GPU: 46 SM × 128 cores = 5,888 CUDA Cores
  → So sánh: CPU có 8-16 cores, GPU có ~6,000 cores!
```

> **Tên gọi khác nhau cùng ý nghĩa:**
> - NVIDIA: SM (Streaming Multiprocessor), CUDA Core, Warp (32 threads)
> - AMD: CU (Compute Unit), Stream Processor, Wavefront (64 threads)
> - Apple: GPU Core, Execution Unit, SIMD Group (32 threads)

### 2.2. SIMT — Single Instruction, Multiple Threads

```
SIMT là mô hình thực thi của GPU — tương tự SIMD của CPU nhưng ở mức THREAD:

  CPU SIMD: 1 lệnh xử lý 4-8 data elements trong 1 register
  GPU SIMT: 1 lệnh điều khiển 32 threads CÙNG LÚC (= 1 Warp)


Ví dụ — Fragment Shader xử lý pixel:

  Shader code (chạy cho MỖI pixel):
  ─────────────────────────────────
  float4 FragMain(float2 uv) {
      float4 color = tex2D(_MainTex, uv);     // Lệnh 1: Sample texture
      color.rgb *= _LightColor;                // Lệnh 2: Áp ánh sáng
      color.rgb = pow(color.rgb, 2.2);         // Lệnh 3: Gamma correction
      return color;                            // Lệnh 4: Output
  }


  GPU thực thi (1 Warp = 32 threads = 32 pixels):
  ────────────────────────────────────────────────

  Warp #0 (Pixel 0-31):
  ┌────────────────────────────────────────────────────────────────┐
  │ Clock 1: TẤT CẢ 32 threads chạy tex2D CÙNG LÚC              │
  │          Thread 0: tex2D(uv_0)                                 │
  │          Thread 1: tex2D(uv_1)                                 │
  │          ...                                                   │
  │          Thread 31: tex2D(uv_31)                               │
  │                                                                │
  │ Clock 2: TẤT CẢ 32 threads nhân _LightColor CÙNG LÚC         │
  │          Thread 0: color_0 *= light                            │
  │          Thread 1: color_1 *= light                            │
  │          ...                                                   │
  │                                                                │
  │ Clock 3: TẤT CẢ 32 threads tính pow() CÙNG LÚC               │
  │          ...                                                   │
  │                                                                │
  │ Clock 4: TẤT CẢ 32 output CÙNG LÚC                           │
  └────────────────────────────────────────────────────────────────┘

  → 4 clocks xử lý 32 pixels!
  → 46 SM × 4 Warp Schedulers = 184 Warps chạy đồng thời
  → 184 × 32 = 5,888 pixels xử lý CÙNG 1 clock
```

### 2.3. Branch Divergence — Kẻ giết hiệu năng Shader

```
Khi if/else trong Shader, các threads trong Warp có thể đi nhánh KHÁC NHAU:

  Shader code:
  float4 FragMain(float2 uv) {
      float4 color = tex2D(_MainTex, uv);
      
      if (color.a > 0.5) {          // ← BRANCH!
          // Nhánh A: Compute lighting (đắt)
          color = ComputePBRLighting(color, normal, lightDir);
      } else {
          // Nhánh B: Discard (rẻ)
          discard;
      }
      return color;
  }


  Warp thực thi khi threads đi KHÁC NHÁNH (Divergence):
  ┌────────────────────────────────────────────────────────────────┐
  │  Warp #0: 32 threads, giả sử 20 threads → A, 12 threads → B │
  │                                                                │
  │  Bước 1: Chạy nhánh A (threads 0-19 ACTIVE, 20-31 MASKED)    │
  │  ┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐           │
  │  │ T0  │ T1  │ ... │ T19 │ T20 │ T21 │ ... │ T31 │           │
  │  │ RUN │ RUN │     │ RUN │IDLE │IDLE │     │IDLE │           │
  │  │ PBR │ PBR │     │ PBR │ --- │ --- │     │ --- │           │
  │  └─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘           │
  │  → 12 threads LÃNG PHÍ = 37.5% GPU power wasted!              │
  │                                                                │
  │  Bước 2: Chạy nhánh B (threads 20-31 ACTIVE, 0-19 MASKED)    │
  │  ┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐           │
  │  │ T0  │ T1  │ ... │ T19 │ T20 │ T21 │ ... │ T31 │           │
  │  │IDLE │IDLE │     │IDLE │ RUN │ RUN │     │ RUN │           │
  │  │ --- │ --- │     │ --- │disc │disc │     │disc │           │
  │  └─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘           │
  │  → 20 threads LÃNG PHÍ = 62.5%!                               │
  │                                                                │
  │  Tổng: GPU phải chạy CẢ HAI nhánh tuần tự                     │
  │  Thời gian = cost(A) + cost(B) thay vì max(A, B)              │
  │  → Worst case: divergence 50/50 = 2× chậm hơn!               │
  └────────────────────────────────────────────────────────────────┘


═══ Giải pháp trong Unity Shader ═══

  ❌ TRÁNH: if/else dựa trên per-pixel data
  if (color.r > threshold) { ... } else { ... }

  ✅ DÙNG: Branchless math
  float mask = step(threshold, color.r);   // 0 hoặc 1
  color = lerp(colorB, colorA, mask);      // Blend thay vì branch

  ✅ DÙNG: Texture lookup thay vì complex branching
  float3 result = tex2D(_LookupTable, float2(input, 0));

  ✅ DÙNG: keyword variants thay vì runtime branch
  #pragma multi_compile _ _FEATURE_ON
  #ifdef _FEATURE_ON
      // Code này compile thành shader variant RIÊNG
      // → Không có branch at runtime!
  #endif
```

---

## 3. GPU Memory — Bandwidth là vua

### 3.1. Kiến trúc bộ nhớ GPU

```
┌────────────────────────────────────────────────────────────────────┐
│              GPU Memory Hierarchy                                  │
│                                                                    │
│  ┌─ Per-Thread ─────────────────────────────────────────┐          │
│  │  Registers: ~256 KB per SM                           │          │
│  │  Tốc độ: 0 cycles (tức thì)                          │          │
│  │  → Local variables trong shader                      │          │
│  └──────────────────────────────────────────────────────┘          │
│           │                                                        │
│           ▼                                                        │
│  ┌─ Per-SM (Shared) ────────────────────────────────────┐          │
│  │  Shared Memory / L1: 128 KB per SM                   │          │
│  │  Tốc độ: ~5 cycles                                   │          │
│  │  → Compute Shader groupshared data                   │          │
│  │  → Texture L1 cache                                  │          │
│  └──────────────────────────────────────────────────────┘          │
│           │                                                        │
│           ▼                                                        │
│  ┌─ Chip-wide ──────────────────────────────────────────┐          │
│  │  L2 Cache: 36 MB (RTX 4070)                          │          │
│  │  Tốc độ: ~30-50 cycles                               │          │
│  │  → Texture data reuse, render target readback        │          │
│  └──────────────────────────────────────────────────────┘          │
│           │                                                        │
│           ▼                                                        │
│  ┌─ Off-chip ───────────────────────────────────────────┐          │
│  │  VRAM (GDDR6X): 12 GB                                │          │
│  │  Tốc độ: ~200-400 cycles                              │          │
│  │  Bandwidth: 504 GB/s                                  │          │
│  │  → Textures, Buffers, Render Targets                  │          │
│  └──────────────────────────────────────────────────────┘          │
│           │                                                        │
│           ▼   (Qua PCIe bus — CHẬM NHẤT)                           │
│  ┌─ System RAM ─────────────────────────────────────────┐          │
│  │  DDR5 RAM: 16-64 GB                                   │          │
│  │  Bandwidth: ~50 GB/s qua PCIe 4.0 x16                │          │
│  │  → Upload textures, read-back pixels                  │          │
│  │  → MỖI LẦN CPU↔GPU transfer = BOTTLENECK!            │          │
│  └──────────────────────────────────────────────────────┘          │
└────────────────────────────────────────────────────────────────────┘


Bandwidth là bottleneck #1 trên GPU:

  Ví dụ: Render 1080p, mỗi pixel đọc 1 texture sample (RGBA8 = 4 bytes)
  + bilinear filter = 4 texels = 16 bytes/pixel

  2M pixels × 16 bytes = 32 MB / frame
  × 60 FPS = 1.92 GB/s → OK cho GDDR6X

  NHƯNG: Mỗi pixel thường sample 5-10 textures (albedo, normal,
  roughness, AO, emission, shadow map, ...) + overdraw 2-3×:

  2M × 16 bytes × 8 textures × 2.5 overdraw = 640 MB / frame
  × 60 FPS = 38.4 GB/s → Bắt đầu đáng lo!
  × 120 FPS (VR) = 76.8 GB/s → GẦN GIỚI HẠN!

  → Đây là lý do tối ưu texture fetch CỰC KỲ quan trọng.
```

### 3.2. Latency Hiding — Bí quyết của GPU

```
CPU ẩn latency bằng: Cache lớn + Out-of-Order + Branch Prediction
GPU ẩn latency bằng: CHUYỂN SANG WARP KHÁC

  ┌────────────────────────────────────────────────────────────────┐
  │  SM có 32 Warps active. Khi Warp #0 chờ texture:              │
  │                                                                │
  │  Clock 1-4:   Warp #0 chạy lệnh tính toán                    │
  │  Clock 5:     Warp #0 gọi tex2D() → chờ VRAM (~200 cycles)   │
  │                                                                │
  │  Clock 6:     SM CHUYỂN sang Warp #1 (tức thì, 0 cycles!)     │
  │  Clock 6-10:  Warp #1 chạy                                    │
  │  Clock 11:    Warp #1 chờ VRAM → chuyển sang Warp #2          │
  │  ...                                                           │
  │  Clock ~200:  Warp #0 nhận data từ VRAM → tiếp tục            │
  │                                                                │
  │  → Trong 200 cycles chờ, SM đã xử lý ~40 Warps khác!          │
  │  → GPU LUÔN BẬN: không bao giờ stall nếu đủ Warps             │
  └────────────────────────────────────────────────────────────────┘

  Điều kiện: Phải có ĐỦ active Warps (= Occupancy cao)
  
  Occupancy = Active Warps / Max Warps per SM
  
  Occupancy thấp (ít Warps):
    → GPU hết Warp để chuyển khi chờ VRAM
    → SM stall → hiệu năng giảm

  Nguyên nhân Occupancy thấp:
    ❌ Shader dùng quá nhiều registers (register pressure)
    ❌ Shader dùng quá nhiều shared memory
    ❌ Thread Group quá lớn hoặc quá nhỏ

  → Đây là lý do shader ĐÔGIAN hơn thường NHANH hơn shader phức tạp,
    NGAY CẢ KHI tổng phép tính ít hơn!
```

---

## 4. Giao tiếp CPU ↔ GPU & "Gót chân Von Neumann"

### 4.1. Von Neumann Bottleneck — "Bức tường Bộ nhớ" (Memory Wall)

Kiến trúc máy tính hiện đại vẫn dựa trên mô hình Von Neumann: **CPU/GPU tách biệt hoàn toàn với Bộ nhớ (RAM/VRAM)**.

```
VẤN ĐỀ:
  Tốc độ tính toán của Core (ALU) tăng trưởng ~50%/năm.
  Tốc độ truyền tải của Bus (dây dẫn) chỉ tăng ~10%/năm.

  → Hiện tượng: "Procesor is fast, Memory is slow."
  → CPU/GPU dành 90% thời gian để CHỜ dữ liệu từ RAM.
  → Đây chính là "Gót chân Von Neumann" (Memory Wall).
```

### 4.2. Hạ tầng PCIe — Nút thắt cổ chai vật lý

Dữ liệu đi từ CPU (RAM) sang GPU (VRAM) phải đi qua **PCIe Bus**.

```
So sánh Bandwidth (Băng thông):
  - Bên trong GPU (VRAM ↔ L2): ~500 - 1000 GB/s (GDDR6X/HBM3)
  - Giữa CPU và GPU (PCIe 4.0 x16): ~32 GB/s
  - Giữa CPU và GPU (PCIe 5.0 x16): ~64 GB/s

  → Kết luận: Con đường PCIe hẹp hơn nội bộ GPU gấp 20-30 lần!
  → Quy tắc vàng: Hạn chế tối đa việc gửi dữ liệu qua lại giữa CPU và GPU trong mỗi frame.
```

### 4.3. Command Buffer & Ring Buffer — Cách "nói chuyện"

CPU và GPU không nói chuyện trực tiếp. Chúng giao tiếp qua một "Hộp thư" (Mailbox).

1.  **Command Buffer (CPU soạn thảo):**
    *   CPU (Driver) viết một danh sách các lệnh (SetTexture, DrawCall, ...) vào một vùng nhớ RAM đặc biệt.
2.  **Ring Buffer (Dây chuyền sản xuất):**
    *   GPU liên tục "quét" vùng nhớ này theo vòng tròn (Ring).
    *   GPU đọc lệnh nào thì thực hiện lệnh đó (In-Order).
3.  **Driver (Thông dịch viên):**
    *   Dịch mã C# Unity (Graphics.DrawMesh) thành mã nhị phân mà phần cứng GPU cụ thể (NVIDIA/AMD) hiểu được.

### 4.4. Giải pháp hiện đại: Phá vỡ bức tường

Để vượt qua giới hạn Von Neumann, các công nghệ mới đang xóa nhòa ranh giới:
*   **Unified Memory (Apple Silicon M1/M2/M3):** CPU và GPU dùng chung 1 bể RAM duy nhất. Không còn tốn thời gian "copy" qua PCIe.
*   **HBM (High Bandwidth Memory):** Chồng chip nhớ trực tiếp lên trên GPU die để rút ngắn khoảng cách vật lý của dây dẫn.
*   **DirectStorage / RTX IO:** GPU tự đọc dữ liệu từ SSD mà không cần "nhờ" CPU copy hộ.

---

## 5. Rendering Pipeline — Từ Draw Call đến Pixel

### 4.1. Tổng quan luồng dữ liệu

```
Từ CPU đến Màn hình — Toàn bộ pipeline:

  CPU Side:                          GPU Side:
  ─────────                          ─────────

  ① Game Logic (C#/ECS)
     │
     ▼
  ② Culling
     (Frustum, Occlusion)
     │
     ▼
  ③ Sorting
     (Front-to-back opaque,
      back-to-front transparent)
     │
     ▼
  ④ Batching                    ═══════════════════════════
     │                           Command Buffer
     ▼                           ═══════════════════════════
  ⑤ Draw Call:                        │
     SetPassCall(shader)              ▼
     SetTexture(albedo)          ⑥ Input Assembly
     SetBuffer(vertices)         ⑦ Vertex Shader        ← PROGRAMMABLE
     DrawIndexed(triCount)       ⑧ Hull/Domain Shader    ← (Tessellation)
                                 ⑨ Geometry Shader       ← (ít dùng)
                                 ⑩ Rasterization         ← FIXED-FUNCTION
                                 ⑪ Fragment Shader       ← PROGRAMMABLE
                                 ⑫ Output Merger
                                      │
                                      ▼
                                 ⑬ Framebuffer → Display
```

### 4.2. Từng giai đoạn chi tiết

```
═══ ⑥ Input Assembly — Thu thập dữ liệu đỉnh ═══

  GPU đọc Vertex Buffer + Index Buffer từ VRAM:

  Vertex Buffer:
  ┌──────────────────────────────────────────────────────────────┐
  │ V0: pos(1,0,0) norm(0,1,0) uv(0,0) │ V1: pos(0,1,0)...    │
  │ V2: pos(-1,0,0)...                  │ V3: pos(0,-1,0)...   │
  └──────────────────────────────────────────────────────────────┘

  Index Buffer:
  ┌────────────────────────────────┐
  │ 0, 1, 2,  │ 2, 1, 3,  │ ...  │  ← Mỗi 3 indices = 1 tam giác
  └────────────────────────────────┘

  → Unity Mesh.vertices, Mesh.triangles map trực tiếp tới đây.


═══ ⑦ VERTEX SHADER — Biến đổi từ Object Space → Screen Space ═══

  Chạy 1 lần PER VERTEX. GPU thực thi hàng triệu vertices song song.

  Input:  Object Space position (tọa độ local của mesh)
  Output: Clip Space position (tọa độ chuẩn hóa cho màn hình)

  HLSL:
  ┌─────────────────────────────────────────────────────────────┐
  │  struct Varyings {                                          │
  │      float4 positionCS : SV_POSITION;  // Clip Space        │
  │      float2 uv         : TEXCOORD0;                        │
  │      float3 normalWS   : TEXCOORD1;    // World Space       │
  │  };                                                         │
  │                                                             │
  │  Varyings vert(Attributes IN) {                             │
  │      Varyings OUT;                                          │
  │      // Ma trận MVP: Model → View → Projection              │
  │      OUT.positionCS = TransformObjectToHClip(IN.positionOS);│
  │      OUT.uv = TRANSFORM_TEX(IN.uv, _MainTex);              │
  │      OUT.normalWS = TransformObjectToWorldNormal(IN.normal);│
  │      return OUT;                                            │
  │  }                                                          │
  └─────────────────────────────────────────────────────────────┘

  Biến đổi tọa độ:
  ┌───────────┐   Model    ┌───────────┐   View    ┌───────────┐
  │  Object   │──Matrix───►│   World   │──Matrix──►│  Camera   │
  │  Space    │            │   Space   │           │  Space    │
  └───────────┘            └───────────┘           └─────┬─────┘
                                                         │
                                                   Projection
                                                     Matrix
                                                         │
                                                         ▼
                                                   ┌───────────┐
                                                   │   Clip     │
                                                   │   Space    │
                                                   │ (-1 to +1) │
                                                   └───────────┘


═══ ⑩ RASTERIZATION — Tam giác → Pixel (Fixed-Function) ═══

  GPU hardware chuyển tam giác thành danh sách pixel (fragments):

  Clip Space Triangle:           Screen Pixels (Fragments):
       ▲ V0                      ┌───┬───┬───┬───┬───┐
      / \                        │   │   │ ● │   │   │
     /   \                       ├───┼───┼───┼───┼───┤
    /     \                      │   │ ● │ ● │ ● │   │
   /       \                     ├───┼───┼───┼───┼───┤
  V1───────V2                    │ ● │ ● │ ● │ ● │ ● │
                                 └───┴───┴───┴───┴───┘
                                  ● = Fragment (pixel candidate)

  Quá trình:
  1. Edge Function: Xác định pixel nào nằm TRONG tam giác
  2. Interpolation: Tính UV, Normal, Color cho mỗi fragment
     bằng Barycentric Coordinates (nội suy trọng tâm)
  3. Output: Danh sách fragments → đưa vào Fragment Shader

  Đây là hardware CỐ ĐỊNH (không lập trình được) — cực nhanh.


═══ ⑪ FRAGMENT (PIXEL) SHADER — Tô màu từng pixel ═══

  Chạy 1 lần PER FRAGMENT. Đây là stage TỐN NHẤT (nhiều fragments nhất).

  HLSL:
  ┌─────────────────────────────────────────────────────────────┐
  │  float4 frag(Varyings IN) : SV_Target {                    │
  │                                                             │
  │      // 1. Sample textures                                  │
  │      float4 albedo = tex2D(_MainTex, IN.uv);               │
  │      float3 normal = UnpackNormal(tex2D(_BumpMap, IN.uv)); │
  │      float  rough  = tex2D(_RoughnessTex, IN.uv).r;        │
  │                                                             │
  │      // 2. Lighting (PBR - Cook-Torrance BRDF)              │
  │      float3 N = normalize(IN.normalWS);                     │
  │      float3 L = normalize(_LightDir);                       │
  │      float  NdotL = saturate(dot(N, L));                    │
  │                                                             │
  │      float3 diffuse = albedo.rgb * NdotL * _LightColor;    │
  │      float3 specular = CookTorranceBRDF(N, L, V, rough);   │
  │                                                             │
  │      // 3. Shadows, AO, Emission, ...                       │
  │      float shadow = SampleShadowMap(IN.positionWS);         │
  │      float ao = tex2D(_AOTex, IN.uv).r;                    │
  │                                                             │
  │      float3 final = (diffuse + specular) * shadow * ao;     │
  │      return float4(final, albedo.a);                        │
  │  }                                                          │
  └─────────────────────────────────────────────────────────────┘

  Chi phí:
  - Mỗi tex2D() = 1 texture fetch (~4-200 cycles tùy cache)
  - PBR lighting = ~50-100 ALU ops
  - Shadow sampling = 1-16 texture fetches (PCF/PCSS)
  - Nhân với 2M pixels × overdraw 2-3× = THỤ NGHIỆP LỚN NHẤT

  → Fragment Shader optimization = ĐÒN BẨY LỚN NHẤT cho FPS!


═══ ⑫ OUTPUT MERGER — Test & Blend ═══

  ┌────────────────────────────────────────────────────────────┐
  │  Depth Test (Z-Buffer):                                    │
  │    if (fragment.z < zbuffer[x,y]) {                        │
  │        zbuffer[x,y] = fragment.z;    // Cập nhật depth     │
  │        colorbuffer[x,y] = fragment.color;                  │
  │    }                                                       │
  │    // else: fragment bị che bởi object gần hơn → DISCARD   │
  │                                                            │
  │  Stencil Test: Masking (UI, portals, decals)               │
  │                                                            │
  │  Blending (cho transparent objects):                        │
  │    finalColor = src.rgb * src.a + dst.rgb * (1 - src.a)    │
  │    → Transparent objects phải render SAU opaque             │
  │    → Phải sort BACK-TO-FRONT                               │
  │    → KHÔNG viết depth → overdraw tăng!                     │
  └────────────────────────────────────────────────────────────┘
```

---

## 6. Draw Calls & Batching — CPU↔GPU Communication

### 5.1. Draw Call là gì?

```
Draw Call = 1 lần CPU ra lệnh cho GPU render.

  Mỗi Draw Call, CPU phải:
  1. Set Shader (Pipeline State)        → GPU state change
  2. Set Textures (Albedo, Normal, ...) → Bind textures
  3. Set Constant Buffers (MVP matrix)  → Upload uniforms
  4. Set Vertex/Index Buffers           → Bind geometry
  5. Gọi DrawIndexed(triangleCount)     → GPU bắt đầu render

  Chi phí: ~5-20 μs per draw call (phía CPU)
  
  → 1,000 draw calls = 5-20ms → GẦN HẾT budget 16.67ms/frame!
  → GPU thường NHANH hơn CPU render → CPU-bound!


  ┌── Frame Timeline ─────────────────────────────────────────────┐
  │                                                               │
  │  CPU:  [Draw1][Draw2][Draw3]...[Draw500][Submit]              │
  │        ████████████████████████████████████████  = 12ms       │
  │                                                               │
  │  GPU:        [Render1][Render2][Render3]...[Render500]        │
  │              ████████████████████████████████████  = 6ms      │
  │                                                               │
  │  → CPU is BOTTLENECK! GPU chờ CPU gửi tiếp.                  │
  │  → Frame time = max(CPU, GPU) = 12ms                          │
  │  → Giảm draw calls = giảm CPU time = tăng FPS                │
  └───────────────────────────────────────────────────────────────┘
```

### 5.2. Batching Strategies

```
┌─────────────────────────────────────────────────────────────────────┐
│                    BATCHING TECHNIQUES                               │
├───────────────────┬─────────────────────────────────────────────────┤
│ Static Batching   │ Combine meshes dùng CÙNG material tại          │
│                   │ build time (bake thành 1 mesh lớn)              │
│                   │ ✅ No CPU cost at runtime                       │
│                   │ ❌ Tăng memory (duplicate vertices)             │
│                   │ ❌ Objects không thể move / animate              │
│                   │ 🎯 Dùng cho: environment, props cố định         │
├───────────────────┼─────────────────────────────────────────────────┤
│ Dynamic Batching  │ Combine meshes nhỏ (<300 verts) mỗi frame      │
│                   │ ✅ Objects có thể move                          │
│                   │ ❌ CPU cost cho combining                        │
│                   │ ❌ Chỉ meshes rất nhỏ                           │
│                   │ 🎯 Dùng cho: particles, small props             │
├───────────────────┼─────────────────────────────────────────────────┤
│ GPU Instancing    │ 1 Draw Call render N copies của CÙNG mesh       │
│                   │ ✅ Minimal CPU overhead                         │
│                   │ ✅ Mỗi instance có thể khác position/color      │
│                   │ ❌ Cùng mesh + cùng material                    │
│                   │ 🎯 Dùng cho: trees, grass, enemies cùng model   │
├───────────────────┼─────────────────────────────────────────────────┤
│ SRP Batcher       │ Cache GPU state → reduce state changes          │
│                   │ ✅ Không cần cùng mesh                          │
│                   │ ✅ Chỉ cần cùng shader variant                  │
│                   │ ❌ URP/HDRP only (SRP = Scriptable RP)          │
│                   │ 🎯 Chiến lược mặc định cho URP projects         │
├───────────────────┼─────────────────────────────────────────────────┤
│ DrawMeshInstanced │ Render từ Compute Buffer — GPU-driven           │
│ Indirect          │ ✅ CPU gần như ZERO cost                        │
│                   │ ✅ GPU tự culling + sorting                     │
│                   │ ❌ Phức tạp để implement                        │
│                   │ 🎯 Dùng cho: grass, foliage, massive crowds     │
│                   │    (100K+ instances)                             │
└───────────────────┴─────────────────────────────────────────────────┘


Ví dụ DrawMeshInstancedIndirect (GPU-Driven Pipeline):

  ┌────────────────────────────────────────────────────────────────┐
  │                                                                │
  │  Bước 1: CPU upload instance data → Compute Buffer (1 lần)    │
  │    StructuredBuffer<InstanceData> _InstanceBuffer;             │
  │    // position, rotation, scale, color cho 100K instances      │
  │                                                                │
  │  Bước 2: GPU Compute Shader culling (mỗi frame)               │
  │    → Test mỗi instance vs frustum → output visible list       │
  │    → AppendStructuredBuffer<uint> _VisibleInstances;           │
  │                                                                │
  │  Bước 3: CPU gọi DrawMeshInstancedIndirect                    │
  │    → 1 DRAW CALL cho 100,000 instances!                       │
  │    → GPU tự lấy data từ buffer, không cần CPU per-instance    │
  │                                                                │
  │  Kết quả:                                                      │
  │    Truyền thống: 100,000 draw calls = 500ms (impossible)       │
  │    Instancing:   1 draw call = ~0.5ms (GPU only)               │
  └────────────────────────────────────────────────────────────────┘
```

---

## 7. Tile-Based Rendering — Kiến trúc GPU Mobile

### 6.1. IMR vs TBR

```
Desktop GPU (Immediate Mode Rendering — IMR):
  → Render tam giác → ghi pixel NGAY vào Framebuffer (VRAM)
  → Mỗi pixel ghi = 1 VRAM write = tốn bandwidth
  → VRAM bandwidth cao (504 GB/s) → không sao

Mobile GPU (Tile-Based Rendering — TBR):
  → Chia màn hình thành Tiles (16×16 hoặc 32×32 pixels)
  → Render toàn bộ geometry cho 1 Tile → ghi kết quả TRONG on-chip memory
  → Chỉ ghi ra VRAM 1 lần khi Tile hoàn thành
  → Tiết kiệm bandwidth KHỔNG LỒ (10-20×!)


┌──────────────────────────────────────────────────────────────────┐
│  Immediate Mode (Desktop):              Tile-Based (Mobile):     │
│                                                                  │
│  Tam giác 1: Ghi pixel A,B,C          Binning Phase:            │
│  Tam giác 2: Ghi pixel D,E,F          → Phân tam giác vào Tiles │
│  Tam giác 3: Ghi pixel G,H,I                                    │
│  ...                                   Rendering Phase:          │
│  → N lần ghi VRAM                      Tile 0: [T1,T5,T8]      │
│                                         → Render trên chip       │
│  ┌────────────────┐                     → Ghi 1 lần ra VRAM     │
│  │ VRAM           │                                              │
│  │ bandwidth:     │                    Tile 1: [T2,T3,T7]       │
│  │ 504 GB/s (PC)  │                    → Render trên chip        │
│  │ ~50 GB/s (Mobile)│ ← Bandwidth GẤP 10× thấp hơn!            │
│  └────────────────┘                    ...                       │
│                                                                  │
│  Hệ quả cho Unity Developer:                                    │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  ❌ TRÁNH trên Mobile:                                   │   │
│  │  - Đọc Framebuffer giữa chừng (_CameraOpaqueTexture)    │   │
│  │    → Force flush Tile → ghi ra VRAM → đọc lại = 2× cost │   │
│  │  - RenderTexture.GetTemporary() không cẩn thận           │   │
│  │  - Quá nhiều render passes                                │   │
│  │                                                           │   │
│  │  ✅ DÙNG trên Mobile:                                    │   │
│  │  - Load/Store Actions hiệu quả (DontCare, Clear)         │   │
│  │  - Memoryless render targets (transient attachments)      │   │
│  │  - NativeRenderPass API (URP 12+)                         │   │
│  │  - MSAA (gần như miễn phí trên TBR — resolve trên chip!) │   │
│  └──────────────────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────────────────┘


MSAA trên TBR vs IMR:

  Desktop (IMR):
    MSAA 4× = 4× bandwidth (đọc/ghi 4 samples per pixel vào VRAM)
    → Đắt! (thường dùng FXAA/TAA thay thế)

  Mobile (TBR):
    MSAA 4× = resolve trên Tile Memory (on-chip, cực nhanh!)
    → Chỉ ghi 1 resolved pixel ra VRAM
    → MSAA 4× trên mobile GẦN NHƯ MIỄN PHÍ!
    → Đây là lý do URP default bật MSAA trên mobile.
```

---

## 8. Compute Shaders — GPU không chỉ render

### 7.1. GPGPU trong Unity

```
Compute Shader = Chạy code trên GPU KHÔNG liên quan đến rendering.

Bất kỳ tính toán nào cần XỬ LÝ SONG SONG lượng lớn dữ liệu:
  ✅ Particle simulation (100K+ particles)
  ✅ Frustum/Occlusion culling trên GPU
  ✅ Skinned mesh animation (GPU skinning)
  ✅ Terrain sculpting / erosion
  ✅ AI pathfinding (flow fields)
  ✅ Physics (broad phase collision)
  ✅ Image processing (blur, bloom, color grading)


Thread Group = Tương đương Warp/Wavefront:

  [numthreads(64, 1, 1)]    // 64 threads per group
  void CSMain(uint3 id : SV_DispatchThreadID) {
      float3 pos = _Positions[id.x];
      float3 vel = _Velocities[id.x];
      
      // Simulate particle
      vel.y -= 9.81 * _DeltaTime;     // Gravity
      pos += vel * _DeltaTime;          // Euler integration
      
      _Positions[id.x] = pos;
      _Velocities[id.x] = vel;
  }

  C# dispatch:
  int groups = Mathf.CeilToInt(particleCount / 64.0f);
  computeShader.Dispatch(kernel, groups, 1, 1);

  → 100,000 particles ÷ 64 = 1,563 thread groups
  → GPU xử lý ~5,888 threads đồng thời
  → Hoàn thành trong ~27 "waves"
  → Total: <0.5ms thay vì CPU ~15ms


  ┌─────────────────────────────────────────────────────────────┐
  │  CPU (Burst + Jobs, 8 cores):                               │
  │    100K particles ÷ 8 cores = 12,500 particles/core         │
  │    ~12,500 × 10ns = 0.125ms per core → ~0.15ms total        │
  │                                                             │
  │  GPU (Compute Shader):                                      │
  │    100K particles ÷ 5,888 threads = ~17 "waves"             │
  │    ~17 × 20ns/wave = ~0.34ms                                │
  │                                                             │
  │  → Cho 100K: CPU Burst ≈ GPU Compute                        │
  │  → Cho 1M+: GPU Compute WIN (5,888 >> 8 cores)              │
  │  → BONUS: GPU compute GIẢI PHÓNG CPU cho game logic!        │
  └─────────────────────────────────────────────────────────────┘
```

---

## 9. Shader Optimization — Quy tắc vàng

```
┌─────────────────────────────────────────────────────────────────────┐
│              SHADER OPTIMIZATION CHECKLIST                           │
├──────┬──────────────────────────────────────────────────────────────┤
│  #1  │ GIẢM TEXTURE FETCHES                                        │
│      │ - Pack data: metallic+roughness+AO vào 1 texture (RGB)      │
│      │ - Channel packing: mask vào alpha channel                    │
│      │ - Atlas textures: nhiều sprites trong 1 texture             │
│      │ - Giảm shadow cascade quality khi xa camera                 │
├──────┼──────────────────────────────────────────────────────────────┤
│  #2  │ TRÁNH BRANCH DIVERGENCE                                     │
│      │ - step(), lerp(), smoothstep() thay if/else                 │
│      │ - #pragma multi_compile cho feature toggles                 │
│      │ - Precompute vào lookup texture                             │
├──────┼──────────────────────────────────────────────────────────────┤
│  #3  │ DÙNG PRECISION THẤP KHI ĐỦ                                 │
│      │ - half (16-bit) cho colors, UVs, normals                    │
│      │ - float (32-bit) chỉ cho positions, depth                   │
│      │ - min16float / min16int cho mobile                          │
│      │ → Mobile GPU có native half ALU → 2× throughput!            │
├──────┼──────────────────────────────────────────────────────────────┤
│  #4  │ GIẢM OVERDRAW                                               │
│      │ - Render opaque objects FRONT-TO-BACK (early-z reject)      │
│      │ - Avoid alpha test (clip/discard) khi có thể               │
│      │ - Z-prepass cho complex scenes                              │
│      │ - LOD system (ít triangles ở xa = ít fragments)             │
├──────┼──────────────────────────────────────────────────────────────┤
│  #5  │ TỐI ƯU ALU                                                  │
│      │ - rsqrt() thay 1/sqrt()                                    │
│      │ - mad(a,b,c) thay a*b+c (1 lệnh thay 2)                   │
│      │ - Tránh pow(), sin(), cos() trong fragment shader           │
│      │   → Precompute vào LUT texture                              │
├──────┼──────────────────────────────────────────────────────────────┤
│  #6  │ BANDWIDTH AWARENESS                                         │
│      │ - Texture compression (BC7/ASTC) giảm 4-8× size            │
│      │ - Mipmaps luôn bật (ít texels fetch khi xa)                 │
│      │ - Render Scale < 1.0 cho mobile (FSR upscale)               │
│      │ - Prefer Compute over Fragment cho heavy transforms         │
└──────┴──────────────────────────────────────────────────────────────┘
```

---

## 9. Tổng kết Chapter 4 — GPU trong 1 Frame

```
Bạn nhấn Play. Frame N render:

  ┌──────────────────────────────────────────────────────────────────┐
  │                                                                  │
  │  CPU (Chapter 3):                                                │
  │   ① ECS Systems → ScheduleParallel Jobs → Burst → SIMD          │
  │   ② Camera Culling: Frustum test 10,000 objects → 2,000 visible │
  │   ③ Sort: Opaque front-to-back, Transparent back-to-front       │
  │   ④ Build Command Buffer: ~200 draw calls                       │
  │   ⑤ Submit Command Buffer → GPU qua PCIe/shared memory         │
  │      → CPU bắt đầu frame N+1 NGAY (CPU và GPU chạy song song!) │
  │                                                                  │
  │  GPU:                                                            │
  │   ⑥ Shadow Pass: Render depth từ góc nhìn light → Shadow Map    │
  │   ⑦ Z-Prepass: Render depth từ camera (optional, cho early-z)   │
  │   ⑧ Opaque Pass:                                                │
  │      - Vertex Shader: MVP transform × 500K vertices             │
  │      - Rasterizer: Tam giác → ~4M fragments                     │
  │      - Fragment Shader: PBR lighting × 4M pixels                │
  │      - Early-Z: Reject ~2M fragments (behind other objects)     │
  │   ⑨ Transparent Pass:                                           │
  │      - Back-to-front, alpha blending                             │
  │   ⑩ Post-Processing:                                             │
  │      - Bloom, Color Grading, Tonemapping, FXAA/TAA              │
  │      - (Mỗi pass = fullscreen quad = 2M fragments)              │
  │   ⑪ Final Blit → Framebuffer → Display                          │
  │                                                                  │
  │  Tổng GPU time: ~8ms = 120 FPS ✅                                │
  │  (Bottleneck thường ở Fragment Shader hoặc Bandwidth)            │
  └──────────────────────────────────────────────────────────────────┘
```

> **Bài học thực tiễn:**
> 1. **GPU ≠ faster CPU.** GPU là bộ xử lý song song khổng lồ, giỏi ở throughput, yếu ở latency.
> 2. **Branch = kẻ thù #1** trên GPU. Branchless math (step/lerp/select) luôn ưu tiên.
> 3. **Bandwidth > Compute** trên mobile. Giảm texture fetches, dùng half precision, compression.
> 4. **Draw calls = CPU cost.** SRP Batcher + GPU Instancing + Indirect = giảm CPU overhead.
> 5. **Profile bằng Frame Debugger + GPU Profiler** trước khi tối ưu. Biết bottleneck ở đâu mới fix đúng chỗ.

---

> **Chương tiếp theo:** [Chapter 5 — Unity Case Study]() — Kiến trúc dual-language (C++ Engine + C# Scripting), Mono vs IL2CPP, DOTS full stack, và tổng kết chuỗi Transistor → Frame.

---
*Chapter 4 — Nghiên cứu cho Unity High-Performance Agent*
