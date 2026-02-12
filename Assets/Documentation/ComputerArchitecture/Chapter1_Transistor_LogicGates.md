# Chương 1: Transistor & Logic Gates — Từ Electron đến Tính toán

> **Mục tiêu chương:** Hiểu cách một linh kiện vật lý nhỏ bé (transistor) tạo ra nền tảng cho MỌI phép tính trong máy tính — từ phép cộng đơn giản đến việc render hàng triệu polygon trong Unity.

---

## 1. Tại sao phải bắt đầu từ đây?

Khi bạn viết dòng code C# này trong Unity:

```csharp
float3 newPosition = currentPosition + velocity * deltaTime;
```

Bên dưới mọi abstraction layer, phép cộng và nhân đó **thực sự xảy ra** bên trong các mạch transistor vật lý. Không có phép màu — chỉ có electron chạy qua các công tắc bán dẫn, theo quy luật vật lý.

Hiểu điều này giúp bạn trả lời câu hỏi: **"Tại sao cách tôi tổ chức dữ liệu lại ảnh hưởng đến tốc độ?"** — bởi vì mọi thứ cuối cùng đều quay về cách phần cứng xử lý tín hiệu điện.

---

## 2. Chất bán dẫn — Vật liệu nền tảng

### 2.1. Ba loại vật liệu dẫn điện

| Loại | Đặc điểm | Ví dụ |
| :--- | :--- | :--- |
| **Dẫn điện (Conductor)** | Electron di chuyển tự do | Đồng (Cu), Nhôm (Al), Vàng (Au) |
| **Cách điện (Insulator)** | Electron bị giữ chặt, không di chuyển | Cao su, Thủy tinh, Nhựa |
| **Bán dẫn (Semiconductor)** | **Có thể bật/tắt** khả năng dẫn điện | Silicon (Si), Germanium (Ge) |

### 2.2. Silicon — "Đất" của ngành công nghiệp chip

Silicon (Si) là nguyên tố phổ biến thứ 2 trên vỏ Trái Đất (sau Oxy). Ở trạng thái nguyên chất, nó **gần như không dẫn điện**. Nhưng khi ta "pha tạp" (doping) thêm các nguyên tố khác, nó trở thành vật liệu kỳ diệu:

```
Silicon nguyên chất (4 electron lớp ngoài):

    Si --- Si --- Si --- Si
    |      |      |      |
    Si --- Si --- Si --- Si      ← Liên kết cộng hóa trị bền vững
    |      |      |      |         Không có electron tự do → KHÔNG dẫn điện
    Si --- Si --- Si --- Si


Pha tạp loại N (thêm Phosphorus - 5 electron):

    Si --- Si --- Si --- Si
    |      |      |      |
    Si --- [P]•── Si --- Si      ← Phosphorus có 5 electron, 4 liên kết với Si
    |      |      |      |         Thừa 1 electron tự do (•) → DẪN ĐIỆN (mang điện âm)
    Si --- Si --- Si --- Si


Pha tạp loại P (thêm Boron - 3 electron):

    Si --- Si --- Si --- Si
    |      |      |      |
    Si --- [B]○── Si --- Si      ← Boron có 3 electron, thiếu 1 liên kết
    |      |      |      |         Tạo "lỗ trống" (○) → DẪN ĐIỆN (mang điện dương)
    Si --- Si --- Si --- Si
```

> **Điểm mấu chốt:** Bằng cách kết hợp vùng N và vùng P, ta tạo ra "cửa" cho phép hoặc chặn dòng electron đi qua. Đó chính là nguyên lý của transistor.

---

## 3. MOSFET — Transistor hiện đại

### 3.1. Cấu tạo MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor)

MOSFET là loại transistor phổ biến nhất, chiếm **99%** transistor trong CPU/GPU hiện đại.

```
                         Gate (Cổng điều khiển)
                           │
                     ┌─────┴─────┐
                     │  Metal    │
                     ├───────────┤
                     │  Oxide    │   ← SiO₂ (Lớp cách điện siêu mỏng, ~1-2nm)
                     │  (SiO₂)  │
   ──────────────────┴───────────┴──────────────────
   │    Source (N)    │  Channel  │    Drain (N)    │
   │  (Vùng N-type)  │  (P-type) │  (Vùng N-type)  │
   └─────────────────┴───────────┴─────────────────┘
                      Substrate (P-type Nền Silicon)
                           │
                         Body (Nối đất)
```

### 3.2. Hoạt động — Như một vòi nước điện tử

Hãy tưởng tượng MOSFET như **vòi nước**:

```
┌──────────────────────────────────────────────────────────────────┐
│                     MOSFET = VÒI NƯỚC                            │
│                                                                  │
│    Source (Bể nước)                Drain (Cốc nước)              │
│        ┌───┐           Tay vặn         ┌───┐                    │
│        │///│          (= Gate)          │   │                    │
│        │///│            │               │   │                    │
│        │///│      ┌─────┴─────┐         │   │                    │
│        │///│──────│   Valve   │─────────│   │                    │
│        │///│      └───────────┘         │   │                    │
│        └───┘                            └───┘                    │
│                                                                  │
│   Gate = 0V (Tắt):  Valve ĐÓNG → Nước KHÔNG chảy → Bit "0"     │
│   Gate > Vth (Bật): Valve MỞ   → Nước CHẢY qua   → Bit "1"    │
│                                                                  │
│   Vth (Threshold Voltage) ≈ 0.3V - 0.7V tùy công nghệ          │
└──────────────────────────────────────────────────────────────────┘
```

### 3.3. Hai trạng thái — Nền tảng của nhị phân

**Trạng thái OFF (Logic 0):** Gate = 0V
```
    Gate = 0V
      │
   ───┴───
   │Oxide│
   ───────
   N │ P █████ N      ← Vùng P chặn electron
   ──┘         └──       Không có dòng điện Source → Drain
                         OUTPUT = 0 (LOW)
```

**Trạng thái ON (Logic 1):** Gate = Vdd (ví dụ 3.3V hoặc 1.0V)
```
    Gate = Vdd
      │
   ───┴───
   │Oxide│         Điện trường "kéo" electron lên tạo kênh dẫn
   ───────
   N │ n-channel │ N   ← Kênh N hình thành giữa Source và Drain
   ──┘            └──     Electron di chuyển tự do
                          OUTPUT = 1 (HIGH)
```

### 3.4. Kích thước thực tế — Sự thu nhỏ kinh ngạc

| Năm | Công nghệ | Kích thước Gate | Transistors/Chip | Ví dụ |
| :--- | :--- | :--- | :--- | :--- |
| 1971 | Intel 4004 | 10 μm | 2,300 | Máy tính bỏ túi |
| 1993 | Pentium | 800 nm | 3.1 triệu | PC đầu tiên phổ biến |
| 2013 | Haswell | 22 nm | 1.4 tỷ | Desktop gaming |
| 2020 | Apple M1 | 5 nm | 16 tỷ | MacBook |
| 2024 | Apple M4 | 3 nm | 28 tỷ | iPad Pro |
| 2025 | TSMC N2 | **2 nm** | 50+ tỷ | Next-gen chips |

> **Để so sánh trực quan:** 1 sợi tóc con người dày khoảng **80,000 nm**. Transistor 3nm có nghĩa là bạn có thể xếp **~26,000 transistor** trên bề rộng một sợi tóc.

---

## 4. Từ Transistor → Logic Gates (Cổng Logic)

### 4.1. Ý tưởng cốt lõi

Một transistor đơn lẻ chỉ là công tắc ON/OFF. Nhưng khi **kết hợp nhiều transistor**, ta tạo ra các **mạch logic** — nền tảng của mọi phép tính.

Có hai họ transistor bổ sung cho nhau:
- **NMOS (N-channel):** Dẫn điện khi Gate = 1 (kéo xuống GND = logic 0)
- **PMOS (P-channel):** Dẫn điện khi Gate = 0 (kéo lên Vdd = logic 1)

Kết hợp cả hai → **CMOS (Complementary MOS):** Mạch tiêu thụ điện cực thấp, chỉ tốn năng lượng khi chuyển trạng thái.

---

### 4.2. Cổng NOT (Inverter) — Cổng đơn giản nhất

**Chức năng:** Đảo ngược tín hiệu. Input 0 → Output 1. Input 1 → Output 0.

```
        Vdd (Nguồn dương)
         │
    ┌────┴────┐
    │  PMOS   │─── Gate = Input A
    └────┬────┘
         │
         ├─────────── Output (Y = NOT A)
         │
    ┌────┴────┐
    │  NMOS   │─── Gate = Input A
    └────┬────┘
         │
        GND (Đất)


Khi A = 0:                          Khi A = 1:
  PMOS ON (dẫn Vdd)                   PMOS OFF
  NMOS OFF                            NMOS ON (dẫn GND)
  Output = Vdd = 1                    Output = GND = 0

Bảng chân lý:
┌───────┬────────┐
│ A (In)│ Y (Out)│
├───────┼────────┤
│   0   │   1    │
│   1   │   0    │
└───────┴────────┘
```

> **2 transistor** → 1 phép tính logic đầu tiên!

---

### 4.3. Cổng NAND — "Cổng Vạn năng" (Universal Gate)

**Chức năng:** Output = 0 **chỉ khi** cả A VÀ B đều bằng 1. Mọi trường hợp khác = 1.

```
        Vdd                    Vdd
         │                      │
    ┌────┴────┐            ┌────┴────┐
    │  PMOS   │─ A         │  PMOS   │─ B       (Mắc SONG SONG)
    └────┬────┘            └────┬────┘
         │                      │
         └──────────┬───────────┘
                    │
                    ├──────────── Output (Y = NOT(A AND B))
                    │
               ┌────┴────┐
               │  NMOS   │─── A
               └────┬────┘                      (Mắc NỐI TIẾP)
               ┌────┴────┐
               │  NMOS   │─── B
               └────┬────┘
                    │
                   GND


Bảng chân lý:
┌───┬───┬───────────┐
│ A │ B │ NAND(A,B) │
├───┼───┼───────────┤
│ 0 │ 0 │     1     │     ← NMOS cả hai OFF → Output kéo lên Vdd
│ 0 │ 1 │     1     │     ← NMOS A OFF → đường xuống GND bị chặn
│ 1 │ 0 │     1     │     ← NMOS B OFF → đường xuống GND bị chặn
│ 1 │ 1 │     0     │     ← Cả hai NMOS ON → Output nối xuống GND
└───┴───┴───────────┘

Tổng: 4 transistors
```

**Tại sao NAND là "Universal"?** Vì mọi cổng logic khác đều có thể xây từ NAND:

```
NOT A        =  NAND(A, A)           ← Nối cả 2 input thành 1

A AND B      =  NOT(NAND(A, B))      ← NAND rồi đảo
             =  NAND(NAND(A,B), NAND(A,B))

A OR B       =  NAND(NOT A, NOT B)
             =  NAND(NAND(A,A), NAND(B,B))

→ Chỉ cần biết NAND, ta xây được MỌI THỨ.
  Đây là lý do bộ nhớ Flash (SSD) gọi là "NAND Flash".
```

---

### 4.4. Cổng AND, OR, XOR — Bộ công cụ đầy đủ

```
  ╔════════════════════════════════════════════════════════════════╗
  ║                 CÁC CỔNG LOGIC CƠ BẢN                        ║
  ╠════════════════════════════════════════════════════════════════╣
  ║                                                               ║
  ║  AND (VÀ) ── 6 transistors                                   ║
  ║  "Cả hai phải đúng"                                           ║
  ║  ┌───┬───┬──────────┐                                        ║
  ║  │ A │ B │ A AND B  │      Ẩn dụ: Khóa cửa cần CẢ HAI chìa  ║
  ║  ├───┼───┼──────────┤      → Chìa A VÀ Chìa B mới mở được   ║
  ║  │ 0 │ 0 │    0     │                                        ║
  ║  │ 0 │ 1 │    0     │                                        ║
  ║  │ 1 │ 0 │    0     │                                        ║
  ║  │ 1 │ 1 │    1     │  ← Chỉ trường hợp này ra 1             ║
  ║  └───┴───┴──────────┘                                        ║
  ║                                                               ║
  ║  OR (HOẶC) ── 6 transistors                                  ║
  ║  "Ít nhất một đúng"                                           ║
  ║  ┌───┬───┬──────────┐                                        ║
  ║  │ A │ B │ A OR B   │      Ẩn dụ: 2 công tắc đèn song song   ║
  ║  ├───┼───┼──────────┤      → Bất kỳ ai bật cũng sáng đèn     ║
  ║  │ 0 │ 0 │    0     │  ← Chỉ trường hợp này ra 0             ║
  ║  │ 0 │ 1 │    1     │                                        ║
  ║  │ 1 │ 0 │    1     │                                        ║
  ║  │ 1 │ 1 │    1     │                                        ║
  ║  └───┴───┴──────────┘                                        ║
  ║                                                               ║
  ║  XOR (HOẶC LOẠI TRỪ) ── 8-12 transistors                    ║
  ║  "Khác nhau mới đúng"                                        ║
  ║  ┌───┬───┬──────────┐                                        ║
  ║  │ A │ B │ A XOR B  │      Ẩn dụ: 2 công tắc cầu thang       ║
  ║  ├───┼───┼──────────┤      → Đèn đổi trạng thái mỗi khi     ║
  ║  │ 0 │ 0 │    0     │        BẤT KỲ AI bật/tắt               ║
  ║  │ 0 │ 1 │    1     │                                        ║
  ║  │ 1 │ 0 │    1     │                                        ║
  ║  │ 1 │ 1 │    0     │                                        ║
  ║  └───┴───┴──────────┘                                        ║
  ║                                                               ║
  ║  XOR rất đặc biệt vì: A XOR B = Bit tổng của phép cộng!     ║
  ║  Đây là nền tảng xây dựng mạch CỘNG (Adder).                 ║
  ║                                                               ║
  ╚════════════════════════════════════════════════════════════════╝
```

---

## 5. Xây dựng mạch Tính toán — Từ Gates đến ALU

### 5.1. Half Adder — Bộ cộng nửa (Cộng 2 bit)

**Bài toán:** Cộng 2 bit (A + B), cho ra kết quả **Sum** (tổng) và **Carry** (nhớ).

```
Ví dụ thực tế (cộng nhị phân):
   0 + 0 = 00  (Sum=0, Carry=0)
   0 + 1 = 01  (Sum=1, Carry=0)
   1 + 0 = 01  (Sum=1, Carry=0)
   1 + 1 = 10  (Sum=0, Carry=1)    ← "10" nhị phân = 2 thập phân

Nhận xét:
   Sum  = A XOR B   (Giống nhau → 0, Khác nhau → 1)
   Carry = A AND B   (Cả hai = 1 → Nhớ 1)


Sơ đồ mạch:
          ┌─────────┐
   A ─────┤         │
          │   XOR   ├──────── Sum (Bit tổng)
   B ──┬──┤         │
       │  └─────────┘
       │
       │  ┌─────────┐
       └──┤         │
          │   AND   ├──────── Carry (Bit nhớ)
   A ─────┤         │
          └─────────┘

Tổng: 1 XOR + 1 AND ≈ 14-18 transistors
```

### 5.2. Full Adder — Bộ cộng đầy đủ (Cộng 2 bit + Carry trước)

**Bài toán:** Cộng A + B + Cin (bit nhớ từ phép cộng trước đó).

```
Ví dụ:  Cộng 5 + 3 ở dạng nhị phân (4-bit)

         Carry: 1 1
                0 1 0 1    (5)
              + 0 0 1 1    (3)
              ─────────
                1 0 0 0    (8)

Từ phải sang trái:
  Bit 0: 1+1+0   = 10 → Sum=0, Carry=1        (Full Adder #0)
  Bit 1: 0+1+1   = 10 → Sum=0, Carry=1        (Full Adder #1)
  Bit 2: 1+0+1   = 10 → Sum=0, Carry=1        (Full Adder #2)
  Bit 3: 0+0+1   = 01 → Sum=1, Carry=0        (Full Adder #3)
  Kết quả: 1000 = 8 ✓


Sơ đồ Full Adder (= 2 Half Adders + 1 OR):
              ┌──────────────┐
   A ─────────┤ Half Adder 1 ├─── S1 ────┐
   B ─────────┤              ├─── C1 ──┐ │
              └──────────────┘         │ │
                                       │ │  ┌──────────────┐
                                       │ └──┤ Half Adder 2 ├─── Sum (Kết quả)
   Cin (Carry in) ─────────────────────┘────┤              ├─── C2
                                            └──────────────┘  │
                                                              │
              ┌───────┐                                       │
   C1 ────────┤  OR   ├──── Cout (Carry out tới bit tiếp)    │
   C2 ────────┤       │                                       │
              └───────┘◄──────────────────────────────────────┘

Tổng: ~40 transistors cho 1 Full Adder
```

### 5.3. Ripple Carry Adder — Cộng số nhiều bit

Để cộng hai số 32-bit, ta nối **32 Full Adders** lại:

```
32-bit Ripple Carry Adder:

   A[0] B[0]     A[1] B[1]     A[2] B[2]          A[31] B[31]
     │   │         │   │         │   │               │    │
   ┌─▼───▼─┐     ┌─▼───▼─┐     ┌─▼───▼─┐          ┌─▼────▼─┐
   │  FA   │     │  FA   │     │  FA   │   ····   │   FA   │
   │  #0   │     │  #1   │     │  #2   │          │  #31   │
   └──┬──┬─┘     └──┬──┬─┘     └──┬──┬─┘          └──┬──┬──┘
      │  └─Cout──►Cin┘  └─Cout──►Cin┘               │  └─ Overflow?
    Sum[0]       Sum[1]       Sum[2]              Sum[31]

   Carry "gợn sóng" (ripple) từ phải sang trái.
   Tổng: 32 × 40 = ~1,280 transistors cho phép cộng 32-bit.

   ⚠ Nhược điểm: Bit cao nhất phải ĐỢI carry từ bit thấp nhất.
     → Giải pháp: Carry-Lookahead Adder (tính carry song song, nhanh hơn).
```

#### > Code to Hardware: ADD
Khi bạn viết `c = a + b;` trong C#:
1.  **Compiler:** Dịch sang Assembly `ADD R1, R2` (cộng giá trị R2 vào R1).
2.  **Hardware:**
    *   `R1` và `R2` đưa tín hiệu điện vào 32 cặp input `A` và `B`.
    *   Tín hiệu lan truyền qua 1,280 transistors trong Ripple Carry Adder.
    *   Sau ~1 clock cycle, kết quả xuất hiện ở output `Sum` và được ghi lại vào `R1`.

---

### 5.4. Subtractor — Mạch trừ (Tái sử dụng Adder!)

**Insight quan trọng:** CPU KHÔNG CÓ mạch trừ riêng! Nó DÙNG LẠI mạch cộng.

```
Cách tính A - B bằng mạch cộng:

  Trong hệ nhị phân có dấu (Two's Complement):
    -B = NOT(B) + 1    (đảo tất cả bits rồi cộng 1)

  Vậy:
    A - B = A + (-B) = A + NOT(B) + 1
                             ↑         ↑
                          XOR gates   Cin = 1


Ví dụ: 5 - 3 = ?

    A    =  0101  (5)
    B    =  0011  (3)
    NOT B =  1100
    +1   → Cin=1

    Thực hiện: 0101 + 1100 + 1 = 10010
    Bỏ bit tràn → 0010 = 2 ✓


Mạch Subtractor = Adder + XOR gates:

   A[0] B[0]     A[1] B[1]     A[2] B[2]          A[31] B[31]
     │   │         │   │         │   │               │    │
     │  ┌▼┐        │  ┌▼┐        │  ┌▼┐              │   ┌▼┐
     │  │X│←SUB    │  │X│←SUB    │  │X│←SUB          │   │X│←SUB
     │  │O│        │  │O│        │  │O│              │   │O│
     │  │R│        │  │R│        │  │R│              │   │R│
     │  └┬┘        │  └┬┘        │  └┬┘              │   └┬┘
   ┌─▼───▼─┐     ┌─▼───▼─┐     ┌─▼───▼─┐          ┌─▼────▼─┐
   │  FA   │     │  FA   │     │  FA   │   ····   │   FA   │
   │  #0   │     │  #1   │     │  #2   │          │  #31   │
   └──┬──┬─┘     └──┬──┬─┘     └──┬──┬─┘          └──┬──┬──┘
      │  └─Cout──►Cin┘  └─Cout──►Cin┘               │
    R[0]          R[1]          R[2]               R[31]
         ▲
         │
   Cin = SUB signal (0 = cộng, 1 = trừ)

   Khi SUB = 0: XOR gates pass B through (B XOR 0 = B), Cin = 0 → A + B
   Khi SUB = 1: XOR gates flip B (B XOR 1 = NOT B), Cin = 1 → A + NOT(B) + 1 = A - B

   → CÙNG 1 MẠCH VẬT LÝ làm được CẢ cộng VÀ trừ!
   → Tiết kiệm transistor + diện tích chip → Đây là thiết kế thực tế trong CPU
```

#### > Code to Hardware: SUB
Khi bạn viết `health -= damage;`:
1.  **Assembly:** `SUB EAX, EBX` (x86) hoặc `SUB R0, R1, R2` (ARM).
2.  **Hardware:**
    *   ALU nhận tín hiệu `SUB` (Opcode).
    *   Tín hiệu này kích hoạt các cổng **XOR** ở đầu vào B để đảo bit (`NOT B`).
    *   Đồng thời kích hoạt `Cin = 1` vào Full Adder đầu tiên.
    *   Mạch cộng chạy bình thường → Ra kết quả phép trừ!

> **Kết nối Unity:** Khi Burst compile `a - b`, CPU thực thi lệnh `SUB` — nhưng bên trong ALU, nó chỉ là `ADD` với B được đảo + Cin=1. Cùng mạch cộng ở trên.

---

### 5.5. Multiplexer (MUX) — Bộ chọn tín hiệu

**MUX là "cổng chọn"** — quyết định output lấy từ input nào, dựa trên tín hiệu select.

```
MUX 2:1 (chọn 1 trong 2 inputs):

   I0 ───┐
         │    ┌─────┐
         ├────┤ MUX ├──── Y (Output)
         │    │ 2:1 │
   I1 ───┘    └──┬──┘
                 │
   S ────────────┘ (Select)

   Bảng chân lý:
   ┌───┬───┬───┬────────┐
   │ S │ I0│ I1│ Y      │
   ├───┼───┼───┼────────┤
   │ 0 │ * │ * │ Y = I0 │   ← S=0: chọn input I0
   │ 1 │ * │ * │ Y = I1 │   ← S=1: chọn input I1
   └───┴───┴───┴────────┘

   Công thức: Y = (NOT S AND I0) OR (S AND I1)
   → Xây từ: 1 NOT + 2 AND + 1 OR = ~12 transistors


MUX 4:1 (chọn 1 trong 4 — dùng 2 bit select):

   I0 ──┐
   I1 ──┤    ┌─────┐
         ├────┤ MUX ├──── Y
   I2 ──┤    │ 4:1 │
   I3 ──┘    └──┬──┘
                │
   S[1:0] ──────┘

   S = 00 → Y = I0
   S = 01 → Y = I1
   S = 10 → Y = I2
   S = 11 → Y = I3


TẠI SAO MUX QUAN TRỌNG CHO ALU?

   ALU chạy TẤT CẢ mạch tính toán CÙNG LÚC (adder, AND, OR, shift, ...)
   MUX ở output CHỌN kết quả đúng dựa trên Opcode.

   Ví dụ: ALU nhận Opcode = ADD
   → Adder, AND unit, OR unit, Shifter... tất cả đều tính
   → MUX chọn output từ Adder, bỏ qua phần còn lại
   → Hiệu quả hơn là routing tín hiệu tùy theo lệnh!

   Opcode 2-bit → MUX 4:1 → chọn 1 trong 4 phép tính
   Opcode 3-bit → MUX 8:1 → chọn 1 trong 8 phép tính
```

#### > Code to Hardware: Conditional Move
Khi bạn dùng `math.select(a, b, condition)` trong Burst:
1.  **Assembly:** `CMOVNE EAX, EBX` (Conditional Move - x86) hoặc `CSEL W0, W1, W2, NE` (ARM).
2.  **Hardware:**
    *   Thay vì dùng `JUMP` (nhảy dòng lệnh), CPU dùng MUX để chọn giá trị.
    *   Nếu `condition` đúng, MUX chọn `b`. Sai chọn `a`.
    *   **Không có Branch Prediction penalty!**

---

### 5.6. Shifter — Mạch dịch bit

**Shifter dịch tất cả bits sang trái hoặc phải.** Dịch trái 1 bit = nhân 2, dịch phải 1 bit = chia 2.

```
Shift Left Logical (SHL) — Ví dụ: 00001010 << 2

   Trước:   0 0 0 0 1 0 1 0   = 10
   Dịch ←2: 0 0 1 0 1 0 0 0   = 40
                         ↑ ↑
                     Điền 0 vào

   10 << 2 = 10 × 4 = 40 ✓  (Mỗi dịch trái = ×2)


Shift Right Logical (SHR) — Ví dụ: 00101000 >> 2

   Trước:   0 0 1 0 1 0 0 0   = 40
   Dịch →2: 0 0 0 0 1 0 1 0   = 10
             ↑ ↑
         Điền 0 vào

   40 >> 2 = 40 ÷ 4 = 10 ✓  (Mỗi dịch phải = ÷2)


Barrel Shifter — Dịch N bit trong 1 clock cycle:

   Mạch tổ hợp dùng MUXes nhiều tầng:

   Tầng 0: MUX quyết định dịch 0 hay 1 bit   (dựa trên shift[0])
   Tầng 1: MUX quyết định dịch 0 hay 2 bits  (dựa trên shift[1])
   Tầng 2: MUX quyết định dịch 0 hay 4 bits  (dựa trên shift[2])
   Tầng 3: MUX quyết định dịch 0 hay 8 bits  (dựa trên shift[3])
   Tầng 4: MUX quyết định dịch 0 hay 16 bits (dựa trên shift[4])

   → 5 tầng MUX = dịch bất kỳ 0-31 bit cho số 32-bit!
   → Tổng: ~32 MUXes × 5 tầng × 12 transistors = ~1,920 transistors


   Input:    [b31][b30][b29]...[b1][b0]
                │    │    │        │   │
             ┌──▼────▼────▼────────▼───▼──┐
             │  Tầng 0: Shift 0 or 1?     │ ← shift[0]
             └──┬────┬────┬────────┬───┬──┘
             ┌──▼────▼────▼────────▼───▼──┐
             │  Tầng 1: Shift 0 or 2?     │ ← shift[1]
             └──┬────┬────┬────────┬───┬──┘
             ┌──▼────▼────▼────────▼───▼──┐
             │  Tầng 2: Shift 0 or 4?     │ ← shift[2]
             └──┬────┬────┬────────┬───┬──┘
                │    │    │        │   │
             ... (tầng 3, 4)
                │    │    │        │   │
             [r31][r30][r29]...[r1][r0]  = Result
```

#### > Code to Hardware: SHL / SHR
1.  **C#:** `int x = a << 2;` (hoặc `a * 4`)
2.  **Assembly (x86):** `SHL EAX, 2`
3.  **Hardware:**
    *   Tín hiệu điện chạy qua tầng MUX số 1 (dịch 2 bit).
    *   Bỏ qua các tầng MUX khác.
    *   Kết quả có ngay trong 1 cycle. Nhanh hơn mạch nhân (`IMUL`) nhiều (mất 3-4 cycles).

> **Kết nối Unity:** Trong Burst-compiled code, `x << n` hoặc `x >> n` = 1 lệnh Assembly (`SHL`/`SHR`). Bitwises operations trong Lab 1 (BitFlags) — mỗi shift chạy qua chính mạch Barrel Shifter này. Shift nhanh hơn multiply (`x * 4` = `x << 2`), đây là lý do compilers tự convert `x * 2^n` thành shift!

---

### 5.7. Multiplier — Mạch nhân (Shift-and-Add)

**Nhân chỉ là cộng lặp lại** — nhưng thông minh hơn: shift-and-add.

```
Nhân nhị phân giống nhân thập phân trên giấy:

   Ví dụ: 0101 × 0011 (5 × 3):

         0 1 0 1    (A = 5)
       × 0 0 1 1    (B = 3)
       ──────────
         0 1 0 1    ← A × B[0] = A × 1 = A          (không shift)
       0 1 0 1 0    ← A × B[1] = A × 1 = A << 1     (shift trái 1)
     0 0 0 0 0 0    ← A × B[2] = A × 0 = 0           (skip)
   0 0 0 0 0 0 0    ← A × B[3] = A × 0 = 0           (skip)
   ──────────────
     0 0 0 1 1 1 1  = 15 ✓

   Quy tắc:
   - Nếu bit B[i] = 1: Cộng A đã shift trái i bit
   - Nếu bit B[i] = 0: Bỏ qua (cộng 0)
   - Tổng tất cả partial products = kết quả


Mạch Multiplier 4-bit:

   A[3:0]    B[3:0]
     │          │
     │    ┌─────┴─────┐
     │    │ B[0]=1?   │ → Partial Product 0 = A[3:0] AND B[0]
     │    │ B[1]=1?   │ → Partial Product 1 = (A[3:0] AND B[1]) << 1
     │    │ B[2]=1?   │ → Partial Product 2 = (A[3:0] AND B[2]) << 2
     │    │ B[3]=1?   │ → Partial Product 3 = (A[3:0] AND B[3]) << 3
     │    └───────────┘
     │         │
     │    ┌────▼────┐
     │    │  Adder  │  ← Cộng tất cả partial products
     │    │  Tree   │    (Wallace Tree hoặc Dadda Tree)
     │    └────┬────┘
     │         │
          Result[7:0]  ← Kết quả 8-bit (4-bit × 4-bit = tối đa 8-bit)


   ● "B[i] AND A" = 4 AND gates (mỗi bit) → quyết định cộng A hay 0
   ● Partial products cộng bằng Adder tree
   ● Kết quả: width gấp đôi (4-bit × 4-bit = 8-bit, 32×32 = 64-bit)
   ● Transistor count: Multiplier 32-bit = ~30,000-50,000 transistors
     (ĐẮT hơn nhiều so với Adder ~1,300!)


Wallace Tree — Cộng nhanh partial products:

   Thay vì cộng tuần tự (P0+P1, rồi +P2, rồi +P3...):
   → Wallace Tree cộng SONG SONG bằng cách dùng Full Adders liên tầng

   Tầng 1: Nhóm 3 partial products → FA → giảm xuống 2 dòng
   Tầng 2: Nhóm tiếp → giảm tiếp
   ...
   Tầng cuối: 1 phép cộng cuối cùng

   → Thay vì O(N) tầng cộng tuần tự → O(log N) tầng!
   → Multiplier 32-bit hoàn thành trong ~3-4 clock cycles thay vì ~32
```

#### > Code to Hardware: MUL / IMUL
1.  **C#:** `float3 c = a * b;`
2.  **Assembly (Burst AVX):** `VMULPS YMM0, YMM1, YMM2`
3.  **Hardware:**
    *   Lệnh này kích hoạt **8 bộ nhân FPU** chạy song song (vì YMM là 256-bit chứa 8 floats).
    *   Mỗi bộ nhân tiêu tốn khoảng 3-5 clock cycles (latency) nhưng có thể pipelined (throughput 0.5-1 cycle).

> **Kết nối Unity:** Mỗi `float3 result = a * b` trong Burst Job = 3 phép nhân float. Mỗi phép nhân chạy qua FPU Multiplier (~50,000 transistors). SIMD AVX2: `VMULPS ymm0, ymm1, ymm2` = 8 phép nhân song song — 8 multiplier units chạy cùng lúc!

---

### 5.8. Comparator — Mạch so sánh

**So sánh A và B** → xuất ra flags: A==B? A>B? A<B?

```
So sánh 1 bit (A vs B):

   A == B:  NOT(A XOR B)     ← XOR = khác nhau → NOT → giống nhau!
   A > B:   A AND (NOT B)    ← A=1 và B=0 → A lớn hơn
   A < B:   (NOT A) AND B    ← A=0 và B=1 → A nhỏ hơn


So sánh nhiều bit — Từ bit cao nhất xuống:

   Ví dụ: A = 0110 (6), B = 0100 (4)

   Bit 3: A[3]=0, B[3]=0 → Bằng → Xét bit tiếp
   Bit 2: A[2]=1, B[2]=1 → Bằng → Xét bit tiếp
   Bit 1: A[1]=1, B[1]=0 → A > B → DỪNG! Kết quả: A > B ✓


Mạch Comparator 4-bit (cascade):

   A[3] B[3]     A[2] B[2]     A[1] B[1]     A[0] B[0]
     │   │         │   │         │   │         │   │
   ┌─▼───▼─┐     ┌─▼───▼─┐     ┌─▼───▼─┐     ┌─▼───▼─┐
   │ 1-bit │     │ 1-bit │     │ 1-bit │     │ 1-bit │
   │ Comp  │     │ Comp  │     │ Comp  │     │ Comp  │
   │ #3    │     │ #2    │     │ #1    │     │ #0    │
   └───┬───┘     └───┬───┘     └───┬───┘     └───┬───┘
       │ EQ,GT,LT    │             │             │
       └──priority──►└──priority──►└──priority──►└──► Flags
                                                       │
                                                  Zero (A==B)
                                                  Negative (A<B)
                                                  Carry (A>B)

   Output → CPU Flags Register:
   ┌──────────────────────────────────────────────────┐
   │  Z (Zero)    = 1 nếu A == B                     │
   │  N (Negative)= 1 nếu A < B (kết quả A-B < 0)   │
   │  C (Carry)   = 1 nếu A > B (overflow khi trừ)   │
   └──────────────────────────────────────────────────┘

   CPU dùng flags này cho "branch instructions":
     CMP R1, R2     → Subtractor: R1 - R2, ghi flags
     JE  label      → Nhảy nếu Z=1 (Jump if Equal)
     JG  label      → Nhảy nếu Z=0 AND N=0 (Jump if Greater)
     JL  label      → Nhảy nếu N=1 (Jump if Less)
```

#### > Code to Hardware: CMP + JUMP
1.  **C#:** `if (health <= 0) Die();`
2.  **Assembly:**
    ```asm
    CMP  EAX, 0      ; So sánh EAX (health) với 0 -> Mạch Comparator chạy
    JLE  Label_Die   ; Jump if Less or Equal (Kiểm tra Flag Z=1 hoặc N=1)
    ```
3.  **Hardware:**
    *   `CMP` thực chất là phép trừ `health - 0` mà **bỏ qua kết quả**, chỉ giữ lại Flags.
    *   Nếu `health=0`, kết quả trừ = 0 → Flag Z bật lên 1.
    *   Lệnh `JLE` chỉ nhìn vào Flag Z và N để quyết định nạp lệnh tiếp theo từ đâu.

> **Kết nối Unity:** Mỗi `if (health <= 0)` trong C# → Burst/IL2CPP compile thành `CMP` + `JLE`. `CMP` = mạch Subtractor (tính `health - 0`) + ghi flags. `JLE` = kiểm tra flags Z hoặc N. Branch prediction (Chapter 3) dự đoán kết quả flags TRƯỚC KHI comparator hoàn thành!

---

### 5.9. ALU (Arithmetic Logic Unit) — Bộ não hoàn chỉnh

Bây giờ ta thấy ALU = **ghép TẤT CẢ mạch trên bằng MUX**:

```
                    ┌──────────────────────────────────────────────┐
                    │               ALU (32-bit)                    │
                    │                                              │
   A (32-bit) ─────►│  ┌─────────────┐                            │
                    │  │   Adder     │─── Kết quả nếu ADD         │
   B (32-bit) ─────►│  │ (1,280 tr.) │                            │
                    │  ├─────────────┤                            │
                    │  │ Subtractor  │─── Kết quả nếu SUB         │
                    │  │ (=Adder+XOR)│  (dùng lại Adder!)         │
                    │  ├─────────────┤                            │
                    │  │  Multiplier │─── Kết quả nếu MUL         │
                    │  │(30,000 tr.) │                  │         │
                    │  ├─────────────┤                  │         │
                    │  │  AND (32×)  │─── Kết quả nếu AND│         │
                    │  ├─────────────┤                  │  ┌─────┐│
                    │  │  OR  (32×)  │─── Kết quả nếu OR│  │ MUX ││──► Result
                    │  ├─────────────┤                  │  │ 8:1 ││
                    │  │  XOR (32×)  │─── Kết quả nếu XOR│ │     ││
                    │  ├─────────────┤                  │  └──┬──┘│
                    │  │  Shifter    │─── Kết quả nếu SHL│    │   │
                    │  │ (1,920 tr.) │                  │    │   │
                    │  ├─────────────┤                  │    │   │
                    │  │ Comparator  │─── Flags ───────►│ FLAG│   │
                    │  └─────────────┘                       REG │
                    │                                              │
   Opcode (3-bit) ──►──────────────── Select line cho MUX ────────┘
                    │                                              │
                    │  ┌─────────────────────────────────────────┐ │
                    │  │ Opcode Map:                             │ │
                    │  │   000 = ADD    100 = AND                │ │
                    │  │   001 = SUB    101 = OR                 │ │
                    │  │   010 = MUL    110 = XOR                │ │
                    │  │   011 = SHL/R  111 = CMP                │ │
                    │  └─────────────────────────────────────────┘ │
                    │                                              │
                    │  Tổng: ~50,000-80,000 transistors             │
                    │  CPU hiện đại: 4-8 ALU + FPU per core       │
                    │  GPU: 128 ALU per SM × 46 SM = 5,888 ALU!   │
                    └──────────────────────────────────────────────┘
```

**Ví dụ cụ thể — Lệnh `ADD R1, R2`:**
```
Bước 1: CPU đọc lệnh "ADD" → Giải mã Opcode = 0010
Bước 2: Lấy giá trị R1 (= 5 = 00000101) và R2 (= 3 = 00000011) từ Registers
Bước 3: ALU nhận A=R1, B=R2, Opcode=ADD
Bước 4: MUX chọn output từ Adder
Bước 5: Adder tính: 00000101 + 00000011 = 00001000 (= 8)
Bước 6: Kết quả 8 ghi lại vào R1

→ Tất cả diễn ra trong 1 clock cycle (~0.2 nanosecond ở 5GHz)
→ Chỉ là electron chạy qua ~1,300 transistors trong Adder
```

---

## 6. Kết nối tới Unity — Tại sao điều này quan trọng?

### 6.1. Phép tính trong Shader chính là ALU đang chạy

```csharp
// Vertex Shader (chạy trên GPU):
float4 clipPos = mul(UNITY_MATRIX_MVP, vertexPos);
```

Phép nhân ma trận `mul()` này = **16 phép nhân + 12 phép cộng** `float`.
Mỗi phép tính `float` sử dụng một **FPU (Floating Point Unit)** — phiên bản ALU cho số thực.

Với 10,000 vertices → GPU thực hiện **280,000 phép tính** chỉ cho bước MVP transform.
Mỗi phép tính = hàng nghìn transistor đóng/mở trong FPU.

### 6.2. Tại sao NAND quan trọng cho Game Developer?

```
SSD trong máy bạn = hàng tỷ NAND Gates xếp chồng lên nhau (3D NAND).
  → Load texture, load scene, streaming assets = đọc từ NAND Flash.
  → SSD nhanh hơn HDD vì NAND truy cập tức thời (không quay đĩa).

RAM trong máy bạn = hàng tỷ transistors đơn (DRAM).
  → Mỗi pixel trong RenderTexture = dữ liệu nằm trên DRAM.
  → GC allocation trong C# = cấp phát thêm vùng DRAM mới.
```

### 6.3. Tại sao kích thước transistor ảnh hưởng đến game?

| Transistor nhỏ hơn → | Lý do | Hệ quả cho Game |
| :--- | :--- | :--- |
| Nhiều transistor hơn/chip | Nhiều ALU hơn, nhiều cores hơn | Chạy được nhiều logic & render phức tạp hơn |
| Tiêu thụ ít điện hơn | Ít nhiệt → clock speed cao hơn | FPS cao hơn ở cùng TDP |
| Tốc độ đóng/mở nhanh hơn | Khoảng cách electron di chuyển ngắn hơn | Mỗi clock cycle nhanh hơn |

> **Kết luận Chapter 1:** Mỗi dòng code bạn viết — từ `if (health <= 0)` đến `Shader.SetFloat()` — cuối cùng đều biến thành tín hiệu điện chạy qua hàng tỷ transistor. Hiểu điều này không chỉ là kiến thức lý thuyết, mà là nền tảng để bạn hiểu tại sao **cách tổ chức dữ liệu** (DOD) và **cách viết shader** (branchless) lại ảnh hưởng trực tiếp đến hiệu năng.

---

## 7. Mảnh ghép còn thiếu — Kẻ đã quên mình là ai

Chúng ta đã xây dựng được ALU — một cỗ máy tính toán siêu việt từ hàng nghìn cổng logic.
- Nó có thể tính `5000 + 3000` trong nháy mắt.
- Nó có thể so sánh `health <= 0` cực nhanh.

**NHƯNG... có một vấn đề chết người:**
Ngay khi dòng điện đi qua, cổng logic trả về kết quả, và sau đó... **nó quên sạch**.
- Input tắt → Output tắt.
- Không có cách nào để lưu số "8000" lại để dùng cho phép tính sau.

Một CPU mà không có bộ nhớ (Memory) thì chỉ là một chiếc máy tính bỏ túi không có nút "M+" — vô dụng với các chương trình phức tạp.

Để biến chiếc máy tính này thành một **Computer** thực thụ, ta cần một loại mạch điện mới: Một loại mạch có thể **tự duy trì dòng điện** của chính nó.

👉 **Mời bước sang Chapter 2: Nơi ta học cách "bẫy" electron để tạo ra Ký ức.**

---

> **Chương tiếp theo:** [Chapter 2 — Memory & Storage: Từ Flip-flop đến RAM]() — Cách transistor tạo ra bộ nhớ, và tại sao Memory Hierarchy là chìa khóa của hiệu năng DOTS.

---
*Chapter 1 — Nghiên cứu cho Unity High-Performance Agent*
