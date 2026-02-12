# Kiến trúc Máy tính — Từ Transistor đến Unity Engine

> Tài liệu nghiên cứu toàn diện cho Unity High-Performance Developer.
> Mỗi chương đi sâu vào 1 tầng của computing stack, với ví dụ thực tế, ASCII diagrams, và kết nối trực tiếp đến DOTS/ECS/Burst.

---

## Mục lục

| # | Chương | Nội dung chính | File |
|---|--------|---------------|------|
| 1 | [Transistor & Logic Gates](ComputerArchitecture/Chapter1_Transistor_LogicGates.md) | MOSFET, CMOS, Logic Gates, Half/Full Adder, ALU | `Chapter1_Transistor_LogicGates.md` |
| 2 | [Memory & Storage](ComputerArchitecture/Chapter2_Memory_Storage.md) | Flip-flops, Registers, SRAM/DRAM, Cache Lines, False Sharing, MESI, ECS Cache Locality | `Chapter2_Memory_Storage.md` |
| 3 | [CPU, ISA & Languages](ComputerArchitecture/Chapter3_CPU_ISA_Languages.md) | CISC/RISC, Assembly/SIMD, Pipeline, Branch Prediction, Call Stack, Mono/IL2CPP/Burst, GC | `Chapter3_CPU_ISA_Languages.md` |
| 4 | [GPU & Rendering Pipeline](ComputerArchitecture/Chapter4_GPU_RenderingPipeline.md) | SM/CUDA Cores, SIMT, Branch Divergence, GPU Memory, Full Pipeline, Draw Calls, Batching, TBR, Compute Shaders | `Chapter4_GPU_RenderingPipeline.md` |
| 5 | [Unity Case Study](ComputerArchitecture/Chapter5_Unity_CaseStudy.md) | Dual-Language Architecture, C#↔C++ Binding, Mono vs IL2CPP, DOTS (ECS+Jobs+Burst), Transistor→Frame Walkthrough | `Chapter5_Unity_CaseStudy.md` |

---

## Hành trình tổng hợp

```
Electron → Transistor → Logic Gate → ALU → CPU Core
     → Cache → RAM → Assembly → C++ → C# → IL → Burst/IL2CPP
          → Native SIMD code → Multi-core Jobs → ECS Chunks
               → Command Buffer → GPU Pipeline → Pixels
                    → Display → MẮT NGƯỜI (60 lần/giây)
```

Toàn bộ chuỗi diễn ra trong **16.67 milliseconds** (60 FPS).

---

## Quick Reference

| Khái niệm | Ảnh hưởng trong Unity |
|:-----------|:---------------------|
| Cache Line 64B | ECS Chunks: contiguous → Cache Hit 95%+ |
| Branch Prediction | `math.select()` thay `if/else` trong Burst |
| SIMD (AVX2) | Burst: 8 entities/instruction |
| False Sharing | Mỗi Job có read/write set riêng |
| GC Stop-the-World | Zero alloc: NativeArray, struct, pool |
| Branch Divergence | Branchless shader: `step()`, `lerp()` |
| Bandwidth (GPU) | ASTC compression, half precision, LODs |
| Draw Calls | SRP Batcher + Instancing + Indirect |
| TBR (Mobile) | Minimize render passes, MSAA miễn phí |
| Managed↔Native | Cache refs ở Awake, prefer DOTS queries |
| IL2CPP vs Mono | Dev=Mono, Build=IL2CPP, HotPath=Burst |

---
*Nghiên cứu cho Unity High-Performance Agent*
