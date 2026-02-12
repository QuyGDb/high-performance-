# Bài Thực Hành — Computer Architecture cho Unity Developer

> **Mục tiêu:** Biến kiến thức lý thuyết từ 5 chương thành kỹ năng thực chiến.
> Mỗi Lab có thể chạy trực tiếp trong Unity. Kết quả đo bằng số liệu cụ thể.

---

## Lab 1: Bitwise Operations — Logic Gates trong Code (Chapter 1)

### Mục tiêu
Hiểu rằng `AND`, `OR`, `XOR`, `NOT` trong code C# **chính là** logic gates ở Chapter 1, chạy trên ALU thật.

### Bài 1.1: Bit Flags — Quản lý trạng thái bằng bits

```csharp
// File: BitFlagsLab.cs
using UnityEngine;

/// <summary>
/// BÀI TẬP: Thay vì dùng 8 biến bool riêng lẻ (8 bytes),
/// pack tất cả trạng thái vào 1 byte duy nhất.
/// → Tiết kiệm 8× bộ nhớ + bitwise ops = 1 clock cycle trên ALU.
/// </summary>
public class BitFlagsLab : MonoBehaviour
{
    // Mỗi flag = 1 bit. Tổng cộng 8 flag trong 1 byte.
    [System.Flags]
    public enum UnitState : byte
    {
        None       = 0,         // 0000_0000
        IsAlive    = 1 << 0,    // 0000_0001 = AND gate check bit 0
        IsMoving   = 1 << 1,    // 0000_0010
        IsAttacking= 1 << 2,   // 0000_0100
        IsDefending= 1 << 3,   // 0000_1000
        IsStunned  = 1 << 4,   // 0001_0000
        IsPoisoned = 1 << 5,   // 0010_0000
        IsInvisible= 1 << 6,   // 0100_0000
        IsBoss     = 1 << 7,   // 1000_0000
    }

    UnitState state = UnitState.IsAlive;

    void Start()
    {
        // ═══ BÀI TẬP ═══
        // Hoàn thành các TODO bên dưới bằng bitwise operations.
        // KHÔNG dùng if/else. CHỈ dùng |, &, ^, ~

        // TODO 1: Bật trạng thái IsMoving (dùng OR gate)
        // state = state | UnitState.IsMoving;
        // Giải thích: OR gate → bit nào = 1 sẽ BẬT, bit khác giữ nguyên

        // TODO 2: Kiểm tra unit có đang Attack không? (dùng AND gate)
        // bool attacking = (state & UnitState.IsAttacking) != 0;
        // Giải thích: AND gate → chỉ bit IsAttacking được kiểm tra

        // TODO 3: Toggle IsInvisible (bật↔tắt) (dùng XOR gate)
        // state = state ^ UnitState.IsInvisible;
        // Giải thích: XOR → 0^1=1 (bật), 1^1=0 (tắt)

        // TODO 4: Tắt IsStunned (dùng AND + NOT)
        // state = state & ~UnitState.IsStunned;
        // Giải thích: NOT lật mask → AND xóa bit đó

        // TODO 5: Kiểm tra unit vừa Alive VÀ đang Attack
        // bool canDamage = (state & (UnitState.IsAlive | UnitState.IsAttacking))
        //                  == (UnitState.IsAlive | UnitState.IsAttacking);

        Debug.Log($"State: {state} = {(byte)state:B8}");
        // In ra binary → BẠN ĐANG NHÌN THẤY logic gates output!
    }
}
```

### ✅ Kiểm tra hiểu bài
> Mỗi phép `|`, `&`, `^`, `~` bạn viết → CPU thực thi trên ALU bằng đúng loại gate ở Chapter 1.
> `byte` = 8 bits = 8 transistor pairs xử lý song song trong 1 clock cycle.

---

### Bài 1.2: Bitmask Collision Layers

```csharp
// File: CollisionMaskLab.cs
using UnityEngine;

/// <summary>
/// Unity LayerMask hoạt động CHÍNH XÁC theo nguyên lý này.
/// Physics.Raycast dùng AND gate để check layer mask ở mức phần cứng.
/// </summary>
public class CollisionMaskLab : MonoBehaviour
{
    // 32 layers = 32 bits = 1 uint (register size trên CPU 32-bit)
    const uint Layer_Player    = 1u << 0;   // Layer 0
    const uint Layer_Enemy     = 1u << 1;   // Layer 1
    const uint Layer_Bullet    = 1u << 2;   // Layer 2
    const uint Layer_Wall      = 1u << 3;   // Layer 3
    const uint Layer_Trigger   = 1u << 4;   // Layer 4

    void Start()
    {
        // ═══ BÀI TẬP ═══

        // TODO 1: Tạo mask để Bullet chỉ va chạm với Enemy và Wall
        // uint bulletMask = Layer_Enemy | Layer_Wall;

        // TODO 2: Kiểm tra 1 object (layer=Enemy) có nằm trong mask không
        // uint objectLayer = Layer_Enemy;
        // bool willCollide = (objectLayer & bulletMask) != 0;
        // → AND gate: nếu BẤT KỲ bit nào trùng → va chạm!

        // TODO 3: Tạo mask "tất cả trừ Trigger"
        // uint allExceptTrigger = ~Layer_Trigger;
        // → NOT gate: lật toàn bộ 32 bits

        // TODO 4: Kết hợp 2 masks
        // uint combinedMask = bulletMask | Layer_Player;
        // → OR gate: merge 2 masks

        // HW Connection: Unity's Physics engine dùng CHÍNH XÁC phép AND
        // này trên uint32 để check collision layers. 1 instruction = 1 cycle!
    }
}
```

---

## Lab 2: Cache Locality Benchmark (Chapter 2)

### Mục tiêu
ĐO LƯỜNG sự khác biệt giữa truy cập bộ nhớ tuần tự vs ngẫu nhiên. Chứng minh Cache Line 64 bytes bằng số liệu thực.

### Bài 2.1: Sequential vs Random Access

```csharp
// File: CacheLocalityBenchmark.cs
using UnityEngine;
using System.Diagnostics;
using Debug = UnityEngine.Debug;

/// <summary>
/// BÀI TẬP: Chạy test này và quan sát sự khác biệt thời gian.
/// Sau đó giải thích TẠI SAO bằng kiến thức Cache Line từ Chapter 2.
/// </summary>
public class CacheLocalityBenchmark : MonoBehaviour
{
    const int SIZE = 1_000_000; // 1 triệu phần tử

    void Start()
    {
        // ═══ TEST 1: Sequential Access (Cache-friendly) ═══
        float[] data = new float[SIZE];
        var sw = Stopwatch.StartNew();

        float sum = 0;
        for (int i = 0; i < SIZE; i++)
        {
            sum += data[i]; // Truy cập tuần tự: data[0], data[1], data[2], ...
        }
        sw.Stop();
        long sequentialMs = sw.ElapsedTicks;

        // ═══ TEST 2: Random Access (Cache-unfriendly) ═══
        int[] indices = new int[SIZE];
        for (int i = 0; i < SIZE; i++) indices[i] = i;
        // Shuffle indices (Fisher-Yates)
        var rng = new System.Random(42);
        for (int i = SIZE - 1; i > 0; i--)
        {
            int j = rng.Next(i + 1);
            (indices[i], indices[j]) = (indices[j], indices[i]);
        }

        sw.Restart();
        sum = 0;
        for (int i = 0; i < SIZE; i++)
        {
            sum += data[indices[i]]; // Truy cập ngẫu nhiên: nhảy lung tung!
        }
        sw.Stop();
        long randomMs = sw.ElapsedTicks;

        Debug.Log($"Sequential: {sequentialMs} ticks");
        Debug.Log($"Random:     {randomMs} ticks");
        Debug.Log($"Ratio:      {(float)randomMs / sequentialMs:F1}× slower");

        // ═══ CÂU HỎI ═══
        // Q1: Tại sao Random chậm hơn? (Gợi ý: Cache Miss)
        // Q2: Mỗi float = 4 bytes. Cache Line = 64 bytes.
        //     Sequential access sẽ hit cache bao nhiêu % ?
        //     (64 / 4 = 16 floats per cache line → 15/16 = 93.75% hit rate!)
        // Q3: Random access cache hit rate? (Gần 0% vì mỗi access = new line)
    }
}
```

### Bài 2.2: AOS vs SOA — Chứng minh ECS Layout

```csharp
// File: AOSvsSOABenchmark.cs
using UnityEngine;
using System.Diagnostics;
using Debug = UnityEngine.Debug;

/// <summary>
/// BÀI TẬP: Chứng minh tại sao ECS (SOA) nhanh hơn MonoBehaviour (AOS).
/// Đo thời gian duyệt Position trong 2 layout khác nhau.
/// </summary>
public class AOSvsSOABenchmark : MonoBehaviour
{
    const int COUNT = 500_000;

    // ═══ AOS Layout (Array of Structs) — giống MonoBehaviour ═══
    struct EnemyAOS
    {
        public float posX, posY, posZ;          // 12 bytes — CẦN
        public float velX, velY, velZ;          // 12 bytes — CẦN
        public float health;                     // 4 bytes  — KHÔNG CẦN cho movement
        public int   state;                      // 4 bytes  — KHÔNG CẦN
        public float attackRange;                // 4 bytes  — KHÔNG CẦN
        public float armor;                      // 4 bytes  — KHÔNG CẦN
        // Total: 40 bytes, nhưng chỉ cần 24 bytes (pos+vel) = 40% lãng phí!
    }

    // ═══ SOA Layout (Struct of Arrays) — giống ECS ═══
    struct PositionSOA { public float x, y, z; } // 12 bytes — PACKED
    struct VelocitySOA { public float x, y, z; } // 12 bytes — PACKED

    void Start()
    {
        // --- Setup AOS ---
        EnemyAOS[] enemies = new EnemyAOS[COUNT];
        for (int i = 0; i < COUNT; i++)
        {
            enemies[i].posX = i; enemies[i].posY = 0; enemies[i].posZ = 0;
            enemies[i].velX = 1; enemies[i].velY = 0; enemies[i].velZ = 0;
        }

        // --- Setup SOA ---
        PositionSOA[] positions = new PositionSOA[COUNT];
        VelocitySOA[] velocities = new VelocitySOA[COUNT];
        for (int i = 0; i < COUNT; i++)
        {
            positions[i].x = i; positions[i].y = 0; positions[i].z = 0;
            velocities[i].x = 1; velocities[i].y = 0; velocities[i].z = 0;
        }

        float dt = 0.016f;

        // --- Benchmark AOS ---
        var sw = Stopwatch.StartNew();
        for (int i = 0; i < COUNT; i++)
        {
            enemies[i].posX += enemies[i].velX * dt;
            enemies[i].posY += enemies[i].velY * dt;
            enemies[i].posZ += enemies[i].velZ * dt;
            // Mỗi iteration load 40 bytes, dùng 24 = 40% waste
        }
        sw.Stop();
        long aosTicks = sw.ElapsedTicks;

        // --- Benchmark SOA ---
        sw.Restart();
        for (int i = 0; i < COUNT; i++)
        {
            positions[i].x += velocities[i].x * dt;
            positions[i].y += velocities[i].y * dt;
            positions[i].z += velocities[i].z * dt;
            // Mỗi iteration load 24 bytes, dùng 24 = 0% waste!
        }
        sw.Stop();
        long soaTicks = sw.ElapsedTicks;

        Debug.Log($"AOS (MonoBehaviour-like): {aosTicks} ticks");
        Debug.Log($"SOA (ECS-like):           {soaTicks} ticks");
        Debug.Log($"SOA speedup:              {(float)aosTicks / soaTicks:F2}×");

        // ═══ CÂU HỎI ═══
        // Q1: Tại sao SOA nhanh hơn? (Cache Line utilization)
        // Q2: AOS struct = 40 bytes. Cache Line = 64 bytes.
        //     Bao nhiêu enemies fit trong 1 cache line? (64/40 = 1.6 → chỉ 1!)
        //     SOA: (pos=12B) → 64/12 = 5.3 → 5 positions per cache line!
        // Q3: Nếu thêm 10 fields vào EnemyAOS (total 120B), speedup tăng hay giảm?
        //     (Tăng! Vì AOS waste càng nhiều, SOA không bị ảnh hưởng)
    }
}
```

---

## Lab 3: Branch Prediction & Burst (Chapter 3)

### Mục tiêu
Đo chi phí branch misprediction, viết branchless code, và so sánh Mono vs Burst output.

### Bài 3.1: Sorted vs Unsorted — Branch Prediction

```csharp
// File: BranchPredictionLab.cs
using UnityEngine;
using System.Diagnostics;
using Debug = UnityEngine.Debug;

/// <summary>
/// BÀI TẬP KINH ĐIỂN: Tại sao xử lý mảng ĐÃ SORT nhanh hơn mảng CHƯA SORT?
/// (Đây là câu hỏi nổi tiếng nhất trên StackOverflow!)
/// </summary>
public class BranchPredictionLab : MonoBehaviour
{
    const int SIZE = 1_000_000;
    const int ITERATIONS = 10;

    void Start()
    {
        int[] data = new int[SIZE];
        var rng = new System.Random(42);
        for (int i = 0; i < SIZE; i++)
            data[i] = rng.Next(0, 256); // Random 0-255

        // ═══ TEST 1: Unsorted ═══
        long sum = 0;
        var sw = Stopwatch.StartNew();
        for (int iter = 0; iter < ITERATIONS; iter++)
        {
            for (int i = 0; i < SIZE; i++)
            {
                if (data[i] >= 128) // ← Branch: 50% chance → UNPREDICTABLE!
                    sum += data[i];
            }
        }
        sw.Stop();
        long unsortedTicks = sw.ElapsedTicks;

        // ═══ TEST 2: Sorted ═══
        System.Array.Sort(data);
        sum = 0;
        sw.Restart();
        for (int iter = 0; iter < ITERATIONS; iter++)
        {
            for (int i = 0; i < SIZE; i++)
            {
                if (data[i] >= 128) // ← Branch: PREDICTABLE! (000...111...)
                    sum += data[i];
            }
        }
        sw.Stop();
        long sortedTicks = sw.ElapsedTicks;

        Debug.Log($"Unsorted: {unsortedTicks} ticks (branch misprediction!)");
        Debug.Log($"Sorted:   {sortedTicks} ticks (branch predicted!)");
        Debug.Log($"Ratio:    {(float)unsortedTicks / sortedTicks:F1}× slower unsorted");

        // ═══ CÂU HỎI ═══
        // Q1: Tại sao sorted nhanh hơn? (Chapter 3: Branch Predictor pattern)
        //     Sorted: [0,0,0,...,128,129,...,255] → predictor học "not taken" rồi "taken"
        //     Unsorted: [random] → predictor đoán sai ~50% = pipeline flush!
        // Q2: Pipeline flush cost bao nhiêu cycles? (15-20 trên modern CPU)
        // Q3: Nếu threshold = 1 (hầu hết >= 1), kết quả thay đổi thế nào?
        //     (Cả 2 nhanh như nhau! Vì predictor luôn đoán "taken" đúng ~99%)
    }
}
```

### Bài 3.2: Branchless — Loại bỏ branch hoàn toàn

```csharp
// File: BranchlessLab.cs
using UnityEngine;
using Unity.Mathematics;
using Unity.Burst;
using Unity.Jobs;
using Unity.Collections;
using System.Diagnostics;
using Debug = UnityEngine.Debug;

/// <summary>
/// BÀI TẬP: So sánh if/else vs branchless math.select() trong Burst Job.
/// Sau đó mở Burst Inspector xem assembly → tìm lệnh CMOV hoặc VBLENDPS.
/// </summary>
public class BranchlessLab : MonoBehaviour
{
    const int COUNT = 1_000_000;

    // ═══ Job 1: Có Branch ═══
    [BurstCompile]
    struct BranchedJob : IJobParallelFor
    {
        [ReadOnly] public NativeArray<float> healths;
        public NativeArray<float> damages;

        public void Execute(int i)
        {
            // if/else → Burst tạo branch instruction → có thể misprediction
            if (healths[i] > 50f)
                damages[i] = 10f;  // Khỏe → dame 10
            else
                damages[i] = 25f;  // Yếu → dame 25 (mercy kill)
        }
    }

    // ═══ Job 2: Branchless ═══
    [BurstCompile]
    struct BranchlessJob : IJobParallelFor
    {
        [ReadOnly] public NativeArray<float> healths;
        public NativeArray<float> damages;

        public void Execute(int i)
        {
            // math.select → Burst tạo CMOV hoặc VBLENDPS → NO BRANCH!
            damages[i] = math.select(25f, 10f, healths[i] > 50f);
        }
    }

    void Start()
    {
        var healths = new NativeArray<float>(COUNT, Allocator.TempJob);
        var damages1 = new NativeArray<float>(COUNT, Allocator.TempJob);
        var damages2 = new NativeArray<float>(COUNT, Allocator.TempJob);

        // Random health → 50% chance → worst case cho branch predictor
        var rng = new System.Random(42);
        for (int i = 0; i < COUNT; i++)
            healths[i] = (float)(rng.NextDouble() * 100.0);

        // Benchmark
        var sw = Stopwatch.StartNew();
        new BranchedJob { healths = healths, damages = damages1 }
            .Schedule(COUNT, 64).Complete();
        sw.Stop();
        long branchedTicks = sw.ElapsedTicks;

        sw.Restart();
        new BranchlessJob { healths = healths, damages = damages2 }
            .Schedule(COUNT, 64).Complete();
        sw.Stop();
        long branchlessTicks = sw.ElapsedTicks;

        Debug.Log($"Branched:   {branchedTicks} ticks");
        Debug.Log($"Branchless: {branchlessTicks} ticks");
        Debug.Log($"Speedup:    {(float)branchedTicks / branchlessTicks:F2}×");

        healths.Dispose();
        damages1.Dispose();
        damages2.Dispose();

        // ═══ BÀI TẬP THÊM ═══
        // 1. Mở Burst Inspector (Jobs → Burst → Open Inspector)
        // 2. Tìm BranchedJob → tab Assembly → tìm lệnh "jg", "jle" (branch)
        // 3. Tìm BranchlessJob → tab Assembly → tìm "vblendvps" hoặc "cmov"
        // 4. So sánh: Branchless KHÔNG có jump → pipeline KHÔNG bao giờ flush!
    }
}
```

### Bài 3.3: GC Pressure — Tạo rác vs Zero-GC

```csharp
// File: GCPressureLab.cs
using UnityEngine;
using Unity.Collections;
using System.Collections.Generic;

/// <summary>
/// BÀI TẬP: Chạy trong Play Mode và mở Profiler (Window → Analysis → Profiler).
/// Quan sát GC.Alloc ở "GC Allocation" column.
/// </summary>
public class GCPressureLab : MonoBehaviour
{
    // ═══ CÁC "TỘI ĐỒ" GC ═══

    // Tội đồ 1: String concatenation mỗi frame
    string status;

    // Tội đồ 2: List tạo mới mỗi frame
    List<int> nearbyEnemies;

    // Tội đồ 3: Lambda / closure
    System.Action cachedAction;

    // ═══ PHIÊN BẢN ZERO-GC ═══
    // Fix 1: StringBuilder (tái dùng)
    System.Text.StringBuilder sb = new System.Text.StringBuilder(128);

    // Fix 2: List tạo 1 lần, Clear() mỗi frame
    List<int> nearbyEnemiesPooled = new List<int>(100);

    // Fix 3: NativeArray thay managed array
    NativeArray<int> nativeResults;

    bool useGCFriendly = false;

    void OnEnable()
    {
        nativeResults = new NativeArray<int>(100, Allocator.Persistent);
    }

    void OnDisable()
    {
        if (nativeResults.IsCreated) nativeResults.Dispose();
    }

    void Update()
    {
        if (!useGCFriendly)
        {
            // ══ BAD: Tạo rác mỗi frame ══

            // GC: ~100 bytes/frame (string allocation)
            status = "Health: " + 100 + " | Mana: " + 50;

            // GC: ~300 bytes/frame (new List + add)
            nearbyEnemies = new List<int>();
            for (int i = 0; i < 50; i++)
                nearbyEnemies.Add(i);

            // GC: ~100 bytes/frame (lambda closure boxing)
            int capturedValue = Time.frameCount;
            cachedAction = () => Debug.Log(capturedValue);
        }
        else
        {
            // ══ GOOD: Zero GC ══

            // 0 bytes: StringBuilder reuse
            sb.Clear();
            sb.Append("Health: ").Append(100).Append(" | Mana: ").Append(50);
            // status = sb.ToString(); // Nếu cần string thì vẫn alloc!

            // 0 bytes: Clear + reuse
            nearbyEnemiesPooled.Clear();
            for (int i = 0; i < 50; i++)
                nearbyEnemiesPooled.Add(i);

            // 0 bytes: NativeArray (unmanaged heap)
            for (int i = 0; i < 50; i++)
                nativeResults[i] = i;
        }
    }

    // ═══ BÀI TẬP ═══
    // 1. Enter Play Mode với useGCFriendly = false
    // 2. Mở Profiler → CPU → chọn "GC Alloc" column
    // 3. Quan sát GC spike mỗi vài giây (Stop-the-world!)
    // 4. Đổi useGCFriendly = true → GC.Alloc = 0!
    // 5. CÂU HỎI: Tại sao NativeArray không gây GC? (Chapter 2: Unmanaged heap)
}
```

---

## Lab 4: GPU & Shader Performance (Chapter 4)

### Mục tiêu
Đo ảnh hưởng thực tế của branch divergence trong shader, và thực hành tối ưu bằng branchless math.

### Bài 4.1: Branch Divergence trong Shader

```hlsl
// File: BranchDivergenceLab.shader
Shader "Lab/BranchDivergence"
{
    Properties
    {
        _MainTex ("Texture", 2D) = "white" {}
        _Threshold ("Threshold", Range(0, 1)) = 0.5
        [Toggle] _UseBranch ("Use Branch (slower)", Float) = 1
    }

    SubShader
    {
        Tags { "RenderPipeline" = "UniversalPipeline" "RenderType" = "Opaque" }

        Pass
        {
            HLSLPROGRAM
            #pragma vertex vert
            #pragma fragment frag
            #pragma multi_compile _ _USEBRANCH_ON

            #include "Packages/com.unity.render-pipelines.universal/ShaderLibrary/Core.hlsl"

            struct Attributes { float4 posOS : POSITION; float2 uv : TEXCOORD0; };
            struct Varyings  { float4 posCS : SV_POSITION; float2 uv : TEXCOORD0; };

            TEXTURE2D(_MainTex);
            SAMPLER(sampler_MainTex);
            float _Threshold;

            Varyings vert(Attributes IN)
            {
                Varyings OUT;
                OUT.posCS = TransformObjectToHClip(IN.posOS.xyz);
                OUT.uv = IN.uv;
                return OUT;
            }

            half4 frag(Varyings IN) : SV_Target
            {
                half4 color = SAMPLE_TEXTURE2D(_MainTex, sampler_MainTex, IN.uv);
                half luminance = dot(color.rgb, half3(0.2126, 0.7152, 0.0722));

                #ifdef _USEBRANCH_ON
                // ❌ BAD: Branch Divergence!
                // Các pixels trong cùng 1 Warp (32 threads) có luminance khác nhau
                // → Một số đi nhánh A, một số đi nhánh B
                // → GPU phải chạy CẢ HAI nhánh tuần tự!
                if (luminance > _Threshold)
                {
                    // Nhánh A: Complex color grading (đắt)
                    color.rgb = pow(color.rgb, 2.2);
                    color.rgb *= half3(1.2, 1.1, 0.9);
                    color.rgb = pow(color.rgb, 1.0 / 2.2);
                }
                else
                {
                    // Nhánh B: Desaturate (rẻ hơn nhưng GPU vẫn phải chờ)
                    color.rgb = luminance.xxx * half3(0.5, 0.5, 0.8);
                }
                #else
                // ✅ GOOD: Branchless! Tất cả threads chạy CÙNG code path.
                half mask = step(_Threshold, luminance);

                // Nhánh A result
                half3 graded = pow(color.rgb, 2.2);
                graded *= half3(1.2, 1.1, 0.9);
                graded = pow(graded, 1.0 / 2.2);

                // Nhánh B result
                half3 desat = luminance.xxx * half3(0.5, 0.5, 0.8);

                // Blend thay vì branch
                color.rgb = lerp(desat, graded, mask);
                #endif

                return color;
            }
            ENDHLSL
        }
    }
}

// ═══ BÀI TẬP ═══
// 1. Tạo material dùng shader này, gán texture bất kỳ
// 2. Tạo Plane + gán material
// 3. Mở Frame Debugger (Window → Analysis → Frame Debugger)
// 4. Toggle _UseBranch bật/tắt → so sánh GPU time trong Profiler
// 5. CÂU HỎI: Với _Threshold = 0.5, bao nhiêu % pixels diverge?
//    (Gợi ý: phụ thuộc texture — ảnh đồng màu = ít diverge)
```

### Bài 4.2: Draw Call Benchmark

```csharp
// File: DrawCallBenchmark.cs
using UnityEngine;

/// <summary>
/// BÀI TẬP: Spawn objects theo 3 cách và đo draw calls trong Stats window.
/// </summary>
public class DrawCallBenchmark : MonoBehaviour
{
    public Mesh mesh;
    public Material material;          // Cùng material cho instancing
    public Material[] materials;       // Khác material mỗi object (worst case)

    [Range(100, 5000)]
    public int objectCount = 1000;

    public enum Mode { Worst_DifferentMaterials, Better_SameMaterial, Best_GPUInstancing }
    public Mode mode = Mode.Worst_DifferentMaterials;

    void Start()
    {
        switch (mode)
        {
            case Mode.Worst_DifferentMaterials:
                // ═══ WORST: Mỗi object 1 material → 1000 draw calls! ═══
                for (int i = 0; i < objectCount; i++)
                {
                    var go = GameObject.CreatePrimitive(PrimitiveType.Cube);
                    go.transform.position = Random.insideUnitSphere * 20f;
                    // Mỗi object renderer khác material instance
                    go.GetComponent<Renderer>().material.color = Random.ColorHSV();
                    // ↑ .material tạo COPY mới = material instance MỚI = draw call MỚI
                }
                break;

            case Mode.Better_SameMaterial:
                // ═══ BETTER: Cùng material → SRP Batcher gom ═══
                for (int i = 0; i < objectCount; i++)
                {
                    var go = GameObject.CreatePrimitive(PrimitiveType.Cube);
                    go.transform.position = Random.insideUnitSphere * 20f;
                    go.GetComponent<Renderer>().sharedMaterial = material;
                    // ↑ .sharedMaterial = CÙNG material → SRP Batcher!
                }
                break;

            case Mode.Best_GPUInstancing:
                // ═══ BEST: GPU Instancing → 1 draw call! ═══
                if (material != null)
                    material.enableInstancing = true;
                for (int i = 0; i < objectCount; i++)
                {
                    var go = GameObject.CreatePrimitive(PrimitiveType.Cube);
                    go.transform.position = Random.insideUnitSphere * 20f;
                    go.GetComponent<Renderer>().sharedMaterial = material;
                }
                break;
        }
    }

    // ═══ BÀI TẬP ═══
    // 1. Chạy Mode = Worst → mở Stats window (Game tab → Stats)
    //    → Ghi số Batches và SetPass Calls
    // 2. Chạy Mode = Better → so sánh Batches giảm bao nhiêu?
    // 3. Chạy Mode = Best → GPU Instancing → Batches = ?
    // 4. Tăng objectCount lên 5000 → mode nào FPS ổn nhất?
    // 5. CÂU HỎI: Tại sao .material gây draw call mới? (Chapter 4: State Change)
}
```

---

## Lab 5: Full DOTS Pipeline (Chapter 5)

### Mục tiêu
Xây dựng 1 system hoàn chỉnh bằng DOTS, sau đó mở Burst Inspector phân tích assembly output.

### Bài 5.1: MonoBehaviour vs DOTS — Head-to-Head

```csharp
// ═══ FILE 1: MonoBehaviourEnemy.cs ═══
using UnityEngine;

/// <summary>
/// PHẦN 1: Implement movement bằng MonoBehaviour truyền thống.
/// Spawn 10,000 objects → đo ms/frame trong Profiler.
/// </summary>
public class MonoBehaviourEnemy : MonoBehaviour
{
    public Vector3 velocity;

    void Update()
    {
        // Mỗi enemy gọi Update() riêng → 10K virtual calls
        // transform.position = managed→native transition
        // Vector3 = không SIMD
        transform.position += velocity * Time.deltaTime;
    }
}

// Spawner:
// for (int i = 0; i < 10000; i++) {
//     var go = new GameObject("Enemy" + i);
//     go.AddComponent<MonoBehaviourEnemy>().velocity =
//         Random.insideUnitSphere * 5f;
// }
```

```csharp
// ═══ FILE 2: ECS Version — Components ═══
// File: MoveComponents.cs
using Unity.Entities;
using Unity.Mathematics;

// Pure data — không logic, không inheritance
public struct MoveSpeed : IComponentData
{
    public float3 velocity;
}

// Tag component — zero bytes, chỉ dùng để filter
public struct EnemyTag : IComponentData { }
```

```csharp
// ═══ FILE 3: ECS Version — System ═══
// File: MoveSystem.cs
using Unity.Burst;
using Unity.Entities;
using Unity.Mathematics;
using Unity.Transforms;

[BurstCompile]
public partial struct MoveSystem : ISystem
{
    [BurstCompile]
    public void OnUpdate(ref SystemState state)
    {
        float dt = SystemAPI.Time.DeltaTime;

        // ScheduleParallel → phân chia cho TẤT CẢ CPU cores
        // Burst → AVX2 SIMD: 8 entities per instruction
        // ECS query → iterate trực tiếp trên Archetype Chunks
        new MoveJob { deltaTime = dt }.ScheduleParallel();
    }

    [BurstCompile]
    partial struct MoveJob : IJobEntity
    {
        public float deltaTime;

        // RefRW = read+write reference vào chunk memory (zero copy!)
        // RefRO = read-only → cho phép parallel access
        void Execute(ref LocalTransform transform, in MoveSpeed speed)
        {
            transform.Position += speed.velocity * deltaTime;
        }
    }
}

// ═══ BÀI TẬP ═══
// 1. Implement BOTH versions (MonoBehaviour + DOTS)
// 2. Spawn 10,000 entities mỗi bên
// 3. Mở Profiler → CPU tab → so sánh ms/frame:
//    - MonoBehaviour.Update (dự đoán: ~5-8ms)
//    - MoveSystem (dự đoán: ~0.05-0.1ms)
// 4. Mở Burst Inspector → tìm MoveJob → xem Assembly:
//    - Tìm lệnh VFMADD hoặc VADDPS → đó là SIMD!
//    - Đếm instructions per entity → so sánh với dự đoán Chapter 3
// 5. CÂU HỎI:
//    Q1: Speedup thực tế là bao nhiêu ×?
//    Q2: Tách thành ba phần: Cache (ECS), SIMD (Burst), Parallel (Jobs)
//        → Ước tính mỗi phần đóng góp bao nhiêu %?
//    Q3: Nếu tắt [BurstCompile], speedup giảm bao nhiêu?
//    Q4: Nếu dùng .Schedule() thay .ScheduleParallel(), mất mấy ×?
```

---

## Bảng điểm tự đánh giá

```
┌──────┬──────────────────────────────────────────────┬──────────┐
│ Lab  │ Tiêu chí "Đạt"                                │ Chương   │
├──────┼──────────────────────────────────────────────┼──────────┤
│ 1.1  │ Viết đúng 5 bitwise operations               │ Ch.1     │
│ 1.2  │ Giải thích AND gate ↔ LayerMask               │ Ch.1     │
│ 2.1  │ Random/Sequential ratio > 3×                  │ Ch.2     │
│ 2.2  │ SOA nhanh hơn AOS, giải thích bằng Cache Line │ Ch.2     │
│ 3.1  │ Sorted nhanh hơn 2-5×, giải thích prediction  │ Ch.3     │
│ 3.2  │ Tìm được CMOV/VBLENDPS trong Burst Inspector  │ Ch.3     │
│ 3.3  │ Profiler hiển thị GC.Alloc = 0 cho fixed code │ Ch.3     │
│ 4.1  │ Branch shader chậm hơn branchless (GPU time)  │ Ch.4     │
│ 4.2  │ Batches giảm 10-50× khi dùng Instancing       │ Ch.4     │
│ 5.1  │ DOTS nhanh hơn MonoBehaviour > 50×             │ Ch.5     │
│ 5.1+ │ Tìm được VFMADD trong Burst Inspector output  │ Ch.3+5   │
└──────┴──────────────────────────────────────────────┴──────────┘
```

---

> **Lời khuyên:** Đừng chỉ chạy code và nhìn kết quả. Trước khi chạy, hãy **DỰ ĐOÁN** kết quả dựa trên kiến thức từ 5 chương. Nếu dự đoán SAI → đó là lúc bạn học được nhiều nhất. 

---
*Practical Labs — Unity High-Performance Agent*
