# ChÆ°Æ¡ng 1: Transistor & Logic Gates â€” Tá»« Electron Ä‘áº¿n TÃ­nh toÃ¡n

> **Má»¥c tiÃªu chÆ°Æ¡ng:** Hiá»ƒu cÃ¡ch má»™t linh kiá»‡n váº­t lÃ½ nhá» bÃ© (transistor) táº¡o ra ná»n táº£ng cho Má»ŒI phÃ©p tÃ­nh trong mÃ¡y tÃ­nh â€” tá»« phÃ©p cá»™ng Ä‘Æ¡n giáº£n Ä‘áº¿n viá»‡c render hÃ ng triá»‡u polygon trong Unity.

---

## 1. Táº¡i sao pháº£i báº¯t Ä‘áº§u tá»« Ä‘Ã¢y?

Khi báº¡n viáº¿t dÃ²ng code C# nÃ y trong Unity:

```csharp
float3 newPosition = currentPosition + velocity * deltaTime;
```

BÃªn dÆ°á»›i má»i abstraction layer, phÃ©p cá»™ng vÃ  nhÃ¢n Ä‘Ã³ **thá»±c sá»± xáº£y ra** bÃªn trong cÃ¡c máº¡ch transistor váº­t lÃ½. KhÃ´ng cÃ³ phÃ©p mÃ u â€” chá»‰ cÃ³ electron cháº¡y qua cÃ¡c cÃ´ng táº¯c bÃ¡n dáº«n, theo quy luáº­t váº­t lÃ½.

Hiá»ƒu Ä‘iá»u nÃ y giÃºp báº¡n tráº£ lá»i cÃ¢u há»i: **"Táº¡i sao cÃ¡ch tÃ´i tá»• chá»©c dá»¯ liá»‡u láº¡i áº£nh hÆ°á»Ÿng Ä‘áº¿n tá»‘c Ä‘á»™?"** â€” bá»Ÿi vÃ¬ má»i thá»© cuá»‘i cÃ¹ng Ä‘á»u quay vá» cÃ¡ch pháº§n cá»©ng xá»­ lÃ½ tÃ­n hiá»‡u Ä‘iá»‡n.

---

## 2. Cháº¥t bÃ¡n dáº«n â€” Váº­t liá»‡u ná»n táº£ng

### 2.1. Ba loáº¡i váº­t liá»‡u dáº«n Ä‘iá»‡n

| Loáº¡i | Äáº·c Ä‘iá»ƒm | VÃ­ dá»¥ |
| :--- | :--- | :--- |
| **Dáº«n Ä‘iá»‡n (Conductor)** | Electron di chuyá»ƒn tá»± do | Äá»“ng (Cu), NhÃ´m (Al), VÃ ng (Au) |
| **CÃ¡ch Ä‘iá»‡n (Insulator)** | Electron bá»‹ giá»¯ cháº·t, khÃ´ng di chuyá»ƒn | Cao su, Thá»§y tinh, Nhá»±a |
| **BÃ¡n dáº«n (Semiconductor)** | **CÃ³ thá»ƒ báº­t/táº¯t** kháº£ nÄƒng dáº«n Ä‘iá»‡n | Silicon (Si), Germanium (Ge) |

### 2.2. Silicon â€” "Äáº¥t" cá»§a ngÃ nh cÃ´ng nghiá»‡p chip

Silicon (Si) lÃ  nguyÃªn tá»‘ phá»• biáº¿n thá»© 2 trÃªn vá» TrÃ¡i Äáº¥t (sau Oxy). á»ž tráº¡ng thÃ¡i nguyÃªn cháº¥t, nÃ³ **gáº§n nhÆ° khÃ´ng dáº«n Ä‘iá»‡n**. NhÆ°ng khi ta "pha táº¡p" (doping) thÃªm cÃ¡c nguyÃªn tá»‘ khÃ¡c, nÃ³ trá»Ÿ thÃ nh váº­t liá»‡u ká»³ diá»‡u:

```
Silicon nguyÃªn cháº¥t (4 electron lá»›p ngoÃ i):

    Si --- Si --- Si --- Si
    |      |      |      |
    Si --- Si --- Si --- Si      â† LiÃªn káº¿t cá»™ng hÃ³a trá»‹ bá»n vá»¯ng
    |      |      |      |         KhÃ´ng cÃ³ electron tá»± do â†’ KHÃ”NG dáº«n Ä‘iá»‡n
    Si --- Si --- Si --- Si


Pha táº¡p loáº¡i N (thÃªm Phosphorus - 5 electron):

    Si --- Si --- Si --- Si
    |      |      |      |
    Si --- [P]â€¢â”€â”€ Si --- Si      â† Phosphorus cÃ³ 5 electron, 4 liÃªn káº¿t vá»›i Si
    |      |      |      |         Thá»«a 1 electron tá»± do (â€¢) â†’ DáºªN ÄIá»†N (mang Ä‘iá»‡n Ã¢m)
    Si --- Si --- Si --- Si


Pha táº¡p loáº¡i P (thÃªm Boron - 3 electron):

    Si --- Si --- Si --- Si
    |      |      |      |
    Si --- [B]â—‹â”€â”€ Si --- Si      â† Boron cÃ³ 3 electron, thiáº¿u 1 liÃªn káº¿t
    |      |      |      |         Táº¡o "lá»— trá»‘ng" (â—‹) â†’ DáºªN ÄIá»†N (mang Ä‘iá»‡n dÆ°Æ¡ng)
    Si --- Si --- Si --- Si
```

> **Äiá»ƒm máº¥u chá»‘t:** Báº±ng cÃ¡ch káº¿t há»£p vÃ¹ng N vÃ  vÃ¹ng P, ta táº¡o ra "cá»­a" cho phÃ©p hoáº·c cháº·n dÃ²ng electron Ä‘i qua. ÄÃ³ chÃ­nh lÃ  nguyÃªn lÃ½ cá»§a transistor.

---

## 3. MOSFET â€” Transistor hiá»‡n Ä‘áº¡i

### 3.1. Cáº¥u táº¡o MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor)

MOSFET lÃ  loáº¡i transistor phá»• biáº¿n nháº¥t, chiáº¿m **99%** transistor trong CPU/GPU hiá»‡n Ä‘áº¡i.

```
                         Gate (Cá»•ng Ä‘iá»u khiá»ƒn)
                           â”‚
                     â”Œâ”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”
                     â”‚  Metal    â”‚
                     â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
                     â”‚  Oxide    â”‚   â† SiOâ‚‚ (Lá»›p cÃ¡ch Ä‘iá»‡n siÃªu má»ng, ~1-2nm)
                     â”‚  (SiOâ‚‚)  â”‚
   â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
   â”‚    Source (N)    â”‚  Channel  â”‚    Drain (N)    â”‚
   â”‚  (VÃ¹ng N-type)  â”‚  (P-type) â”‚  (VÃ¹ng N-type)  â”‚
   â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                      Substrate (P-type Ná»n Silicon)
                           â”‚
                         Body (Ná»‘i Ä‘áº¥t)
```

### 3.2. Hoáº¡t Ä‘á»™ng â€” NhÆ° má»™t vÃ²i nÆ°á»›c Ä‘iá»‡n tá»­

HÃ£y tÆ°á»Ÿng tÆ°á»£ng MOSFET nhÆ° **vÃ²i nÆ°á»›c**:

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                     MOSFET = VÃ’I NÆ¯á»šC                            â”‚
â”‚                                                                  â”‚
â”‚    Source (Bá»ƒ nÆ°á»›c)                Drain (Cá»‘c nÆ°á»›c)              â”‚
â”‚        â”Œâ”€â”€â”€â”           Tay váº·n         â”Œâ”€â”€â”€â”                    â”‚
â”‚        â”‚///â”‚          (= Gate)          â”‚   â”‚                    â”‚
â”‚        â”‚///â”‚            â”‚               â”‚   â”‚                    â”‚
â”‚        â”‚///â”‚      â”Œâ”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”         â”‚   â”‚                    â”‚
â”‚        â”‚///â”‚â”€â”€â”€â”€â”€â”€â”‚   Valve   â”‚â”€â”€â”€â”€â”€â”€â”€â”€â”€â”‚   â”‚                    â”‚
â”‚        â”‚///â”‚      â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜         â”‚   â”‚                    â”‚
â”‚        â””â”€â”€â”€â”˜                            â””â”€â”€â”€â”˜                    â”‚
â”‚                                                                  â”‚
â”‚   Gate = 0V (Táº¯t):  Valve ÄÃ“NG â†’ NÆ°á»›c KHÃ”NG cháº£y â†’ Bit "0"     â”‚
â”‚   Gate > Vth (Báº­t): Valve Má»ž   â†’ NÆ°á»›c CHáº¢Y qua   â†’ Bit "1"    â”‚
â”‚                                                                  â”‚
â”‚   Vth (Threshold Voltage) â‰ˆ 0.3V - 0.7V tÃ¹y cÃ´ng nghá»‡          â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 3.3. Hai tráº¡ng thÃ¡i â€” Ná»n táº£ng cá»§a nhá»‹ phÃ¢n

**Tráº¡ng thÃ¡i OFF (Logic 0):** Gate = 0V
```
    Gate = 0V
      â”‚
   â”€â”€â”€â”´â”€â”€â”€
   â”‚Oxideâ”‚
   â”€â”€â”€â”€â”€â”€â”€
   N â”‚ P â–ˆâ–ˆâ–ˆâ–ˆâ–ˆ N      â† VÃ¹ng P cháº·n electron
   â”€â”€â”˜         â””â”€â”€       KhÃ´ng cÃ³ dÃ²ng Ä‘iá»‡n Source â†’ Drain
                         OUTPUT = 0 (LOW)
```

**Tráº¡ng thÃ¡i ON (Logic 1):** Gate = Vdd (vÃ­ dá»¥ 3.3V hoáº·c 1.0V)
```
    Gate = Vdd
      â”‚
   â”€â”€â”€â”´â”€â”€â”€
   â”‚Oxideâ”‚         Äiá»‡n trÆ°á»ng "kÃ©o" electron lÃªn táº¡o kÃªnh dáº«n
   â”€â”€â”€â”€â”€â”€â”€
   N â”‚ n-channel â”‚ N   â† KÃªnh N hÃ¬nh thÃ nh giá»¯a Source vÃ  Drain
   â”€â”€â”˜            â””â”€â”€     Electron di chuyá»ƒn tá»± do
                          OUTPUT = 1 (HIGH)
```

### 3.4. KÃ­ch thÆ°á»›c thá»±c táº¿ â€” Sá»± thu nhá» kinh ngáº¡c

| NÄƒm | CÃ´ng nghá»‡ | KÃ­ch thÆ°á»›c Gate | Transistors/Chip | VÃ­ dá»¥ |
| :--- | :--- | :--- | :--- | :--- |
| 1971 | Intel 4004 | 10 Î¼m | 2,300 | MÃ¡y tÃ­nh bá» tÃºi |
| 1993 | Pentium | 800 nm | 3.1 triá»‡u | PC Ä‘áº§u tiÃªn phá»• biáº¿n |
| 2013 | Haswell | 22 nm | 1.4 tá»· | Desktop gaming |
| 2020 | Apple M1 | 5 nm | 16 tá»· | MacBook |
| 2024 | Apple M4 | 3 nm | 28 tá»· | iPad Pro |
| 2025 | TSMC N2 | **2 nm** | 50+ tá»· | Next-gen chips |

> **Äá»ƒ so sÃ¡nh trá»±c quan:** 1 sá»£i tÃ³c con ngÆ°á»i dÃ y khoáº£ng **80,000 nm**. Transistor 3nm cÃ³ nghÄ©a lÃ  báº¡n cÃ³ thá»ƒ xáº¿p **~26,000 transistor** trÃªn bá» rá»™ng má»™t sá»£i tÃ³c.

---

## 4. Tá»« Transistor â†’ Logic Gates (Cá»•ng Logic)

### 4.1. Ã tÆ°á»Ÿng cá»‘t lÃµi

Má»™t transistor Ä‘Æ¡n láº» chá»‰ lÃ  cÃ´ng táº¯c ON/OFF. NhÆ°ng khi **káº¿t há»£p nhiá»u transistor**, ta táº¡o ra cÃ¡c **máº¡ch logic** â€” ná»n táº£ng cá»§a má»i phÃ©p tÃ­nh.

CÃ³ hai há» transistor bá»• sung cho nhau:
- **NMOS (N-channel):** Dáº«n Ä‘iá»‡n khi Gate = 1 (kÃ©o xuá»‘ng GND = logic 0)
- **PMOS (P-channel):** Dáº«n Ä‘iá»‡n khi Gate = 0 (kÃ©o lÃªn Vdd = logic 1)

Káº¿t há»£p cáº£ hai â†’ **CMOS (Complementary MOS):** Máº¡ch tiÃªu thá»¥ Ä‘iá»‡n cá»±c tháº¥p, chá»‰ tá»‘n nÄƒng lÆ°á»£ng khi chuyá»ƒn tráº¡ng thÃ¡i.

---

### 4.2. Cá»•ng NOT (Inverter) â€” Cá»•ng Ä‘Æ¡n giáº£n nháº¥t

**Chá»©c nÄƒng:** Äáº£o ngÆ°á»£c tÃ­n hiá»‡u. Input 0 â†’ Output 1. Input 1 â†’ Output 0.

```
        Vdd (Nguá»“n dÆ°Æ¡ng)
         â”‚
    â”Œâ”€â”€â”€â”€â”´â”€â”€â”€â”€â”
    â”‚  PMOS   â”‚â”€â”€â”€ Gate = Input A
    â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜
         â”‚
         â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€ Output (Y = NOT A)
         â”‚
    â”Œâ”€â”€â”€â”€â”´â”€â”€â”€â”€â”
    â”‚  NMOS   â”‚â”€â”€â”€ Gate = Input A
    â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜
         â”‚
        GND (Äáº¥t)


Khi A = 0:                          Khi A = 1:
  PMOS ON (dáº«n Vdd)                   PMOS OFF
  NMOS OFF                            NMOS ON (dáº«n GND)
  Output = Vdd = 1                    Output = GND = 0

Báº£ng chÃ¢n lÃ½:
â”Œâ”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚ A (In)â”‚ Y (Out)â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚   0   â”‚   1    â”‚
â”‚   1   â”‚   0    â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

> **2 transistor** â†’ 1 phÃ©p tÃ­nh logic Ä‘áº§u tiÃªn!

---

### 4.3. Cá»•ng NAND â€” "Cá»•ng Váº¡n nÄƒng" (Universal Gate)

**Chá»©c nÄƒng:** Output = 0 **chá»‰ khi** cáº£ A VÃ€ B Ä‘á»u báº±ng 1. Má»i trÆ°á»ng há»£p khÃ¡c = 1.

```
        Vdd                    Vdd
         â”‚                      â”‚
    â”Œâ”€â”€â”€â”€â”´â”€â”€â”€â”€â”            â”Œâ”€â”€â”€â”€â”´â”€â”€â”€â”€â”
    â”‚  PMOS   â”‚â”€ A         â”‚  PMOS   â”‚â”€ B       (Máº¯c SONG SONG)
    â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜            â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜
         â”‚                      â”‚
         â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                    â”‚
                    â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€ Output (Y = NOT(A AND B))
                    â”‚
               â”Œâ”€â”€â”€â”€â”´â”€â”€â”€â”€â”
               â”‚  NMOS   â”‚â”€â”€â”€ A
               â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜                      (Máº¯c Ná»I TIáº¾P)
               â”Œâ”€â”€â”€â”€â”´â”€â”€â”€â”€â”
               â”‚  NMOS   â”‚â”€â”€â”€ B
               â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜
                    â”‚
                   GND


Báº£ng chÃ¢n lÃ½:
â”Œâ”€â”€â”€â”¬â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚ A â”‚ B â”‚ NAND(A,B) â”‚
â”œâ”€â”€â”€â”¼â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ 0 â”‚ 0 â”‚     1     â”‚     â† NMOS cáº£ hai OFF â†’ Output kÃ©o lÃªn Vdd
â”‚ 0 â”‚ 1 â”‚     1     â”‚     â† NMOS A OFF â†’ Ä‘Æ°á»ng xuá»‘ng GND bá»‹ cháº·n
â”‚ 1 â”‚ 0 â”‚     1     â”‚     â† NMOS B OFF â†’ Ä‘Æ°á»ng xuá»‘ng GND bá»‹ cháº·n
â”‚ 1 â”‚ 1 â”‚     0     â”‚     â† Cáº£ hai NMOS ON â†’ Output ná»‘i xuá»‘ng GND
â””â”€â”€â”€â”´â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

Tá»•ng: 4 transistors
```

**Táº¡i sao NAND lÃ  "Universal"?** VÃ¬ má»i cá»•ng logic khÃ¡c Ä‘á»u cÃ³ thá»ƒ xÃ¢y tá»« NAND:

```
NOT A        =  NAND(A, A)           â† Ná»‘i cáº£ 2 input thÃ nh 1

A AND B      =  NOT(NAND(A, B))      â† NAND rá»“i Ä‘áº£o
             =  NAND(NAND(A,B), NAND(A,B))

A OR B       =  NAND(NOT A, NOT B)
             =  NAND(NAND(A,A), NAND(B,B))

â†’ Chá»‰ cáº§n biáº¿t NAND, ta xÃ¢y Ä‘Æ°á»£c Má»ŒI THá»¨.
  ÄÃ¢y lÃ  lÃ½ do bá»™ nhá»› Flash (SSD) gá»i lÃ  "NAND Flash".
```

---

### 4.4. Cá»•ng AND, OR, XOR â€” Bá»™ cÃ´ng cá»¥ Ä‘áº§y Ä‘á»§

```
  â•”â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•—
  â•‘                 CÃC Cá»”NG LOGIC CÆ  Báº¢N                        â•‘
  â• â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•£
  â•‘                                                               â•‘
  â•‘  AND (VÃ€) â”€â”€ 6 transistors                                   â•‘
  â•‘  "Cáº£ hai pháº£i Ä‘Ãºng"                                           â•‘
  â•‘  â”Œâ”€â”€â”€â”¬â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                                        â•‘
  â•‘  â”‚ A â”‚ B â”‚ A AND B  â”‚      áº¨n dá»¥: KhÃ³a cá»­a cáº§n Cáº¢ HAI chÃ¬a  â•‘
  â•‘  â”œâ”€â”€â”€â”¼â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤      â†’ ChÃ¬a A VÃ€ ChÃ¬a B má»›i má»Ÿ Ä‘Æ°á»£c   â•‘
  â•‘  â”‚ 0 â”‚ 0 â”‚    0     â”‚                                        â•‘
  â•‘  â”‚ 0 â”‚ 1 â”‚    0     â”‚                                        â•‘
  â•‘  â”‚ 1 â”‚ 0 â”‚    0     â”‚                                        â•‘
  â•‘  â”‚ 1 â”‚ 1 â”‚    1     â”‚  â† Chá»‰ trÆ°á»ng há»£p nÃ y ra 1             â•‘
  â•‘  â””â”€â”€â”€â”´â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                                        â•‘
  â•‘                                                               â•‘
  â•‘  OR (HOáº¶C) â”€â”€ 6 transistors                                  â•‘
  â•‘  "Ãt nháº¥t má»™t Ä‘Ãºng"                                           â•‘
  â•‘  â”Œâ”€â”€â”€â”¬â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                                        â•‘
  â•‘  â”‚ A â”‚ B â”‚ A OR B   â”‚      áº¨n dá»¥: 2 cÃ´ng táº¯c Ä‘Ã¨n song song   â•‘
  â•‘  â”œâ”€â”€â”€â”¼â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤      â†’ Báº¥t ká»³ ai báº­t cÅ©ng sÃ¡ng Ä‘Ã¨n     â•‘
  â•‘  â”‚ 0 â”‚ 0 â”‚    0     â”‚  â† Chá»‰ trÆ°á»ng há»£p nÃ y ra 0             â•‘
  â•‘  â”‚ 0 â”‚ 1 â”‚    1     â”‚                                        â•‘
  â•‘  â”‚ 1 â”‚ 0 â”‚    1     â”‚                                        â•‘
  â•‘  â”‚ 1 â”‚ 1 â”‚    1     â”‚                                        â•‘
  â•‘  â””â”€â”€â”€â”´â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                                        â•‘
  â•‘                                                               â•‘
  â•‘  XOR (HOáº¶C LOáº I TRá»ª) â”€â”€ 8-12 transistors                    â•‘
  â•‘  "KhÃ¡c nhau má»›i Ä‘Ãºng"                                        â•‘
  â•‘  â”Œâ”€â”€â”€â”¬â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                                        â•‘
  â•‘  â”‚ A â”‚ B â”‚ A XOR B  â”‚      áº¨n dá»¥: 2 cÃ´ng táº¯c cáº§u thang       â•‘
  â•‘  â”œâ”€â”€â”€â”¼â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤      â†’ ÄÃ¨n Ä‘á»•i tráº¡ng thÃ¡i má»—i khi     â•‘
  â•‘  â”‚ 0 â”‚ 0 â”‚    0     â”‚        Báº¤T Ká»² AI báº­t/táº¯t               â•‘
  â•‘  â”‚ 0 â”‚ 1 â”‚    1     â”‚                                        â•‘
  â•‘  â”‚ 1 â”‚ 0 â”‚    1     â”‚                                        â•‘
  â•‘  â”‚ 1 â”‚ 1 â”‚    0     â”‚                                        â•‘
  â•‘  â””â”€â”€â”€â”´â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                                        â•‘
  â•‘                                                               â•‘
  â•‘  XOR ráº¥t Ä‘áº·c biá»‡t vÃ¬: A XOR B = Bit tá»•ng cá»§a phÃ©p cá»™ng!     â•‘
  â•‘  ÄÃ¢y lÃ  ná»n táº£ng xÃ¢y dá»±ng máº¡ch Cá»˜NG (Adder).                 â•‘
  â•‘                                                               â•‘
  â•šâ•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
```

---

## 5. XÃ¢y dá»±ng máº¡ch TÃ­nh toÃ¡n â€” Tá»« Gates Ä‘áº¿n ALU

### 5.1. Half Adder â€” Bá»™ cá»™ng ná»­a (Cá»™ng 2 bit)

**BÃ i toÃ¡n:** Cá»™ng 2 bit (A + B), cho ra káº¿t quáº£ **Sum** (tá»•ng) vÃ  **Carry** (nhá»›).

```
VÃ­ dá»¥ thá»±c táº¿ (cá»™ng nhá»‹ phÃ¢n):
   0 + 0 = 00  (Sum=0, Carry=0)
   0 + 1 = 01  (Sum=1, Carry=0)
   1 + 0 = 01  (Sum=1, Carry=0)
   1 + 1 = 10  (Sum=0, Carry=1)    â† "10" nhá»‹ phÃ¢n = 2 tháº­p phÃ¢n

Nháº­n xÃ©t:
   Sum  = A XOR B   (Giá»‘ng nhau â†’ 0, KhÃ¡c nhau â†’ 1)
   Carry = A AND B   (Cáº£ hai = 1 â†’ Nhá»› 1)


SÆ¡ Ä‘á»“ máº¡ch:
          â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”
   A â”€â”€â”€â”€â”€â”¤         â”‚
          â”‚   XOR   â”œâ”€â”€â”€â”€â”€â”€â”€â”€ Sum (Bit tá»•ng)
   B â”€â”€â”¬â”€â”€â”¤         â”‚
       â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
       â”‚
       â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”
       â””â”€â”€â”¤         â”‚
          â”‚   AND   â”œâ”€â”€â”€â”€â”€â”€â”€â”€ Carry (Bit nhá»›)
   A â”€â”€â”€â”€â”€â”¤         â”‚
          â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

Tá»•ng: 1 XOR + 1 AND â‰ˆ 14-18 transistors
```

### 5.2. Full Adder â€” Bá»™ cá»™ng Ä‘áº§y Ä‘á»§ (Cá»™ng 2 bit + Carry trÆ°á»›c)

**BÃ i toÃ¡n:** Cá»™ng A + B + Cin (bit nhá»› tá»« phÃ©p cá»™ng trÆ°á»›c Ä‘Ã³).

```
VÃ­ dá»¥:  Cá»™ng 5 + 3 á»Ÿ dáº¡ng nhá»‹ phÃ¢n (4-bit)

         Carry: 1 1
                0 1 0 1    (5)
              + 0 0 1 1    (3)
              â”€â”€â”€â”€â”€â”€â”€â”€â”€
                1 0 0 0    (8)

Tá»« pháº£i sang trÃ¡i:
  Bit 0: 1+1+0   = 10 â†’ Sum=0, Carry=1        (Full Adder #0)
  Bit 1: 0+1+1   = 10 â†’ Sum=0, Carry=1        (Full Adder #1)
  Bit 2: 1+0+1   = 10 â†’ Sum=0, Carry=1        (Full Adder #2)
  Bit 3: 0+0+1   = 01 â†’ Sum=1, Carry=0        (Full Adder #3)
  Káº¿t quáº£: 1000 = 8 âœ“


SÆ¡ Ä‘á»“ Full Adder (= 2 Half Adders + 1 OR):
              â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
   A â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤ Half Adder 1 â”œâ”€â”€â”€ S1 â”€â”€â”€â”€â”
   B â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤              â”œâ”€â”€â”€ C1 â”€â”€â” â”‚
              â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜         â”‚ â”‚
                                       â”‚ â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
                                       â”‚ â””â”€â”€â”¤ Half Adder 2 â”œâ”€â”€â”€ Sum (Káº¿t quáº£)
   Cin (Carry in) â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜â”€â”€â”€â”€â”¤              â”œâ”€â”€â”€ C2
                                            â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â”‚
                                                              â”‚
              â”Œâ”€â”€â”€â”€â”€â”€â”€â”                                       â”‚
   C1 â”€â”€â”€â”€â”€â”€â”€â”€â”¤  OR   â”œâ”€â”€â”€â”€ Cout (Carry out tá»›i bit tiáº¿p)    â”‚
   C2 â”€â”€â”€â”€â”€â”€â”€â”€â”¤       â”‚                                       â”‚
              â””â”€â”€â”€â”€â”€â”€â”€â”˜â—„â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

Tá»•ng: ~40 transistors cho 1 Full Adder
```

### 5.3. Ripple Carry Adder â€” Cá»™ng sá»‘ nhiá»u bit

Äá»ƒ cá»™ng hai sá»‘ 32-bit, ta ná»‘i **32 Full Adders** láº¡i:

```
32-bit Ripple Carry Adder:

   A[0] B[0]     A[1] B[1]     A[2] B[2]          A[31] B[31]
     â”‚   â”‚         â”‚   â”‚         â”‚   â”‚               â”‚    â”‚
   â”Œâ”€â–¼â”€â”€â”€â–¼â”€â”     â”Œâ”€â–¼â”€â”€â”€â–¼â”€â”     â”Œâ”€â–¼â”€â”€â”€â–¼â”€â”          â”Œâ”€â–¼â”€â”€â”€â”€â–¼â”€â”
   â”‚  FA   â”‚     â”‚  FA   â”‚     â”‚  FA   â”‚   Â·Â·Â·Â·   â”‚   FA   â”‚
   â”‚  #0   â”‚     â”‚  #1   â”‚     â”‚  #2   â”‚          â”‚  #31   â”‚
   â””â”€â”€â”¬â”€â”€â”¬â”€â”˜     â””â”€â”€â”¬â”€â”€â”¬â”€â”˜     â””â”€â”€â”¬â”€â”€â”¬â”€â”˜          â””â”€â”€â”¬â”€â”€â”¬â”€â”€â”˜
      â”‚  â””â”€Coutâ”€â”€â–ºCinâ”˜  â””â”€Coutâ”€â”€â–ºCinâ”˜               â”‚  â””â”€ Overflow?
    Sum[0]       Sum[1]       Sum[2]              Sum[31]

   Carry "gá»£n sÃ³ng" (ripple) tá»« pháº£i sang trÃ¡i.
   Tá»•ng: 32 Ã— 40 = ~1,280 transistors cho phÃ©p cá»™ng 32-bit.

   âš  NhÆ°á»£c Ä‘iá»ƒm: Bit cao nháº¥t pháº£i Äá»¢I carry tá»« bit tháº¥p nháº¥t.
     â†’ Giáº£i phÃ¡p: Carry-Lookahead Adder (tÃ­nh carry song song, nhanh hÆ¡n).
```

#### > Code to Hardware: ADD
Khi báº¡n viáº¿t `c = a + b;` trong C#:
1.  **Compiler:** Dá»‹ch sang Assembly `ADD R1, R2` (cá»™ng giÃ¡ trá»‹ R2 vÃ o R1).
2.  **Hardware:**
    *   `R1` vÃ  `R2` Ä‘Æ°a tÃ­n hiá»‡u Ä‘iá»‡n vÃ o 32 cáº·p input `A` vÃ  `B`.
    *   TÃ­n hiá»‡u lan truyá»n qua 1,280 transistors trong Ripple Carry Adder.
    *   Sau ~1 clock cycle, káº¿t quáº£ xuáº¥t hiá»‡n á»Ÿ output `Sum` vÃ  Ä‘Æ°á»£c ghi láº¡i vÃ o `R1`.

---

### 5.4. Subtractor â€” Máº¡ch trá»« (TÃ¡i sá»­ dá»¥ng Adder!)

**Insight quan trá»ng:** CPU KHÃ”NG CÃ“ máº¡ch trá»« riÃªng! NÃ³ DÃ™NG Láº I máº¡ch cá»™ng.

```
CÃ¡ch tÃ­nh A - B báº±ng máº¡ch cá»™ng:

  Trong há»‡ nhá»‹ phÃ¢n cÃ³ dáº¥u (Two's Complement):
    -B = NOT(B) + 1    (Ä‘áº£o táº¥t cáº£ bits rá»“i cá»™ng 1)

  Váº­y:
    A - B = A + (-B) = A + NOT(B) + 1
                             â†‘         â†‘
                          XOR gates   Cin = 1


VÃ­ dá»¥: 5 - 3 = ?

    A    =  0101  (5)
    B    =  0011  (3)
    NOT B =  1100
    +1   â†’ Cin=1

    Thá»±c hiá»‡n: 0101 + 1100 + 1 = 10010
    Bá» bit trÃ n â†’ 0010 = 2 âœ“


Máº¡ch Subtractor = Adder + XOR gates:

   A[0] B[0]     A[1] B[1]     A[2] B[2]          A[31] B[31]
     â”‚   â”‚         â”‚   â”‚         â”‚   â”‚               â”‚    â”‚
     â”‚  â”Œâ–¼â”        â”‚  â”Œâ–¼â”        â”‚  â”Œâ–¼â”              â”‚   â”Œâ–¼â”
     â”‚  â”‚Xâ”‚â†SUB    â”‚  â”‚Xâ”‚â†SUB    â”‚  â”‚Xâ”‚â†SUB          â”‚   â”‚Xâ”‚â†SUB
     â”‚  â”‚Oâ”‚        â”‚  â”‚Oâ”‚        â”‚  â”‚Oâ”‚              â”‚   â”‚Oâ”‚
     â”‚  â”‚Râ”‚        â”‚  â”‚Râ”‚        â”‚  â”‚Râ”‚              â”‚   â”‚Râ”‚
     â”‚  â””â”¬â”˜        â”‚  â””â”¬â”˜        â”‚  â””â”¬â”˜              â”‚   â””â”¬â”˜
   â”Œâ”€â–¼â”€â”€â”€â–¼â”€â”     â”Œâ”€â–¼â”€â”€â”€â–¼â”€â”     â”Œâ”€â–¼â”€â”€â”€â–¼â”€â”          â”Œâ”€â–¼â”€â”€â”€â”€â–¼â”€â”
   â”‚  FA   â”‚     â”‚  FA   â”‚     â”‚  FA   â”‚   Â·Â·Â·Â·   â”‚   FA   â”‚
   â”‚  #0   â”‚     â”‚  #1   â”‚     â”‚  #2   â”‚          â”‚  #31   â”‚
   â””â”€â”€â”¬â”€â”€â”¬â”€â”˜     â””â”€â”€â”¬â”€â”€â”¬â”€â”˜     â””â”€â”€â”¬â”€â”€â”¬â”€â”˜          â””â”€â”€â”¬â”€â”€â”¬â”€â”€â”˜
      â”‚  â””â”€Coutâ”€â”€â–ºCinâ”˜  â””â”€Coutâ”€â”€â–ºCinâ”˜               â”‚
    R[0]          R[1]          R[2]               R[31]
         â–²
         â”‚
   Cin = SUB signal (0 = cá»™ng, 1 = trá»«)

   Khi SUB = 0: XOR gates pass B through (B XOR 0 = B), Cin = 0 â†’ A + B
   Khi SUB = 1: XOR gates flip B (B XOR 1 = NOT B), Cin = 1 â†’ A + NOT(B) + 1 = A - B

   â†’ CÃ™NG 1 Máº CH Váº¬T LÃ lÃ m Ä‘Æ°á»£c Cáº¢ cá»™ng VÃ€ trá»«!
   â†’ Tiáº¿t kiá»‡m transistor + diá»‡n tÃ­ch chip â†’ ÄÃ¢y lÃ  thiáº¿t káº¿ thá»±c táº¿ trong CPU
```

#### > Code to Hardware: SUB
Khi báº¡n viáº¿t `health -= damage;`:
1.  **Assembly:** `SUB EAX, EBX` (x86) hoáº·c `SUB R0, R1, R2` (ARM).
2.  **Hardware:**
    *   ALU nháº­n tÃ­n hiá»‡u `SUB` (Opcode).
    *   TÃ­n hiá»‡u nÃ y kÃ­ch hoáº¡t cÃ¡c cá»•ng **XOR** á»Ÿ Ä‘áº§u vÃ o B Ä‘á»ƒ Ä‘áº£o bit (`NOT B`).
    *   Äá»“ng thá»i kÃ­ch hoáº¡t `Cin = 1` vÃ o Full Adder Ä‘áº§u tiÃªn.
    *   Máº¡ch cá»™ng cháº¡y bÃ¬nh thÆ°á»ng â†’ Ra káº¿t quáº£ phÃ©p trá»«!

> **Káº¿t ná»‘i Unity:** Khi Burst compile `a - b`, CPU thá»±c thi lá»‡nh `SUB` â€” nhÆ°ng bÃªn trong ALU, nÃ³ chá»‰ lÃ  `ADD` vá»›i B Ä‘Æ°á»£c Ä‘áº£o + Cin=1. CÃ¹ng máº¡ch cá»™ng á»Ÿ trÃªn.

---

### 5.5. Multiplexer (MUX) â€” Bá»™ chá»n tÃ­n hiá»‡u

**MUX lÃ  "cá»•ng chá»n"** â€” quyáº¿t Ä‘á»‹nh output láº¥y tá»« input nÃ o, dá»±a trÃªn tÃ­n hiá»‡u select.

```
MUX 2:1 (chá»n 1 trong 2 inputs):

   I0 â”€â”€â”€â”
         â”‚    â”Œâ”€â”€â”€â”€â”€â”
         â”œâ”€â”€â”€â”€â”¤ MUX â”œâ”€â”€â”€â”€ Y (Output)
         â”‚    â”‚ 2:1 â”‚
   I1 â”€â”€â”€â”˜    â””â”€â”€â”¬â”€â”€â”˜
                 â”‚
   S â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜ (Select)

   Báº£ng chÃ¢n lÃ½:
   â”Œâ”€â”€â”€â”¬â”€â”€â”€â”¬â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”
   â”‚ S â”‚ I0â”‚ I1â”‚ Y      â”‚
   â”œâ”€â”€â”€â”¼â”€â”€â”€â”¼â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”¤
   â”‚ 0 â”‚ * â”‚ * â”‚ Y = I0 â”‚   â† S=0: chá»n input I0
   â”‚ 1 â”‚ * â”‚ * â”‚ Y = I1 â”‚   â† S=1: chá»n input I1
   â””â”€â”€â”€â”´â”€â”€â”€â”´â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”˜

   CÃ´ng thá»©c: Y = (NOT S AND I0) OR (S AND I1)
   â†’ XÃ¢y tá»«: 1 NOT + 2 AND + 1 OR = ~12 transistors


MUX 4:1 (chá»n 1 trong 4 â€” dÃ¹ng 2 bit select):

   I0 â”€â”€â”
   I1 â”€â”€â”¤    â”Œâ”€â”€â”€â”€â”€â”
         â”œâ”€â”€â”€â”€â”¤ MUX â”œâ”€â”€â”€â”€ Y
   I2 â”€â”€â”¤    â”‚ 4:1 â”‚
   I3 â”€â”€â”˜    â””â”€â”€â”¬â”€â”€â”˜
                â”‚
   S[1:0] â”€â”€â”€â”€â”€â”€â”˜

   S = 00 â†’ Y = I0
   S = 01 â†’ Y = I1
   S = 10 â†’ Y = I2
   S = 11 â†’ Y = I3


Táº I SAO MUX QUAN TRá»ŒNG CHO ALU?

   ALU cháº¡y Táº¤T Cáº¢ máº¡ch tÃ­nh toÃ¡n CÃ™NG LÃšC (adder, AND, OR, shift, ...)
   MUX á»Ÿ output CHá»ŒN káº¿t quáº£ Ä‘Ãºng dá»±a trÃªn Opcode.

   VÃ­ dá»¥: ALU nháº­n Opcode = ADD
   â†’ Adder, AND unit, OR unit, Shifter... táº¥t cáº£ Ä‘á»u tÃ­nh
   â†’ MUX chá»n output tá»« Adder, bá» qua pháº§n cÃ²n láº¡i
   â†’ Hiá»‡u quáº£ hÆ¡n lÃ  routing tÃ­n hiá»‡u tÃ¹y theo lá»‡nh!

   Opcode 2-bit â†’ MUX 4:1 â†’ chá»n 1 trong 4 phÃ©p tÃ­nh
   Opcode 3-bit â†’ MUX 8:1 â†’ chá»n 1 trong 8 phÃ©p tÃ­nh
```

#### > Code to Hardware: Conditional Move
Khi báº¡n dÃ¹ng `math.select(a, b, condition)` trong Burst:
1.  **Assembly:** `CMOVNE EAX, EBX` (Conditional Move - x86) hoáº·c `CSEL W0, W1, W2, NE` (ARM).
2.  **Hardware:**
    *   Thay vÃ¬ dÃ¹ng `JUMP` (nháº£y dÃ²ng lá»‡nh), CPU dÃ¹ng MUX Ä‘á»ƒ chá»n giÃ¡ trá»‹.
    *   Náº¿u `condition` Ä‘Ãºng, MUX chá»n `b`. Sai chá»n `a`.
    *   **KhÃ´ng cÃ³ Branch Prediction penalty!**

---

### 5.6. Shifter â€” Máº¡ch dá»‹ch bit

**Shifter dá»‹ch táº¥t cáº£ bits sang trÃ¡i hoáº·c pháº£i.** Dá»‹ch trÃ¡i 1 bit = nhÃ¢n 2, dá»‹ch pháº£i 1 bit = chia 2.

```
Shift Left Logical (SHL) â€” VÃ­ dá»¥: 00001010 << 2

   TrÆ°á»›c:   0 0 0 0 1 0 1 0   = 10
   Dá»‹ch â†2: 0 0 1 0 1 0 0 0   = 40
                         â†‘ â†‘
                     Äiá»n 0 vÃ o

   10 << 2 = 10 Ã— 4 = 40 âœ“  (Má»—i dá»‹ch trÃ¡i = Ã—2)


Shift Right Logical (SHR) â€” VÃ­ dá»¥: 00101000 >> 2

   TrÆ°á»›c:   0 0 1 0 1 0 0 0   = 40
   Dá»‹ch â†’2: 0 0 0 0 1 0 1 0   = 10
             â†‘ â†‘
         Äiá»n 0 vÃ o

   40 >> 2 = 40 Ã· 4 = 10 âœ“  (Má»—i dá»‹ch pháº£i = Ã·2)


Barrel Shifter â€” Dá»‹ch N bit trong 1 clock cycle:

   Máº¡ch tá»• há»£p dÃ¹ng MUXes nhiá»u táº§ng:

   Táº§ng 0: MUX quyáº¿t Ä‘á»‹nh dá»‹ch 0 hay 1 bit   (dá»±a trÃªn shift[0])
   Táº§ng 1: MUX quyáº¿t Ä‘á»‹nh dá»‹ch 0 hay 2 bits  (dá»±a trÃªn shift[1])
   Táº§ng 2: MUX quyáº¿t Ä‘á»‹nh dá»‹ch 0 hay 4 bits  (dá»±a trÃªn shift[2])
   Táº§ng 3: MUX quyáº¿t Ä‘á»‹nh dá»‹ch 0 hay 8 bits  (dá»±a trÃªn shift[3])
   Táº§ng 4: MUX quyáº¿t Ä‘á»‹nh dá»‹ch 0 hay 16 bits (dá»±a trÃªn shift[4])

   â†’ 5 táº§ng MUX = dá»‹ch báº¥t ká»³ 0-31 bit cho sá»‘ 32-bit!
   â†’ Tá»•ng: ~32 MUXes Ã— 5 táº§ng Ã— 12 transistors = ~1,920 transistors


   Input:    [b31][b30][b29]...[b1][b0]
                â”‚    â”‚    â”‚        â”‚   â”‚
             â”Œâ”€â”€â–¼â”€â”€â”€â”€â–¼â”€â”€â”€â”€â–¼â”€â”€â”€â”€â”€â”€â”€â”€â–¼â”€â”€â”€â–¼â”€â”€â”
             â”‚  Táº§ng 0: Shift 0 or 1?     â”‚ â† shift[0]
             â””â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”¬â”€â”€â”˜
             â”Œâ”€â”€â–¼â”€â”€â”€â”€â–¼â”€â”€â”€â”€â–¼â”€â”€â”€â”€â”€â”€â”€â”€â–¼â”€â”€â”€â–¼â”€â”€â”
             â”‚  Táº§ng 1: Shift 0 or 2?     â”‚ â† shift[1]
             â””â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”¬â”€â”€â”˜
             â”Œâ”€â”€â–¼â”€â”€â”€â”€â–¼â”€â”€â”€â”€â–¼â”€â”€â”€â”€â”€â”€â”€â”€â–¼â”€â”€â”€â–¼â”€â”€â”
             â”‚  Táº§ng 2: Shift 0 or 4?     â”‚ â† shift[2]
             â””â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”¬â”€â”€â”˜
                â”‚    â”‚    â”‚        â”‚   â”‚
             ... (táº§ng 3, 4)
                â”‚    â”‚    â”‚        â”‚   â”‚
             [r31][r30][r29]...[r1][r0]  = Result
```

#### > Code to Hardware: SHL / SHR
1.  **C#:** `int x = a << 2;` (hoáº·c `a * 4`)
2.  **Assembly (x86):** `SHL EAX, 2`
3.  **Hardware:**
    *   TÃ­n hiá»‡u Ä‘iá»‡n cháº¡y qua táº§ng MUX sá»‘ 1 (dá»‹ch 2 bit).
    *   Bá» qua cÃ¡c táº§ng MUX khÃ¡c.
    *   Káº¿t quáº£ cÃ³ ngay trong 1 cycle. Nhanh hÆ¡n máº¡ch nhÃ¢n (`IMUL`) nhiá»u (máº¥t 3-4 cycles).

> **Káº¿t ná»‘i Unity:** Trong Burst-compiled code, `x << n` hoáº·c `x >> n` = 1 lá»‡nh Assembly (`SHL`/`SHR`). Bitwises operations trong Lab 1 (BitFlags) â€” má»—i shift cháº¡y qua chÃ­nh máº¡ch Barrel Shifter nÃ y. Shift nhanh hÆ¡n multiply (`x * 4` = `x << 2`), Ä‘Ã¢y lÃ  lÃ½ do compilers tá»± convert `x * 2^n` thÃ nh shift!

---

### 5.7. Multiplier â€” Máº¡ch nhÃ¢n (Shift-and-Add)

**NhÃ¢n chá»‰ lÃ  cá»™ng láº·p láº¡i** â€” nhÆ°ng thÃ´ng minh hÆ¡n: shift-and-add.

```
NhÃ¢n nhá»‹ phÃ¢n giá»‘ng nhÃ¢n tháº­p phÃ¢n trÃªn giáº¥y:

   VÃ­ dá»¥: 0101 Ã— 0011 (5 Ã— 3):

         0 1 0 1    (A = 5)
       Ã— 0 0 1 1    (B = 3)
       â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
         0 1 0 1    â† A Ã— B[0] = A Ã— 1 = A          (khÃ´ng shift)
       0 1 0 1 0    â† A Ã— B[1] = A Ã— 1 = A << 1     (shift trÃ¡i 1)
     0 0 0 0 0 0    â† A Ã— B[2] = A Ã— 0 = 0           (skip)
   0 0 0 0 0 0 0    â† A Ã— B[3] = A Ã— 0 = 0           (skip)
   â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
     0 0 0 1 1 1 1  = 15 âœ“

   Quy táº¯c:
   - Náº¿u bit B[i] = 1: Cá»™ng A Ä‘Ã£ shift trÃ¡i i bit
   - Náº¿u bit B[i] = 0: Bá» qua (cá»™ng 0)
   - Tá»•ng táº¥t cáº£ partial products = káº¿t quáº£


Máº¡ch Multiplier 4-bit:

   A[3:0]    B[3:0]
     â”‚          â”‚
     â”‚    â”Œâ”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”
     â”‚    â”‚ B[0]=1?   â”‚ â†’ Partial Product 0 = A[3:0] AND B[0]
     â”‚    â”‚ B[1]=1?   â”‚ â†’ Partial Product 1 = (A[3:0] AND B[1]) << 1
     â”‚    â”‚ B[2]=1?   â”‚ â†’ Partial Product 2 = (A[3:0] AND B[2]) << 2
     â”‚    â”‚ B[3]=1?   â”‚ â†’ Partial Product 3 = (A[3:0] AND B[3]) << 3
     â”‚    â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
     â”‚         â”‚
     â”‚    â”Œâ”€â”€â”€â”€â–¼â”€â”€â”€â”€â”
     â”‚    â”‚  Adder  â”‚  â† Cá»™ng táº¥t cáº£ partial products
     â”‚    â”‚  Tree   â”‚    (Wallace Tree hoáº·c Dadda Tree)
     â”‚    â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜
     â”‚         â”‚
          Result[7:0]  â† Káº¿t quáº£ 8-bit (4-bit Ã— 4-bit = tá»‘i Ä‘a 8-bit)


   â— "B[i] AND A" = 4 AND gates (má»—i bit) â†’ quyáº¿t Ä‘á»‹nh cá»™ng A hay 0
   â— Partial products cá»™ng báº±ng Adder tree
   â— Káº¿t quáº£: width gáº¥p Ä‘Ã´i (4-bit Ã— 4-bit = 8-bit, 32Ã—32 = 64-bit)
   â— Transistor count: Multiplier 32-bit = ~30,000-50,000 transistors
     (Äáº®T hÆ¡n nhiá»u so vá»›i Adder ~1,300!)


Wallace Tree â€” Cá»™ng nhanh partial products:

   Thay vÃ¬ cá»™ng tuáº§n tá»± (P0+P1, rá»“i +P2, rá»“i +P3...):
   â†’ Wallace Tree cá»™ng SONG SONG báº±ng cÃ¡ch dÃ¹ng Full Adders liÃªn táº§ng

   Táº§ng 1: NhÃ³m 3 partial products â†’ FA â†’ giáº£m xuá»‘ng 2 dÃ²ng
   Táº§ng 2: NhÃ³m tiáº¿p â†’ giáº£m tiáº¿p
   ...
   Táº§ng cuá»‘i: 1 phÃ©p cá»™ng cuá»‘i cÃ¹ng

   â†’ Thay vÃ¬ O(N) táº§ng cá»™ng tuáº§n tá»± â†’ O(log N) táº§ng!
   â†’ Multiplier 32-bit hoÃ n thÃ nh trong ~3-4 clock cycles thay vÃ¬ ~32
```

#### > Code to Hardware: MUL / IMUL
1.  **C#:** `float3 c = a * b;`
2.  **Assembly (Burst AVX):** `VMULPS YMM0, YMM1, YMM2`
3.  **Hardware:**
    *   Lá»‡nh nÃ y kÃ­ch hoáº¡t **8 bá»™ nhÃ¢n FPU** cháº¡y song song (vÃ¬ YMM lÃ  256-bit chá»©a 8 floats).
    *   Má»—i bá»™ nhÃ¢n tiÃªu tá»‘n khoáº£ng 3-5 clock cycles (latency) nhÆ°ng cÃ³ thá»ƒ pipelined (throughput 0.5-1 cycle).

> **Káº¿t ná»‘i Unity:** Má»—i `float3 result = a * b` trong Burst Job = 3 phÃ©p nhÃ¢n float. Má»—i phÃ©p nhÃ¢n cháº¡y qua FPU Multiplier (~50,000 transistors). SIMD AVX2: `VMULPS ymm0, ymm1, ymm2` = 8 phÃ©p nhÃ¢n song song â€” 8 multiplier units cháº¡y cÃ¹ng lÃºc!

---

### 5.8. Comparator â€” Máº¡ch so sÃ¡nh

**So sÃ¡nh A vÃ  B** â†’ xuáº¥t ra flags: A==B? A>B? A<B?

```
So sÃ¡nh 1 bit (A vs B):

   A == B:  NOT(A XOR B)     â† XOR = khÃ¡c nhau â†’ NOT â†’ giá»‘ng nhau!
   A > B:   A AND (NOT B)    â† A=1 vÃ  B=0 â†’ A lá»›n hÆ¡n
   A < B:   (NOT A) AND B    â† A=0 vÃ  B=1 â†’ A nhá» hÆ¡n


So sÃ¡nh nhiá»u bit â€” Tá»« bit cao nháº¥t xuá»‘ng:

   VÃ­ dá»¥: A = 0110 (6), B = 0100 (4)

   Bit 3: A[3]=0, B[3]=0 â†’ Báº±ng â†’ XÃ©t bit tiáº¿p
   Bit 2: A[2]=1, B[2]=1 â†’ Báº±ng â†’ XÃ©t bit tiáº¿p
   Bit 1: A[1]=1, B[1]=0 â†’ A > B â†’ Dá»ªNG! Káº¿t quáº£: A > B âœ“


Máº¡ch Comparator 4-bit (cascade):

   A[3] B[3]     A[2] B[2]     A[1] B[1]     A[0] B[0]
     â”‚   â”‚         â”‚   â”‚         â”‚   â”‚         â”‚   â”‚
   â”Œâ”€â–¼â”€â”€â”€â–¼â”€â”     â”Œâ”€â–¼â”€â”€â”€â–¼â”€â”     â”Œâ”€â–¼â”€â”€â”€â–¼â”€â”     â”Œâ”€â–¼â”€â”€â”€â–¼â”€â”
   â”‚ 1-bit â”‚     â”‚ 1-bit â”‚     â”‚ 1-bit â”‚     â”‚ 1-bit â”‚
   â”‚ Comp  â”‚     â”‚ Comp  â”‚     â”‚ Comp  â”‚     â”‚ Comp  â”‚
   â”‚ #3    â”‚     â”‚ #2    â”‚     â”‚ #1    â”‚     â”‚ #0    â”‚
   â””â”€â”€â”€â”¬â”€â”€â”€â”˜     â””â”€â”€â”€â”¬â”€â”€â”€â”˜     â””â”€â”€â”€â”¬â”€â”€â”€â”˜     â””â”€â”€â”€â”¬â”€â”€â”€â”˜
       â”‚ EQ,GT,LT    â”‚             â”‚             â”‚
       â””â”€â”€priorityâ”€â”€â–ºâ””â”€â”€priorityâ”€â”€â–ºâ””â”€â”€priorityâ”€â”€â–ºâ””â”€â”€â–º Flags
                                                       â”‚
                                                  Zero (A==B)
                                                  Negative (A<B)
                                                  Carry (A>B)

   Output â†’ CPU Flags Register:
   â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
   â”‚  Z (Zero)    = 1 náº¿u A == B                     â”‚
   â”‚  N (Negative)= 1 náº¿u A < B (káº¿t quáº£ A-B < 0)   â”‚
   â”‚  C (Carry)   = 1 náº¿u A > B (overflow khi trá»«)   â”‚
   â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

   CPU dÃ¹ng flags nÃ y cho "branch instructions":
     CMP R1, R2     â†’ Subtractor: R1 - R2, ghi flags
     JE  label      â†’ Nháº£y náº¿u Z=1 (Jump if Equal)
     JG  label      â†’ Nháº£y náº¿u Z=0 AND N=0 (Jump if Greater)
     JL  label      â†’ Nháº£y náº¿u N=1 (Jump if Less)
```

#### > Code to Hardware: CMP + JUMP
1.  **C#:** `if (health <= 0) Die();`
2.  **Assembly:**
    ```asm
    CMP  EAX, 0      ; So sÃ¡nh EAX (health) vá»›i 0 -> Máº¡ch Comparator cháº¡y
    JLE  Label_Die   ; Jump if Less or Equal (Kiá»ƒm tra Flag Z=1 hoáº·c N=1)
    ```
3.  **Hardware:**
    *   `CMP` thá»±c cháº¥t lÃ  phÃ©p trá»« `health - 0` mÃ  **bá» qua káº¿t quáº£**, chá»‰ giá»¯ láº¡i Flags.
    *   Náº¿u `health=0`, káº¿t quáº£ trá»« = 0 â†’ Flag Z báº­t lÃªn 1.
    *   Lá»‡nh `JLE` chá»‰ nhÃ¬n vÃ o Flag Z vÃ  N Ä‘á»ƒ quyáº¿t Ä‘á»‹nh náº¡p lá»‡nh tiáº¿p theo tá»« Ä‘Ã¢u.

> **Káº¿t ná»‘i Unity:** Má»—i `if (health <= 0)` trong C# â†’ Burst/IL2CPP compile thÃ nh `CMP` + `JLE`. `CMP` = máº¡ch Subtractor (tÃ­nh `health - 0`) + ghi flags. `JLE` = kiá»ƒm tra flags Z hoáº·c N. Branch prediction (Chapter 3) dá»± Ä‘oÃ¡n káº¿t quáº£ flags TRÆ¯á»šC KHI comparator hoÃ n thÃ nh!

---

### 5.9. ALU (Arithmetic Logic Unit) â€” Bá»™ nÃ£o hoÃ n chá»‰nh

BÃ¢y giá» ta tháº¥y ALU = **ghÃ©p Táº¤T Cáº¢ máº¡ch trÃªn báº±ng MUX**:

```
                    â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
                    â”‚               ALU (32-bit)                    â”‚
                    â”‚                                              â”‚
   A (32-bit) â”€â”€â”€â”€â”€â–ºâ”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                            â”‚
                    â”‚  â”‚   Adder     â”‚â”€â”€â”€ Káº¿t quáº£ náº¿u ADD         â”‚
   B (32-bit) â”€â”€â”€â”€â”€â–ºâ”‚  â”‚ (1,280 tr.) â”‚                            â”‚
                    â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤                            â”‚
                    â”‚  â”‚ Subtractor  â”‚â”€â”€â”€ Káº¿t quáº£ náº¿u SUB         â”‚
                    â”‚  â”‚ (=Adder+XOR)â”‚  (dÃ¹ng láº¡i Adder!)         â”‚
                    â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤                            â”‚
                    â”‚  â”‚  Multiplier â”‚â”€â”€â”€ Káº¿t quáº£ náº¿u MUL         â”‚
                    â”‚  â”‚(30,000 tr.) â”‚                  â”‚         â”‚
                    â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤                  â”‚         â”‚
                    â”‚  â”‚  AND (32Ã—)  â”‚â”€â”€â”€ Káº¿t quáº£ náº¿u ANDâ”‚         â”‚
                    â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤                  â”‚  â”Œâ”€â”€â”€â”€â”€â”â”‚
                    â”‚  â”‚  OR  (32Ã—)  â”‚â”€â”€â”€ Káº¿t quáº£ náº¿u ORâ”‚  â”‚ MUX â”‚â”‚â”€â”€â–º Result
                    â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤                  â”‚  â”‚ 8:1 â”‚â”‚
                    â”‚  â”‚  XOR (32Ã—)  â”‚â”€â”€â”€ Káº¿t quáº£ náº¿u XORâ”‚ â”‚     â”‚â”‚
                    â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤                  â”‚  â””â”€â”€â”¬â”€â”€â”˜â”‚
                    â”‚  â”‚  Shifter    â”‚â”€â”€â”€ Káº¿t quáº£ náº¿u SHLâ”‚    â”‚   â”‚
                    â”‚  â”‚ (1,920 tr.) â”‚                  â”‚    â”‚   â”‚
                    â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤                  â”‚    â”‚   â”‚
                    â”‚  â”‚ Comparator  â”‚â”€â”€â”€ Flags â”€â”€â”€â”€â”€â”€â”€â–ºâ”‚ FLAGâ”‚   â”‚
                    â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                       REG â”‚
                    â”‚                                              â”‚
   Opcode (3-bit) â”€â”€â–ºâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€ Select line cho MUX â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                    â”‚                                              â”‚
                    â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â” â”‚
                    â”‚  â”‚ Opcode Map:                             â”‚ â”‚
                    â”‚  â”‚   000 = ADD    100 = AND                â”‚ â”‚
                    â”‚  â”‚   001 = SUB    101 = OR                 â”‚ â”‚
                    â”‚  â”‚   010 = MUL    110 = XOR                â”‚ â”‚
                    â”‚  â”‚   011 = SHL/R  111 = CMP                â”‚ â”‚
                    â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜ â”‚
                    â”‚                                              â”‚
                    â”‚  Tá»•ng: ~50,000-80,000 transistors             â”‚
                    â”‚  CPU hiá»‡n Ä‘áº¡i: 4-8 ALU + FPU per core       â”‚
                    â”‚  GPU: 128 ALU per SM Ã— 46 SM = 5,888 ALU!   â”‚
                    â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

**VÃ­ dá»¥ cá»¥ thá»ƒ â€” Lá»‡nh `ADD R1, R2`:**
```
BÆ°á»›c 1: CPU Ä‘á»c lá»‡nh "ADD" â†’ Giáº£i mÃ£ Opcode = 0010
BÆ°á»›c 2: Láº¥y giÃ¡ trá»‹ R1 (= 5 = 00000101) vÃ  R2 (= 3 = 00000011) tá»« Registers
BÆ°á»›c 3: ALU nháº­n A=R1, B=R2, Opcode=ADD
BÆ°á»›c 4: MUX chá»n output tá»« Adder
BÆ°á»›c 5: Adder tÃ­nh: 00000101 + 00000011 = 00001000 (= 8)
BÆ°á»›c 6: Káº¿t quáº£ 8 ghi láº¡i vÃ o R1

â†’ Táº¥t cáº£ diá»…n ra trong 1 clock cycle (~0.2 nanosecond á»Ÿ 5GHz)
â†’ Chá»‰ lÃ  electron cháº¡y qua ~1,300 transistors trong Adder
```

---

## 6. Káº¿t ná»‘i tá»›i Unity â€” Táº¡i sao Ä‘iá»u nÃ y quan trá»ng?

### 6.1. PhÃ©p tÃ­nh trong Shader chÃ­nh lÃ  ALU Ä‘ang cháº¡y

```csharp
// Vertex Shader (cháº¡y trÃªn GPU):
float4 clipPos = mul(UNITY_MATRIX_MVP, vertexPos);
```

PhÃ©p nhÃ¢n ma tráº­n `mul()` nÃ y = **16 phÃ©p nhÃ¢n + 12 phÃ©p cá»™ng** `float`.
Má»—i phÃ©p tÃ­nh `float` sá»­ dá»¥ng má»™t **FPU (Floating Point Unit)** â€” phiÃªn báº£n ALU cho sá»‘ thá»±c.

Vá»›i 10,000 vertices â†’ GPU thá»±c hiá»‡n **280,000 phÃ©p tÃ­nh** chá»‰ cho bÆ°á»›c MVP transform.
Má»—i phÃ©p tÃ­nh = hÃ ng nghÃ¬n transistor Ä‘Ã³ng/má»Ÿ trong FPU.

### 6.2. Táº¡i sao NAND quan trá»ng cho Game Developer?

```
SSD trong mÃ¡y báº¡n = hÃ ng tá»· NAND Gates xáº¿p chá»“ng lÃªn nhau (3D NAND).
  â†’ Load texture, load scene, streaming assets = Ä‘á»c tá»« NAND Flash.
  â†’ SSD nhanh hÆ¡n HDD vÃ¬ NAND truy cáº­p tá»©c thá»i (khÃ´ng quay Ä‘Ä©a).

RAM trong mÃ¡y báº¡n = hÃ ng tá»· transistors Ä‘Æ¡n (DRAM).
  â†’ Má»—i pixel trong RenderTexture = dá»¯ liá»‡u náº±m trÃªn DRAM.
  â†’ GC allocation trong C# = cáº¥p phÃ¡t thÃªm vÃ¹ng DRAM má»›i.
```

### 6.3. Táº¡i sao kÃ­ch thÆ°á»›c transistor áº£nh hÆ°á»Ÿng Ä‘áº¿n game?

| Transistor nhá» hÆ¡n â†’ | LÃ½ do | Há»‡ quáº£ cho Game |
| :--- | :--- | :--- |
| Nhiá»u transistor hÆ¡n/chip | Nhiá»u ALU hÆ¡n, nhiá»u cores hÆ¡n | Cháº¡y Ä‘Æ°á»£c nhiá»u logic & render phá»©c táº¡p hÆ¡n |
| TiÃªu thá»¥ Ã­t Ä‘iá»‡n hÆ¡n | Ãt nhiá»‡t â†’ clock speed cao hÆ¡n | FPS cao hÆ¡n á»Ÿ cÃ¹ng TDP |
| Tá»‘c Ä‘á»™ Ä‘Ã³ng/má»Ÿ nhanh hÆ¡n | Khoáº£ng cÃ¡ch electron di chuyá»ƒn ngáº¯n hÆ¡n | Má»—i clock cycle nhanh hÆ¡n |

> **Káº¿t luáº­n Chapter 1:** Má»—i dÃ²ng code báº¡n viáº¿t â€” tá»« `if (health <= 0)` Ä‘áº¿n `Shader.SetFloat()` â€” cuá»‘i cÃ¹ng Ä‘á»u biáº¿n thÃ nh tÃ­n hiá»‡u Ä‘iá»‡n cháº¡y qua hÃ ng tá»· transistor. Hiá»ƒu Ä‘iá»u nÃ y khÃ´ng chá»‰ lÃ  kiáº¿n thá»©c lÃ½ thuyáº¿t, mÃ  lÃ  ná»n táº£ng Ä‘á»ƒ báº¡n hiá»ƒu táº¡i sao **cÃ¡ch tá»• chá»©c dá»¯ liá»‡u** (DOD) vÃ  **cÃ¡ch viáº¿t shader** (branchless) láº¡i áº£nh hÆ°á»Ÿng trá»±c tiáº¿p Ä‘áº¿n hiá»‡u nÄƒng.

---

## 7. Máº£nh ghÃ©p cÃ²n thiáº¿u â€” Káº» Ä‘Ã£ quÃªn mÃ¬nh lÃ  ai

ChÃºng ta Ä‘Ã£ xÃ¢y dá»±ng Ä‘Æ°á»£c ALU â€” má»™t cá»— mÃ¡y tÃ­nh toÃ¡n siÃªu viá»‡t tá»« hÃ ng nghÃ¬n cá»•ng logic.
- NÃ³ cÃ³ thá»ƒ tÃ­nh `5000 + 3000` trong nhÃ¡y máº¯t.
- NÃ³ cÃ³ thá»ƒ so sÃ¡nh `health <= 0` cá»±c nhanh.

**NHÆ¯NG... cÃ³ má»™t váº¥n Ä‘á» cháº¿t ngÆ°á»i:**
Ngay khi dÃ²ng Ä‘iá»‡n Ä‘i qua, cá»•ng logic tráº£ vá» káº¿t quáº£, vÃ  sau Ä‘Ã³... **nÃ³ quÃªn sáº¡ch**.
- Input táº¯t â†’ Output táº¯t.
- KhÃ´ng cÃ³ cÃ¡ch nÃ o Ä‘á»ƒ lÆ°u sá»‘ "8000" láº¡i Ä‘á»ƒ dÃ¹ng cho phÃ©p tÃ­nh sau.

Má»™t CPU mÃ  khÃ´ng cÃ³ bá»™ nhá»› (Memory) thÃ¬ chá»‰ lÃ  má»™t chiáº¿c mÃ¡y tÃ­nh bá» tÃºi khÃ´ng cÃ³ nÃºt "M+" â€” vÃ´ dá»¥ng vá»›i cÃ¡c chÆ°Æ¡ng trÃ¬nh phá»©c táº¡p.

Äá»ƒ biáº¿n chiáº¿c mÃ¡y tÃ­nh nÃ y thÃ nh má»™t **Computer** thá»±c thá»¥, ta cáº§n má»™t loáº¡i máº¡ch Ä‘iá»‡n má»›i: Má»™t loáº¡i máº¡ch cÃ³ thá»ƒ **tá»± duy trÃ¬ dÃ²ng Ä‘iá»‡n** cá»§a chÃ­nh nÃ³.

ðŸ‘‰ **Má»i bÆ°á»›c sang Chapter 2: NÆ¡i ta há»c cÃ¡ch "báº«y" electron Ä‘á»ƒ táº¡o ra KÃ½ á»©c.**

---

> **ChÆ°Æ¡ng tiáº¿p theo:** [Chapter 2 â€” Memory & Storage: Tá»« Flip-flop Ä‘áº¿n RAM]() â€” CÃ¡ch transistor táº¡o ra bá»™ nhá»›, vÃ  táº¡i sao Memory Hierarchy lÃ  chÃ¬a khÃ³a cá»§a hiá»‡u nÄƒng DOTS.

---
*Chapter 1 â€” NghiÃªn cá»©u cho Unity High-Performance Agent*
# ChÆ°Æ¡ng 2: Memory & Storage â€” Tá»« Flip-flop Ä‘áº¿n RAM

> **Má»¥c tiÃªu chÆ°Æ¡ng:** Hiá»ƒu cÃ¡ch transistor táº¡o ra bá»™ nhá»›, táº¡i sao cÃ³ nhiá»u táº§ng bá»™ nhá»› khÃ¡c nhau (Memory Hierarchy), vÃ  táº¡i sao **Cache Locality** lÃ  yáº¿u tá»‘ quyáº¿t Ä‘á»‹nh hiá»‡u nÄƒng trong Unity DOTS.

---

## 1. Váº¥n Ä‘á»: CPU nhanh, Bá»™ nhá»› cháº­m

á»ž **Chapter 1**, chÃºng ta Ä‘Ã£ táº¡o ra bá»™ nÃ£o biáº¿t tÃ­nh toÃ¡n (ALU). NÃ³ cÃ³ thá»ƒ cá»™ng trá»« nhÃ¢n chia siÃªu tá»‘c.
NhÆ°ng bá»™ nÃ£o Ä‘Ã³ cÃ³ má»™t Ä‘iá»ƒm yáº¿u cháº¿t ngÆ°á»i: **NÃ³ khÃ´ng cÃ³ trÃ­ nhá»›.** (Input táº¯t â†’ Output máº¥t).

Äá»ƒ giáº£i quyáº¿t, ta cáº§n cung cáº¥p cho nÃ³ "nguyÃªn liá»‡u" (Data) Ä‘á»ƒ tÃ­nh toÃ¡n vÃ  má»™t nÆ¡i Ä‘á»ƒ lÆ°u káº¿t quáº£.

HÃ£y tÆ°á»Ÿng tÆ°á»£ng báº¡n lÃ  má»™t Ä‘áº§u báº¿p thiÃªn tÃ i (CPU), cÃ³ thá»ƒ cháº¿ biáº¿n báº¥t ká»³ mÃ³n Äƒn nÃ o trong **1 giÃ¢y**. NhÆ°ng:

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  Äáº¦U Báº¾P (CPU) cáº§n nguyÃªn liá»‡u (Data):                             â”‚
â”‚                                                                      â”‚
â”‚  ðŸ“‹ Báº£ng ghi chÃº trÆ°á»›c máº·t (Registers):    Láº¥y ngay = 0 giÃ¢y       â”‚
â”‚  ðŸ§Š Tá»§ láº¡nh cáº¡nh báº¿p (L1 Cache):           Má»Ÿ láº¥y  = 2 giÃ¢y       â”‚
â”‚  ðŸ§Š Tá»§ láº¡nh ngoÃ i hÃ nh lang (L2 Cache):    Äi láº¥y  = 5 giÃ¢y       â”‚
â”‚  ðŸ§Š Kho láº¡nh táº§ng háº§m (L3 Cache):          Xuá»‘ng láº¥y = 15 giÃ¢y    â”‚
â”‚  ðŸª SiÃªu thá»‹ gáº§n nhÃ  (RAM):                Cháº¡y Ä‘i = 3 PHÃšT       â”‚
â”‚  ðŸšš NhÃ  kho ngoáº¡i thÃ nh (SSD):             Gá»i giao = 1 GIá»œ       â”‚
â”‚  ðŸš¢ Nháº­p kháº©u tá»« nÆ°á»›c ngoÃ i (HDD):         Äá»£i ship = 1 TUáº¦N      â”‚
â”‚                                                                      â”‚
â”‚  â†’ Äáº§u báº¿p (CPU) pháº£i Äá»¨NG Äá»¢I khi nguyÃªn liá»‡u á»Ÿ xa.              â”‚
â”‚    ÄÃ¢y gá»i lÃ  "Memory Stall" â€” CPU khÃ´ng lÃ m gÃ¬ cáº£, chá»‰ chá» data.  â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

**Giáº£i phÃ¡p cá»§a ngÃ nh cÃ´ng nghiá»‡p:** Táº¡o ra nhiá»u táº§ng bá»™ nhá»› â€” nhá» nhÆ°ng nhanh á»Ÿ gáº§n CPU, lá»›n nhÆ°ng cháº­m á»Ÿ xa CPU. ÄÃ¢y lÃ  **Memory Hierarchy**.

---

## 2. Clock & Cycle â€” "Nhá»‹p tim" cá»§a CPU

> **ðŸŽ¯ áº¨n dá»¥ â€” Nháº¡c trÆ°á»Ÿng dÃ n nháº¡c:**
> TÆ°á»Ÿng tÆ°á»£ng dÃ n nháº¡c 100 ngÆ°á»i. Náº¿u ai cÅ©ng chÆ¡i lÃºc nÃ o tÃ¹y thÃ­ch â†’ **Há»–N LOáº N**.
> Nháº¡c trÆ°á»Ÿng giÆ¡ Ä‘Å©a â€” **"ÄÃNH!"** â€” táº¥t cáº£ 100 nháº¡c cÃ´ng cÃ¹ng Ä‘Ã¡nh ná»‘t tiáº¿p theo **Äá»’NG LOáº T**.
> Clock signal = **CÃ¢y Ä‘Å©a nháº¡c trÆ°á»Ÿng** cá»§a CPU.
> Má»—i láº§n "Ä‘Ã¡nh" = táº¥t cáº£ hÃ ng tá»· transistors trong CPU cáº­p nháº­t tráº¡ng thÃ¡i **CÃ™NG Má»˜T KHOáº¢NH KHáº®C**.

### Clock lÃ  gÃ¬?

**Clock** = Má»˜T TÃN HIá»†U ÄIá»†N cá»© láº·p Ä‘i láº·p láº¡i: CAO â†’ THáº¤P â†’ CAO â†’ THáº¤P...

```wavedrom
{
  "signal": [
    { "name": "Voltage", "wave": "lh.lh.lh.lh.lh." },
    { "name": "Tick",    "wave": "x.2..2..2..2..2.", "data": ["Tick", "Tick", "Tick", "Tick", "Tick"] }
  ],
  "head": {
    "text": "TÃ­n hiá»‡u Clock"
  },
  "foot": {
    "tick": 0
  },
  "config": { "hscale": 2 }
}
```

> **CÆ¡ cháº¿:**
> - Chá»‰ táº¡i má»—i **Cáº NH LÃŠN** (Low â†’ High), má»i thá»© xáº£y ra (**Tick**).
> - Giá»¯a 2 cáº¡nh lÃªn = CPU Ä‘ang **CHá»œ** tÃ­n hiá»‡u á»•n Ä‘á»‹nh.

**Clock Ä‘Æ°á»£c táº¡o ra tá»« Ä‘Ã¢u? â€” TrÃ¡i tim Tháº¡ch anh**

TÃ­n hiá»‡u Clock khÃ´ng tá»± nhiÃªn cÃ³. NÃ³ Ä‘áº¿n tá»« má»™t linh kiá»‡n nhá» trÃªn Mainboard gá»i lÃ  **Bá»™ dao Ä‘á»™ng Tháº¡ch anh (Crystal Oscillator)**.

1.  **Hiá»‡u á»©ng Ã¡p Ä‘iá»‡n:** Khi cho dÃ²ng Ä‘iá»‡n cháº¡y qua tinh thá»ƒ tháº¡ch anh, nÃ³ sáº½ **rung** (co giÃ£n) vá»›i táº§n sá»‘ cá»±c ká»³ á»•n Ä‘á»‹nh vÃ  chÃ­nh xÃ¡c (vÃ­ dá»¥: 100 MHz).
2.  **NhÃ¢n táº§n sá»‘ (PLL):** CPU khÃ´ng cháº¡y á»Ÿ 100 MHz. NÃ³ dÃ¹ng máº¡ch nhÃ¢n táº§n (Multiplier) Ä‘á»ƒ nhÃ¢n lÃªn 30-50 láº§n â†’ táº¡o ra 3 GHz, 5 GHz.
3.  **Táº¡i sao cáº§n tháº¡ch anh?** VÃ¬ náº¿u dÃ¹ng máº¡ch Ä‘iá»‡n thÆ°á»ng, nhiá»‡t Ä‘á»™ thay Ä‘á»•i sáº½ lÃ m táº§n sá»‘ sai lá»‡ch â†’ CPU cháº¡y khÃ´ng á»•n Ä‘á»‹nh (treo mÃ¡y). Tháº¡ch anh giá»¯ nhá»‹p "chuáº©n tá»«ng mili-giÃ¢y".

> **VÃ­ dá»¥:** Giá»‘ng nhÆ° quáº£ láº¯c Ä‘á»“ng há»“ cÆ¡. Quáº£ láº¯c dao Ä‘á»™ng Ä‘á»u Ä‘áº·n (gá»‘c), vÃ  cÃ¡c bÃ¡nh rÄƒng (PLL) nhÃ¢n chuyá»ƒn Ä‘á»™ng Ä‘Ã³ lÃªn Ä‘á»ƒ quay kim giÃ¢y, kim phÃºt.

---

### 2.1. Cycle â€” 1 "nhá»‹p Ä‘áº­p" = 1 Ä‘Æ¡n vá»‹ thá»i gian

**1 Cycle = Khoáº£ng thá»i gian GIá»®A 2 cáº¡nh lÃªn liÃªn tiáº¿p**

```wavedrom
{
  "signal": [
    { "name": "CLK",   "wave": "P........" },
    { "name": "Cycle", "wave": "x.3.4.5..", "data": ["Fetch ADD", "Decode", "Execute"] }
  ],
  "head": {
    "text": "Chu trÃ¬nh xá»­ lÃ½ lá»‡nh (Pipeline)",
    "tick": 0
  },
  "foot": {
    "tick": 0
  },
  "config": { "hscale": 2 }
}
```

> **Giáº£i thÃ­ch:**
> - Trong 1 cycle (giá»¯a 2 Tick), CPU lÃ m trá»n váº¹n 1 bÆ°á»›c cÃ´ng viá»‡c.
> - VÃ­ dá»¥: Táº£i lá»‡nh â†’ Giáº£i mÃ£ â†’ Thá»±c thi.


â•â•â• Clock Speed = Bao nhiÃªu cycles Má»–I GIÃ‚Y? â•â•â•

  1 GHz  =  1,000,000,000 cycles/giÃ¢y    (1 cycle = 1.0 ns)
  3 GHz  =  3,000,000,000 cycles/giÃ¢y    (1 cycle = 0.33 ns)
  5 GHz  =  5,000,000,000 cycles/giÃ¢y    (1 cycle = 0.2 ns)
                                                     â†‘
                                          Ãnh sÃ¡ng Ä‘i Ä‘Æ°á»£c 6cm
                                          trong thá»i gian nÃ y!

  Nhá»‹p tim ngÆ°á»i:    ~1.2 Hz   (1.2 nhá»‹p/giÃ¢y)
  Nhá»‹p tim CPU:      ~5 GHz    (5 Tá»¶ nhá»‹p/giÃ¢y)
  â†’ CPU nhanh hÆ¡n tim báº¡n khoáº£ng 4,000,000,000 láº§n.
```

### 2.2. Táº¡i sao cáº§n Clock? â€” Chaos vs Order

```
  â•â•â• KHÃ”NG CÃ“ CLOCK â•â•â•

  Transistor A xong â†’ gá»­i káº¿t quáº£ cho B
  NhÆ°ng B chÆ°a sáºµn sÃ ng! â†’ Káº¿t quáº£ bá»‹ Máº¤T hoáº·c SAI
  Transistor C xong trÆ°á»›c A? â†’ Thá»© tá»± loáº¡n, káº¿t quáº£ vÃ´ nghÄ©a

  = 100 nháº¡c cÃ´ng chÆ¡i tÃ¹y há»©ng â†’ CACophony ðŸ”‡


  â•â•â• CÃ“ CLOCK â•â•â•

  TICK â†’ Táº¤T Cáº¢ flip-flops "chá»¥p áº£nh" dá»¯ liá»‡u CÃ™NG LÃšC
       â†’ Káº¿t quáº£ á»•n Ä‘á»‹nh, Ä‘Ãºng thá»© tá»±
       â†’ BÆ°á»›c tiáº¿p theo chá»‰ báº¯t Ä‘áº§u khi bÆ°á»›c trÆ°á»›c Ä‘Ã£ xong

  = 100 nháº¡c cÃ´ng cÃ¹ng nhÃ¬n nháº¡c trÆ°á»Ÿng â†’ Symphony ðŸŽµ


  CPU 5 GHz = Nháº¡c trÆ°á»Ÿng Ä‘Ã¡nh 5 Tá»¶ nhá»‹p má»—i giÃ¢y.
  Má»—i nhá»‹p = hÃ ng tá»· transistors cÃ¹ng bÆ°á»›c sang tráº¡ng thÃ¡i má»›i.
  â†’ ÄÃ¢y lÃ  lÃ½ do "overclock" (tÄƒng GHz) nguy hiá»ƒm:
     Náº¿u nháº¡c trÆ°á»Ÿng Ä‘Ã¡nh quÃ¡ nhanh, nháº¡c cÃ´ng chÆ°a ká»‹p Ä‘Ã¡nh ná»‘t
     trÆ°á»›c Ä‘Ã³ â†’ SAI Ná»T â†’ CPU crash / BSOD / artifact rendering.
```

---

## 3. Flip-flop â€” ViÃªn gáº¡ch Ä‘áº§u tiÃªn cá»§a Bá»™ nhá»›

### BÃ i toÃ¡n: LÃ m sao "nhá»›" 1 bit?

á»ž Chapter 1, ta biáº¿t cá»•ng logic cho output **tá»©c thÃ¬** dá»±a trÃªn input hiá»‡n táº¡i. NhÆ°ng nÃ³ **khÃ´ng nhá»›** gÃ¬ cáº£ â€” thay Ä‘á»•i input thÃ¬ output Ä‘á»•i ngay.

**Flip-flop** giáº£i quyáº¿t váº¥n Ä‘á» nÃ y báº±ng 1 trick Ä‘Æ¡n giáº£n: **ná»‘i output ngÆ°á»£c láº¡i input** (feedback loop).

> **ðŸŽ¯ áº¨n dá»¥ â€” CÃ´ng táº¯c Ä‘Ã¨n:**
> - Báº¡n **báº­t** Ä‘Ã¨n (Set) â†’ Ä‘Ã¨n sÃ¡ng. Bá» tay ra â€” Ä‘Ã¨n **VáºªN SÃNG**.
> - Báº¡n **táº¯t** Ä‘Ã¨n (Reset) â†’ Ä‘Ã¨n táº¯t. Bá» tay ra â€” Ä‘Ã¨n **VáºªN Táº®T**.
> - ÄÃ¨n "nhá»›" tráº¡ng thÃ¡i cuá»‘i cÃ¹ng mÃ  khÃ´ng cáº§n báº¡n giá»¯ tay.
> - ÄÃ³ chÃ­nh lÃ  **feedback loop**: tráº¡ng thÃ¡i tá»± duy trÃ¬ chÃ­nh nÃ³.

**Chá»‰ cáº§n nhá»› 3 Ä‘iá»u vá» Flip-flop:**

| # | Äiá»u cáº§n nhá»› | Chi tiáº¿t |
|---|---|---|
| 1 | **Nhá»› Ä‘Ãºng 1 bit** (0 hoáº·c 1) | ÄÆ°á»£c xÃ¢y tá»« ~2 cá»•ng logic + feedback loop |
| 2 | **Chá»‰ thay Ä‘á»•i khi Clock "tick"** | Giá»‘ng mÃ¡y áº£nh: chá»‰ "chá»¥p" dá»¯ liá»‡u táº¡i Ä‘Ãºng nhá»‹p Clock â†‘ |
| 3 | **LÃ  ná»n táº£ng cá»§a Má»ŒI bá»™ nhá»›** | Register, Cache, RAM â€” táº¥t cáº£ Ä‘á»u báº¯t nguá»“n tá»« nguyÃªn lÃ½ nÃ y |

> Chá»‰ tá»« ~8 transistors, ta táº¡o ra thá»© cÃ³ thá»ƒ **NHá»š**. Má»i bá»™ nhá»› trÃªn tháº¿ giá»›i â€” tá»« Register trong CPU Ä‘áº¿n thanh RAM 64GB â€” Ä‘á»u báº¯t nguá»“n tá»« nguyÃªn lÃ½ feedback loop nÃ y.

---

## 4. Tá»« Flip-flop â†’ Register â†’ Register File

### 4.1. Register â€” 32 Flip-flops = 1 tá»« dá»¯ liá»‡u

```mermaid
block-beta
    columns 7
    d31["D-FF<br/>#31"]
    d30["D-FF<br/>#30"]
    d29["D-FF<br/>#29"]
    d28["D-FF<br/>#28"]
    space["..."]
    d1["D-FF<br/>#1"]
    d0["D-FF<br/>#0"]

    clk(("CLOCK"))
    
    clk --> d31
    clk --> d30
    clk --> d29
    clk --> d28
    clk --> d1
    clk --> d0

    style d31 fill:#f9fbe7,stroke:#827717
    style d30 fill:#f9fbe7,stroke:#827717
    style d29 fill:#f9fbe7,stroke:#827717
    style d28 fill:#f9fbe7,stroke:#827717
    style d1 fill:#f9fbe7,stroke:#827717
    style d0 fill:#f9fbe7,stroke:#827717
    style clk fill:#ffecb3,stroke:#ff6f00
```

> **CÆ¡ cháº¿:**
> - Táº¥t cáº£ 32 flip-flops nháº­n **CÃ™NG** tÃ­n hiá»‡u Clock.
> - Khi Clock â†‘ (cáº¡nh lÃªn): Cáº£ 32 bit Ä‘Æ°á»£c ghi **Äá»’NG THá»œI**.
> - â†’ Ghi má»™t sá»‘ `int` 32-bit chá»‰ máº¥t **1 clock cycle**.
#### > Code to Hardware: MOV
1.  **C#:** `int x = 42;`
2.  **Assembly:** `MOV EAX, 42`
3.  **Hardware:**
    *   `42` (nhá»‹ phÃ¢n `101010`) Ä‘Æ°á»£c Ä‘Æ°a vÃ o Ä‘áº§u vÃ o D cá»§a cÃ¡c Flip-flop tÆ°Æ¡ng á»©ng trong Register EAX.
    *   TÃ­n hiá»‡u `Write Enable` cho EAX Ä‘Æ°á»£c báº­t.
    *   Táº¡i cáº¡nh lÃªn Clock tiáº¿p theo: EAX chá»‘t giÃ¡ trá»‹ 42.

#### > Register vs RAM:
*   `MOV EAX, EBX` (Register to Register): **0.2 ns** (ngay láº­p tá»©c).
*   `MOV EAX, [EBX]` (RAM to Register): **100 ns** (pháº£i Ä‘á»£i tÃ­n hiá»‡u Ä‘i ra mainboard vÃ  quay láº¡i!).


VÃ­ dá»¥ cá»¥ thá»ƒ:
  Sá»‘ nguyÃªn 42 = 00000000 00000000 00000000 00101010
  â†’ 32 flip-flops lÆ°u:
     FF#31=0, FF#30=0, ... FF#5=1, FF#4=0, FF#3=1, FF#2=0, FF#1=1, FF#0=0
```

> **ðŸŽ¯ áº¨n dá»¥ â€” BÃ n tay cá»§a Äáº§u báº¿p:**
> Register = **MÃ“N Äá»’ ÄANG Cáº¦M TRÃŠN TAY** Ä‘áº§u báº¿p.
> - Äáº§u báº¿p (CPU) chá»‰ cÃ³ 2 tay (Ã­t registers).
> - CÃ¡i gÃ¬ trÃªn tay â†’ dÃ¹ng Ä‘Æ°á»£c NGAY Láº¬P Tá»¨C (0 delay).
> - NhÆ°ng chá»‰ cáº§m Ä‘Æ°á»£c 2-3 thá»© cÃ¹ng lÃºc â†’ pháº£i bá» xuá»‘ng bÃ n (Cache) hoáº·c cáº¥t vÃ o tá»§ (RAM) náº¿u muá»‘n láº¥y thá»© khÃ¡c.
> - Tá»‘c Ä‘á»™: Cáº§m trÃªn tay > Láº¥y tá»« bÃ n > Äi bá»™ tá»›i tá»§ > Cháº¡y ra kho ngoÃ i sÃ¢n.

### 4.2. Register File â€” Bá»™ nhá»› "ngay tay" cá»§a CPU

*(Xem sÆ¡ Ä‘á»“ chi tiáº¿t vá»‹ trÃ­ cá»§a Register File trong kiáº¿n trÃºc CPU Core táº¡i **Section 7**)*

**DÃ²ng cháº£y dá»¯ liá»‡u trong 1 phÃ©p tÃ­nh:**

```
VÃ­ dá»¥: ADD EAX, EBX  (EAX = EAX + EBX)

  Cycle 1:
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚ REGISTER FILEâ”‚
  â”‚              â”‚
  â”‚  EAX â”€â”€ 42 â”€â”¼â”€â”€â”€â”€ Port A â”€â”€â”€â”€â–ºâ”Œâ”€â”€â”€â”€â”€â”€â”€â”
  â”‚              â”‚                 â”‚       â”‚
  â”‚  EBX â”€â”€ 10 â”€â”¼â”€â”€â”€â”€ Port B â”€â”€â”€â”€â–ºâ”‚  ALU  â”‚â”€â”€â”€â”€ Result: 52
  â”‚              â”‚                 â”‚       â”‚
  â”‚              â”‚â—„â”€â”€ Write Port â”€â”€â”˜â”€â”€â”€â”€â”€â”€â”€â”˜
  â”‚  EAX â”€â”€ 52  â”‚   (Ghi káº¿t quáº£ láº¡i vÃ o EAX)
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

  Táº¥t cáº£ xáº£y ra trong 1 CYCLE duy nháº¥t:
  1. Äá»c EAX (42) qua Port A         } CÃ¹ng
  2. Äá»c EBX (10) qua Port B         } lÃºc!
  3. ALU tÃ­nh 42 + 10 = 52            }
  4. Ghi 52 láº¡i vÃ o EAX qua Write Port}

  â†’ Register File cÃ³ NHIá»€U cá»•ng (ports) Ä‘á»ƒ Ä‘á»c/ghi Äá»’NG THá»œI.
  â†’ ÄÃ¢y lÃ  Multi-ported Register File = 2 Read + 1 Write cÃ¹ng lÃºc.
  â†’ So sÃ¡nh: RAM chá»‰ cÃ³ 1 cá»•ng, pháº£i Ä‘á»c rá»“i má»›i ghi â†’ cháº­m hÆ¡n.
```

**Registers "tháº­t" vs Registers "áº£o" â€” Register Renaming:**

```
Báº¡n NHÃŒN THáº¤Y 16 registers (RAX, RBX, ..., R15) trong Assembly.
NhÆ°ng CPU THáº¬T Sá»° cÃ³ ~180-200 registers váº­t lÃ½ bÃªn trong!

Táº¡i sao? Äá»ƒ cháº¡y Out-of-Order (xÃ¡o trá»™n thá»© tá»± lá»‡nh):

  VÃ­ dá»¥ 2 lá»‡nh Äá»˜C Láº¬P nhÆ°ng dÃ¹ng CÃ™NG thanh ghi:
  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  Lá»‡nh 1:  ADD  EAX, 5       ; EAX = EAX + 5
  Lá»‡nh 2:  MOV  EAX, [mem]   ; EAX = giÃ¡ trá»‹ tá»« RAM â† CÃ™NG EAX!

  Váº¥n Ä‘á»: Lá»‡nh 2 GHI ÄÃˆ lÃªn EAX, nhÆ°ng lá»‡nh 1 cÅ©ng cáº§n EAX.
  â†’ CPU khÃ´ng thá»ƒ cháº¡y song song!

  Giáº£i phÃ¡p â€” Register Renaming:
  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  CPU Ä‘á»•i tÃªn bÃªn trong:
  Lá»‡nh 1:  ADD  P47, 5       ; EAX â†’ mapped sang Physical Register #47
  Lá»‡nh 2:  MOV  P92, [mem]   ; EAX â†’ mapped sang Physical Register #92

  â†’ BÃ¢y giá» 2 lá»‡nh KHÃ”NG Äá»¤NG NHAU â†’ cháº¡y song song Ä‘Æ°á»£c!
  â†’ Programmer váº«n tháº¥y "EAX" â€” nhÆ°ng bÃªn trong lÃ  registers khÃ¡c nhau.

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Architectural Registers     Physical Registers              â”‚
  â”‚  (Báº¡n tháº¥y trong Assembly)   (CPU tháº­t sá»± dÃ¹ng bÃªn trong)  â”‚
  â”‚                                                              â”‚
  â”‚  EAX  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â–º  P47, P92, P15, ...               â”‚
  â”‚  EBX  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â–º  P03, P88, ...                    â”‚
  â”‚  ECX  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â–º  P55, P12, ...                    â”‚
  â”‚  ...                       (Pool ~180-200 registers)        â”‚
  â”‚                                                              â”‚
  â”‚  16 tÃªn â† mapping â†’ ~200 registers váº­t lÃ½                   â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

```
Register File trong CPU x86-64 (Ä‘Æ¡n giáº£n hÃ³a):

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                   REGISTER FILE                         â”‚
  â”‚                                                         â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”‚
  â”‚  â”‚  RAX   â”‚ 0000 0000 0000 0000 0000 0000 0010 1010 â”‚  â”‚  â† 64-bit
  â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤  â”‚
  â”‚  â”‚  RBX   â”‚ 0000 0000 0000 0000 0000 0000 0000 0011 â”‚  â”‚
  â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤  â”‚
  â”‚  â”‚  RCX   â”‚ 0000 0000 0000 0000 0000 0000 0000 1010 â”‚  â”‚
  â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤  â”‚
  â”‚  â”‚  RDX   â”‚ 0000 0000 0000 0000 0000 0000 0000 0101 â”‚  â”‚
  â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤  â”‚
  â”‚  â”‚  RSP   â”‚ â† Stack Pointer (Ä‘á»‰nh Stack)            â”‚  â”‚
  â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤  â”‚
  â”‚  â”‚  RBP   â”‚ â† Base Pointer (Ä‘Ã¡y Stack Frame)        â”‚  â”‚
  â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤  â”‚
  â”‚  â”‚  RIP   â”‚ â† Instruction Pointer (lá»‡nh tiáº¿p theo)  â”‚  â”‚
  â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤  â”‚
  â”‚  â”‚  ...   â”‚ (tá»•ng ~16 registers general-purpose)     â”‚  â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â”‚
  â”‚                                                         â”‚
  â”‚  SIMD Registers (cho Burst Compiler):                   â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”‚
  â”‚  â”‚ XMM0   â”‚ 128-bit (4 Ã— float32)                   â”‚  â”‚  â† SSE
  â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤  â”‚
  â”‚  â”‚ YMM0   â”‚ 256-bit (8 Ã— float32)                   â”‚  â”‚  â† AVX
  â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤  â”‚
  â”‚  â”‚ ZMM0   â”‚ 512-bit (16 Ã— float32)                  â”‚  â”‚  â† AVX-512
  â”‚  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤  â”‚
  â”‚  â”‚  ...   â”‚ (XMM0-XMM15 / YMM0-YMM15)              â”‚  â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â”‚
  â”‚                                                         â”‚
  â”‚  Tá»•ng dung lÆ°á»£ng Register File: ~1-2 KB                 â”‚
  â”‚  Tá»‘c Ä‘á»™ truy cáº­p: 0 cycles (tá»©c thÃ¬, cÃ¹ng clock)       â”‚
  â”‚  Transistor cost: ~VÃ i nghÃ¬n transistor (ráº»)            â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

> **Unity DOTS Connection:** Khi Burst Compiler biÃªn dá»‹ch `float3 a + float3 b`, nÃ³ Ä‘áº·t `a` vÃ o XMM0 vÃ  `b` vÃ o XMM1, rá»“i gá»i lá»‡nh `ADDPS` â€” cá»™ng cáº£ 3 thÃ nh pháº§n (x,y,z) **cÃ¹ng 1 lá»‡nh** trÃªn thanh ghi 128-bit. ÄÃ³ lÃ  sá»©c máº¡nh SIMD.

---

## 5. SRAM vs DRAM â€” Hai cÃ¡ch xÃ¢y bá»™ nhá»› tá»« Transistor

### 5.1. SRAM (Static RAM) â€” DÃ¹ng cho Cache

```
SRAM Cell â€” 1 bit = 6 Transistors:

        Vdd                Vdd
         â”‚                  â”‚
    â”Œâ”€â”€â”€â”€â”´â”€â”€â”€â”€â”        â”Œâ”€â”€â”€â”€â”´â”€â”€â”€â”€â”
    â”‚  PMOS   â”‚        â”‚  PMOS   â”‚
    â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜        â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜
         â”‚    â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”    â”‚
         â”œâ”€â”€â”€â”€â”¤Inverterâ”œâ”€â”€â”€â”€â”¤
         â”‚    â”‚  Loop  â”‚    â”‚        â† VÃ²ng feedback (2 inverters)
         â”‚    â””â”€â”€â”€â”€â”€â”€â”€â”€â”˜    â”‚           Giá»¯ nguyÃªn tráº¡ng thÃ¡i
    â”Œâ”€â”€â”€â”€â”´â”€â”€â”€â”€â”        â”Œâ”€â”€â”€â”€â”´â”€â”€â”€â”€â”     mÃ  KHÃ”NG cáº§n lÃ m má»›i
    â”‚  NMOS   â”‚        â”‚  NMOS   â”‚
    â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜        â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜
         â”‚                  â”‚
        GND                GND

  + 2 NMOS transistor lÃ m "cá»•ng truy cáº­p" (Access Transistors)
  = Tá»•ng 6 Transistors / bit

Äáº·c Ä‘iá»ƒm SRAM:
  âœ… Cá»±c nhanh (~1ns)
  âœ… KhÃ´ng cáº§n refresh (giá»¯ data náº¿u cÃ³ Ä‘iá»‡n)
  âŒ Äáº¯t (6 transistors/bit)
  âŒ Tá»‘n diá»‡n tÃ­ch (lá»›n gáº¥p 6Ã— DRAM)
  â†’ DÃ¹ng cho: L1, L2, L3 Cache
```

### 5.2. DRAM (Dynamic RAM) â€” DÃ¹ng cho RAM chÃ­nh

```
DRAM Cell â€” 1 bit = 1 Transistor + 1 Tá»¥ Ä‘iá»‡n:

    Word Line (HÃ ng)
         â”‚
    â”Œâ”€â”€â”€â”€â”´â”€â”€â”€â”€â”
    â”‚  NMOS   â”‚â”€â”€â”€â”€ Bit Line (Cá»™t)
    â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜
         â”‚
    â”Œâ”€â”€â”€â”€â”´â”€â”€â”€â”€â”
    â”‚  Tá»¥     â”‚     â† Tá»¥ Ä‘iá»‡n (Capacitor) LÆ¯U ÄIá»†N TÃCH
    â”‚ Ä‘iá»‡n    â”‚        CÃ³ Ä‘iá»‡n = 1, KhÃ´ng Ä‘iá»‡n = 0
    â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜
         â”‚
        GND

Äáº·c Ä‘iá»ƒm DRAM:
  âœ… Ráº» (1 transistor + 1 tá»¥ / bit)
  âœ… Máº­t Ä‘á»™ cao (nhiá»u GB trong chip nhá»)
  âŒ Cháº­m hÆ¡n SRAM (~50-100ns)
  âŒ Pháº£i REFRESH liÃªn tá»¥c (tá»¥ Ä‘iá»‡n rÃ² rá»‰ charge)
     â†’ Cá»© ~64ms pháº£i Ä‘á»c láº¡i vÃ  ghi láº¡i Táº¤T Cáº¢ cells
     â†’ Trong lÃºc refresh, RAM KHÃ”NG THá»‚ Ä‘á»c/ghi â†’ thÃªm trá»…
  â†’ DÃ¹ng cho: RAM chÃ­nh (DDR4, DDR5)
```

### 5.3. So sÃ¡nh trá»±c quan

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚          SRAM vs DRAM â€” CÃ¹ng lÆ°u 1 bit, khÃ¡c hoÃ n toÃ n           â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚               â”‚     SRAM         â”‚         DRAM                  â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ Transistor    â”‚ 6 / bit          â”‚ 1 / bit + 1 tá»¥ Ä‘iá»‡n           â”‚
â”‚ Tá»‘c Ä‘á»™       â”‚ ~1 ns            â”‚ ~50-100 ns                    â”‚
â”‚ Chi phÃ­       â”‚ $$$$             â”‚ $                              â”‚
â”‚ Cáº§n Refresh?  â”‚ KhÃ´ng            â”‚ CÃ³ (má»—i ~64ms)               â”‚
â”‚ Dung lÆ°á»£ng    â”‚ MB (nhá»)         â”‚ GB (lá»›n)                     â”‚
â”‚ Vá»‹ trÃ­       â”‚ TrÃªn chip CPU    â”‚ Chip riÃªng trÃªn mainboard      â”‚
â”‚ Vai trÃ²      â”‚ L1/L2/L3 Cache   â”‚ RAM chÃ­nh (DDR5)              â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚                                                                   â”‚
â”‚  áº¨n dá»¥:                                                           â”‚
â”‚  SRAM = NgÄƒn kÃ©o bÃ n lÃ m viá»‡c (nhá», láº¥y ngay, Ä‘áº¯t)              â”‚
â”‚  DRAM = Tá»§ há»“ sÆ¡ á»Ÿ gÃ³c phÃ²ng (lá»›n, pháº£i Ä‘á»©ng dáº­y Ä‘i láº¥y, ráº»)   â”‚
â”‚                                                                   â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 5.4. Bá»©c tranh toÃ n cáº£nh â€” Flip-flop vs Register vs SRAM vs DRAM

> **ðŸŽ¯ áº¨n dá»¥ thá»‘ng nháº¥t â€” "BÃ n há»c cá»§a Sinh viÃªn":**
>
> HÃ£y tÆ°á»Ÿng tÆ°á»£ng báº¡n Ä‘ang **Ã´n thi** trong kÃ½ tÃºc xÃ¡:
>
> | Loáº¡i bá»™ nhá»› | áº¨n dá»¥ | VÃ­ dá»¥ thá»±c táº¿ |
> |---|---|---|
> | **1 Flip-flop** | **1 Ã´ Post-it** â€” dÃ¡n 1 chá»¯ sá»‘ (0 hoáº·c 1) | Nhá»› Ä‘Ãºng 1 bit |
> | **1 Register** | **1 dÃ²ng Post-it** â€” 32 Ã´ dÃ¡n liá»n nhau = 1 con sá»‘ | Nhá»› 1 sá»‘ int (VD: `42`) |
> | **SRAM (Cache)** | **Máº·t bÃ n há»c** â€” vÃ i tá» giáº¥y Ä‘ang má»Ÿ, Ä‘á»c ngay | L1/L2/L3 Cache trÃªn CPU |
> | **DRAM (RAM)** | **Ká»‡ sÃ¡ch trong phÃ²ng** â€” pháº£i Ä‘á»©ng dáº­y Ä‘i láº¥y | DDR5 RAM 16-64 GB |
> | *(SSD/HDD)* | **ThÆ° viá»‡n downstairs** â€” pháº£i Ä‘i thang mÃ¡y | á»” cá»©ng lÆ°u trá»¯ |
>
> **Äiá»ƒm máº¥u chá»‘t:**
> - Flip-flop â†’ Register â†’ SRAM â†’ DRAM **khÃ´ng pháº£i** 4 thá»© khÃ¡c nhau.
> - ChÃºng lÃ  **CÃ™NG 1 Ã½ TÆ¯á»žNG** ("nhá»› bit") nhÆ°ng Ä‘Æ°á»£c **xÃ¢y khÃ¡c nhau** Ä‘á»ƒ Ä‘Ã¡nh Ä‘á»•i giá»¯a **tá»‘c Ä‘á»™** vÃ  **dung lÆ°á»£ng**.

```
CÃ¡ch xÃ¢y tá»« nhá» â†’ lá»›n:

  1 Flip-flop = 1 bit nhá»›
       â”‚
       â”‚ Ã— 32 cÃ¡i ghÃ©p láº¡i
       â–¼
  1 Register = 32 bits = 1 con sá»‘
       â”‚
       â”‚  QuÃ¡ Ä‘áº¯t Ä‘á»ƒ lÃ m nhiá»u â†’ dÃ¹ng máº¡ch SRAM Ä‘Æ¡n giáº£n hÆ¡n
       â–¼
  SRAM = Bá» bá»›t máº¡ch (6 transistor/bit thay vÃ¬ ~20)
       â”‚  â†’ Cháº­m hÆ¡n Register nhÆ°ng chá»©a Ä‘Æ°á»£c MB
       â”‚
       â”‚  Váº«n quÃ¡ Ä‘áº¯t â†’ thay transistor báº±ng tá»¥ Ä‘iá»‡n
       â–¼
  DRAM = 1 transistor + 1 tá»¥ Ä‘iá»‡n / bit
         â†’ Cháº­m hÆ¡n SRAM nhÆ°ng chá»©a Ä‘Æ°á»£c GB
         â†’ Pháº£i refresh (tá»¥ rÃ² rá»‰) â†’ thÃªm cháº­m


  Tá»‘c Ä‘á»™:    Register >>>>>>> SRAM >>>>>> DRAM
  Dung lÆ°á»£ng: Register <<<<<<< SRAM <<<<<< DRAM  
  GiÃ¡ tiá»n:   Register $$$$$$$ SRAM $$$$$$ DRAM $
```

---

## 6. Cache â€” Bá»™ Ä‘á»‡m thay Ä‘á»•i cuá»™c chÆ¡i

### 6.1. Táº¡i sao cáº§n Cache?

```
Tá»‘c Ä‘á»™ qua cÃ¡c tháº¿ há»‡ (1980 â†’ nay):

  CPU Speed:     â–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆ  Ã—10,000 láº§n
  RAM Speed:     â–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆ                                 Ã—100 láº§n

  â†’ "Memory Wall": CPU pháº£i CHá»œ RAM hÃ ng trÄƒm chu ká»³.
     Má»—i chu ká»³ chá» = lÃ£ng phÃ­ hÃ ng tá»· phÃ©p tÃ­nh/giÃ¢y.


Giáº£i phÃ¡p = Cache (Bá»™ Ä‘á»‡m SRAM náº±m trÃªn chip CPU):

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  CPU Die (Máº·t cáº¯t chip tháº­t)    â”‚
  â”‚                                  â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”             â”‚
  â”‚  â”‚Core 0â”‚  â”‚Core 1â”‚             â”‚
  â”‚  â”‚â”Œâ”€L1â”€â”â”‚  â”‚â”Œâ”€L1â”€â”â”‚             â”‚
  â”‚  â”‚â””â”€â”€â”€â”€â”˜â”‚  â”‚â””â”€â”€â”€â”€â”˜â”‚             â”‚
  â”‚  â”‚â”Œâ”€L2â”€â”â”‚  â”‚â”Œâ”€L2â”€â”â”‚             â”‚
  â”‚  â”‚â””â”€â”€â”€â”€â”˜â”‚  â”‚â””â”€â”€â”€â”€â”˜â”‚             â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”˜             â”‚
  â”‚                                  â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”    â”‚
  â”‚  â”‚     L3 Cache (Shared)    â”‚    â”‚    â† SRAM chiáº¿m >50% diá»‡n tÃ­ch chip!
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜    â”‚
  â”‚                                  â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
         â”‚
         â”‚  (ÄÆ°á»ng bus ra ngoÃ i chip)
         â–¼
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  DDR5 RAM (DRAM) â”‚   â† Chip riÃªng biá»‡t trÃªn mainboard
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 6.2. Cache Line â€” ÄÆ¡n vá»‹ truyá»n dá»¯ liá»‡u cÆ¡ báº£n

**ÄÃ¢y lÃ  khÃ¡i niá»‡m QUAN TRá»ŒNG NHáº¤T cho hiá»‡u nÄƒng Unity DOTS.**

```
CPU KHÃ”NG BAO GIá»œ Ä‘á»c 1 byte Ä‘Æ¡n láº» tá»« RAM.
NÃ³ luÃ´n Ä‘á»c 1 CACHE LINE = 64 BYTES.

VÃ­ dá»¥: Báº¡n truy cáº­p array[0] (4 bytes int):

  RAM:
  â”Œâ”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”
  â”‚ [0]â”‚ [1]â”‚ [2]â”‚ [3]â”‚ [4]â”‚ [5]â”‚ [6]â”‚ [7]â”‚ [8]â”‚ [9]â”‚[10]â”‚[11]â”‚[12]â”‚[13]â”‚[14]â”‚[15]â”‚
  â”‚ 4B â”‚ 4B â”‚ 4B â”‚ 4B â”‚ 4B â”‚ 4B â”‚ 4B â”‚ 4B â”‚ 4B â”‚ 4B â”‚ 4B â”‚ 4B â”‚ 4B â”‚ 4B â”‚ 4B â”‚ 4B â”‚
  â””â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”´â”€â”€â”€â”€â”˜
  â—„â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€ 64 bytes (1 Cache Line) â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â–º

  Báº¡n chá»‰ cáº§n [0], nhÆ°ng CPU táº£i TOÃ€N Bá»˜ 64 bytes vÃ o L1 Cache.
  â†’ [1] Ä‘áº¿n [15] Ä‘Ã£ cÃ³ sáºµn trong Cache â†’ truy cáº­p miá»…n phÃ­!


Há»‡ quáº£:
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Náº¾U báº¡n duyá»‡t array TUáº¦N Tá»° ([0], [1], [2], ...):        â”‚
  â”‚    â†’ Cache Hit gáº§n 100% (chá»‰ 1 láº§n táº£i / 16 pháº§n tá»­)      â”‚
  â”‚    â†’ Cá»°C NHANH                                              â”‚
  â”‚                                                              â”‚
  â”‚  Náº¾U báº¡n duyá»‡t array NGáºªU NHIÃŠN ([7], [1023], [3], ...):  â”‚
  â”‚    â†’ Cache Miss liÃªn tá»¥c (má»—i truy cáº­p = táº£i cache line má»›i)â”‚
  â”‚    â†’ Cá»°C CHáº¬M (100-300Ã— cháº­m hÆ¡n!)                         â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

> **ðŸŽ¯ áº¨n dá»¥ â€” Kho hÃ ng Amazon:**
> Cache Line = **ThÃ¹ng hÃ ng Ä‘Ã³ng gÃ³i sáºµn** trong kho Amazon.
> - Báº¡n Ä‘áº·t mua **1 cuá»‘n sÃ¡ch** (4 bytes). Amazon khÃ´ng gá»­i riÃªng 1 cuá»‘n.
> - Há» gá»­i **cáº£ thÃ¹ng 16 cuá»‘n** cÃ¹ng chá»§ Ä‘á» (64 bytes = 1 Cache Line).
> - Náº¿u báº¡n Ä‘á»c háº¿t bá»™ sÃ¡ch theo thá»© tá»± â†’ 15 cuá»‘n sau miá»…n phÃ­ ship! (**Cache Hit**)
> - Náº¿u báº¡n Ä‘á»c ngáº«u nhiÃªn sÃ¡ch tá»« kháº¯p nÆ¡i â†’ má»—i cuá»‘n = 1 thÃ¹ng hÃ ng má»›i â†’ phÃ­ ship cá»±c Ä‘áº¯t! (**Cache Miss**)

### 6.3. VÃ­ dá»¥ thá»±c táº¿: Cache Hit vs Miss

#### > Under the Hood: Táº¡i sao Random cháº­m?
HÃ£y nhÃ¬n vÃ o Assembly cá»§a vÃ²ng láº·p:

```asm
; VÃ²ng láº·p tÃ­nh tá»•ng (Simplified x86)
Loop_Start:
    MOV  RBX, [IndexArr + RCX*4]   ; 1. Táº£i index ngáº«u nhiÃªn tá»« máº£ng IndexArr
                                   ;    (Náº¿u láº·p tuáº§n tá»±, Index cÃ³ sáºµn trong L1)

    MOV  EAX, [DataArr + RBX*4]    ; 2. DÃ¹ng index Ä‘Ã³ Ä‘á»ƒ táº£i Data
                                   ;    âš ï¸ CACHE MISS Lá»šN á»ž ÄÃ‚Y!
                                   ;    VÃ¬ RBX nháº£y lung tung, CPU khÃ´ng Ä‘oÃ¡n Ä‘Æ°á»£c.
                                   ;    CPU pháº£i Dá»ªNG (Stall) ~300 cycles Ä‘á»ƒ Ä‘á»£i RAM.

    ADD  SUM, EAX                  ; 3. Cá»™ng (chá»‰ máº¥t 1 cycle)
    INC  RCX                       ; 4. TÄƒng Ä‘áº¿m
    CMP  RCX, 1000000
    JNE  Loop_Start
```
*   **Sequential:** DÃ²ng 2 luÃ´n trÃºng Cache (Hit) vÃ¬ CPU tá»± Ä‘á»™ng prefetch dÃ²ng tiáº¿p theo.
*   **Random:** DÃ²ng 2 trÆ°á»£t Cache (Miss) liÃªn tá»¥c. Lá»‡nh `ADD` á»Ÿ dÃ²ng 3 khÃ´ng thá»ƒ cháº¡y cho Ä‘áº¿n khi dÃ²ng 2 xong. CPU ngá»“i chÆ¡i 99% thá»i gian!

```
BÃ i toÃ¡n: TÃ­nh tá»•ng 1 triá»‡u sá»‘ (1,000,000 ints = ~4 MB)

â•â•â• Ká»‹ch báº£n 1: Duyá»‡t tuáº§n tá»± (Sequential) â•â•â•

  for (int i = 0; i < 1000000; i++)
      sum += data[i];    // Cache Hit 15/16 láº§n = 93.75%

  PhÃ¢n tÃ­ch:
  - Táº£i cache line chá»©a data[0..15] â†’ ~100 cycles   (Miss)
  - Äá»c data[0]: 0 cycles  (Hit)
  - Äá»c data[1]: 0 cycles  (Hit)
  - ...
  - Äá»c data[15]: 0 cycles (Hit)
  - Táº£i cache line chá»©a data[16..31] â†’ ~100 cycles  (Miss)
  - ... láº·p láº¡i

  Tá»•ng thá»i gian: ~62,500 cache misses Ã— 100 cycles = ~6.25M cycles
  Tá»‘c Ä‘á»™ thá»±c táº¿: â˜…â˜…â˜…â˜…â˜… Cá»°C NHANH


â•â•â• Ká»‹ch báº£n 2: Duyá»‡t ngáº«u nhiÃªn (Random) â•â•â•

  for (int i = 0; i < 1000000; i++)
      sum += data[random_index[i]];    // Cache Miss ~100%

  PhÃ¢n tÃ­ch:
  - Má»—i random_index chá»‰ Ä‘áº¿n vá»‹ trÃ­ khÃ¡c nhau trong 4MB
  - 4MB >> L1 Cache (64KB) â†’ gáº§n nhÆ° má»i truy cáº­p Ä‘á»u Miss
  - 1,000,000 misses Ã— 100 cycles = ~100M cycles

  Tá»‘c Ä‘á»™ thá»±c táº¿: â˜…â˜†â˜†â˜†â˜† CHáº¬M Gáº¤P 16 Láº¦N!
```

### 6.4. Báº£ng tá»‘c Ä‘á»™ chi tiáº¿t â€” Memory Hierarchy

```mermaid
block-beta
    columns 1
    
    block:HighSpeed
        registers["Registers<br/>0ns"]
        l1["L1 Cache<br/>~1ns"]
    end
    
    block:MediumSpeed
        l2["L2 Cache<br/>~3ns"]
        l3["L3 Cache<br/>~10ns"]
    end
    
    block:MainMemory
        ram["DDR5 RAM<br/>~50-100ns"]
    end
    
    block:Storage
        ssd["SSD (NVMe)<br/>~10,000ns"]
        hdd["HDD<br/>~5,000,000ns"]
    end

    registers --> l1
    l1 --> l2
    l2 --> l3
    l3 --> ram
    ram --> ssd
    ssd --> hdd

    style registers fill:#ffcdd2,stroke:#b71c1c
    style l1 fill:#ffcdd2,stroke:#b71c1c
    style l2 fill:#fff9c4,stroke:#fbc02d
    style l3 fill:#fff9c4,stroke:#fbc02d
    style ram fill:#e1f5fe,stroke:#0277bd
    style ssd fill:#e0e0e0,stroke:#616161
    style hdd fill:#e0e0e0,stroke:#616161
```

> **Quy táº¯c vÃ ng:**
> - Má»—i táº§ng cháº­m hÆ¡n táº§ng trÃªn khoáº£ng 3-10Ã—
> - Má»—i táº§ng lá»›n hÆ¡n táº§ng trÃªn khoáº£ng 10-1000Ã—

---

## 7. Kiáº¿n trÃºc CPU Core â€” NÆ¡i má»i thá»© há»™i tá»¥

**Register File náº±m á»Ÿ Ä‘Ã¢u trong CPU?**

```mermaid
graph TD
    classDef unit fill:#e1f5fe,stroke:#01579b,stroke-width:2px;
    classDef storage fill:#fff3e0,stroke:#e65100,stroke-width:2px;
    classDef memory fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px;

    subgraph CPU_Core [CPU CORE #0]
        direction TB

        subgraph Control_Unit [â˜… CU â€” CONTROL UNIT - Báº¿p trÆ°á»Ÿng]
            direction TB
            Fetch[Fetch<br/>Táº£i lá»‡nh tá»« L1i]
            Decoder[Decoder<br/>Giáº£i mÃ£ â†’ Î¼ops]
            Scheduler[Scheduler / Rename<br/>PhÃ¢n cÃ´ng lá»‡nh]
            
            Fetch --> Decoder --> Scheduler
        end
        
        BP[Branch Predictor<br/>ÄoÃ¡n nhÃ¡nh if/else] -.-> Fetch

        RF[â˜…â˜…â˜… REGISTER FILE â˜…â˜…â˜…<br/>TRUNG TÃ‚M â€” Máº·t bÃ n báº¿p]:::storage

        subgraph Execution_Units [Execution Units - Äáº§u báº¿p]
            direction LR
            ALU[ALU INT<br/>+, -, logic]:::unit
            FPU[FPU FLOAT<br/>Ã—, Ã·, float]:::unit
        end

        subgraph Memory_Unit [â˜… MU â€” MEMORY UNIT - NV Kho]
            direction TB
            Load[Load Unit<br/>Äá»c data]
            Store[Store Unit<br/>Ghi data]
            TLB[TLB<br/>Cache Ä‘á»‹a chá»‰]
        end

        Scheduler --> RF
        Scheduler --> Memory_Unit
        Scheduler --> Execution_Units
        
        RF <==> Execution_Units
        RF <==> Memory_Unit
        
        subgraph L1_Cache [L1 Cache - Tá»§ láº¡nh báº¿p]
            L1d[L1 Data Cache<br/>32-64 KB<br/>SRAM]:::memory
        end

        subgraph L2_Cache [L2 Cache - Kho phá»¥]
            L2c[L2 Cache<br/>256KB-1MB]:::memory
        end

        Memory_Unit <==> L1d
        L1d <==> L2c
    end

    L3[L3 Cache (Shared)<br/>8-96 MB<br/>Kho táº§ng háº§m]:::memory
    RAM[DDR5 RAM<br/>16-64 GB<br/>SiÃªu thá»‹]:::memory

    L2c <==> L3
    L3 <==> RAM
```

| ThÃ nh pháº§n | Vai trÃ² | áº¨n dá»¥ nhÃ  báº¿p |
|---|---|---|
| **CU** | Äá»c lá»‡nh, giáº£i mÃ£, phÃ¢n cÃ´ng | ðŸ‘¨â€ðŸ³ Báº¿p trÆ°á»Ÿng |
| **Register File** | LÆ°u data Ä‘ang dÃ¹ng NGAY | ðŸ½ï¸ Máº·t bÃ n báº¿p |
| **ALU/FPU** | TÃ­nh toÃ¡n (+, -, Ã—, float) | ðŸ”ª Äáº§u báº¿p |
| **MU** | Láº¥y/cáº¥t data tá»« Cache/RAM | ðŸ“¦ NhÃ¢n viÃªn kho |
| **L1 Cache** | Kho nhá» ngay cáº¡nh báº¿p | ðŸ§Š Tá»§ láº¡nh báº¿p |
| **L2 Cache** | Kho dá»± trá»¯ trong nhÃ  | ðŸ  Kho phá»¥ |
| **L3 Cache** | Kho chung cho táº¥t cáº£ báº¿p | ðŸ—ï¸ Kho táº§ng háº§m |
| **DDR5 RAM** | Kho hÃ ng ngoáº¡i vi | ðŸª SiÃªu thá»‹ |

**DÃ²ng cháº£y lá»‡nh `MOV EAX, [address]`:**

1. **CU** Ä‘á»c lá»‡nh â†’ "Ã€, cáº§n load data tá»« bá»™ nhá»›"
2. **CU** giao cho **MU** (Load Unit) â†’ "Äi láº¥y data á»Ÿ Ä‘á»‹a chá»‰ nÃ y!"
3. **MU** kiá»ƒm tra L1 Cache:
   - **HIT?** â†’ Tráº£ data ngay (3-4 cycles)
   - **MISS?** â†’ Há»i L2 (10 cycles) â†’ L3 (30 cycles) â†’ RAM (200 cycles)
4. **MU** nháº­n data â†’ Ghi vÃ o **Register File** (EAX)
5. **CU** tiáº¿p tá»¥c lá»‡nh tiáº¿p theo (vÃ­ dá»¥: `ADD EAX, 5` â†’ gá»­i EAX tá»›i ALU)

> **Äiá»ƒm máº¥u chá»‘t:** Register File náº±m **NGAY TRUNG TÃ‚M** CPU Core, cÃ¡ch ALU chá»‰ vÃ i **micromet** (1 micromet = 1/1000 mm). TÃ­n hiá»‡u Ä‘iá»‡n Ä‘i tá»« Register â†’ ALU â†’ Register trong **cÃ¹ng 1 clock cycle**. ÄÃ¢y lÃ  lÃ½ do nÃ³ nhanh nháº¥t.

### 7.1. Register Renaming â€” áº¢o thuáº­t cá»§a CPU (NÃ¢ng cao)

Code Assembly dÃ¹ng cÃ¡c tÃªn cá»‘ Ä‘á»‹nh (`RAX`, `RBX`...), gá»i lÃ  **Architectural Registers** (16 cÃ¡i).
NhÆ°ng CPU hiá»‡n Ä‘áº¡i thá»±c sá»± cÃ³ hÃ ng trÄƒm **Physical Registers** (168+ cÃ¡i trÃªn Core i9).

**Táº¡i sao cáº§n Renaming?** â€” Äá»ƒ cháº¡y song song (Instruction Level Parallelism).

```asm
1. MOV EAX, 1     ; EAX(logic) â†’ Physical_Reg_10
2. ADD EAX, 5     ; DÃ¹ng PR_10

3. MOV EAX, 100   ; EAX(logic) â†’ Physical_Reg_99 (Äá»•i tÃªn!)
                  ; CPU khÃ´ng cáº§n chá» dÃ²ng 2 xong. NÃ³ cáº¥p ngay PR_99 má»›i.
4. ADD EAX, 2     ; DÃ¹ng PR_99
```

â†’ Lá»‡nh (3)-(4) cháº¡y **SONG SONG** vá»›i (1)-(2) vÃ¬ chÃºng dÃ¹ng thanh ghi váº­t lÃ½ KHÃC NHAU, dÃ¹ chung tÃªn `EAX`.

---

## 8. Cache Associativity â€” Dá»¯ liá»‡u náº±m á»Ÿ Ä‘Ã¢u trong Cache?

### 8.1. Ba cÃ¡ch tá»• chá»©c Cache

#### 1. Direct Mapped (Ãnh xáº¡ trá»±c tiáº¿p)
Má»—i Ä‘á»‹a chá»‰ RAM chá»‰ cÃ³ THá»‚ náº±m á»Ÿ **1 vá»‹ trÃ­ cá»‘ Ä‘á»‹nh** trong Cache.

```mermaid
graph LR
    subgraph RAM
        B0[Block 0]:::ram
        B4[Block 4]:::ram
        B8[Block 8]:::ram
    end
    
    subgraph Cache [Cache Lines]
        L0[Line 0]:::conflict
        L1[Line 1]:::cache
    end

    B0 --> L0
    B4 -.->|Conflict!| L0
    B8 -.->|Conflict!| L0

    classDef ram fill:#e1f5fe,stroke:#01579b
    classDef cache fill:#e8f5e9,stroke:#2e7d32
    classDef conflict fill:#ffcdd2,stroke:#c62828
```

- âœ… **Æ¯u:** ÄÆ¡n giáº£n, ráº», nhanh nháº¥t (do khÃ´ng cáº§n tÃ¬m kiáº¿m).
- âŒ **NhÆ°á»£c:** **Conflict Miss**. Náº¿u chÆ°Æ¡ng trÃ¬nh cáº§n dÃ¹ng cáº£ Block 0 vÃ  Block 4 cÃ¹ng lÃºc, chÃºng sáº½ Ä‘Ã¡ nhau liÃªn tá»¥c khá»i Line 0.

#### 2. Fully Associative (LiÃªn káº¿t hoÃ n toÃ n)
Má»—i block RAM cÃ³ thá»ƒ náº±m á»Ÿ **Báº¤T Ká»²** cache line nÃ o.

- âœ… **Æ¯u:** KhÃ´ng bao giá» cÃ³ Conflict Miss (trá»« khi cache Ä‘áº§y).
- âŒ **NhÆ°á»£c:** Pháº£i so sÃ¡nh tag vá»›i **TOÃ€N Bá»˜** cache lines song song â†’ Máº¡ch Ä‘iá»‡n cá»±c phá»©c táº¡p, tá»‘n Ä‘iá»‡n. Chá»‰ dÃ¹ng cho cache siÃªu nhá» (nhÆ° TLB).

#### 3. Set-Associative (N-way) â€” Phá»• biáº¿n nháº¥t
Cache chia thÃ nh cÃ¡c **Sets**. Block RAM thuá»™c vá» 1 Set cá»‘ Ä‘á»‹nh, nhÆ°ng cÃ³ thá»ƒ náº±m á»Ÿ **báº¥t ká»³ Way** nÃ o trong Set Ä‘Ã³.

**VÃ­ dá»¥: 4-Way Set Associative**
(Block 0, 4, 8 Ä‘á»u thuá»™c Set 0, nhÆ°ng Set 0 cÃ³ 4 chá»— chá»©a)

```mermaid
graph LR
    subgraph RAM
        B0[Blk 0]:::ram
        B4[Blk 4]:::ram
        B8[Blk 8]:::ram
    end

    subgraph Set0 [Set 0 (4 Ways)]
        direction TB
        W0[Way 0: Blk 0]:::cache
        W1[Way 1: Blk 4]:::cache
        W2[Way 2: Blk 8]:::cache
        W3[Way 3: Trá»‘ng]:::empty
    end

    B0 --> W0
    B4 --> W1
    B8 --> W2

    classDef ram fill:#e1f5fe,stroke:#01579b
    classDef cache fill:#fff9c4,stroke:#fbc02d
    classDef empty fill:#f5f5f5,stroke:#bdbdbd,stroke-dasharray: 5 5
```

- âœ… **CÃ¢n báº±ng:** Giáº£m conflict miss Ä‘Ã¡ng ká»ƒ mÃ  khÃ´ng quÃ¡ Ä‘áº¯t Ä‘á» nhÆ° Fully Associative.
- ðŸ’¡ **Thá»±c táº¿:** L1 thÆ°á»ng lÃ  8-way, L2 lÃ  16-way.

> **ðŸŽ¯ áº¨n dá»¥ â€” Tá»§ khÃ³a KÃ½ tÃºc xÃ¡:**
> - **Direct Mapped** = Má»—i sinh viÃªn Ä‘Æ°á»£c gÃ¡n **Ä‘Ãºng 1 tá»§ cá»‘ Ä‘á»‹nh** (theo sá»‘ MSSV). Náº¿u 2 SV cÃ¹ng hash vá» 1 tá»§ â†’ tranh nhau, pháº£i luÃ¢n phiÃªn bá» Ä‘á»“ ra.
> - **Fully Associative** = Sinh viÃªn Ä‘Æ°á»£c chá»n **Báº¤T Ká»² tá»§ nÃ o trá»‘ng**. Tuyá»‡t vá»i! NhÆ°ng má»—i láº§n tÃ¬m Ä‘á»“ pháº£i má»Ÿ **Táº¤T Cáº¢** tá»§ Ä‘á»ƒ check â†’ cháº­m.
> - **Set-Associative (4-way)** = Má»—i SV Ä‘Æ°á»£c gÃ¡n **1 dÃ£y (set) gá»“m 4 tá»§**. Chá»n tá»§ nÃ o trá»‘ng trong dÃ£y Ä‘Ã³. TÃ¬m Ä‘á»“ chá»‰ cáº§n check 4 tá»§ thay vÃ¬ hÃ ng trÄƒm â†’ cÃ¢n báº±ng hoÃ n háº£o!

---

## 9. Cache Coherency â€” Váº¥n Ä‘á» Ä‘a lÃµi

### 9.1. False Sharing â€” "Káº» thÃ¹ giáº¥u máº·t" cá»§a Ä‘a luá»“ng

```
Ká»‹ch báº£n:
  2 lÃµi CPU cÃ¹ng truy cáº­p máº£ng counters[], nhÆ°ng TRÃŠ2 pháº§n tá»­ khÃ¡c nhau.

  struct Counters {
      public int countA;  // Core 0 dÃ¹ng
      public int countB;  // Core 1 dÃ¹ng
  }
  // sizeof(Counters) = 8 bytes
  // Cáº£ countA vÃ  countB náº±m trÃªn CÃ™NG 1 cache line (64 bytes)!


  Core 0                           Core 1
  â”€â”€â”€â”€â”€â”€                           â”€â”€â”€â”€â”€â”€
  countA++                         countB++
     â”‚                                â”‚
     â–¼                                â–¼
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Cache Line (64 bytes):                         â”‚
  â”‚  [countA=1] [countB=0] [padding...............]  â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
     â”‚                                â”‚
     â”‚  "TÃ´i sá»­a cache line nÃ y!"    â”‚  "TÃ´i CÅ¨NG sá»­a cache line nÃ y!"
     â”‚                                â”‚
     â–¼                                â–¼
  MESI Protocol báº¯t buá»™c:
  1. Core 0 ghi countA â†’ Ä‘Ã¡nh dáº¥u cache line = "Modified"
  2. Core 1 muá»‘n ghi countB â†’ pháº£i INVALIDATE cache line á»Ÿ Core 0
  3. Core 0 flush cache line vá» L3 â†’ Core 1 táº£i láº¡i tá»« L3
  4. Core 1 ghi countB â†’ Ä‘Ã¡nh dáº¥u "Modified"
  5. Core 0 muá»‘n ghi countA láº§n ná»¯a â†’ láº¡i pháº£i invalidate...
  
  â†’ PING-PONG liÃªn tá»¥c! Má»—i láº§n = ~40-100 cycles wasted
  â†’ Hiá»‡u nÄƒng GIáº¢M tá»›i 10-100Ã— so vá»›i dÃ¹ng 1 lÃµi!
```

> **ðŸŽ¯ áº¨n dá»¥ â€” 2 ngÆ°á»i viáº¿t cÃ¹ng 1 trang vá»Ÿ:**
> TÆ°á»Ÿng tÆ°á»£ng 2 ngÆ°á»i ngá»“i 2 bÃ n, má»—i ngÆ°á»i viáº¿t **á»Ÿ GÃ“C RIÃŠNG** cá»§a cÃ¹ng 1 trang giáº¥y.
> - NgÆ°á»i A viáº¿t gÃ³c trÃ¡i â†’ xong, Ä‘Æ°a trang giáº¥y cho NgÆ°á»i B.
> - NgÆ°á»i B viáº¿t gÃ³c pháº£i â†’ xong, Ä‘Æ°a láº¡i cho NgÆ°á»i A.
> - DÃ¹ há» **KHÃ”NG CHáº M vÃ o chá»¯ cá»§a nhau**, nhÆ°ng vÃ¬ cÃ¹ng 1 trang giáº¥y (= cÃ¹ng 1 Cache Line), há» pháº£i **chuyá»n qua chuyá»n láº¡i** liÃªn tá»¥c.
> - **Giáº£i phÃ¡p:** Cho má»—i ngÆ°á»i viáº¿t trÃªn **TRANG RIÃŠNG** (= padding Ä‘á»ƒ tÃ¡ch cache line) â†’ khÃ´ng cáº§n chá» nhau ná»¯a!

**Giáº£i phÃ¡p: Äá»‡m (Padding) Ä‘á»ƒ tÃ¡ch cache line**

```csharp
struct CountersPadded {
    public int countA;
    // 60 bytes padding â†’ Ä‘áº©y countB sang cache line khÃ¡c
    fixed byte _pad[60];
    public int countB;
}

// Hoáº·c trong Unity DOTS:
// [NativeDisableContainerSafetyRestriction]
// â†’ Äáº·t dá»¯ liá»‡u cá»§a má»—i Job trÃªn chunk riÃªng biá»‡t
```

### 9.2. MESI Protocol â€” Quy Æ°á»›c Ä‘á»“ng bá»™ Cache

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  MESI = 4 tráº¡ng thÃ¡i cá»§a má»—i Cache Line                     â”‚
â”‚                                                              â”‚
â”‚  M (Modified):   Chá»‰ core nÃ y cÃ³ data Má»šI NHáº¤T              â”‚
â”‚                  RAM Ä‘Ã£ lá»—i thá»i (pháº£i ghi láº¡i khi evict)   â”‚
â”‚                                                              â”‚
â”‚  E (Exclusive):  Chá»‰ core nÃ y cÃ³, nhÆ°ng GIá»NG vá»›i RAM       â”‚
â”‚                  CÃ³ thá»ƒ chuyá»ƒn sang M mÃ  khÃ´ng bÃ¡o ai       â”‚
â”‚                                                              â”‚
â”‚  S (Shared):     NHIá»€U cores Ä‘á»u cÃ³ copy giá»‘ng nhau          â”‚
â”‚                  Muá»‘n ghi â†’ pháº£i invalidate cÃ¡c core khÃ¡c   â”‚
â”‚                                                              â”‚
â”‚  I (Invalid):    Cache line nÃ y KHÃ”NG Há»¢P Lá»†                â”‚
â”‚                  Pháº£i táº£i láº¡i tá»« L3/RAM náº¿u cáº§n             â”‚
â”‚                                                              â”‚
â”‚  Chuyá»ƒn tráº¡ng thÃ¡i:                                          â”‚
â”‚  I â”€â”€Readâ”€â”€â–º E â”€â”€Writeâ”€â”€â–º M                                  â”‚
â”‚  E â”€â”€Other core readsâ”€â”€â–º S                                   â”‚
â”‚  S â”€â”€Writeâ”€â”€â–º M (+ Invalidate others â†’ I)                    â”‚
â”‚  M â”€â”€Other core readsâ”€â”€â–º S (+ Flush to L3)                   â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## 10. Káº¿t ná»‘i Unity â€” Cache Locality lÃ  táº¥t cáº£

### 10.1. MonoBehaviour vs ECS â€” CÃ¢u chuyá»‡n Cache Line

**â•â•â• Classic MonoBehaviour (OOP) â€” Cache NIGHTMARE â•â•â•**

```csharp
class Enemy : MonoBehaviour {
    Vector3 position;     // 12 bytes
    float health;          // 4 bytes
    string name;           // 8 bytes (reference)
    Rigidbody rb;          // 8 bytes (reference)
    Animator animator;     // 8 bytes (reference)
    // ... + MonoBehaviour overhead = ~100+ bytes
}
```

```
Bá»™ nhá»› Heap (rá»i ráº¡c, ngáº«u nhiÃªn):
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚Enemy[0]â”‚  â”‚ String â”‚  â”‚Enemy[1]â”‚  â”‚ Sound  â”‚
  â”‚ @0x100 â”‚  â”‚ @0x280 â”‚  â”‚ @0x500 â”‚  â”‚ @0x390 â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”˜
       â†‘           â†‘           â†‘           â†‘
  Cache Line A  Cache Line E  Cache Line I  Cache Line G

  Duyá»‡t Enemy[0] â†’ Cache Miss (táº£i Line A)
  Duyá»‡t Enemy[1] â†’ Cache Miss (táº£i Line I)  â† KHÃC cache line!
  Duyá»‡t Enemy[2] â†’ Cache Miss (á»Ÿ Ä‘Ã¢u Ä‘Ã³ khÃ¡c trÃªn Heap)

  â†’ Cá»© Má»–I enemy = 1 Cache Miss = 200 cycles wasted
  â†’ 10,000 enemies = 2,000,000 cycles wasted = ~0.4ms á»Ÿ 5GHz
     (ChÆ°a ká»ƒ pointer chasing: position â†’ rb â†’ collider â†’ ...)
```

#### > The Pointer Chasing Problem (Assembly):
Äá»ƒ láº¥y `enemy.transform.position`, CPU pháº£i "sÄƒn tÃ¬m Ä‘á»‹a chá»‰" (pointer chasing):

```asm
MOV  R1, [EnemyAddress]        ; Táº£i Ä‘á»‹a chá»‰ object Enemy
MOV  R2, [R1 + TransformOffset]; Táº£i Ä‘á»‹a chá»‰ Transform component (CACHE MISS?)
MOV  R3, [R2 + PositionOffset] ; Táº£i dá»¯ liá»‡u Position (CACHE MISS?)
```

- Tá»‡ háº¡i: Lá»‡nh 2 **PHá»¤ THUá»˜C** vÃ o R1 tá»« lá»‡nh 1. Lá»‡nh 3 **PHá»¤ THUá»˜C** vÃ o R2 tá»« lá»‡nh 2.
- CPU khÃ´ng thá»ƒ "cháº¡y trÆ°á»›c" (Instruction Level Parallelism).
- Náº¿u lá»‡nh 1 Miss Cache, lá»‡nh 2 vÃ  3 pháº£i Ä‘á»£i â†’ **Chuá»—i dÃ¢y chuyá»n tháº£m há»a.**

---

**â•â•â• Unity ECS (DOD) â€” Cache PARADISE â•â•â•**

```csharp
struct Position : IComponentData { public float3 Value; }  // 12 bytes
struct Health : IComponentData { public float Value; }       // 4 bytes
```

```
Archetype Chunk (16 KB, contiguous):
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚ Position Data (liÃªn tá»¥c):                                    â”‚
  â”‚ [pos0][pos1][pos2][pos3][pos4][pos5]...[pos659]              â”‚
  â”‚  12B   12B   12B   12B   12B   12B      12B                 â”‚
  â”‚ â—„â”€â”€â”€â”€ Cache Line (64B) = 5 positions â”€â”€â”€â”€â–º                  â”‚
  â”‚                                                              â”‚
  â”‚ Health Data (liÃªn tá»¥c):                                      â”‚
  â”‚ [hp0][hp1][hp2][hp3][hp4][hp5]...[hp659]                    â”‚
  â”‚  4B   4B   4B   4B   4B   4B      4B                        â”‚
  â”‚ â—„â”€â”€â”€â”€ Cache Line (64B) = 16 healths â”€â”€â”€â”€â–º                   â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

  Duyá»‡t Position:
  - Táº£i cache line â†’ cÃ³ 5 positions miá»…n phÃ­!
  - Cache Hit 4/5 = 80%
  - 10,000 entities Ã· 5 per line = 2,000 misses
  - 2,000 Ã— 100 cycles = 200,000 cycles = ~0.04ms

  â†’ ECS nhanh hÆ¡n MonoBehaviour ~10Ã— chá»‰ nhá» Cache Locality!
```

### 10.2. Táº¡i sao NativeArray khÃ´ng cÃ³ GC?

**C# Managed Array** (`new int[]`):
- Cáº¥p phÃ¡t trÃªn **Managed Heap**
- GC pháº£i quÃ©t (scan) Ä‘á»ƒ biáº¿t array cÃ²n dÃ¹ng khÃ´ng
- GC cÃ³ thá»ƒ **DI CHUYá»‚N** array (compaction) â†’ Ä‘á»‹a chá»‰ thay Ä‘á»•i
- KhÃ´ng thá»ƒ dÃ¹ng trong Burst (Burst cáº§n Ä‘á»‹a chá»‰ cá»‘ Ä‘á»‹nh cho SIMD)

**NativeArray\<int\>:**
- Cáº¥p phÃ¡t trÃªn **Unmanaged Heap** (qua `Marshal.AllocHGlobal` hoáº·c `UnsafeUtility`)
- GC **KHÃ”NG BIáº¾T** nÃ³ tá»“n táº¡i â†’ Zero GC pressure
- Äá»‹a chá»‰ **Cá» Äá»ŠNH** â†’ Burst dÃ¹ng trá»±c tiáº¿p cho SIMD
- Developer **PHáº¢I tá»± Dispose()** â†’ náº¿u quÃªn = Memory Leak

```
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Managed Heap (GC quáº£n lÃ½):                         â”‚
  â”‚  [string] [List<T>] [MonoBehaviour] [GameObject]    â”‚
  â”‚  â†‘ GC scan toÃ n bá»™ vÃ¹ng nÃ y Ä‘á»‹nh ká»³                â”‚
  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
  â”‚  Unmanaged Heap (Dev tá»± quáº£n lÃ½):                   â”‚
  â”‚  [NativeArray] [NativeList] [NativeHashMap]         â”‚
  â”‚  â†‘ GC KHÃ”NG CHáº M vÃ o vÃ¹ng nÃ y                      â”‚
  â”‚  â†‘ Burst Compiler truy cáº­p TRá»°C TIáº¾P               â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 10.3. Allocator Types â€” Chá»n Ä‘Ãºng táº§ng bá»™ nhá»›

| Allocator | MÃ´ táº£ | Æ¯u/NhÆ°á»£c | DÃ¹ng cho |
|---|---|---|---|
| **`Allocator.Temp`** | Stack-like, xÃ³a cuá»‘i frame | âœ… Cá»±c nhanh (khÃ´ng lock) Â· âŒ Chá»‰ sá»‘ng 1 frame | Káº¿t quáº£ táº¡m trong `Update()` |
| **`Allocator.TempJob`** | Sá»‘ng qua nhiá»u frame, tá»± xÃ³a sau 4 frame | âœ… An toÃ n cho Jobs Â· âŒ KhÃ´ng quÃ¡ lÃ¢u dÃ i | `IJobParallelFor` data |
| **`Allocator.Persistent`** | Sá»‘ng Ä‘áº¿n khi báº¡n `Dispose()` | âœ… DÃ i háº¡n Â· âŒ Cháº­m hÆ¡n, PHáº¢I tá»± Dispose | Lookup tables, spatial hash |

---

## 11. Tá»•ng káº¿t Chapter 2

```
Chuá»—i tiáº¿n hÃ³a bá»™ nhá»›:

  2 NOR Gates (8 transistors) â†’ SR Latch (nhá»› 1 bit)
       â”‚
       â–¼
  D Flip-flop (nhá»› 1 bit theo nhá»‹p Clock)
       â”‚
       â–¼
  32 D-FF = 1 Register (nhá»› 1 sá»‘ 32-bit)
       â”‚
       â–¼
  SRAM (6T/bit) â†’ L1/L2/L3 Cache (nhanh, Ä‘áº¯t, nhá»)
       â”‚
       â–¼
  DRAM (1T+1C/bit) â†’ DDR5 RAM (cháº­m hÆ¡n, ráº», lá»›n)
       â”‚
       â–¼
  NAND Flash â†’ SSD (ráº¥t cháº­m, ráº¥t ráº», ráº¥t lá»›n)
```

> **BÃ i há»c quan trá»ng nháº¥t:**
> - KhÃ´ng pháº£i **thuáº­t toÃ¡n nÃ o nhanh hÆ¡n** mÃ  lÃ  **dá»¯ liá»‡u nÃ o gáº§n CPU hÆ¡n**.
> - `O(n)` tuáº§n tá»± trÃªn Cache nhanh hÆ¡n `O(log n)` nháº£y ngáº«u nhiÃªn trÃªn RAM.
> - Unity ECS nhanh khÃ´ng pháº£i vÃ¬ ECS "thÃ´ng minh hÆ¡n", mÃ  vÃ¬ nÃ³ **Ä‘áº·t dá»¯ liá»‡u Ä‘Ãºng chá»—** Ä‘á»ƒ CPU Cache hoáº¡t Ä‘á»™ng hiá»‡u quáº£ nháº¥t.

---

> **ChÆ°Æ¡ng tiáº¿p theo:** [Chapter 3 â€” CPU, ISA & Programming Languages]() â€” CÃ¡ch CPU thá»±c thi lá»‡nh, Pipeline, Branch Prediction, vÃ  con Ä‘Æ°á»ng tá»« C# â†’ IL â†’ Native Code.

---
*Chapter 2 â€” NghiÃªn cá»©u cho Unity High-Performance Agent*
# ChÆ°Æ¡ng 3: CPU Execution, ISA & Programming Languages

> **Má»¥c tiÃªu chÆ°Æ¡ng:** Hiá»ƒu cÃ¡ch CPU thá»±c thi mÃ£ mÃ¡y tá»«ng bÆ°á»›c, táº¡i sao Pipeline vÃ  Branch Prediction áº£nh hÆ°á»Ÿng trá»±c tiáº¿p Ä‘áº¿n game performance, vÃ  con Ä‘Æ°á»ng Ä‘áº§y Ä‘á»§ tá»« C# source code â†’ mÃ£ mÃ¡y native trong Unity.

---

## 1. Instruction Set Architecture (ISA) â€” NgÃ´n ngá»¯ máº¹ Ä‘áº» cá»§a CPU

### 1.1. ISA lÃ  gÃ¬?

ISA lÃ  **báº£n há»£p Ä‘á»“ng** giá»¯a pháº§n cá»©ng (CPU) vÃ  pháº§n má»m (Compiler/OS). NÃ³ Ä‘á»‹nh nghÄ©a:
- Táº­p lá»‡nh CPU hiá»ƒu Ä‘Æ°á»£c (ADD, MOV, JUMP, ...)
- Thanh ghi nÃ o cÃ³ sáºµn (RAX, RSP, XMM0, ...)
- CÃ¡ch Ä‘Ã¡nh Ä‘á»‹a chá»‰ bá»™ nhá»› (Addressing Modes)
- KÃ­ch thÆ°á»›c dá»¯ liá»‡u (8/16/32/64-bit)

```
Táº§ng abstraction:

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  C#:  health -= damage;                          â”‚   â† NgÃ´n ngá»¯ báº­c cao
  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
  â”‚  IL:  ldarg.0                                    â”‚   â† Bytecode trung gian
  â”‚       ldfld float Health::Value                  â”‚
  â”‚       ldarg.1                                    â”‚
  â”‚       sub                                        â”‚
  â”‚       stfld float Health::Value                  â”‚
  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
  â”‚  x86 ASM:                                        â”‚   â† Assembly (1:1 vá»›i ISA)
  â”‚       movss  xmm0, [rcx+0x10]   ; load health   â”‚
  â”‚       subss  xmm0, xmm1         ; health -= dmg â”‚
  â”‚       movss  [rcx+0x10], xmm0   ; store back    â”‚
  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
  â”‚  Machine Code:                                   â”‚   â† Nhá»‹ phÃ¢n thuáº§n
  â”‚       F3 0F 10 41 10                             â”‚
  â”‚       F3 0F 5C C1                                â”‚
  â”‚       F3 0F 11 41 10                             â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
       â†‘
  Má»—i byte â†’ bá»™ giáº£i mÃ£ â†’ tÃ­n hiá»‡u Ä‘iá»u khiá»ƒn ALU/FPU/Load-Store Unit.
```

#### > Anatomy of an Instruction (Giáº£i pháº«u lá»‡nh):
Lá»‡nh `ADD EAX, EBX` (01 03) trong x86:

```
  0000 0001   0000 0011
  â””â”€â”€â”¬â”€â”€â”€â”€â”˜   â””â”€â”€â”¬â”€â”€â”€â”€â”˜
    Opcode      ModR/M
    (ADD)      (EAX, EBX)

  CPU Decoder Ä‘á»c 2 bytes nÃ y â†’ Biáº¿t ráº±ng:
  1. Cáº§n dÃ¹ng máº¡ch ADDER (Chapter 1).
  2. Input 1 lÃ  Register EAX (Chapter 2).
  3. Input 2 lÃ  Register EBX (Chapter 2).
  4. Káº¿t quáº£ ghi láº¡i vÃ o EAX.
```

### 1.2. CISC vs RISC â€” Hai triáº¿t lÃ½ thiáº¿t káº¿ ISA

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                    CISC vs RISC                                     â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚        CISC             â”‚            RISC                           â”‚
â”‚  (Complex Instruction   â”‚    (Reduced Instruction                   â”‚
â”‚   Set Computer)         â”‚     Set Computer)                         â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ Äáº¡i diá»‡n: x86-64        â”‚ Äáº¡i diá»‡n: ARM, RISC-V                    â”‚
â”‚ Intel, AMD              â”‚ Apple Silicon, Qualcomm                   â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ Lá»‡nh PHá»¨C Táº P:          â”‚ Lá»‡nh ÄÆ N GIáº¢N:                          â”‚
â”‚ 1 lá»‡nh cÃ³ thá»ƒ lÃ m      â”‚ 1 lá»‡nh chá»‰ lÃ m 1 viá»‡c                   â”‚
â”‚ nhiá»u viá»‡c cÃ¹ng lÃºc     â”‚                                           â”‚
â”‚                         â”‚                                           â”‚
â”‚ VÃ­ dá»¥:                  â”‚ VÃ­ dá»¥:                                    â”‚
â”‚ ADD [mem], reg           â”‚ LDR  R1, [mem]    ; Load                â”‚
â”‚ (Äá»c RAM + Cá»™ng +       â”‚ ADD  R1, R1, R2   ; Cá»™ng                â”‚
â”‚  Ghi láº¡i RAM trong      â”‚ STR  R1, [mem]    ; Ghi                 â”‚
â”‚  1 lá»‡nh duy nháº¥t)       â”‚ (3 lá»‡nh riÃªng biá»‡t)                     â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ KÃ­ch thÆ°á»›c lá»‡nh:        â”‚ KÃ­ch thÆ°á»›c lá»‡nh:                         â”‚
â”‚ 1 â†’ 15 bytes (biáº¿n Ä‘á»•i)â”‚ 4 bytes Cá» Äá»ŠNH (ARM)                   â”‚
â”‚ â†’ Bá»™ giáº£i mÃ£ phá»©c táº¡p  â”‚ â†’ Bá»™ giáº£i mÃ£ Ä‘Æ¡n giáº£n, nhanh             â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ Æ¯u Ä‘iá»ƒm:                â”‚ Æ¯u Ä‘iá»ƒm:                                  â”‚
â”‚ âœ… Code compact (Ã­t byte)â”‚ âœ… Pipeline hiá»‡u quáº£ hÆ¡n                 â”‚
â”‚ âœ… TÆ°Æ¡ng thÃ­ch ngÆ°á»£c     â”‚ âœ… Tiáº¿t kiá»‡m nÄƒng lÆ°á»£ng                  â”‚
â”‚    (cháº¡y code tá»« 1978)  â”‚ âœ… Dá»… tá»‘i Æ°u cho compiler                 â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ Ná»n táº£ng:                â”‚ Ná»n táº£ng:                                 â”‚
â”‚ PC, PlayStation, Xbox    â”‚ Mobile, Switch, Mac (M-series)           â”‚
â”‚ Server                   â”‚ VR Headset (Quest)                       â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ Unity build target:      â”‚ Unity build target:                       â”‚
â”‚ Windows x64, Linux x64  â”‚ Android ARM64, iOS ARM64                 â”‚
â”‚ macOS x64 (Intel Mac)   â”‚ macOS ARM64 (Apple Silicon)              â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

> **Thá»±c táº¿ hiá»‡n Ä‘áº¡i:** CPU x86 cá»§a Intel/AMD bÃªn ngoÃ i lÃ  CISC, nhÆ°ng bÃªn trong giáº£i mÃ£ thÃ nh **micro-ops** (Î¼ops) giá»‘ng RISC rá»“i má»›i thá»±c thi. Ranh giá»›i CISC/RISC ngÃ y nay Ä‘Ã£ má» Ä‘i ráº¥t nhiá»u.

### 1.3. Má»™t sá»‘ lá»‡nh Assembly quan trá»ng cho Unity Developer

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                  x86-64 ASSEMBLY â€” Lá»†NH THÆ¯á»œNG Gáº¶P                      â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚  Lá»‡nh    â”‚  Ã nghÄ©a            â”‚  Gáº·p á»Ÿ Ä‘Ã¢u trong Unity?                â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ MOV      â”‚ Copy dá»¯ liá»‡u        â”‚ Má»i nÆ¡i (gÃ¡n biáº¿n, load field)        â”‚
â”‚ ADD/SUB  â”‚ Cá»™ng/Trá»«            â”‚ position += velocity                   â”‚
â”‚ MUL/IMUL â”‚ NhÃ¢n                â”‚ scale * direction                      â”‚
â”‚ CMP      â”‚ So sÃ¡nh             â”‚ if (health <= 0)                       â”‚
â”‚ JE/JNE   â”‚ Nháº£y náº¿u báº±ng/khÃ¡c â”‚ Branching (if/else/switch)             â”‚
â”‚ CALL     â”‚ Gá»i hÃ m            â”‚ Má»—i method call                        â”‚
â”‚ RET      â”‚ Return tá»« hÃ m      â”‚ Káº¿t thÃºc method                        â”‚
â”‚ PUSH/POP â”‚ Stack operations    â”‚ LÆ°u/khÃ´i phá»¥c registers khi gá»i hÃ m   â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚          â”‚   SIMD (Burst)       â”‚                                        â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ MOVAPS   â”‚ Load 128-bit alignedâ”‚ Load float4 vÃ o XMM register           â”‚
â”‚ ADDPS    â”‚ Add Packed Singles  â”‚ float4 a + b (4 phÃ©p cá»™ng cÃ¹ng lÃºc)   â”‚
â”‚ MULPS    â”‚ Mul Packed Singles  â”‚ float4 a * b (4 phÃ©p nhÃ¢n cÃ¹ng lÃºc)   â”‚
â”‚ SHUFPS   â”‚ Shuffle floats     â”‚ Swizzle (a.xyzw â†’ a.wzyx)             â”‚
â”‚ DPPS     â”‚ Dot Product         â”‚ math.dot(a, b)                         â”‚
â”‚ RSQRTPS  â”‚ Fast 1/sqrt        â”‚ math.rsqrt() cho normalize             â”‚
â”‚ VFMADD   â”‚ Fused Multiply-Add â”‚ a * b + c trong 1 lá»‡nh (AVX2)         â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


VÃ­ dá»¥ thá»±c táº¿ â€” Burst biÃªn dá»‹ch float3 addition:

  C# (trong IJobParallelFor):
  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  position.Value += velocity.Value * deltaTime;


  Burst output (x86-64 + AVX):
  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  vbroadcastss  ymm2, [deltaTime]         ; NhÃ¢n rá»™ng deltaTime sang 8 slots
  vmulps        ymm1, ymm0, ymm2          ; velocity * deltaTime (8 floats)
  vaddps        ymm3, ymm1, [positions]   ; position + result    (8 floats)
  vmovaps       [positions], ymm3         ; Store káº¿t quáº£


  â†’ 3 lá»‡nh SIMD thay cho 24 lá»‡nh scalar!
  â†’ Burst tá»± phÃ¡t hiá»‡n pattern vÃ  vectorize.
  â†’ ÄÃ¢y lÃ  lÃ½ do [BurstCompile] nhanh hÆ¡n Mono 5-10Ã—.
```

---

## 2. CPU Pipeline â€” DÃ¢y chuyá»n láº¯p rÃ¡p lá»‡nh

### 2.1. Pipeline cÆ¡ báº£n (5 giai Ä‘oáº¡n)

Náº¿u má»—i lá»‡nh pháº£i hoÃ n thÃ nh táº¥t cáº£ bÆ°á»›c trÆ°á»›c khi báº¯t Ä‘áº§u lá»‡nh tiáº¿p, CPU sáº½ cá»±c ká»³ lÃ£ng phÃ­. **Pipeline** giáº£i quyáº¿t Ä‘iá»u nÃ y báº±ng cÃ¡ch overlap cÃ¡c giai Ä‘oáº¡n:

```
â•â•â• KHÃ”NG cÃ³ Pipeline (Sequential) â•â•â•

  Lá»‡nh 1: [Fetch][Decode][Execute][Memory][WriteBack]
  Lá»‡nh 2:                                             [Fetch][Decode][Execute][Memory][WriteBack]
  Lá»‡nh 3:                                                                                        [Fetch]...

  â†’ 5 cycles/lá»‡nh. Äá»ƒ xá»­ lÃ½ 3 lá»‡nh cáº§n 15 cycles.
  â†’ 4/5 bá»™ pháº­n CPU NGá»’I KHÃ”NG trong má»—i cycle!


â•â•â• CÃ“ Pipeline (Overlapped) â•â•â•

  Cycle:       1      2      3      4      5      6      7
  Lá»‡nh 1: [Fetch][Decode][Exec ][Mem  ][Write]
  Lá»‡nh 2:        [Fetch][Decode][Exec ][Mem  ][Write]
  Lá»‡nh 3:               [Fetch][Decode][Exec ][Mem  ][Write]

  â†’ Sau khi pipeline Ä‘áº§y (cycle 5), má»—i cycle hoÃ n thÃ nh 1 lá»‡nh!
  â†’ 3 lá»‡nh chá»‰ cáº§n 7 cycles thay vÃ¬ 15.
  â†’ Throughput: ~1 lá»‡nh/cycle (IPC â‰ˆ 1)

#### > Visualizing the Pipeline (Assembly View):
Giáº£ sá»­ ta cÃ³ 3 lá»‡nh Assembly liÃªn tiáº¿p:
1. `MOV EAX, 10`
2. `ADD EAX, 5`
3. `MOV [Ptr], EAX`

```
Time (Cycles) â”€â”€â–º
      1      2      3      4      5      6      7
   â”Œâ”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”
1. â”‚ IF â”‚ â”‚ ID â”‚ â”‚ EX â”‚ â”‚ MEMâ”‚ â”‚ WB â”‚  (MOV EAX, 10)
   â””â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”˜
          â”Œâ”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”
2.        â”‚ IF â”‚ â”‚ ID â”‚ â”‚ EX â”‚ â”‚ MEMâ”‚ â”‚ WB â”‚  (ADD EAX, 5)
          â””â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”˜
                 â”Œâ”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”
3.               â”‚ IF â”‚ â”‚ ID â”‚ â”‚ EX â”‚ â”‚ MEMâ”‚ â”‚ WB â”‚  (MOV [Ptr], EAX)
                 â””â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”˜
```
**Táº¡i cycle 3:**
*   Lá»‡nh 1 Ä‘ang Thá»±c thi (EX).
*   Lá»‡nh 2 Ä‘ang Giáº£i mÃ£ (ID).
*   Lá»‡nh 3 Ä‘ang Ä‘Æ°á»£c Táº£i vá» (IF).
*   â†’ **3 pháº§n cá»§a CPU Ä‘ang lÃ m viá»‡c CÃ™NG LÃšC!**


áº¨n dá»¥ â€” Giáº·t Ä‘á»“:
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Báº¡n cÃ³ 3 bÆ°á»›c: Giáº·t (30p) â†’ Sáº¥y (30p) â†’ Gáº¥p (30p)          â”‚
  â”‚                                                                â”‚
  â”‚  KhÃ´ng Pipeline: Cuá»™n 1 xong háº¿t má»›i báº¯t Ä‘áº§u Cuá»™n 2           â”‚
  â”‚    â†’ 3 cuá»™n Ã— 90 phÃºt = 270 phÃºt                              â”‚
  â”‚                                                                â”‚
  â”‚  CÃ³ Pipeline: Cuá»™n 1 Ä‘ang Sáº¥y â†’ bá» Cuá»™n 2 vÃ o Giáº·t           â”‚
  â”‚    â†’ Cuá»™n 1: 90p, Cuá»™n 2: thÃªm 30p, Cuá»™n 3: thÃªm 30p        â”‚
  â”‚    â†’ Tá»•ng: 150 phÃºt (tiáº¿t kiá»‡m 44%!)                          â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 2.2. Pipeline hiá»‡n Ä‘áº¡i â€” Superscalar & Out-of-Order

CPU hiá»‡n Ä‘áº¡i (Zen 5, Intel Core Ultra) cÃ³ pipeline **19-25 stages** vÃ  lÃ  **superscalar** (nhiá»u pipeline cháº¡y song song):

```
CPU Pipeline hiá»‡n Ä‘áº¡i (Ä‘Æ¡n giáº£n hÃ³a):

  Instruction Stream (DÃ²ng lá»‡nh tá»« RAM/Cache):
  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  â”‚ ADD â”‚ SUB â”‚ MUL â”‚ LOAD â”‚ CMP â”‚ JNE â”‚ ...
  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
       â”‚
       â–¼
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  FRONT-END (Thu tháº­p & Giáº£i mÃ£)                             â”‚
  â”‚                                                             â”‚
  â”‚  â‘  Fetch: Táº£i 16-32 bytes lá»‡nh tá»« L1i Cache                â”‚
  â”‚     â†“                                                       â”‚
  â”‚  â‘¡ Pre-decode: XÃ¡c Ä‘á»‹nh ranh giá»›i lá»‡nh (x86 = biáº¿n Ä‘á»•i)   â”‚
  â”‚     â†“                                                       â”‚
  â”‚  â‘¢ Decode: Chuyá»ƒn x86 â†’ Î¼ops (micro-operations)            â”‚
  â”‚     - 1 lá»‡nh Ä‘Æ¡n giáº£n â†’ 1 Î¼op                              â”‚
  â”‚     - 1 lá»‡nh phá»©c táº¡p â†’ 2-4 Î¼ops                           â”‚
  â”‚     â†“                                                       â”‚
  â”‚  â‘£ Î¼op Cache: LÆ°u Î¼ops Ä‘Ã£ decode (trÃ¡nh decode láº¡i)        â”‚
  â”‚     â†“                                                       â”‚
  â”‚  â‘¤ Rename: Äá»•i tÃªn registers áº£o â†’ váº­t lÃ½ (trÃ¡nh hazards)   â”‚
  â”‚     â†“                                                       â”‚
  â”‚  â‘¥ Allocate & Dispatch: ÄÆ°a Î¼ops vÃ o Reservation Stations  â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                               â”‚
                               â–¼
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  BACK-END (Thá»±c thi â€” Out-of-Order)                         â”‚
  â”‚                                                             â”‚
  â”‚  Reservation Station (HÃ ng Ä‘á»£i cho má»—i loáº¡i Ä‘Æ¡n vá»‹):       â”‚
  â”‚                                                             â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”   â”‚
  â”‚  â”‚  ALU #0  â”‚  â”‚  ALU #1  â”‚  â”‚  ALU #2  â”‚  â”‚  ALU #3  â”‚   â”‚  â† 4 ALU
  â”‚  â”‚ (Int Add)â”‚  â”‚ (Int Add)â”‚  â”‚(Int Mul) â”‚  â”‚(Bit ops) â”‚   â”‚     song song!
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜   â”‚
  â”‚                                                             â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                                â”‚
  â”‚  â”‚  FPU #0  â”‚  â”‚  FPU #1  â”‚                                â”‚  â† 2 FPU
  â”‚  â”‚(FP Add)  â”‚  â”‚(FP Mul)  â”‚                                â”‚     (float math)
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                                â”‚
  â”‚                                                             â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                                â”‚
  â”‚  â”‚ Load #0  â”‚  â”‚ Load #1  â”‚                                â”‚  â† 2 Load Units
  â”‚  â”‚(Read mem)â”‚  â”‚(Read mem)â”‚                                â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                                â”‚
  â”‚                                                             â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                                              â”‚
  â”‚  â”‚ Store #0 â”‚                                              â”‚  â† 1 Store Unit
  â”‚  â”‚(Write)   â”‚                                              â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                                              â”‚
  â”‚                                                             â”‚
  â”‚  â†’ CPU cÃ³ thá»ƒ thá»±c thi 6-8 Î¼ops CÃ™NG LÃšC má»—i cycle!       â”‚
  â”‚  â†’ Lá»‡nh khÃ´ng cáº§n cháº¡y theo thá»© tá»± (Out-of-Order)          â”‚
  â”‚    miá»…n lÃ  káº¿t quáº£ cuá»‘i cÃ¹ng ÄÃšNG thá»© tá»±.                  â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                               â”‚
                               â–¼
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  RETIRE (HoÃ n táº¥t â€” In-Order)                               â”‚
  â”‚                                                             â”‚
  â”‚  Re-Order Buffer (ROB): Sáº¯p xáº¿p láº¡i káº¿t quáº£ theo thá»© tá»±   â”‚
  â”‚  gá»‘c, rá»“i commit vÃ o Register File / Cache.                â”‚
  â”‚                                                             â”‚
  â”‚  â†’ Äáº£m báº£o chÆ°Æ¡ng trÃ¬nh "nhÃ¬n" Ä‘Ãºng thá»© tá»± dÃ¹ CPU         â”‚
  â”‚    thá»±c thi xÃ¡o trá»™n bÃªn trong.                             â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

> **IPC (Instructions Per Cycle):** CPU hiá»‡n Ä‘áº¡i Ä‘áº¡t IPC = 4-6 (hoÃ n thÃ nh 4-6 lá»‡nh má»—i clock cycle nhá» superscalar). ÄÃ¢y lÃ  lÃ½ do tá»‘c Ä‘á»™ GHz khÃ´ng pháº£i táº¥t cáº£ â€” IPC quan trá»ng khÃ´ng kÃ©m.

---

## 3. Pipeline Hazards â€” Ba káº» phÃ¡ hoáº¡i Pipeline

### 3.1. Data Hazard â€” Phá»¥ thuá»™c dá»¯ liá»‡u

```
VÃ­ dá»¥:
  ADD  R1, R2, R3    ; R1 = R2 + R3
  SUB  R4, R1, R5    ; R4 = R1 - R5  â† Cáº¦N R1 tá»« lá»‡nh trÃªn!

Váº¥n Ä‘á»: SUB cáº§n R1, nhÆ°ng ADD chÆ°a ghi káº¿t quáº£ vÃ o R1 xong.

  Cycle:      1      2      3      4      5
  ADD R1:  [Fetch][Decode][Exec ][Mem  ][Write] â† R1 cÃ³ á»Ÿ cycle 5
  SUB R4:         [Fetch][Decode][â–ˆâ–ˆâ–ˆâ–ˆ ][â–ˆâ–ˆâ–ˆâ–ˆ ] â† SUB cáº§n R1 á»Ÿ cycle 3!
                                  STALL!! (Äá»©ng chá» 2 cycles)

Giáº£i phÃ¡p â€” Forwarding (Bypass):
  CPU "chuyá»n" káº¿t quáº£ tá»« output cá»§a ALU TRá»°C TIáº¾P sang input
  mÃ  KHÃ”NG Äá»¢I ghi vÃ o Register File:

  Cycle:      1      2      3      4      5
  ADD R1:  [Fetch][Decode][Execâ†’][Mem  ][Write]
  SUB R4:         [Fetch][Decode][Exec ][Mem  ]
                              â†‘
                    Forwarding! R1 sáºµn sÃ ng ngay sau Exec cá»§a ADD
                    â†’ KhÃ´ng stall!
```

### 3.2. Control Hazard â€” Branch (NhÃ¡nh ráº½) â€” Káºº THÃ™ Lá»šN NHáº¤T

```
VÃ­ dá»¥ C#:
  if (enemy.health <= 0)
      DestroyEntity(enemy);
  else
      UpdateAI(enemy);


Assembly tÆ°Æ¡ng Ä‘Æ°Æ¡ng:
  CMP   [health], 0          ; So sÃ¡nh health vá»›i 0
  JLE   destroy_label        ; Nháº£y Ä‘áº¿n destroy Náº¾U health <= 0
  CALL  UpdateAI             ; NhÃ¡nh else
  JMP   done                 
  destroy_label:
  CALL  DestroyEntity        ; NhÃ¡nh if
  destroy_label:
  CALL  DestroyEntity        ; NhÃ¡nh if
  done:

#### > Branch Prediction: CPU "Ä‘oÃ¡n" tháº¿ nÃ o?
Khi CPU gáº·p lá»‡nh `JLE` (cycle 2), nÃ³ **CHÆ¯A BIáº¾T** káº¿t quáº£ so sÃ¡nh `CMP` (pháº£i Ä‘áº¿n cycle 3-4 má»›i tÃ­nh xong).
*   Äá»ƒ khÃ´ng dá»«ng láº¡i (stall), CPU **ÄOÃN** luÃ´n: "Cháº¯c lÃ  sáº½ nháº£y (Taken)".
*   NÃ³ báº¯t Ä‘áº§u náº¡p lá»‡nh táº¡i `destroy_label` (CALL DestroyEntity) vÃ o Pipeline ngay láº­p tá»©c.
*   **Náº¿u Ä‘oÃ¡n Ä‘Ãºng:** Pipeline cháº¡y mÆ°á»£t mÃ  (0 penalty).
*   **Náº¿u Ä‘oÃ¡n sai:** (VD: health > 0), CPU pháº£i **Há»¦Y Bá»Ž (Flush)** toÃ n bá»™ cÃ¡c lá»‡nh `DestroyEntity` Ä‘ang cháº¡y dá»Ÿ vÃ  quay láº¡i náº¡p `CALL UpdateAI`.
    â†’ Máº¥t tráº¯ng 15-20 cycles Ä‘Ã£ "cáº§m Ä‘Ã¨n cháº¡y trÆ°á»›c Ã´ tÃ´"!


Váº¥n Ä‘á» Pipeline:
  Cycle:     1      2      3      4      5
  CMP:    [Fetch][Decode][Exec ]
  JLE:           [Fetch][Decode][Exec ] â† Káº¿t quáº£ nháº£y biáº¿t á»Ÿ cycle 4
  ???:                  [Fetch]         â† CPU KHÃ”NG BIáº¾T fetch lá»‡nh nÃ o!
                                          UpdateAI hay DestroyEntity?

  CPU pháº£i ÄOÃN (Branch Prediction):
  - ÄoÃ¡n Ä‘Ãºng:  Pipeline tiáº¿p tá»¥c bÃ¬nh thÆ°á»ng     â†’ 0 penalty
  - ÄoÃ¡n sai:   Pipeline FLUSH â€” xÃ³a sáº¡ch 15-20 lá»‡nh Ä‘Ã£ fetch sai
                 â†’ 15-20 cycles wasted!


Branch Prediction â€” CPU "Ä‘oÃ¡n" nhÃ¡nh nÃ o:

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Branch History Table (BHT):                                   â”‚
  â”‚                                                                â”‚
  â”‚  Äá»‹a chá»‰ lá»‡nh JLE    â”‚ Lá»‹ch sá»­ (T=Taken, N=Not-Taken)        â”‚
  â”‚  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€              â”‚
  â”‚  0x004010A0           â”‚  T T T T T N T T â†’ Predict: TAKEN      â”‚
  â”‚  0x004010B4           â”‚  N N N N N T N N â†’ Predict: NOT-TAKEN  â”‚
  â”‚  0x004010C8           â”‚  T N T N T N T N â†’ Predict: ???        â”‚
  â”‚                        â”‚  â†‘ Pattern khÃ´ng rÃµ â†’ accuracy tháº¥p    â”‚
  â”‚                                                                â”‚
  â”‚  CPU hiá»‡n Ä‘áº¡i: ~95-97% accuracy cho code thÃ´ng thÆ°á»ng          â”‚
  â”‚  NhÆ°ng: Pattern ngáº«u nhiÃªn â†’ accuracy ~50% â†’ tháº£m há»a!        â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 3.3. áº¢nh hÆ°á»Ÿng thá»±c táº¿ trong Unity â€” VÃ­ dá»¥ Branching

```
â•â•â• Ká»‹ch báº£n: Xá»­ lÃ½ 10,000 entities, 50% alive, 50% dead â•â•â•

--- Code cÃ³ Branch ---
[BurstCompile]
public void Execute(int i)
{
    if (healths[i].Value > 0)        // Branch â€” CPU pháº£i Ä‘oÃ¡n!
    {
        positions[i] += velocities[i] * dt;
        healths[i] -= poisonDamage;
    }
    // else: skip (dead entity)
}

PhÃ¢n tÃ­ch:
  - 50% alive, 50% dead â†’ Pattern NGáºªU NHIÃŠN
  - Branch accuracy: ~50-60%
  - Má»—i miss-predict: ~15 cycles penalty
  - 10,000 Ã— 40% miss Ã— 15 = 60,000 cycles wasted


--- Code Branchless ---
[BurstCompile]
public void Execute(int i)
{
    float alive = math.select(0f, 1f, healths[i].Value > 0);
    // alive = 1.0 náº¿u sá»‘ng, 0.0 náº¿u cháº¿t

    positions[i] += velocities[i] * dt * alive;
    // Dead entity: velocity Ã— 0 = 0 â†’ position khÃ´ng Ä‘á»•i
    
    healths[i] -= poisonDamage * alive;
    // Dead entity: -= 0 â†’ health khÃ´ng Ä‘á»•i
}

PhÃ¢n tÃ­ch:
  - KHÃ”NG CÃ“ BRANCH â†’ KhÃ´ng cÃ³ prediction, khÃ´ng cÃ³ miss
  - CPU + Burst vectorize toÃ n bá»™ báº±ng SIMD
  - TÃ­nh dÆ° (dead entity váº«n nhÃ¢n Ã— 0) nhÆ°ng pipeline KHÃ”NG Bá»Š PHáºªU
  - Nhanh hÆ¡n ~2-3Ã— khi tá»‰ lá»‡ alive/dead gáº§n 50/50!


â•â•â• Quy táº¯c: Khi nÃ o dÃ¹ng Branch vs Branchless? â•â•â•

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Branch (if/else) Tá»T KHI:                              â”‚
  â”‚    - Má»™t nhÃ¡nh chiáº¿m >90% (CPU Ä‘oÃ¡n Ä‘Ãºng gáº§n háº¿t)      â”‚
  â”‚    - NhÃ¡nh Ä‘áº¯t (skip heavy computation khi khÃ´ng cáº§n)   â”‚
  â”‚    - Code clarity quan trá»ng hÆ¡n performance             â”‚
  â”‚                                                          â”‚
  â”‚  Branchless (select/step/lerp) Tá»T KHI:                 â”‚
  â”‚    - Tá»‰ lá»‡ hai nhÃ¡nh gáº§n 50/50 (CPU Ä‘oÃ¡n sai nhiá»u)    â”‚
  â”‚    - Trong tight loop xá»­ lÃ½ hÃ ng nghÃ¬n pháº§n tá»­          â”‚
  â”‚    - Trong Shader (GPU branch divergence cÃ²n tá»‡ hÆ¡n!)   â”‚
  â”‚    - Code trong [BurstCompile] Job                       â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## 4. Stack & Function Calls â€” CÃ¡i giÃ¡ cá»§a má»—i láº§n gá»i hÃ m

### 4.1. Call Stack â€” CÃ¡ch CPU quáº£n lÃ½ hÃ m

```
C# code:
  void GameLoop() {
      float dmg = CalculateDamage(10, 5);
      ApplyDamage(enemy, dmg);
  }
  float CalculateDamage(int baseDmg, int level) {
      return baseDmg * (1 + level * 0.1f);
  }


Assembly flow (Ä‘Æ¡n giáº£n hÃ³a):

  GameLoop:
      PUSH  RBP                    ; LÆ°u Base Pointer cÅ© lÃªn Stack
      MOV   RBP, RSP               ; Set Base Pointer má»›i = Ä‘á»‰nh Stack
      SUB   RSP, 16                ; DÃ nh chá»— cho local variables

      MOV   ECX, 10                ; Arg 1: baseDmg = 10
      MOV   EDX, 5                 ; Arg 2: level = 5
      CALL  CalculateDamage        ; â† Push Return Address + Jump

      ; ... khi CalculateDamage return, káº¿t quáº£ náº±m trong XMM0 ...
      
      MOV   RSP, RBP               ; KhÃ´i phá»¥c Stack
      POP   RBP                    ; KhÃ´i phá»¥c Base Pointer
      RET                          ; Pop Return Address + Jump back


Stack Memory khi Ä‘ang trong CalculateDamage():

  Äá»‹a chá»‰ cao  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
               â”‚  ... (GameLoop caller)    â”‚
               â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
               â”‚  Return Address (RIP cÅ©) â”‚ â† CPU tá»± push khi CALL
               â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
       RBP â”€â”€â–º â”‚  Old RBP (GameLoop)      â”‚ â† NÆ¡i quay láº¡i
               â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
               â”‚  local var: baseDmg = 10 â”‚
               â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
       RSP â”€â”€â–º â”‚  local var: level = 5    â”‚ â† Äá»‰nh Stack hiá»‡n táº¡i
               â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
               â”‚  (Space trá»‘ng â€” grow â†“)  â”‚
  Äá»‹a chá»‰ tháº¥p â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

  Khi RET:
  1. Pop return address
  2. Jump vá» GameLoop
  3. KhÃ´i phá»¥c RBP/RSP
  â†’ Stack Frame bá»‹ "há»§y" (chá»‰ di chuyá»ƒn pointer, KHÃ”NG xÃ³a data)
```

### 4.2. Inlining â€” Loáº¡i bá» chi phÃ­ gá»i hÃ m

```
Chi phÃ­ má»—i CALL:
  1. PUSH return address        (~1 cycle)
  2. Push/Pop registers to save (~2-4 cycles)
  3. Pipeline flush (partial)   (~5-10 cycles)
  4. Return bookkeeping         (~1-2 cycles)
  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  Tá»•ng: ~10-15 cycles overhead Má»–I Láº¦N gá»i hÃ m

Vá»›i 10,000 entities Ã— 5 hÃ m/entity = 50,000 calls
â†’ 50,000 Ã— 12 = 600,000 cycles wasted = ~0.12ms á»Ÿ 5GHz


â•â•â• Giáº£i phÃ¡p: Inlining â•â•â•

Compiler thay tháº¿ CALL báº±ng cÃ¡ch COPY code cá»§a hÃ m vÃ o caller:

  TrÆ°á»›c Inline:                    Sau Inline:
  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€                   â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  void Update() {                  void Update() {
      float d = CalcDmg(10, 5);       // CalcDmg "paste" trá»±c tiáº¿p:
      Apply(enemy, d);                 float d = 10 * (1 + 5 * 0.1f);
  }                                    Apply(enemy, d);
                                   }
  float CalcDmg(int b, int l) {
      return b * (1 + l * 0.1f);   â†’ KhÃ´ng cÃ³ CALL/RET overhead
  }                                â†’ Burst/IL2CPP cÃ³ thá»ƒ tá»‘i Æ°u thÃªm
                                     (constant folding: d = 15.0f)


Unity & Inlining:
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Mono JIT:   Inline ráº¥t háº¡n cháº¿ (hÃ m <32 bytes IL)          â”‚
  â”‚  IL2CPP:     Inline tá»‘t hÆ¡n (C++ compiler quyáº¿t Ä‘á»‹nh)       â”‚
  â”‚  Burst:      Inline Cá»°C Ká»² aggressive                       â”‚
  â”‚              + Tá»± vectorize sau khi inline                   â”‚
  â”‚              â†’ ÄÃ¢y lÃ  lÃ½ do Burst nhanh hÆ¡n Mono 5-20Ã—      â”‚
  â”‚                                                              â”‚
  â”‚  Tip: ÄÃ¡nh dáº¥u [MethodImpl(MethodImplOptions.AggressiveInlining)] â”‚
  â”‚  Ä‘á»ƒ gá»£i Ã½ compiler inline (khÃ´ng báº¯t buá»™c, compiler quyáº¿t)  â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## 5. Tá»« C# Ä‘áº¿n MÃ£ mÃ¡y â€” Ba con Ä‘Æ°á»ng trong Unity

### 5.1. Con Ä‘Æ°á»ng Mono (JIT â€” Just-In-Time)

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  CON ÄÆ¯á»œNG MONO â€” DÃ¹ng trong Unity Editor & Development        â”‚
â”‚                                                                 â”‚
â”‚  1. Viáº¿t code C# (.cs files)                                    â”‚
â”‚     â”‚                                                           â”‚
â”‚     â–¼                                                           â”‚
â”‚  2. Roslyn Compiler biÃªn dá»‹ch â†’ IL bytecode (.dll files)        â”‚
â”‚     â”‚    (Xáº£y ra khi báº¡n nháº¥n Ctrl+S hoáº·c Domain Reload)       â”‚
â”‚     â”‚                                                           â”‚
â”‚     â”‚    IL bytecode â€” VÃ­ dá»¥:                                   â”‚
â”‚     â”‚    .method void Update() {                                â”‚
â”‚     â”‚        ldarg.0                  ; load "this"             â”‚
â”‚     â”‚        ldfld float3 position    ; load position           â”‚
â”‚     â”‚        ldarg.0                                            â”‚
â”‚     â”‚        ldfld float3 velocity    ; load velocity           â”‚
â”‚     â”‚        ldsfld float deltaTime   ; load Time.deltaTime     â”‚
â”‚     â”‚        mul                      ; velocity * dt           â”‚
â”‚     â”‚        add                      ; position + result       â”‚
â”‚     â”‚        stfld float3 position    ; store back              â”‚
â”‚     â”‚    }                                                      â”‚
â”‚     â”‚                                                           â”‚
â”‚     â–¼                                                           â”‚
â”‚  3. Mono Runtime JIT compile:                                    â”‚
â”‚     - Láº§n Ä‘áº§u gá»i Update() â†’ compile IL â†’ x86-64 native        â”‚
â”‚     - Káº¿t quáº£ cache trong memory (khÃ´ng compile láº¡i)             â”‚
â”‚     - Láº§n gá»i sau: cháº¡y native code trá»±c tiáº¿p                   â”‚
â”‚     â”‚                                                           â”‚
â”‚     â”‚  âš  Váº¥n Ä‘á» JIT:                                           â”‚
â”‚     â”‚  - Láº§n gá»i Ä‘áº§u tiÃªn CHáº¬M (JIT stutter / hiccup)          â”‚
â”‚     â”‚  - JIT compiler pháº£i NHANH â†’ khÃ´ng Ä‘á»§ thá»i gian optimize  â”‚
â”‚     â”‚  - Káº¿t quáº£: native code CHÆ¯A tá»‘i Æ°u báº±ng AOT             â”‚
â”‚     â”‚                                                           â”‚
â”‚     â–¼                                                           â”‚
â”‚  4. Native Code cháº¡y trÃªn CPU                                   â”‚
â”‚                                                                 â”‚
â”‚  âœ… Æ¯u Ä‘iá»ƒm: Iterate nhanh (Save â†’ Play ngay)                   â”‚
â”‚  âŒ NhÆ°á»£c Ä‘iá»ƒm: Runtime performance kÃ©m hÆ¡n IL2CPP/Burst        â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 5.2. Con Ä‘Æ°á»ng IL2CPP (AOT â€” Ahead-of-Time)

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  CON ÄÆ¯á»œNG IL2CPP â€” DÃ¹ng cho Production Builds                  â”‚
â”‚                                                                 â”‚
â”‚  1. C# â†’ IL (giá»‘ng Mono)                                        â”‚
â”‚     â”‚                                                           â”‚
â”‚     â–¼                                                           â”‚
â”‚  2. IL2CPP Transpiler:                                           â”‚
â”‚     Chuyá»ƒn IL bytecode â†’ C++ source code                         â”‚
â”‚     â”‚                                                           â”‚
â”‚     â”‚  VÃ­ dá»¥ output C++:                                        â”‚
â”‚     â”‚  void Update_m1234(MyScript_t* __this) {                  â”‚
â”‚     â”‚      float3 vel = __this->velocity;                       â”‚
â”‚     â”‚      float dt = Time_get_deltaTime();                     â”‚
â”‚     â”‚      float3 delta;                                        â”‚
â”‚     â”‚      delta.x = vel.x * dt;                                â”‚
â”‚     â”‚      delta.y = vel.y * dt;                                â”‚
â”‚     â”‚      delta.z = vel.z * dt;                                â”‚
â”‚     â”‚      __this->position.x += delta.x;                       â”‚
â”‚     â”‚      __this->position.y += delta.y;                       â”‚
â”‚     â”‚      __this->position.z += delta.z;                       â”‚
â”‚     â”‚  }                                                        â”‚
â”‚     â”‚                                                           â”‚
â”‚     â–¼                                                           â”‚
â”‚  3. Platform C++ Compiler:                                       â”‚
â”‚     â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”     â”‚
â”‚     â”‚  Windows: MSVC (cl.exe)     â†’ x86-64 .exe          â”‚     â”‚
â”‚     â”‚  macOS:   Clang (Apple)     â†’ ARM64 .app            â”‚     â”‚
â”‚     â”‚  Android: NDK Clang         â†’ ARM64 .so             â”‚     â”‚
â”‚     â”‚  iOS:     Clang (Xcode)     â†’ ARM64 .ipa            â”‚     â”‚
â”‚     â”‚  WebGL:   Emscripten        â†’ WASM .wasm            â”‚     â”‚
â”‚     â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜     â”‚
â”‚     â”‚                                                           â”‚
â”‚     â”‚  C++ compiler cÃ³ HÃ€NG GIá»œ Ä‘á»ƒ optimize:                    â”‚
â”‚     â”‚  - Loop unrolling                                         â”‚
â”‚     â”‚  - Dead code elimination                                  â”‚
â”‚     â”‚  - Constant propagation                                   â”‚
â”‚     â”‚  - Auto-vectorization (má»™t pháº§n)                          â”‚
â”‚     â”‚  - Link-Time Optimization (LTO)                           â”‚
â”‚     â”‚                                                           â”‚
â”‚     â–¼                                                           â”‚
â”‚  4. Highly optimized native binary                               â”‚
â”‚                                                                 â”‚
â”‚  âœ… Performance gáº§n C++ thuáº§n                                    â”‚
â”‚  âœ… Code stripping giáº£m build size                               â”‚
â”‚  âŒ Build time lÃ¢u (pháº£i compile C++)                            â”‚
â”‚  âŒ Debug khÃ³ hÆ¡n (native stack traces)                          â”‚
â”‚  ðŸ“± Báº®T BUá»˜C cho iOS (Apple cáº¥m JIT)                            â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 5.3. Con Ä‘Æ°á»ng Burst (AOT + SIMD â€” Cao cáº¥p nháº¥t)

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  CON ÄÆ¯á»œNG BURST â€” DÃ nh cho DOTS (ECS + Job System)             â”‚
â”‚                                                                 â”‚
â”‚  1. C# HPC# (High-Performance C#)                               â”‚
â”‚     â”‚  Subset giá»›i háº¡n cá»§a C#:                                  â”‚
â”‚     â”‚  âœ… struct, NativeArray, math.*, fixed arrays              â”‚
â”‚     â”‚  âŒ class, string, List<T>, LINQ, virtual, delegates       â”‚
â”‚     â”‚  âŒ try/catch, reflection, GC allocations                  â”‚
â”‚     â”‚                                                           â”‚
â”‚     â–¼                                                           â”‚
â”‚  2. IL (giá»‘ng Mono/IL2CPP)                                       â”‚
â”‚     â”‚                                                           â”‚
â”‚     â–¼                                                           â”‚
â”‚  3. Burst Compiler (LLVM Backend):                               â”‚
â”‚     â”‚                                                           â”‚
â”‚     â”‚  Burst = Custom LLVM frontend cho C#                      â”‚
â”‚     â”‚  Sá»­ dá»¥ng CÃ™NG backend optimizer nhÆ° Clang/C++ compiler!   â”‚
â”‚     â”‚                                                           â”‚
â”‚     â”‚  Tá»‘i Æ°u hÃ³a Ä‘áº·c biá»‡t cá»§a Burst:                          â”‚
â”‚     â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”   â”‚
â”‚     â”‚  â”‚ âœ… Auto-Vectorization (SIMD)                       â”‚   â”‚
â”‚     â”‚  â”‚    â†’ Tá»± chuyá»ƒn scalar loop â†’ SIMD instructions    â”‚   â”‚
â”‚     â”‚  â”‚                                                    â”‚   â”‚
â”‚     â”‚  â”‚ âœ… Loop Vectorization                              â”‚   â”‚
â”‚     â”‚  â”‚    â†’ for (i=0..N) â†’ xá»­ lÃ½ 4/8/16 pháº§n tá»­/loop    â”‚   â”‚
â”‚     â”‚  â”‚                                                    â”‚   â”‚
â”‚     â”‚  â”‚ âœ… Bounds Check Elimination                        â”‚   â”‚
â”‚     â”‚  â”‚    â†’ XÃ³a [i] bounds check khi Burst chá»©ng minh    â”‚   â”‚
â”‚     â”‚  â”‚      index luÃ´n há»£p lá»‡                             â”‚   â”‚
â”‚     â”‚  â”‚                                                    â”‚   â”‚
â”‚     â”‚  â”‚ âœ… Alias Analysis                                  â”‚   â”‚
â”‚     â”‚  â”‚    â†’ Chá»©ng minh 2 NativeArrays KHÃ”NG overlap      â”‚   â”‚
â”‚     â”‚  â”‚    â†’ Cho phÃ©p tá»‘i Æ°u máº¡nh hÆ¡n                     â”‚   â”‚
â”‚     â”‚  â”‚                                                    â”‚   â”‚
â”‚     â”‚  â”‚ âœ… Constant Folding                                â”‚   â”‚
â”‚     â”‚  â”‚    â†’ math.sin(0) â†’ 0 táº¡i compile time              â”‚   â”‚
â”‚     â”‚  â”‚                                                    â”‚   â”‚
â”‚     â”‚  â”‚ âœ… Aggressive Inlining                             â”‚   â”‚
â”‚     â”‚  â”‚    â†’ Inline Gáº¦N NHÆ¯ Táº¤T Cáº¢ hÃ m nhá»               â”‚   â”‚
â”‚     â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜   â”‚
â”‚     â”‚                                                           â”‚
â”‚     â–¼                                                           â”‚
â”‚  4. Platform-specific native code:                               â”‚
â”‚     - x86-64: SSE4.2 / AVX2 / AVX-512                           â”‚
â”‚     - ARM64:  NEON / SVE                                         â”‚
â”‚     - WASM:   SIMD128 (WebGL/WebGPU)                             â”‚
â”‚                                                                 â”‚
â”‚  âœ… Hiá»‡u nÄƒng NGANG hoáº·c HÆ N C++ hand-optimized                â”‚
â”‚  âœ… An toÃ n hÆ¡n C++ (safety checks á»Ÿ Editor, remove á»Ÿ Build)    â”‚
â”‚  âœ… Compile nhanh (vÃ i giÃ¢y cho Jobs)                            â”‚
â”‚  âŒ Chá»‰ dÃ¹ng Ä‘Æ°á»£c HPC# subset                                   â”‚
â”‚  âŒ KhÃ´ng dÃ¹ng Ä‘Æ°á»£c MonoBehaviour, strings, classes               â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 5.4. So sÃ¡nh ba con Ä‘Æ°á»ng â€” Benchmark thá»±c táº¿

```
BÃ i test: Di chuyá»ƒn 100,000 entities (position += velocity * dt)

â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  Pipeline     â”‚  Thá»i gian   â”‚ So vs  â”‚  LÃ½ do                   â”‚
â”‚               â”‚  (ms/frame)  â”‚ Mono   â”‚                          â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ Mono (JIT)    â”‚  ~8.5 ms     â”‚  1Ã—    â”‚ Scalar, bounds checks,   â”‚
â”‚               â”‚              â”‚        â”‚ GC overhead, no SIMD     â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ IL2CPP (AOT)  â”‚  ~3.2 ms     â”‚  2.7Ã—  â”‚ C++ optimizer, inline,   â”‚
â”‚               â”‚              â”‚        â”‚ minor auto-vectorize     â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ Burst (AOT    â”‚  ~0.4 ms     â”‚  21Ã—   â”‚ Full SIMD (AVX2),        â”‚
â”‚  + SIMD)      â”‚              â”‚        â”‚ no bounds checks,        â”‚
â”‚               â”‚              â”‚        â”‚ perfect cache (ECS),     â”‚
â”‚               â”‚              â”‚        â”‚ ScheduleParallel (8 coresâ”‚
â”‚               â”‚              â”‚        â”‚ Ã— 8-wide SIMD = 64Ã—)     â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ Burst +       â”‚  ~0.05 ms    â”‚  170Ã—  â”‚ Burst + Job System       â”‚
â”‚ Parallel Jobs â”‚              â”‚        â”‚ trÃªn 8 cores             â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

Táº¡i sao chÃªnh lá»‡ch Lá»šN Ä‘áº¿n váº­y?

  Mono:   scalar math (1 entity/lá»‡nh) + bounds check + GC scan
  Burst:  SIMD math (8 entities/lá»‡nh) + no checks + no GC
  + Jobs: chia 100K entities cho 8 cores
          = 100K Ã· 8 cores Ã· 8 SIMD = ~1,562 iterations/core
          thay vÃ¬ 100,000 iterations trÃªn 1 core
```

---

## 6. Garbage Collection â€” "Stop the World"

### 6.1. GC hoáº¡t Ä‘á»™ng nhÆ° tháº¿ nÃ o?

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚              GARBAGE COLLECTOR (Boehm GC trong Unity)             â”‚
â”‚                                                                   â”‚
â”‚  Managed Heap:                                                    â”‚
â”‚  â”Œâ”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ”¬â”€â”€â”€â”€â”€â”¬â–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ”¬â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ”¬â”€â”€â”€â”€â”€â”        â”‚
â”‚  â”‚ Obj â”‚ Obj â”‚DEAD â”‚ Obj â”‚DEAD â”‚ Obj â”‚ Obj â”‚DEAD â”‚ Obj â”‚        â”‚
â”‚  â”‚  A  â”‚  B  â”‚  C  â”‚  D  â”‚  E  â”‚  F  â”‚  G  â”‚  H  â”‚  I  â”‚        â”‚
â”‚  â””â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ”´â”€â”€â”€â”€â”€â”´â–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ”´â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ”´â”€â”€â”€â”€â”€â”˜        â”‚
â”‚                                                                   â”‚
â”‚  GC Cycle:                                                        â”‚
â”‚  1. STOP THE WORLD â€” Táº¥t cáº£ C# code Dá»ªNG Láº I                     â”‚
â”‚     (Game freeze! Player tháº¥y "giáº­t")                             â”‚
â”‚                                                                   â”‚
â”‚  2. MARK Phase:                                                   â”‚
â”‚     Báº¯t Ä‘áº§u tá»« "GC Roots" (static fields, stack variables)       â”‚
â”‚     Äi theo táº¥t cáº£ references â†’ Ä‘Ã¡nh dáº¥u objects "sá»‘ng"          â”‚
â”‚     Objects khÃ´ng Ä‘Æ°á»£c Ä‘Ã¡nh dáº¥u = "cháº¿t" (garbage)                â”‚
â”‚                                                                   â”‚
â”‚  3. SWEEP Phase:                                                  â”‚
â”‚     Giáº£i phÃ³ng bá»™ nhá»› cá»§a objects "cháº¿t"                           â”‚
â”‚     (Boehm GC KHÃ”NG di chuyá»ƒn objects â€” khÃ´ng compact)            â”‚
â”‚                                                                   â”‚
â”‚  4. RESUME â€” Code tiáº¿p tá»¥c cháº¡y                                   â”‚
â”‚                                                                   â”‚
â”‚  Thá»i gian GC: 1-20ms tÃ¹y heap size                               â”‚
â”‚  á»ž 60 FPS: 1 frame = 16.67ms                                      â”‚
â”‚  â†’ GC 5ms = máº¥t 30% thá»i gian frame â†’ GIáº¬T!                      â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


CÃ¡c "tá»™i Ä‘á»“" táº¡o GC trong Unity:

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Code thÆ°á»ng gáº·p             â”‚  Táº¡o GC bao nhiÃªu?              â”‚
  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
  â”‚  string name = "HP: " + hp;  â”‚  ~100 bytes / frame (ná»‘i string)â”‚
  â”‚  new List<int>()             â”‚  ~80 bytes (list object + array) â”‚
  â”‚  GetComponent<T>()           â”‚  ~40 bytes (boxing/wrapper)      â”‚
  â”‚  LINQ (.Where, .Select)      â”‚  ~200+ bytes (iterator objects)  â”‚
  â”‚  foreach (List<T>)           â”‚  ~40 bytes (enumerator object)   â”‚
  â”‚  Closure / Lambda            â”‚  ~60 bytes (delegate + captured) â”‚
  â”‚  params object[]             â”‚  ~variable (boxing + array)      â”‚
  â”‚  ToString()                  â”‚  ~40+ bytes (new string)         â”‚
  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
  â”‚  10 scripts Ã— 5 allocs/frame â”‚  ~2-5 KB / frame                â”‚
  â”‚  Ã— 60 frames/second          â”‚  ~120-300 KB / second            â”‚
  â”‚  â†’ GC trigger má»—i ~10-30 giÃ¢yâ”‚  â†’ Giáº­t Ä‘á»‹nh ká»³!                â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


Giáº£i phÃ¡p Zero-GC:

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  âŒ TRÃNH                     â”‚  âœ… THAY Báº°NG                 â”‚
  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
  â”‚  string concat               â”‚  StringBuilder (reuse)        â”‚
  â”‚  new List<T>() má»—i frame    â”‚  Pool hoáº·c NativeList          â”‚
  â”‚  GetComponent<T>()           â”‚  Cache reference á»Ÿ Awake()    â”‚
  â”‚  LINQ                        â”‚  for loop thá»§ cÃ´ng            â”‚
  â”‚  foreach trÃªn List           â”‚  for (int i=0; ...) loop      â”‚
  â”‚  Lambda / Closure            â”‚  static method + struct data  â”‚
  â”‚  class (reference type)       â”‚  struct (value type)          â”‚
  â”‚  Managed arrays              â”‚  NativeArray<T>               â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## 7. Tá»•ng káº¿t Chapter 3 â€” Con Ä‘Æ°á»ng cá»§a má»™t dÃ²ng code

```
Báº¡n viáº¿t:  position += velocity * deltaTime;

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                               â”‚
  â”‚  â‘  C# Source â†’ Roslyn Compiler â†’ IL Bytecode (.dll)          â”‚
  â”‚                                                               â”‚
  â”‚  â‘¡ IL â†’ [Mono JIT | IL2CPP â†’ C++ â†’ Native | Burst â†’ LLVM]   â”‚
  â”‚                                                               â”‚
  â”‚  â‘¢ Native Code Ä‘Æ°á»£c CPU Fetch vÃ o Pipeline (L1i Cache)        â”‚
  â”‚                                                               â”‚
  â”‚  â‘£ Decoder chuyá»ƒn x86/ARM â†’ Î¼ops                              â”‚
  â”‚                                                               â”‚
  â”‚  â‘¤ Out-of-Order Engine dispatch Î¼ops tá»›i ALU/FPU              â”‚
  â”‚     - Burst: SIMD registers (4-8 entities cÃ¹ng lÃºc)           â”‚
  â”‚     - Jobs: ScheduleParallel â†’ 8 cores Ã— 8 SIMD = 64Ã—        â”‚
  â”‚                                                               â”‚
  â”‚  â‘¥ ALU/FPU thá»±c thi phÃ©p tÃ­nh                                 â”‚
  â”‚     (Transistors Ä‘Ã³ng/má»Ÿ theo Chapter 1)                      â”‚
  â”‚                                                               â”‚
  â”‚  â‘¦ Káº¿t quáº£ ghi vÃ o Register â†’ Cache â†’ RAM                    â”‚
  â”‚     (Memory Hierarchy theo Chapter 2)                         â”‚
  â”‚                                                               â”‚
  â”‚  â‘§ Náº¿u cÃ³ Branch (if/else):                                  â”‚
  â”‚     - Branch Predictor Ä‘oÃ¡n nhÃ¡nh                             â”‚
  â”‚     - ÄoÃ¡n Ä‘Ãºng = 0 penalty                                  â”‚
  â”‚     - ÄoÃ¡n sai = 15-20 cycles flush pipeline                  â”‚
  â”‚                                                               â”‚
  â”‚  ToÃ n bá»™: < 1 nanosecond cho 1 iteration                     â”‚
  â”‚  Ã— 100,000 entities Ã— 60 FPS = ~6 tá»· phÃ©p tÃ­nh/giÃ¢y          â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

> **BÃ i há»c thá»±c tiá»…n:**
> 1. **Chá»n Ä‘Ãºng pipeline:** Mono cho Editor iteration, IL2CPP cho build, **Burst cho hot paths**.
> 2. **TrÃ¡nh Branch** trong tight loops: dÃ¹ng `math.select()`, `step()`, `lerp()`.
> 3. **Inline hÃ m nhá»:** Burst lÃ m tá»± Ä‘á»™ng, nhÆ°ng Mono/IL2CPP cáº§n hint.
> 4. **Zero-GC:** Má»i allocation trong Update() lÃ  "ná»£" mÃ  GC sáº½ Ä‘Ã²i láº¡i (báº±ng frame drop).
> 5. **Profile trÆ°á»›c khi tá»‘i Æ°u:** Unity Profiler + Burst Inspector cho biáº¿t CPU Ä‘ang tá»‘n thá»i gian á»Ÿ Ä‘Ã¢u.

---

> **ChÆ°Æ¡ng tiáº¿p theo:** [Chapter 4 â€” GPU Architecture & Rendering Pipeline]() â€” CÃ¡ch GPU xá»­ lÃ½ hÃ ng triá»‡u pixel song song, vÃ  táº¡i sao shader code cáº§n viáº¿t khÃ¡c hoÃ n toÃ n CPU code.

---
*Chapter 3 â€” NghiÃªn cá»©u cho Unity High-Performance Agent*
# ChÆ°Æ¡ng 4: GPU Architecture & Rendering Pipeline

> **Má»¥c tiÃªu chÆ°Æ¡ng:** Hiá»ƒu kiáº¿n trÃºc pháº§n cá»©ng GPU khÃ¡c CPU nhÆ° tháº¿ nÃ o, cÃ¡ch Rendering Pipeline biáº¿n dá»¯ liá»‡u 3D thÃ nh pixel, vÃ  táº¡i sao má»—i quyáº¿t Ä‘á»‹nh trong Shader code áº£nh hÆ°á»Ÿng trá»±c tiáº¿p Ä‘áº¿n hiá»‡u nÄƒng game.

---

## 1. Táº¡i sao cáº§n GPU? â€” CPU khÃ´ng Ä‘á»§ cho Ä‘á»“ há»a

### 1.1. BÃ i toÃ¡n rendering

```
Render 1 frame Full HD (1920Ã—1080) á»Ÿ 60 FPS:

  Sá»‘ pixel:        1920 Ã— 1080 = 2,073,600 pixels
  Má»—i pixel cáº§n:   ~50-200 phÃ©p tÃ­nh (lighting, texturing, shadows, ...)
  Tá»•ng phÃ©p tÃ­nh:  2M Ã— 100 = ~200 TRIá»†U phÃ©p tÃ­nh / frame
  á»ž 60 FPS:        200M Ã— 60 = ~12 Tá»¶ phÃ©p tÃ­nh / giÃ¢y

  CPU 8 cores Ã— 5 GHz Ã— IPC 4 = ~160 tá»· ops/giÃ¢y
  â†’ CPU CÃ“ THá»‚ render, nhÆ°ng:
    - Háº¿t sáº¡ch CPU cho graphics â†’ khÃ´ng cÃ²n cho game logic
    - Má»—i pixel LÃ€ Äá»˜C Láº¬P â†’ song song hÃ³a hoÃ n háº£o
    - CPU chá»‰ cÃ³ 8-16 cores â†’ lÃ£ng phÃ­ tiá»m nÄƒng song song

  GPU ~4000 cores Ã— 1.5 GHz = khÃ´ng nhanh tá»«ng core, nhÆ°ng:
  â†’ Xá»¬ LÃ 4000 PIXELS CÃ™NG LÃšC
  â†’ Throughput (lÆ°á»£ng cÃ´ng viá»‡c/giÃ¢y) >> CPU gáº¥p nhiá»u láº§n
```

### 1.2. Triáº¿t lÃ½ thiáº¿t káº¿: Latency vs Throughput

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                CPU vs GPU â€” Hai triáº¿t lÃ½ Ä‘á»‘i láº­p                    â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚         CPU                â”‚              GPU                       â”‚
â”‚   "LÃ m 1 viá»‡c Cá»°C NHANH"  â”‚   "LÃ m TRIá»†U viá»‡c song song"         â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ â— 8-24 cores              â”‚ â— 2,000-16,000 cores                  â”‚
â”‚ â— Clock cao: 4-6 GHz      â”‚ â— Clock tháº¥p hÆ¡n: 1.5-2.5 GHz        â”‚
â”‚ â— Out-of-Order execution  â”‚ â— In-Order (Ä‘Æ¡n giáº£n hÆ¡n)             â”‚
â”‚ â— Branch prediction       â”‚ â— Branch = tháº£m há»a                   â”‚
â”‚ â— Cache Lá»šN (32MB L3)     â”‚ â— Cache NHá»Ž (6MB L2 shared)          â”‚
â”‚ â— Latency-oriented        â”‚ â— Throughput-oriented                  â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚                            â”‚                                        â”‚
â”‚  áº¨n dá»¥:                    â”‚  áº¨n dá»¥:                                â”‚
â”‚  1 giÃ¡o sÆ° giáº£i Ä‘á» thi    â”‚  10,000 há»c sinh lá»›p 1                 â”‚
â”‚  â†’ Cá»°C NHANH tá»«ng bÃ i     â”‚  â†’ Má»—i em giáº£i 1 bÃ i ÄÆ N GIáº¢N       â”‚
â”‚  â†’ NhÆ°ng 1 ngÆ°á»i           â”‚  â†’ Tá»•ng: xong 10,000 bÃ i CÃ™NG LÃšC    â”‚
â”‚                            â”‚                                        â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ PhÃ¹ há»£p:                  â”‚ PhÃ¹ há»£p:                               â”‚
â”‚ âœ… Game logic              â”‚ âœ… Rendering (pixel processing)         â”‚
â”‚ âœ… AI phá»©c táº¡p             â”‚ âœ… Particle systems (100K particles)   â”‚
â”‚ âœ… Physics (broad phase)   â”‚ âœ… Post-processing                     â”‚
â”‚ âœ… Networking              â”‚ âœ… Compute Shaders (GPGPU)             â”‚
â”‚ âœ… File I/O                â”‚ âœ… Machine Learning inference          â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## 2. Kiáº¿n trÃºc pháº§n cá»©ng GPU

### 2.1. Cáº¥u trÃºc phÃ¢n cáº¥p â€” SM (Streaming Multiprocessor)

```
GPU Die (vÃ­ dá»¥: NVIDIA RTX 4070 â€” AD104):

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                    GPU CHIP (AD104)                            â”‚
  â”‚                                                               â”‚
  â”‚  â”Œâ”€â”€â”€â”€ GPC 0 â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€ GPC 1 â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€ GPC ... â”€â”€â” â”‚
  â”‚  â”‚                 â”‚  â”‚                 â”‚  â”‚                â”‚ â”‚
  â”‚  â”‚  â”Œâ”€SM 0â”€â”       â”‚  â”‚  â”Œâ”€SM 4â”€â”       â”‚  â”‚                â”‚ â”‚
  â”‚  â”‚  â”‚      â”‚       â”‚  â”‚  â”‚      â”‚       â”‚  â”‚                â”‚ â”‚
  â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”˜       â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”˜       â”‚  â”‚                â”‚ â”‚
  â”‚  â”‚  â”Œâ”€SM 1â”€â”       â”‚  â”‚  â”Œâ”€SM 5â”€â”       â”‚  â”‚                â”‚ â”‚
  â”‚  â”‚  â”‚      â”‚       â”‚  â”‚  â”‚      â”‚       â”‚  â”‚                â”‚ â”‚
  â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”˜       â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”˜       â”‚  â”‚                â”‚ â”‚
  â”‚  â”‚  â”Œâ”€SM 2â”€â”       â”‚  â”‚  â”Œâ”€SM 6â”€â”       â”‚  â”‚                â”‚ â”‚
  â”‚  â”‚  â”‚      â”‚       â”‚  â”‚  â”‚      â”‚       â”‚  â”‚                â”‚ â”‚
  â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”˜       â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”˜       â”‚  â”‚                â”‚ â”‚
  â”‚  â”‚  â”Œâ”€SM 3â”€â”       â”‚  â”‚  â”Œâ”€SM 7â”€â”       â”‚  â”‚                â”‚ â”‚
  â”‚  â”‚  â”‚      â”‚       â”‚  â”‚  â”‚      â”‚       â”‚  â”‚     Ã—5 GPC     â”‚ â”‚
  â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”˜       â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”˜       â”‚  â”‚     = 46 SM    â”‚ â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜ â”‚
  â”‚                                                               â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”       â”‚
  â”‚  â”‚              L2 Cache (36 MB, Shared)              â”‚       â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜       â”‚
  â”‚                         â”‚                                     â”‚
  â”‚                    Memory Controllers                         â”‚
  â”‚                         â”‚                                     â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                            â”‚
                  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
                  â”‚  VRAM (GDDR6X)     â”‚
                  â”‚  12 GB, 192-bit    â”‚
                  â”‚  Bandwidth: 504 GB/sâ”‚
                  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


BÃªn trong 1 SM (Streaming Multiprocessor):

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  SM (Streaming Multiprocessor)                             â”‚
  â”‚                                                            â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”      â”‚
  â”‚  â”‚  Warp Scheduler Ã—4                                â”‚      â”‚
  â”‚  â”‚  (Má»—i scheduler quáº£n lÃ½ nhiá»u Warps)              â”‚      â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜      â”‚
  â”‚                                                            â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”         â”‚
  â”‚  â”‚ FP32 Ã—32â”‚ â”‚ FP32 Ã—32â”‚ â”‚ FP32 Ã—32â”‚ â”‚ FP32 Ã—32â”‚         â”‚
  â”‚  â”‚ (CUDA   â”‚ â”‚ (CUDA   â”‚ â”‚ (CUDA   â”‚ â”‚ (CUDA   â”‚         â”‚
  â”‚  â”‚  cores) â”‚ â”‚  cores) â”‚ â”‚  cores) â”‚ â”‚  cores) â”‚         â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜         â”‚
  â”‚  = 128 FP32 cores / SM                                     â”‚
  â”‚                                                            â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”                                  â”‚
  â”‚  â”‚ INT32Ã—32â”‚ â”‚TensorÃ—4 â”‚  â† Tensor Cores (AI/ML, DLSS)   â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                                  â”‚
  â”‚                                                            â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”                                  â”‚
  â”‚  â”‚  SFU Ã—4 â”‚ â”‚  RT Ã—1  â”‚  â† RT Core (Ray Tracing)        â”‚
  â”‚  â”‚(sin,cos)â”‚ â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                                  â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                                              â”‚
  â”‚                                                            â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                      â”‚
  â”‚  â”‚  Register File: 65,536 Ã— 32-bit â”‚  = 256 KB / SM       â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                      â”‚
  â”‚                                                            â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                      â”‚
  â”‚  â”‚  Shared Memory / L1 Cache       â”‚  = 128 KB / SM       â”‚
  â”‚  â”‚  (Configurable: 64K shared +    â”‚                      â”‚
  â”‚  â”‚   64K L1, hoáº·c 128K shared)     â”‚                      â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                      â”‚
  â”‚                                                            â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                      â”‚
  â”‚  â”‚  Texture Units Ã— 4              â”‚                      â”‚
  â”‚  â”‚  (Bilinear filter, mipmapping)  â”‚                      â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                      â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

  Tá»•ng GPU: 46 SM Ã— 128 cores = 5,888 CUDA Cores
  â†’ So sÃ¡nh: CPU cÃ³ 8-16 cores, GPU cÃ³ ~6,000 cores!
```

> **TÃªn gá»i khÃ¡c nhau cÃ¹ng Ã½ nghÄ©a:**
> - NVIDIA: SM (Streaming Multiprocessor), CUDA Core, Warp (32 threads)
> - AMD: CU (Compute Unit), Stream Processor, Wavefront (64 threads)
> - Apple: GPU Core, Execution Unit, SIMD Group (32 threads)

### 2.2. SIMT â€” Single Instruction, Multiple Threads

```
SIMT lÃ  mÃ´ hÃ¬nh thá»±c thi cá»§a GPU â€” tÆ°Æ¡ng tá»± SIMD cá»§a CPU nhÆ°ng á»Ÿ má»©c THREAD:

  CPU SIMD: 1 lá»‡nh xá»­ lÃ½ 4-8 data elements trong 1 register
  GPU SIMT: 1 lá»‡nh Ä‘iá»u khiá»ƒn 32 threads CÃ™NG LÃšC (= 1 Warp)


VÃ­ dá»¥ â€” Fragment Shader xá»­ lÃ½ pixel:

  Shader code (cháº¡y cho Má»–I pixel):
  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  float4 FragMain(float2 uv) {
      float4 color = tex2D(_MainTex, uv);     // Lá»‡nh 1: Sample texture
      color.rgb *= _LightColor;                // Lá»‡nh 2: Ãp Ã¡nh sÃ¡ng
      color.rgb = pow(color.rgb, 2.2);         // Lá»‡nh 3: Gamma correction
      return color;                            // Lá»‡nh 4: Output
  }


  GPU thá»±c thi (1 Warp = 32 threads = 32 pixels):
  â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€

  Warp #0 (Pixel 0-31):
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚ Clock 1: Táº¤T Cáº¢ 32 threads cháº¡y tex2D CÃ™NG LÃšC              â”‚
  â”‚          Thread 0: tex2D(uv_0)                                 â”‚
  â”‚          Thread 1: tex2D(uv_1)                                 â”‚
  â”‚          ...                                                   â”‚
  â”‚          Thread 31: tex2D(uv_31)                               â”‚
  â”‚                                                                â”‚
  â”‚ Clock 2: Táº¤T Cáº¢ 32 threads nhÃ¢n _LightColor CÃ™NG LÃšC         â”‚
  â”‚          Thread 0: color_0 *= light                            â”‚
  â”‚          Thread 1: color_1 *= light                            â”‚
  â”‚          ...                                                   â”‚
  â”‚                                                                â”‚
  â”‚ Clock 3: Táº¤T Cáº¢ 32 threads tÃ­nh pow() CÃ™NG LÃšC               â”‚
  â”‚          ...                                                   â”‚
  â”‚                                                                â”‚
  â”‚ Clock 4: Táº¤T Cáº¢ 32 output CÃ™NG LÃšC                           â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

  â†’ 4 clocks xá»­ lÃ½ 32 pixels!
  â†’ 46 SM Ã— 4 Warp Schedulers = 184 Warps cháº¡y Ä‘á»“ng thá»i
  â†’ 184 Ã— 32 = 5,888 pixels xá»­ lÃ½ CÃ™NG 1 clock
```

### 2.3. Branch Divergence â€” Káº» giáº¿t hiá»‡u nÄƒng Shader

```
Khi if/else trong Shader, cÃ¡c threads trong Warp cÃ³ thá»ƒ Ä‘i nhÃ¡nh KHÃC NHAU:

  Shader code:
  float4 FragMain(float2 uv) {
      float4 color = tex2D(_MainTex, uv);
      
      if (color.a > 0.5) {          // â† BRANCH!
          // NhÃ¡nh A: Compute lighting (Ä‘áº¯t)
          color = ComputePBRLighting(color, normal, lightDir);
      } else {
          // NhÃ¡nh B: Discard (ráº»)
          discard;
      }
      return color;
  }


  Warp thá»±c thi khi threads Ä‘i KHÃC NHÃNH (Divergence):
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Warp #0: 32 threads, giáº£ sá»­ 20 threads â†’ A, 12 threads â†’ B â”‚
  â”‚                                                                â”‚
  â”‚  BÆ°á»›c 1: Cháº¡y nhÃ¡nh A (threads 0-19 ACTIVE, 20-31 MASKED)    â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”           â”‚
  â”‚  â”‚ T0  â”‚ T1  â”‚ ... â”‚ T19 â”‚ T20 â”‚ T21 â”‚ ... â”‚ T31 â”‚           â”‚
  â”‚  â”‚ RUN â”‚ RUN â”‚     â”‚ RUN â”‚IDLE â”‚IDLE â”‚     â”‚IDLE â”‚           â”‚
  â”‚  â”‚ PBR â”‚ PBR â”‚     â”‚ PBR â”‚ --- â”‚ --- â”‚     â”‚ --- â”‚           â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”˜           â”‚
  â”‚  â†’ 12 threads LÃƒNG PHÃ = 37.5% GPU power wasted!              â”‚
  â”‚                                                                â”‚
  â”‚  BÆ°á»›c 2: Cháº¡y nhÃ¡nh B (threads 20-31 ACTIVE, 0-19 MASKED)    â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”           â”‚
  â”‚  â”‚ T0  â”‚ T1  â”‚ ... â”‚ T19 â”‚ T20 â”‚ T21 â”‚ ... â”‚ T31 â”‚           â”‚
  â”‚  â”‚IDLE â”‚IDLE â”‚     â”‚IDLE â”‚ RUN â”‚ RUN â”‚     â”‚ RUN â”‚           â”‚
  â”‚  â”‚ --- â”‚ --- â”‚     â”‚ --- â”‚disc â”‚disc â”‚     â”‚disc â”‚           â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”˜           â”‚
  â”‚  â†’ 20 threads LÃƒNG PHÃ = 62.5%!                               â”‚
  â”‚                                                                â”‚
  â”‚  Tá»•ng: GPU pháº£i cháº¡y Cáº¢ HAI nhÃ¡nh tuáº§n tá»±                     â”‚
  â”‚  Thá»i gian = cost(A) + cost(B) thay vÃ¬ max(A, B)              â”‚
  â”‚  â†’ Worst case: divergence 50/50 = 2Ã— cháº­m hÆ¡n!               â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


â•â•â• Giáº£i phÃ¡p trong Unity Shader â•â•â•

  âŒ TRÃNH: if/else dá»±a trÃªn per-pixel data
  if (color.r > threshold) { ... } else { ... }

  âœ… DÃ™NG: Branchless math
  float mask = step(threshold, color.r);   // 0 hoáº·c 1
  color = lerp(colorB, colorA, mask);      // Blend thay vÃ¬ branch

  âœ… DÃ™NG: Texture lookup thay vÃ¬ complex branching
  float3 result = tex2D(_LookupTable, float2(input, 0));

  âœ… DÃ™NG: keyword variants thay vÃ¬ runtime branch
  #pragma multi_compile _ _FEATURE_ON
  #ifdef _FEATURE_ON
      // Code nÃ y compile thÃ nh shader variant RIÃŠNG
      // â†’ KhÃ´ng cÃ³ branch at runtime!
  #endif
```

---

## 3. GPU Memory â€” Bandwidth lÃ  vua

### 3.1. Kiáº¿n trÃºc bá»™ nhá»› GPU

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚              GPU Memory Hierarchy                                  â”‚
â”‚                                                                    â”‚
â”‚  â”Œâ”€ Per-Thread â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”          â”‚
â”‚  â”‚  Registers: ~256 KB per SM                           â”‚          â”‚
â”‚  â”‚  Tá»‘c Ä‘á»™: 0 cycles (tá»©c thÃ¬)                          â”‚          â”‚
â”‚  â”‚  â†’ Local variables trong shader                      â”‚          â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜          â”‚
â”‚           â”‚                                                        â”‚
â”‚           â–¼                                                        â”‚
â”‚  â”Œâ”€ Per-SM (Shared) â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”          â”‚
â”‚  â”‚  Shared Memory / L1: 128 KB per SM                   â”‚          â”‚
â”‚  â”‚  Tá»‘c Ä‘á»™: ~5 cycles                                   â”‚          â”‚
â”‚  â”‚  â†’ Compute Shader groupshared data                   â”‚          â”‚
â”‚  â”‚  â†’ Texture L1 cache                                  â”‚          â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜          â”‚
â”‚           â”‚                                                        â”‚
â”‚           â–¼                                                        â”‚
â”‚  â”Œâ”€ Chip-wide â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”          â”‚
â”‚  â”‚  L2 Cache: 36 MB (RTX 4070)                          â”‚          â”‚
â”‚  â”‚  Tá»‘c Ä‘á»™: ~30-50 cycles                               â”‚          â”‚
â”‚  â”‚  â†’ Texture data reuse, render target readback        â”‚          â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜          â”‚
â”‚           â”‚                                                        â”‚
â”‚           â–¼                                                        â”‚
â”‚  â”Œâ”€ Off-chip â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”          â”‚
â”‚  â”‚  VRAM (GDDR6X): 12 GB                                â”‚          â”‚
â”‚  â”‚  Tá»‘c Ä‘á»™: ~200-400 cycles                              â”‚          â”‚
â”‚  â”‚  Bandwidth: 504 GB/s                                  â”‚          â”‚
â”‚  â”‚  â†’ Textures, Buffers, Render Targets                  â”‚          â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜          â”‚
â”‚           â”‚                                                        â”‚
â”‚           â–¼   (Qua PCIe bus â€” CHáº¬M NHáº¤T)                           â”‚
â”‚  â”Œâ”€ System RAM â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”          â”‚
â”‚  â”‚  DDR5 RAM: 16-64 GB                                   â”‚          â”‚
â”‚  â”‚  Bandwidth: ~50 GB/s qua PCIe 4.0 x16                â”‚          â”‚
â”‚  â”‚  â†’ Upload textures, read-back pixels                  â”‚          â”‚
â”‚  â”‚  â†’ Má»–I Láº¦N CPUâ†”GPU transfer = BOTTLENECK!            â”‚          â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜          â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


Bandwidth lÃ  bottleneck #1 trÃªn GPU:

  VÃ­ dá»¥: Render 1080p, má»—i pixel Ä‘á»c 1 texture sample (RGBA8 = 4 bytes)
  + bilinear filter = 4 texels = 16 bytes/pixel

  2M pixels Ã— 16 bytes = 32 MB / frame
  Ã— 60 FPS = 1.92 GB/s â†’ OK cho GDDR6X

  NHÆ¯NG: Má»—i pixel thÆ°á»ng sample 5-10 textures (albedo, normal,
  roughness, AO, emission, shadow map, ...) + overdraw 2-3Ã—:

  2M Ã— 16 bytes Ã— 8 textures Ã— 2.5 overdraw = 640 MB / frame
  Ã— 60 FPS = 38.4 GB/s â†’ Báº¯t Ä‘áº§u Ä‘Ã¡ng lo!
  Ã— 120 FPS (VR) = 76.8 GB/s â†’ Gáº¦N GIá»šI Háº N!

  â†’ ÄÃ¢y lÃ  lÃ½ do tá»‘i Æ°u texture fetch Cá»°C Ká»² quan trá»ng.
```

### 3.2. Latency Hiding â€” BÃ­ quyáº¿t cá»§a GPU

```
CPU áº©n latency báº±ng: Cache lá»›n + Out-of-Order + Branch Prediction
GPU áº©n latency báº±ng: CHUYá»‚N SANG WARP KHÃC

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  SM cÃ³ 32 Warps active. Khi Warp #0 chá» texture:              â”‚
  â”‚                                                                â”‚
  â”‚  Clock 1-4:   Warp #0 cháº¡y lá»‡nh tÃ­nh toÃ¡n                    â”‚
  â”‚  Clock 5:     Warp #0 gá»i tex2D() â†’ chá» VRAM (~200 cycles)   â”‚
  â”‚                                                                â”‚
  â”‚  Clock 6:     SM CHUYá»‚N sang Warp #1 (tá»©c thÃ¬, 0 cycles!)     â”‚
  â”‚  Clock 6-10:  Warp #1 cháº¡y                                    â”‚
  â”‚  Clock 11:    Warp #1 chá» VRAM â†’ chuyá»ƒn sang Warp #2          â”‚
  â”‚  ...                                                           â”‚
  â”‚  Clock ~200:  Warp #0 nháº­n data tá»« VRAM â†’ tiáº¿p tá»¥c            â”‚
  â”‚                                                                â”‚
  â”‚  â†’ Trong 200 cycles chá», SM Ä‘Ã£ xá»­ lÃ½ ~40 Warps khÃ¡c!          â”‚
  â”‚  â†’ GPU LUÃ”N Báº¬N: khÃ´ng bao giá» stall náº¿u Ä‘á»§ Warps             â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

  Äiá»u kiá»‡n: Pháº£i cÃ³ Äá»¦ active Warps (= Occupancy cao)
  
  Occupancy = Active Warps / Max Warps per SM
  
  Occupancy tháº¥p (Ã­t Warps):
    â†’ GPU háº¿t Warp Ä‘á»ƒ chuyá»ƒn khi chá» VRAM
    â†’ SM stall â†’ hiá»‡u nÄƒng giáº£m

  NguyÃªn nhÃ¢n Occupancy tháº¥p:
    âŒ Shader dÃ¹ng quÃ¡ nhiá»u registers (register pressure)
    âŒ Shader dÃ¹ng quÃ¡ nhiá»u shared memory
    âŒ Thread Group quÃ¡ lá»›n hoáº·c quÃ¡ nhá»

  â†’ ÄÃ¢y lÃ  lÃ½ do shader ÄÃ”GIAN hÆ¡n thÆ°á»ng NHANH hÆ¡n shader phá»©c táº¡p,
    NGAY Cáº¢ KHI tá»•ng phÃ©p tÃ­nh Ã­t hÆ¡n!
```

---

## 4. Rendering Pipeline â€” Tá»« Draw Call Ä‘áº¿n Pixel

### 4.1. Tá»•ng quan luá»“ng dá»¯ liá»‡u

```
Tá»« CPU Ä‘áº¿n MÃ n hÃ¬nh â€” ToÃ n bá»™ pipeline:

  CPU Side:                          GPU Side:
  â”€â”€â”€â”€â”€â”€â”€â”€â”€                          â”€â”€â”€â”€â”€â”€â”€â”€â”€

  â‘  Game Logic (C#/ECS)
     â”‚
     â–¼
  â‘¡ Culling
     (Frustum, Occlusion)
     â”‚
     â–¼
  â‘¢ Sorting
     (Front-to-back opaque,
      back-to-front transparent)
     â”‚
     â–¼
  â‘£ Batching                    â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
     â”‚                           Command Buffer
     â–¼                           â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
  â‘¤ Draw Call:                        â”‚
     SetPassCall(shader)              â–¼
     SetTexture(albedo)          â‘¥ Input Assembly
     SetBuffer(vertices)         â‘¦ Vertex Shader        â† PROGRAMMABLE
     DrawIndexed(triCount)       â‘§ Hull/Domain Shader    â† (Tessellation)
                                 â‘¨ Geometry Shader       â† (Ã­t dÃ¹ng)
                                 â‘© Rasterization         â† FIXED-FUNCTION
                                 â‘ª Fragment Shader       â† PROGRAMMABLE
                                 â‘« Output Merger
                                      â”‚
                                      â–¼
                                 â‘¬ Framebuffer â†’ Display
```

### 4.2. Tá»«ng giai Ä‘oáº¡n chi tiáº¿t

```
â•â•â• â‘¥ Input Assembly â€” Thu tháº­p dá»¯ liá»‡u Ä‘á»‰nh â•â•â•

  GPU Ä‘á»c Vertex Buffer + Index Buffer tá»« VRAM:

  Vertex Buffer:
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚ V0: pos(1,0,0) norm(0,1,0) uv(0,0) â”‚ V1: pos(0,1,0)...    â”‚
  â”‚ V2: pos(-1,0,0)...                  â”‚ V3: pos(0,-1,0)...   â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

  Index Buffer:
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚ 0, 1, 2,  â”‚ 2, 1, 3,  â”‚ ...  â”‚  â† Má»—i 3 indices = 1 tam giÃ¡c
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

  â†’ Unity Mesh.vertices, Mesh.triangles map trá»±c tiáº¿p tá»›i Ä‘Ã¢y.


â•â•â• â‘¦ VERTEX SHADER â€” Biáº¿n Ä‘á»•i tá»« Object Space â†’ Screen Space â•â•â•

  Cháº¡y 1 láº§n PER VERTEX. GPU thá»±c thi hÃ ng triá»‡u vertices song song.

  Input:  Object Space position (tá»a Ä‘á»™ local cá»§a mesh)
  Output: Clip Space position (tá»a Ä‘á»™ chuáº©n hÃ³a cho mÃ n hÃ¬nh)

  HLSL:
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  struct Varyings {                                          â”‚
  â”‚      float4 positionCS : SV_POSITION;  // Clip Space        â”‚
  â”‚      float2 uv         : TEXCOORD0;                        â”‚
  â”‚      float3 normalWS   : TEXCOORD1;    // World Space       â”‚
  â”‚  };                                                         â”‚
  â”‚                                                             â”‚
  â”‚  Varyings vert(Attributes IN) {                             â”‚
  â”‚      Varyings OUT;                                          â”‚
  â”‚      // Ma tráº­n MVP: Model â†’ View â†’ Projection              â”‚
  â”‚      OUT.positionCS = TransformObjectToHClip(IN.positionOS);â”‚
  â”‚      OUT.uv = TRANSFORM_TEX(IN.uv, _MainTex);              â”‚
  â”‚      OUT.normalWS = TransformObjectToWorldNormal(IN.normal);â”‚
  â”‚      return OUT;                                            â”‚
  â”‚  }                                                          â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

  Biáº¿n Ä‘á»•i tá»a Ä‘á»™:
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”   Model    â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”   View    â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Object   â”‚â”€â”€Matrixâ”€â”€â”€â–ºâ”‚   World   â”‚â”€â”€Matrixâ”€â”€â–ºâ”‚  Camera   â”‚
  â”‚  Space    â”‚            â”‚   Space   â”‚           â”‚  Space    â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜            â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜           â””â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”˜
                                                         â”‚
                                                   Projection
                                                     Matrix
                                                         â”‚
                                                         â–¼
                                                   â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
                                                   â”‚   Clip     â”‚
                                                   â”‚   Space    â”‚
                                                   â”‚ (-1 to +1) â”‚
                                                   â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


â•â•â• â‘© RASTERIZATION â€” Tam giÃ¡c â†’ Pixel (Fixed-Function) â•â•â•

  GPU hardware chuyá»ƒn tam giÃ¡c thÃ nh danh sÃ¡ch pixel (fragments):

  Clip Space Triangle:           Screen Pixels (Fragments):
       â–² V0                      â”Œâ”€â”€â”€â”¬â”€â”€â”€â”¬â”€â”€â”€â”¬â”€â”€â”€â”¬â”€â”€â”€â”
      / \                        â”‚   â”‚   â”‚ â— â”‚   â”‚   â”‚
     /   \                       â”œâ”€â”€â”€â”¼â”€â”€â”€â”¼â”€â”€â”€â”¼â”€â”€â”€â”¼â”€â”€â”€â”¤
    /     \                      â”‚   â”‚ â— â”‚ â— â”‚ â— â”‚   â”‚
   /       \                     â”œâ”€â”€â”€â”¼â”€â”€â”€â”¼â”€â”€â”€â”¼â”€â”€â”€â”¼â”€â”€â”€â”¤
  V1â”€â”€â”€â”€â”€â”€â”€V2                    â”‚ â— â”‚ â— â”‚ â— â”‚ â— â”‚ â— â”‚
                                 â””â”€â”€â”€â”´â”€â”€â”€â”´â”€â”€â”€â”´â”€â”€â”€â”´â”€â”€â”€â”˜
                                  â— = Fragment (pixel candidate)

  QuÃ¡ trÃ¬nh:
  1. Edge Function: XÃ¡c Ä‘á»‹nh pixel nÃ o náº±m TRONG tam giÃ¡c
  2. Interpolation: TÃ­nh UV, Normal, Color cho má»—i fragment
     báº±ng Barycentric Coordinates (ná»™i suy trá»ng tÃ¢m)
  3. Output: Danh sÃ¡ch fragments â†’ Ä‘Æ°a vÃ o Fragment Shader

  ÄÃ¢y lÃ  hardware Cá» Äá»ŠNH (khÃ´ng láº­p trÃ¬nh Ä‘Æ°á»£c) â€” cá»±c nhanh.


â•â•â• â‘ª FRAGMENT (PIXEL) SHADER â€” TÃ´ mÃ u tá»«ng pixel â•â•â•

  Cháº¡y 1 láº§n PER FRAGMENT. ÄÃ¢y lÃ  stage Tá»N NHáº¤T (nhiá»u fragments nháº¥t).

  HLSL:
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  float4 frag(Varyings IN) : SV_Target {                    â”‚
  â”‚                                                             â”‚
  â”‚      // 1. Sample textures                                  â”‚
  â”‚      float4 albedo = tex2D(_MainTex, IN.uv);               â”‚
  â”‚      float3 normal = UnpackNormal(tex2D(_BumpMap, IN.uv)); â”‚
  â”‚      float  rough  = tex2D(_RoughnessTex, IN.uv).r;        â”‚
  â”‚                                                             â”‚
  â”‚      // 2. Lighting (PBR - Cook-Torrance BRDF)              â”‚
  â”‚      float3 N = normalize(IN.normalWS);                     â”‚
  â”‚      float3 L = normalize(_LightDir);                       â”‚
  â”‚      float  NdotL = saturate(dot(N, L));                    â”‚
  â”‚                                                             â”‚
  â”‚      float3 diffuse = albedo.rgb * NdotL * _LightColor;    â”‚
  â”‚      float3 specular = CookTorranceBRDF(N, L, V, rough);   â”‚
  â”‚                                                             â”‚
  â”‚      // 3. Shadows, AO, Emission, ...                       â”‚
  â”‚      float shadow = SampleShadowMap(IN.positionWS);         â”‚
  â”‚      float ao = tex2D(_AOTex, IN.uv).r;                    â”‚
  â”‚                                                             â”‚
  â”‚      float3 final = (diffuse + specular) * shadow * ao;     â”‚
  â”‚      return float4(final, albedo.a);                        â”‚
  â”‚  }                                                          â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

  Chi phÃ­:
  - Má»—i tex2D() = 1 texture fetch (~4-200 cycles tÃ¹y cache)
  - PBR lighting = ~50-100 ALU ops
  - Shadow sampling = 1-16 texture fetches (PCF/PCSS)
  - NhÃ¢n vá»›i 2M pixels Ã— overdraw 2-3Ã— = THá»¤ NGHIá»†P Lá»šN NHáº¤T

  â†’ Fragment Shader optimization = ÄÃ’N Báº¨Y Lá»šN NHáº¤T cho FPS!


â•â•â• â‘« OUTPUT MERGER â€” Test & Blend â•â•â•

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Depth Test (Z-Buffer):                                    â”‚
  â”‚    if (fragment.z < zbuffer[x,y]) {                        â”‚
  â”‚        zbuffer[x,y] = fragment.z;    // Cáº­p nháº­t depth     â”‚
  â”‚        colorbuffer[x,y] = fragment.color;                  â”‚
  â”‚    }                                                       â”‚
  â”‚    // else: fragment bá»‹ che bá»Ÿi object gáº§n hÆ¡n â†’ DISCARD   â”‚
  â”‚                                                            â”‚
  â”‚  Stencil Test: Masking (UI, portals, decals)               â”‚
  â”‚                                                            â”‚
  â”‚  Blending (cho transparent objects):                        â”‚
  â”‚    finalColor = src.rgb * src.a + dst.rgb * (1 - src.a)    â”‚
  â”‚    â†’ Transparent objects pháº£i render SAU opaque             â”‚
  â”‚    â†’ Pháº£i sort BACK-TO-FRONT                               â”‚
  â”‚    â†’ KHÃ”NG viáº¿t depth â†’ overdraw tÄƒng!                     â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## 5. Draw Calls & Batching â€” CPUâ†”GPU Communication

### 5.1. Draw Call lÃ  gÃ¬?

```
Draw Call = 1 láº§n CPU ra lá»‡nh cho GPU render.

  Má»—i Draw Call, CPU pháº£i:
  1. Set Shader (Pipeline State)        â†’ GPU state change
  2. Set Textures (Albedo, Normal, ...) â†’ Bind textures
  3. Set Constant Buffers (MVP matrix)  â†’ Upload uniforms
  4. Set Vertex/Index Buffers           â†’ Bind geometry
  5. Gá»i DrawIndexed(triangleCount)     â†’ GPU báº¯t Ä‘áº§u render

  Chi phÃ­: ~5-20 Î¼s per draw call (phÃ­a CPU)
  
  â†’ 1,000 draw calls = 5-20ms â†’ Gáº¦N Háº¾T budget 16.67ms/frame!
  â†’ GPU thÆ°á»ng NHANH hÆ¡n CPU render â†’ CPU-bound!


  â”Œâ”€â”€ Frame Timeline â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                               â”‚
  â”‚  CPU:  [Draw1][Draw2][Draw3]...[Draw500][Submit]              â”‚
  â”‚        â–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆ  = 12ms       â”‚
  â”‚                                                               â”‚
  â”‚  GPU:        [Render1][Render2][Render3]...[Render500]        â”‚
  â”‚              â–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆâ–ˆ  = 6ms      â”‚
  â”‚                                                               â”‚
  â”‚  â†’ CPU is BOTTLENECK! GPU chá» CPU gá»­i tiáº¿p.                  â”‚
  â”‚  â†’ Frame time = max(CPU, GPU) = 12ms                          â”‚
  â”‚  â†’ Giáº£m draw calls = giáº£m CPU time = tÄƒng FPS                â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 5.2. Batching Strategies

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                    BATCHING TECHNIQUES                               â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ Static Batching   â”‚ Combine meshes dÃ¹ng CÃ™NG material táº¡i          â”‚
â”‚                   â”‚ build time (bake thÃ nh 1 mesh lá»›n)              â”‚
â”‚                   â”‚ âœ… No CPU cost at runtime                       â”‚
â”‚                   â”‚ âŒ TÄƒng memory (duplicate vertices)             â”‚
â”‚                   â”‚ âŒ Objects khÃ´ng thá»ƒ move / animate              â”‚
â”‚                   â”‚ ðŸŽ¯ DÃ¹ng cho: environment, props cá»‘ Ä‘á»‹nh         â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ Dynamic Batching  â”‚ Combine meshes nhá» (<300 verts) má»—i frame      â”‚
â”‚                   â”‚ âœ… Objects cÃ³ thá»ƒ move                          â”‚
â”‚                   â”‚ âŒ CPU cost cho combining                        â”‚
â”‚                   â”‚ âŒ Chá»‰ meshes ráº¥t nhá»                           â”‚
â”‚                   â”‚ ðŸŽ¯ DÃ¹ng cho: particles, small props             â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ GPU Instancing    â”‚ 1 Draw Call render N copies cá»§a CÃ™NG mesh       â”‚
â”‚                   â”‚ âœ… Minimal CPU overhead                         â”‚
â”‚                   â”‚ âœ… Má»—i instance cÃ³ thá»ƒ khÃ¡c position/color      â”‚
â”‚                   â”‚ âŒ CÃ¹ng mesh + cÃ¹ng material                    â”‚
â”‚                   â”‚ ðŸŽ¯ DÃ¹ng cho: trees, grass, enemies cÃ¹ng model   â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ SRP Batcher       â”‚ Cache GPU state â†’ reduce state changes          â”‚
â”‚                   â”‚ âœ… KhÃ´ng cáº§n cÃ¹ng mesh                          â”‚
â”‚                   â”‚ âœ… Chá»‰ cáº§n cÃ¹ng shader variant                  â”‚
â”‚                   â”‚ âŒ URP/HDRP only (SRP = Scriptable RP)          â”‚
â”‚                   â”‚ ðŸŽ¯ Chiáº¿n lÆ°á»£c máº·c Ä‘á»‹nh cho URP projects         â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ DrawMeshInstanced â”‚ Render tá»« Compute Buffer â€” GPU-driven           â”‚
â”‚ Indirect          â”‚ âœ… CPU gáº§n nhÆ° ZERO cost                        â”‚
â”‚                   â”‚ âœ… GPU tá»± culling + sorting                     â”‚
â”‚                   â”‚ âŒ Phá»©c táº¡p Ä‘á»ƒ implement                        â”‚
â”‚                   â”‚ ðŸŽ¯ DÃ¹ng cho: grass, foliage, massive crowds     â”‚
â”‚                   â”‚    (100K+ instances)                             â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


VÃ­ dá»¥ DrawMeshInstancedIndirect (GPU-Driven Pipeline):

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                                â”‚
  â”‚  BÆ°á»›c 1: CPU upload instance data â†’ Compute Buffer (1 láº§n)    â”‚
  â”‚    StructuredBuffer<InstanceData> _InstanceBuffer;             â”‚
  â”‚    // position, rotation, scale, color cho 100K instances      â”‚
  â”‚                                                                â”‚
  â”‚  BÆ°á»›c 2: GPU Compute Shader culling (má»—i frame)               â”‚
  â”‚    â†’ Test má»—i instance vs frustum â†’ output visible list       â”‚
  â”‚    â†’ AppendStructuredBuffer<uint> _VisibleInstances;           â”‚
  â”‚                                                                â”‚
  â”‚  BÆ°á»›c 3: CPU gá»i DrawMeshInstancedIndirect                    â”‚
  â”‚    â†’ 1 DRAW CALL cho 100,000 instances!                       â”‚
  â”‚    â†’ GPU tá»± láº¥y data tá»« buffer, khÃ´ng cáº§n CPU per-instance    â”‚
  â”‚                                                                â”‚
  â”‚  Káº¿t quáº£:                                                      â”‚
  â”‚    Truyá»n thá»‘ng: 100,000 draw calls = 500ms (impossible)       â”‚
  â”‚    Instancing:   1 draw call = ~0.5ms (GPU only)               â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## 6. Tile-Based Rendering â€” Kiáº¿n trÃºc GPU Mobile

### 6.1. IMR vs TBR

```
Desktop GPU (Immediate Mode Rendering â€” IMR):
  â†’ Render tam giÃ¡c â†’ ghi pixel NGAY vÃ o Framebuffer (VRAM)
  â†’ Má»—i pixel ghi = 1 VRAM write = tá»‘n bandwidth
  â†’ VRAM bandwidth cao (504 GB/s) â†’ khÃ´ng sao

Mobile GPU (Tile-Based Rendering â€” TBR):
  â†’ Chia mÃ n hÃ¬nh thÃ nh Tiles (16Ã—16 hoáº·c 32Ã—32 pixels)
  â†’ Render toÃ n bá»™ geometry cho 1 Tile â†’ ghi káº¿t quáº£ TRONG on-chip memory
  â†’ Chá»‰ ghi ra VRAM 1 láº§n khi Tile hoÃ n thÃ nh
  â†’ Tiáº¿t kiá»‡m bandwidth KHá»”NG Lá»’ (10-20Ã—!)


â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  Immediate Mode (Desktop):              Tile-Based (Mobile):     â”‚
â”‚                                                                  â”‚
â”‚  Tam giÃ¡c 1: Ghi pixel A,B,C          Binning Phase:            â”‚
â”‚  Tam giÃ¡c 2: Ghi pixel D,E,F          â†’ PhÃ¢n tam giÃ¡c vÃ o Tiles â”‚
â”‚  Tam giÃ¡c 3: Ghi pixel G,H,I                                    â”‚
â”‚  ...                                   Rendering Phase:          â”‚
â”‚  â†’ N láº§n ghi VRAM                      Tile 0: [T1,T5,T8]      â”‚
â”‚                                         â†’ Render trÃªn chip       â”‚
â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                     â†’ Ghi 1 láº§n ra VRAM     â”‚
â”‚  â”‚ VRAM           â”‚                                              â”‚
â”‚  â”‚ bandwidth:     â”‚                    Tile 1: [T2,T3,T7]       â”‚
â”‚  â”‚ 504 GB/s (PC)  â”‚                    â†’ Render trÃªn chip        â”‚
â”‚  â”‚ ~50 GB/s (Mobile)â”‚ â† Bandwidth Gáº¤P 10Ã— tháº¥p hÆ¡n!            â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                    ...                       â”‚
â”‚                                                                  â”‚
â”‚  Há»‡ quáº£ cho Unity Developer:                                    â”‚
â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”   â”‚
â”‚  â”‚  âŒ TRÃNH trÃªn Mobile:                                   â”‚   â”‚
â”‚  â”‚  - Äá»c Framebuffer giá»¯a chá»«ng (_CameraOpaqueTexture)    â”‚   â”‚
â”‚  â”‚    â†’ Force flush Tile â†’ ghi ra VRAM â†’ Ä‘á»c láº¡i = 2Ã— cost â”‚   â”‚
â”‚  â”‚  - RenderTexture.GetTemporary() khÃ´ng cáº©n tháº­n           â”‚   â”‚
â”‚  â”‚  - QuÃ¡ nhiá»u render passes                                â”‚   â”‚
â”‚  â”‚                                                           â”‚   â”‚
â”‚  â”‚  âœ… DÃ™NG trÃªn Mobile:                                    â”‚   â”‚
â”‚  â”‚  - Load/Store Actions hiá»‡u quáº£ (DontCare, Clear)         â”‚   â”‚
â”‚  â”‚  - Memoryless render targets (transient attachments)      â”‚   â”‚
â”‚  â”‚  - NativeRenderPass API (URP 12+)                         â”‚   â”‚
â”‚  â”‚  - MSAA (gáº§n nhÆ° miá»…n phÃ­ trÃªn TBR â€” resolve trÃªn chip!) â”‚   â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜   â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


MSAA trÃªn TBR vs IMR:

  Desktop (IMR):
    MSAA 4Ã— = 4Ã— bandwidth (Ä‘á»c/ghi 4 samples per pixel vÃ o VRAM)
    â†’ Äáº¯t! (thÆ°á»ng dÃ¹ng FXAA/TAA thay tháº¿)

  Mobile (TBR):
    MSAA 4Ã— = resolve trÃªn Tile Memory (on-chip, cá»±c nhanh!)
    â†’ Chá»‰ ghi 1 resolved pixel ra VRAM
    â†’ MSAA 4Ã— trÃªn mobile Gáº¦N NHÆ¯ MIá»„N PHÃ!
    â†’ ÄÃ¢y lÃ  lÃ½ do URP default báº­t MSAA trÃªn mobile.
```

---

## 7. Compute Shaders â€” GPU khÃ´ng chá»‰ render

### 7.1. GPGPU trong Unity

```
Compute Shader = Cháº¡y code trÃªn GPU KHÃ”NG liÃªn quan Ä‘áº¿n rendering.

Báº¥t ká»³ tÃ­nh toÃ¡n nÃ o cáº§n Xá»¬ LÃ SONG SONG lÆ°á»£ng lá»›n dá»¯ liá»‡u:
  âœ… Particle simulation (100K+ particles)
  âœ… Frustum/Occlusion culling trÃªn GPU
  âœ… Skinned mesh animation (GPU skinning)
  âœ… Terrain sculpting / erosion
  âœ… AI pathfinding (flow fields)
  âœ… Physics (broad phase collision)
  âœ… Image processing (blur, bloom, color grading)


Thread Group = TÆ°Æ¡ng Ä‘Æ°Æ¡ng Warp/Wavefront:

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

  â†’ 100,000 particles Ã· 64 = 1,563 thread groups
  â†’ GPU xá»­ lÃ½ ~5,888 threads Ä‘á»“ng thá»i
  â†’ HoÃ n thÃ nh trong ~27 "waves"
  â†’ Total: <0.5ms thay vÃ¬ CPU ~15ms


  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  CPU (Burst + Jobs, 8 cores):                               â”‚
  â”‚    100K particles Ã· 8 cores = 12,500 particles/core         â”‚
  â”‚    ~12,500 Ã— 10ns = 0.125ms per core â†’ ~0.15ms total        â”‚
  â”‚                                                             â”‚
  â”‚  GPU (Compute Shader):                                      â”‚
  â”‚    100K particles Ã· 5,888 threads = ~17 "waves"             â”‚
  â”‚    ~17 Ã— 20ns/wave = ~0.34ms                                â”‚
  â”‚                                                             â”‚
  â”‚  â†’ Cho 100K: CPU Burst â‰ˆ GPU Compute                        â”‚
  â”‚  â†’ Cho 1M+: GPU Compute WIN (5,888 >> 8 cores)              â”‚
  â”‚  â†’ BONUS: GPU compute GIáº¢I PHÃ“NG CPU cho game logic!        â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## 8. Shader Optimization â€” Quy táº¯c vÃ ng

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚              SHADER OPTIMIZATION CHECKLIST                           â”‚
â”œâ”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚  #1  â”‚ GIáº¢M TEXTURE FETCHES                                        â”‚
â”‚      â”‚ - Pack data: metallic+roughness+AO vÃ o 1 texture (RGB)      â”‚
â”‚      â”‚ - Channel packing: mask vÃ o alpha channel                    â”‚
â”‚      â”‚ - Atlas textures: nhiá»u sprites trong 1 texture             â”‚
â”‚      â”‚ - Giáº£m shadow cascade quality khi xa camera                 â”‚
â”œâ”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚  #2  â”‚ TRÃNH BRANCH DIVERGENCE                                     â”‚
â”‚      â”‚ - step(), lerp(), smoothstep() thay if/else                 â”‚
â”‚      â”‚ - #pragma multi_compile cho feature toggles                 â”‚
â”‚      â”‚ - Precompute vÃ o lookup texture                             â”‚
â”œâ”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚  #3  â”‚ DÃ™NG PRECISION THáº¤P KHI Äá»¦                                 â”‚
â”‚      â”‚ - half (16-bit) cho colors, UVs, normals                    â”‚
â”‚      â”‚ - float (32-bit) chá»‰ cho positions, depth                   â”‚
â”‚      â”‚ - min16float / min16int cho mobile                          â”‚
â”‚      â”‚ â†’ Mobile GPU cÃ³ native half ALU â†’ 2Ã— throughput!            â”‚
â”œâ”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚  #4  â”‚ GIáº¢M OVERDRAW                                               â”‚
â”‚      â”‚ - Render opaque objects FRONT-TO-BACK (early-z reject)      â”‚
â”‚      â”‚ - Avoid alpha test (clip/discard) khi cÃ³ thá»ƒ               â”‚
â”‚      â”‚ - Z-prepass cho complex scenes                              â”‚
â”‚      â”‚ - LOD system (Ã­t triangles á»Ÿ xa = Ã­t fragments)             â”‚
â”œâ”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚  #5  â”‚ Tá»I Æ¯U ALU                                                  â”‚
â”‚      â”‚ - rsqrt() thay 1/sqrt()                                    â”‚
â”‚      â”‚ - mad(a,b,c) thay a*b+c (1 lá»‡nh thay 2)                   â”‚
â”‚      â”‚ - TrÃ¡nh pow(), sin(), cos() trong fragment shader           â”‚
â”‚      â”‚   â†’ Precompute vÃ o LUT texture                              â”‚
â”œâ”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚  #6  â”‚ BANDWIDTH AWARENESS                                         â”‚
â”‚      â”‚ - Texture compression (BC7/ASTC) giáº£m 4-8Ã— size            â”‚
â”‚      â”‚ - Mipmaps luÃ´n báº­t (Ã­t texels fetch khi xa)                 â”‚
â”‚      â”‚ - Render Scale < 1.0 cho mobile (FSR upscale)               â”‚
â”‚      â”‚ - Prefer Compute over Fragment cho heavy transforms         â”‚
â””â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## 9. Tá»•ng káº¿t Chapter 4 â€” GPU trong 1 Frame

```
Báº¡n nháº¥n Play. Frame N render:

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                                  â”‚
  â”‚  CPU (Chapter 3):                                                â”‚
  â”‚   â‘  ECS Systems â†’ ScheduleParallel Jobs â†’ Burst â†’ SIMD          â”‚
  â”‚   â‘¡ Camera Culling: Frustum test 10,000 objects â†’ 2,000 visible â”‚
  â”‚   â‘¢ Sort: Opaque front-to-back, Transparent back-to-front       â”‚
  â”‚   â‘£ Build Command Buffer: ~200 draw calls                       â”‚
  â”‚   â‘¤ Submit Command Buffer â†’ GPU qua PCIe/shared memory         â”‚
  â”‚      â†’ CPU báº¯t Ä‘áº§u frame N+1 NGAY (CPU vÃ  GPU cháº¡y song song!) â”‚
  â”‚                                                                  â”‚
  â”‚  GPU:                                                            â”‚
  â”‚   â‘¥ Shadow Pass: Render depth tá»« gÃ³c nhÃ¬n light â†’ Shadow Map    â”‚
  â”‚   â‘¦ Z-Prepass: Render depth tá»« camera (optional, cho early-z)   â”‚
  â”‚   â‘§ Opaque Pass:                                                â”‚
  â”‚      - Vertex Shader: MVP transform Ã— 500K vertices             â”‚
  â”‚      - Rasterizer: Tam giÃ¡c â†’ ~4M fragments                     â”‚
  â”‚      - Fragment Shader: PBR lighting Ã— 4M pixels                â”‚
  â”‚      - Early-Z: Reject ~2M fragments (behind other objects)     â”‚
  â”‚   â‘¨ Transparent Pass:                                           â”‚
  â”‚      - Back-to-front, alpha blending                             â”‚
  â”‚   â‘© Post-Processing:                                             â”‚
  â”‚      - Bloom, Color Grading, Tonemapping, FXAA/TAA              â”‚
  â”‚      - (Má»—i pass = fullscreen quad = 2M fragments)              â”‚
  â”‚   â‘ª Final Blit â†’ Framebuffer â†’ Display                          â”‚
  â”‚                                                                  â”‚
  â”‚  Tá»•ng GPU time: ~8ms = 120 FPS âœ…                                â”‚
  â”‚  (Bottleneck thÆ°á»ng á»Ÿ Fragment Shader hoáº·c Bandwidth)            â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

> **BÃ i há»c thá»±c tiá»…n:**
> 1. **GPU â‰  faster CPU.** GPU lÃ  bá»™ xá»­ lÃ½ song song khá»•ng lá»“, giá»i á»Ÿ throughput, yáº¿u á»Ÿ latency.
> 2. **Branch = káº» thÃ¹ #1** trÃªn GPU. Branchless math (step/lerp/select) luÃ´n Æ°u tiÃªn.
> 3. **Bandwidth > Compute** trÃªn mobile. Giáº£m texture fetches, dÃ¹ng half precision, compression.
> 4. **Draw calls = CPU cost.** SRP Batcher + GPU Instancing + Indirect = giáº£m CPU overhead.
> 5. **Profile báº±ng Frame Debugger + GPU Profiler** trÆ°á»›c khi tá»‘i Æ°u. Biáº¿t bottleneck á»Ÿ Ä‘Ã¢u má»›i fix Ä‘Ãºng chá»—.

---

> **ChÆ°Æ¡ng tiáº¿p theo:** [Chapter 5 â€” Unity Case Study]() â€” Kiáº¿n trÃºc dual-language (C++ Engine + C# Scripting), Mono vs IL2CPP, DOTS full stack, vÃ  tá»•ng káº¿t chuá»—i Transistor â†’ Frame.

---
*Chapter 4 â€” NghiÃªn cá»©u cho Unity High-Performance Agent*
# ChÆ°Æ¡ng 5: Unity Engine Case Study â€” Tá»« C++ Core Ä‘áº¿n C# Scripting

> **Má»¥c tiÃªu chÆ°Æ¡ng:** Hiá»ƒu kiáº¿n trÃºc ná»™i bá»™ cá»§a Unity Engine, táº¡i sao nÃ³ dÃ¹ng hai ngÃ´n ngá»¯ (C++ vÃ  C#), cÃ¡ch Mono/IL2CPP/Burst chuyá»ƒn code thÃ nh mÃ£ mÃ¡y, vÃ  cÃ¡ch DOTS táº­n dá»¥ng toÃ n bá»™ kiáº¿n thá»©c pháº§n cá»©ng tá»« Chapter 1-4.

---

## 1. Kiáº¿n trÃºc Unity â€” Táº¡i sao Dual-Language?

### 1.1. BÃ i toÃ¡n thiáº¿t káº¿ Engine

```
Engine game cáº§n giáº£i quyáº¿t HAI bÃ i toÃ¡n TRÃI NGÆ¯á»¢C nhau:

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                                 â”‚
  â”‚  BÃ€I TOÃN 1: HIá»†U NÄ‚NG Cá»°C CAO                                â”‚
  â”‚  â†’ Rendering pipeline: xá»­ lÃ½ hÃ ng triá»‡u tam giÃ¡c/frame         â”‚
  â”‚  â†’ Physics engine: va cháº¡m, ragdoll, fluid                      â”‚
  â”‚  â†’ Memory management: pool, allocator, alignment                â”‚
  â”‚  â†’ Audio mixer: sample processing at 48 KHz                    â”‚
  â”‚                                                                 â”‚
  â”‚  YÃŠU Cáº¦U: C/C++ (truy cáº­p trá»±c tiáº¿p hardware, zero overhead)   â”‚
  â”‚                                                                 â”‚
  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
  â”‚                                                                 â”‚
  â”‚  BÃ€I TOÃN 2: ITERATION NHANH CHO GAME LOGIC                    â”‚
  â”‚  â†’ Viáº¿t AI, UI, gameplay rules, quests, dialogues              â”‚
  â”‚  â†’ Cáº§n hot-reload (sá»­a code â†’ tháº¥y káº¿t quáº£ ngay)              â”‚
  â”‚  â†’ Level designer / artist cÅ©ng cáº§n scripting Ä‘Æ¡n giáº£n          â”‚
  â”‚  â†’ Crash do pointer bug = máº¥t hÃ ng giá» debug                   â”‚
  â”‚                                                                 â”‚
  â”‚  YÃŠU Cáº¦U: NgÃ´n ngá»¯ an toÃ n, dá»… há»c, GC tá»± quáº£n lÃ½ bá»™ nhá»›      â”‚
  â”‚                                                                 â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜

  â†’ GIáº¢I PHÃP: Chia engine thÃ nh 2 táº§ng.
```

### 1.2. Kiáº¿n trÃºc hai táº§ng

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                    UNITY ENGINE ARCHITECTURE                        â”‚
â”‚                                                                     â”‚
â”‚  â”Œâ”€â”€ C# Scripting Layer (Frontend) â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”   â”‚
â”‚  â”‚                                                              â”‚   â”‚
â”‚  â”‚  Game Logic:                                                 â”‚   â”‚
â”‚  â”‚   â— MonoBehaviour scripts (Update, Start, ...)               â”‚   â”‚
â”‚  â”‚   â— ScriptableObjects (data assets)                          â”‚   â”‚
â”‚  â”‚   â— ECS Systems (ISystem, SystemBase)                        â”‚   â”‚
â”‚  â”‚   â— UI Toolkit (UXML, USS)                                  â”‚   â”‚
â”‚  â”‚   â— Editor Extensions (Custom Inspectors, Tools)             â”‚   â”‚
â”‚  â”‚                                                              â”‚   â”‚
â”‚  â”‚  Runtime: Mono JIT (Editor) / IL2CPP AOT (Build)             â”‚   â”‚
â”‚  â”‚  Hot-reload: Domain Reload khi sá»­a script                    â”‚   â”‚
â”‚  â”‚                                                              â”‚   â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜   â”‚
â”‚                            â”‚                                        â”‚
â”‚                   C# â†” C++ Binding Layer                            â”‚
â”‚                   (Internal Calls / P/Invoke)                       â”‚
â”‚                            â”‚                                        â”‚
â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”   â”‚
â”‚  â”‚                                                              â”‚   â”‚
â”‚  â”‚  C++ Native Engine (Backend)                                 â”‚   â”‚
â”‚  â”‚                                                              â”‚   â”‚
â”‚  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”       â”‚   â”‚
â”‚  â”‚  â”‚  Rendering   â”‚  â”‚   Physics    â”‚  â”‚    Audio     â”‚       â”‚   â”‚
â”‚  â”‚  â”‚  (SRP Core,  â”‚  â”‚  (PhysX /    â”‚  â”‚  (FMOD /     â”‚       â”‚   â”‚
â”‚  â”‚  â”‚   Graphics   â”‚  â”‚   Custom)    â”‚  â”‚   Native)    â”‚       â”‚   â”‚
â”‚  â”‚  â”‚   API abstraction) â”‚            â”‚  â”‚              â”‚       â”‚   â”‚
â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜       â”‚   â”‚
â”‚  â”‚                                                              â”‚   â”‚
â”‚  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”       â”‚   â”‚
â”‚  â”‚  â”‚   Memory     â”‚  â”‚  Job System  â”‚  â”‚  Animation   â”‚       â”‚   â”‚
â”‚  â”‚  â”‚  Management  â”‚  â”‚  (Native     â”‚  â”‚  (Mecanim    â”‚       â”‚   â”‚
â”‚  â”‚  â”‚  (Allocators,â”‚  â”‚   threads)   â”‚  â”‚   native)    â”‚       â”‚   â”‚
â”‚  â”‚  â”‚   Pools)     â”‚  â”‚              â”‚  â”‚              â”‚       â”‚   â”‚
â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜       â”‚   â”‚
â”‚  â”‚                                                              â”‚   â”‚
â”‚  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                         â”‚   â”‚
â”‚  â”‚  â”‚  Asset       â”‚  â”‚  Platform    â”‚                         â”‚   â”‚
â”‚  â”‚  â”‚  Pipeline    â”‚  â”‚  Abstraction â”‚                         â”‚   â”‚
â”‚  â”‚  â”‚  (Import,    â”‚  â”‚  (Win, Mac,  â”‚                         â”‚   â”‚
â”‚  â”‚  â”‚   Serialize) â”‚  â”‚   iOS, Andr) â”‚                         â”‚   â”‚
â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                         â”‚   â”‚
â”‚  â”‚                                                              â”‚   â”‚
â”‚  â”‚  Compiled thÃ nh: UnityPlayer.dll (Win), libunity.so (Andr)  â”‚   â”‚
â”‚  â”‚  100% native code â€” compiler tá»‘i Æ°u cho tá»«ng platform        â”‚   â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜   â”‚
â”‚                                                                     â”‚
â”‚  â”Œâ”€â”€ Platform Layer â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”   â”‚
â”‚  â”‚  OS APIs: Win32, Cocoa, JNI, ...                             â”‚   â”‚
â”‚  â”‚  Graphics APIs: Direct3D 12, Vulkan, Metal, WebGPU, OpenGL   â”‚   â”‚
â”‚  â”‚  Input: XInput, HID, Touch events                            â”‚   â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜   â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 1.3. C# â†” C++ Binding â€” Lá»›p keo dÃ­nh

```
Khi báº¡n gá»i transform.position trong C#, Ä‘iá»u gÃ¬ xáº£y ra?

  C# Code:
  â”€â”€â”€â”€â”€â”€â”€â”€
  transform.position = new Vector3(1, 2, 3);


  Thá»±c táº¿ bÃªn dÆ°á»›i:

  â”Œâ”€â”€ C# Layer â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                          â”‚
  â”‚  // UnityEngine.Transform (C# wrapper class)             â”‚
  â”‚  public Vector3 position {                               â”‚
  â”‚      set {                                                â”‚
  â”‚          SetPosition_Injected(ref value);  // â† gá»i C++  â”‚
  â”‚      }                                                    â”‚
  â”‚  }                                                        â”‚
  â”‚                                                          â”‚
  â”‚  [MethodImpl(MethodImplOptions.InternalCall)]             â”‚
  â”‚  extern static void SetPosition_Injected(ref Vector3 v); â”‚
  â”‚  // â†‘ "InternalCall" = hÃ m nÃ y KHÃ”NG cÃ³ body C#          â”‚
  â”‚  //   NÃ³ Ä‘Æ°á»£c link trá»±c tiáº¿p tá»›i hÃ m C++ trong engine    â”‚
  â”‚                                                          â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                         â”‚ Marshalling (chuyá»ƒn Ä‘á»•i data layout)
                         â”‚ Vector3 (C#) â†’ Vector3f (C++)
                         â–¼
  â”Œâ”€â”€ C++ Layer â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                          â”‚
  â”‚  // Transform.cpp (trong Unity C++ engine)                â”‚
  â”‚  void Transform::SetPosition(const Vector3f& pos) {      â”‚
  â”‚      m_LocalPosition = TransformPoint(                    â”‚
  â”‚          GetParent(), pos);                                â”‚
  â”‚      // â†’ Cáº­p nháº­t TransformHierarchy                     â”‚
  â”‚      // â†’ Invalidate bounding boxes                       â”‚
  â”‚      // â†’ Notify Physics engine                           â”‚
  â”‚      // â†’ Mark dirty cho rendering                        â”‚
  â”‚      SetDirty();                                          â”‚
  â”‚  }                                                        â”‚
  â”‚                                                          â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


Chi phÃ­ Managed â†” Native transition:

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Má»—i láº§n gá»i C++ tá»« C#:                                   â”‚
  â”‚    1. Marshalling data types (~10-50ns)                    â”‚
  â”‚    2. Safety checks (null, thread) (~5-20ns)               â”‚
  â”‚    3. Actual C++ execution (varies)                        â”‚
  â”‚    4. Marshal return value back (~10-50ns)                  â”‚
  â”‚                                                            â”‚
  â”‚  Overhead: ~30-100ns PER CALL                              â”‚
  â”‚                                                            â”‚
  â”‚  â†’ 10,000 GetComponent<T>() calls / frame                 â”‚
  â”‚  â†’ 10,000 Ã— 100ns = 1ms OVERHEAD ALONE!                   â”‚
  â”‚  â†’ ÄÃ¢y lÃ  lÃ½ do cache references á»Ÿ Awake()                â”‚
  â”‚                                                            â”‚
  â”‚  DOTS bypass:                                              â”‚
  â”‚  â†’ IComponentData = pure C# structs, KHÃ”NG gá»i C++        â”‚
  â”‚  â†’ SystemAPI.Query = iterate trá»±c tiáº¿p trÃªn bá»™ nhá»› C#     â”‚
  â”‚  â†’ Burst compile = native code KHÃ”NG cáº§n marshalling       â”‚
  â”‚  â†’ Chi phÃ­: 0ns overhead!                                  â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## 2. Mono vs IL2CPP â€” Chi tiáº¿t ká»¹ thuáº­t

### 2.1. Mono Runtime â€” JIT Compilation

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                    MONO RUNTIME                                     â”‚
â”‚                                                                     â”‚
â”‚  Khi Unity Editor cháº¡y Play Mode:                                   â”‚
â”‚                                                                     â”‚
â”‚  â”Œâ”€â”€â”€â”€ Domain Reload â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”‚
â”‚  â”‚ 1. Unload táº¥t cáº£ scripts cÅ©                                  â”‚  â”‚
â”‚  â”‚ 2. Load .dll files má»›i (Assembly-CSharp.dll, ...)             â”‚  â”‚
â”‚  â”‚ 3. Táº¡o láº¡i static state                                      â”‚  â”‚
â”‚  â”‚ 4. Gá»i [RuntimeInitializeOnLoadMethod]                        â”‚  â”‚
â”‚  â”‚ â†’ Domain Reload máº¥t: 2-10 giÃ¢y (tÃ¹y project size)            â”‚  â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â”‚
â”‚                                                                     â”‚
â”‚  â”Œâ”€â”€â”€â”€ JIT Compilation â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”‚
â”‚  â”‚                                                               â”‚  â”‚
â”‚  â”‚  Láº§n Ä‘áº§u gá»i Update() trÃªn EnemyAI script:                   â”‚  â”‚
â”‚  â”‚                                                               â”‚  â”‚
â”‚  â”‚  IL Bytecode (trong .dll):                                    â”‚  â”‚
â”‚  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                     â”‚  â”‚
â”‚  â”‚  â”‚ .method void Update() {              â”‚                     â”‚  â”‚
â”‚  â”‚  â”‚   ldarg.0                            â”‚                     â”‚  â”‚
â”‚  â”‚  â”‚   ldfld float3 position              â”‚ â†’ JIT Compiler      â”‚  â”‚
â”‚  â”‚  â”‚   ldarg.0                            â”‚   phÃ¢n tÃ­ch IL      â”‚  â”‚
â”‚  â”‚  â”‚   ldfld float3 velocity              â”‚   vÃ  sinh ra        â”‚  â”‚
â”‚  â”‚  â”‚   ldsfld float deltaTime             â”‚   native code       â”‚  â”‚
â”‚  â”‚  â”‚   mul                                â”‚   táº¡i runtime       â”‚  â”‚
â”‚  â”‚  â”‚   add                                â”‚                     â”‚  â”‚
â”‚  â”‚  â”‚   stfld float3 position              â”‚                     â”‚  â”‚
â”‚  â”‚  â”‚ }                                    â”‚                     â”‚  â”‚
â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                     â”‚  â”‚
â”‚  â”‚                    â”‚                                           â”‚  â”‚
â”‚  â”‚                    â–¼                                           â”‚  â”‚
â”‚  â”‚  Native Code (trong memory):                                  â”‚  â”‚
â”‚  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                     â”‚  â”‚
â”‚  â”‚  â”‚ ; x86-64 â€” Mono JIT output           â”‚                     â”‚  â”‚
â”‚  â”‚  â”‚ push    rbp                          â”‚                     â”‚  â”‚
â”‚  â”‚  â”‚ mov     rbp, rsp                     â”‚                     â”‚  â”‚
â”‚  â”‚  â”‚ movss   xmm0, [rcx+0x10]  ; pos.x   â”‚ â† Scalar!          â”‚  â”‚
â”‚  â”‚  â”‚ movss   xmm1, [rcx+0x1C]  ; vel.x   â”‚   Mono KHÃ”NG       â”‚  â”‚
â”‚  â”‚  â”‚ movss   xmm2, [rip+dt]    ; dt       â”‚   vectorize.       â”‚  â”‚
â”‚  â”‚  â”‚ mulss   xmm1, xmm2        ; vel*dt   â”‚   Tá»«ng float       â”‚  â”‚
â”‚  â”‚  â”‚ addss   xmm0, xmm1        ; pos+vel  â”‚   má»™t.             â”‚  â”‚
â”‚  â”‚  â”‚ movss   [rcx+0x10], xmm0  ; store    â”‚                     â”‚  â”‚
â”‚  â”‚  â”‚ ; ... láº·p cho y, z                    â”‚ â† 3Ã— lá»‡nh         â”‚  â”‚
â”‚  â”‚  â”‚ pop     rbp                          â”‚   thay vÃ¬ 1Ã—       â”‚  â”‚
â”‚  â”‚  â”‚ ret                                  â”‚   SIMD!             â”‚  â”‚
â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                     â”‚  â”‚
â”‚  â”‚                                                               â”‚  â”‚
â”‚  â”‚  Láº§n gá»i sau: Cháº¡y native code ÄÃƒ COMPILE (khÃ´ng JIT láº¡i)   â”‚  â”‚
â”‚  â”‚                                                               â”‚  â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â”‚
â”‚                                                                     â”‚
â”‚  â”Œâ”€â”€â”€â”€ Garbage Collector (Boehm GC) â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”‚
â”‚  â”‚  - Non-generational, non-compacting                          â”‚  â”‚
â”‚  â”‚  - Stop-the-world khi GC                                     â”‚  â”‚
â”‚  â”‚  - KHÃ”NG di chuyá»ƒn objects â†’ fragmentation theo thá»i gian     â”‚  â”‚
â”‚  â”‚  - Unity 2021+: Incremental GC (chia nhá» GC work)           â”‚  â”‚
â”‚  â”‚    â†’ Má»—i frame GC chá»‰ lÃ m 1-2ms thay vÃ¬ 10-20ms            â”‚  â”‚
â”‚  â”‚    â†’ Váº«n cÃ³ overhead, nhÆ°ng khÃ´ng spike                      â”‚  â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â”‚
â”‚                                                                     â”‚
â”‚  Æ¯u Ä‘iá»ƒm Mono:                                                     â”‚
â”‚  âœ… Iterate Cá»°C NHANH (Save â†’ Play ~2-10s)                        â”‚
â”‚  âœ… Debugging tá»‘t (breakpoints, watches chÃ­nh xÃ¡c)                  â”‚
â”‚  âœ… Reflection Ä‘áº§y Ä‘á»§ (GetType, Activator.CreateInstance)           â”‚
â”‚                                                                     â”‚
â”‚  NhÆ°á»£c Ä‘iá»ƒm Mono:                                                  â”‚
â”‚  âŒ Runtime performance kÃ©m (no SIMD, weak inlining)                â”‚
â”‚  âŒ JIT stutter frame Ä‘áº§u khi method má»›i Ä‘Æ°á»£c gá»i                  â”‚
â”‚  âŒ KhÃ´ng dÃ¹ng Ä‘Æ°á»£c trÃªn iOS (Apple cáº¥m JIT)                       â”‚
â”‚  âŒ Build size lá»›n (kÃ¨m Mono runtime)                               â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 2.2. IL2CPP â€” Ahead-of-Time Compilation

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                      IL2CPP PIPELINE                                â”‚
â”‚                                                                     â”‚
â”‚  Build Process (khi báº¡n báº¥m Build):                                 â”‚
â”‚                                                                     â”‚
â”‚  IL (.dll)                                                          â”‚
â”‚     â”‚                                                               â”‚
â”‚     â–¼                                                               â”‚
â”‚  â”Œâ”€â”€â”€â”€ IL2CPP Transpiler â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”‚
â”‚  â”‚                                                               â”‚  â”‚
â”‚  â”‚  IL â†’ C++ Source Code                                         â”‚  â”‚
â”‚  â”‚                                                               â”‚  â”‚
â”‚  â”‚  VÃ­ dá»¥ chuyá»ƒn Ä‘á»•i:                                            â”‚  â”‚
â”‚  â”‚                                                               â”‚  â”‚
â”‚  â”‚  C# Original:                                                 â”‚  â”‚
â”‚  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”     â”‚  â”‚
â”‚  â”‚  â”‚  public class Enemy {                                â”‚     â”‚  â”‚
â”‚  â”‚  â”‚      public float health = 100f;                     â”‚     â”‚  â”‚
â”‚  â”‚  â”‚      public void TakeDamage(float dmg) {             â”‚     â”‚  â”‚
â”‚  â”‚  â”‚          health -= dmg;                               â”‚     â”‚  â”‚
â”‚  â”‚  â”‚          if (health <= 0) Die();                      â”‚     â”‚  â”‚
â”‚  â”‚  â”‚      }                                                â”‚     â”‚  â”‚
â”‚  â”‚  â”‚  }                                                    â”‚     â”‚  â”‚
â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜     â”‚  â”‚
â”‚  â”‚                         â†“ IL2CPP                               â”‚  â”‚
â”‚  â”‚  C++ Output:                                                  â”‚  â”‚
â”‚  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”     â”‚  â”‚
â”‚  â”‚  â”‚  struct Enemy_t : public RuntimeObject {             â”‚     â”‚  â”‚
â”‚  â”‚  â”‚      float health;    // Public field â†’ direct accessâ”‚     â”‚  â”‚
â”‚  â”‚  â”‚  };                                                  â”‚     â”‚  â”‚
â”‚  â”‚  â”‚                                                      â”‚     â”‚  â”‚
â”‚  â”‚  â”‚  void Enemy_TakeDamage_m1234(                        â”‚     â”‚  â”‚
â”‚  â”‚  â”‚      Enemy_t* __this, float dmg) {                   â”‚     â”‚  â”‚
â”‚  â”‚  â”‚      NullCheck(__this);  // C# null safety            â”‚     â”‚  â”‚
â”‚  â”‚  â”‚      __this->health -= dmg;                           â”‚     â”‚  â”‚
â”‚  â”‚  â”‚      if (__this->health <= 0.0f) {                    â”‚     â”‚  â”‚
â”‚  â”‚  â”‚          Enemy_Die_m5678(__this);                      â”‚     â”‚  â”‚
â”‚  â”‚  â”‚      }                                                â”‚     â”‚  â”‚
â”‚  â”‚  â”‚  }                                                    â”‚     â”‚  â”‚
â”‚  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜     â”‚  â”‚
â”‚  â”‚                                                               â”‚  â”‚
â”‚  â”‚  Äáº·c biá»‡t:                                                   â”‚  â”‚
â”‚  â”‚  - C# class â†’ C++ struct + RuntimeObject header (GC metadata)â”‚  â”‚
â”‚  â”‚  - C# virtual method â†’ C++ vtable lookup                     â”‚  â”‚
â”‚  â”‚  - C# interface â†’ C++ interface table                        â”‚  â”‚
â”‚  â”‚  - GC váº«n hoáº¡t Ä‘á»™ng! (Boehm GC embedded trong IL2CPP runtime)â”‚  â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â”‚
â”‚     â”‚                                                               â”‚
â”‚     â–¼                                                               â”‚
â”‚  â”Œâ”€â”€â”€â”€ Platform C++ Compiler â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”‚
â”‚  â”‚                                                               â”‚  â”‚
â”‚  â”‚  Windows:  MSVC /O2 /GL (Link-Time Optimization)              â”‚  â”‚
â”‚  â”‚  Android:  NDK Clang -O3 -flto                                â”‚  â”‚
â”‚  â”‚  iOS:      Xcode Clang -Os (Size Optimization)                â”‚  â”‚
â”‚  â”‚  WebGL:    Emscripten â†’ WASM                                  â”‚  â”‚
â”‚  â”‚                                                               â”‚  â”‚
â”‚  â”‚  C++ compiler optimizations:                                  â”‚  â”‚
â”‚  â”‚  âœ… Inlining (hÃ m nhá» â†’ paste vÃ o caller)                    â”‚  â”‚
â”‚  â”‚  âœ… Dead Code Elimination (code khÃ´ng dÃ¹ng â†’ xÃ³a)             â”‚  â”‚
â”‚  â”‚  âœ… Loop Unrolling (giáº£m branch overhead)                     â”‚  â”‚
â”‚  â”‚  âœ… Constant Propagation (biáº¿t giÃ¡ trá»‹ â†’ tÃ­nh sáºµn)            â”‚  â”‚
â”‚  â”‚  âœ… Partial SIMD (compiler tá»± vectorize má»™t pháº§n)             â”‚  â”‚
â”‚  â”‚  âœ… LTO (xÃ³a code chÆ°a dÃ¹ng ACROSS all files)                â”‚  â”‚
â”‚  â”‚                                                               â”‚  â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â”‚
â”‚     â”‚                                                               â”‚
â”‚     â–¼                                                               â”‚
â”‚  Native binary (executable/library)                                 â”‚
â”‚                                                                     â”‚
â”‚  â”Œâ”€â”€â”€â”€ Code Stripping â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”‚
â”‚  â”‚  IL2CPP + Linker xÃ³a code KHÃ”NG ÄÆ¯á»¢C Gá»ŒI:                    â”‚  â”‚
â”‚  â”‚  - Unused MonoBehaviours                                      â”‚  â”‚
â”‚  â”‚  - Unused .NET library methods                                â”‚  â”‚
â”‚  â”‚  - Dead code paths                                            â”‚  â”‚
â”‚  â”‚                                                               â”‚  â”‚
â”‚  â”‚  âš  Cáº¢NH BÃO: Náº¿u dÃ¹ng Reflection â†’ code cÃ³ thá»ƒ bá»‹ strip    â”‚  â”‚
â”‚  â”‚  â†’ Cáº§n link.xml Ä‘á»ƒ preserve                                   â”‚  â”‚
â”‚  â”‚  â†’ DOTS SystemAPI.Query trÃ¡nh Ä‘Æ°á»£c váº¥n Ä‘á» nÃ y               â”‚  â”‚
â”‚  â”‚    (vÃ¬ source generators táº¡o direct calls, khÃ´ng reflection) â”‚  â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜  â”‚
â”‚                                                                     â”‚
â”‚  Build time: 5-30 phÃºt (tÃ¹y project size)                           â”‚
â”‚  â†’ ÄÃ¡nh Ä‘á»•i: iteration cháº­m, nhÆ°ng runtime performance cao          â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 2.3. So sÃ¡nh Mono vs IL2CPP â€” Quyáº¿t Ä‘á»‹nh thá»±c tiá»…n

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                    MONO vs IL2CPP                                    â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚                   â”‚ Mono (JIT)           â”‚ IL2CPP (AOT)             â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ Compilation       â”‚ Runtime (JIT)        â”‚ Build time (AOT)         â”‚
â”‚ Build Speed       â”‚ â˜…â˜…â˜…â˜…â˜… (2-10s)       â”‚ â˜…â˜…â˜†â˜†â˜† (5-30 min)        â”‚
â”‚ Runtime Speed     â”‚ â˜…â˜…â˜†â˜†â˜†                â”‚ â˜…â˜…â˜…â˜…â˜†                   â”‚
â”‚ SIMD              â”‚ âŒ KhÃ´ng              â”‚ âš  Háº¡n cháº¿ (auto only)   â”‚
â”‚ GC                â”‚ Boehm                â”‚ Boehm (same!)            â”‚
â”‚ Code Stripping    â”‚ âŒ KhÃ´ng              â”‚ âœ… Aggressive             â”‚
â”‚ Build Size        â”‚ Lá»›n (+Mono runtime)  â”‚ Nhá» hÆ¡n (stripped)       â”‚
â”‚ Debugging         â”‚ â˜…â˜…â˜…â˜…â˜… (nguá»“n C#)    â”‚ â˜…â˜…â˜…â˜†â˜† (C++ stack traces)â”‚
â”‚ Reflection        â”‚ âœ… Äáº§y Ä‘á»§             â”‚ âš  Cáº§n link.xml          â”‚
â”‚ Platform          â”‚ Editor, PC, Mac      â”‚ Táº¤T Cáº¢ (báº¯t buá»™c iOS)  â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ DÃ¹ng khi          â”‚ Development/Editor   â”‚ Production Builds        â”‚
â”‚                   â”‚ Prototype nhanh      â”‚ Ship to players          â”‚
â”‚                   â”‚ Quick testing        â”‚ Performance-critical     â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## 3. DOTS â€” Unity High-Performance Stack

### 3.1. DOTS = 3 Trá»¥ cá»™t

```
DOTS (Data-Oriented Technology Stack):

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                                 â”‚
  â”‚  â”Œâ”€â”€ ECS â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”     â”‚
  â”‚  â”‚  Entity Component System                               â”‚     â”‚
  â”‚  â”‚  â†’ Data layout tá»‘i Æ°u cho Cache (Chapter 2)            â”‚     â”‚
  â”‚  â”‚  â†’ Archetype Chunks: 16 KB contiguous memory           â”‚     â”‚
  â”‚  â”‚  â†’ SOA (Struct of Arrays) thay vÃ¬ AOS                  â”‚     â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜     â”‚
  â”‚                        â”‚                                        â”‚
  â”‚                        â–¼                                        â”‚
  â”‚  â”Œâ”€â”€ Job System â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”     â”‚
  â”‚  â”‚  Multithreaded Execution                               â”‚     â”‚
  â”‚  â”‚  â†’ Chia cÃ´ng viá»‡c cho ALL CPU cores (Chapter 3)        â”‚     â”‚
  â”‚  â”‚  â†’ Safety system: tá»± kiá»ƒm tra race conditions          â”‚     â”‚
  â”‚  â”‚  â†’ Zero locking: Dá»¯ liá»‡u partition theo chunk          â”‚     â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜     â”‚
  â”‚                        â”‚                                        â”‚
  â”‚                        â–¼                                        â”‚
  â”‚  â”Œâ”€â”€ Burst Compiler â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”     â”‚
  â”‚  â”‚  LLVM-based AOT Compiler                               â”‚     â”‚
  â”‚  â”‚  â†’ SIMD auto-vectorization (Chapter 3)                 â”‚     â”‚
  â”‚  â”‚  â†’ Bounds check elimination                            â”‚     â”‚
  â”‚  â”‚  â†’ Aggressive inlining                                 â”‚     â”‚
  â”‚  â”‚  â†’ Platform-specific: SSE/AVX/NEON/WASM-SIMD           â”‚     â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜     â”‚
  â”‚                                                                 â”‚
  â”‚  Káº¿t há»£p: ECS Ã— Jobs Ã— Burst = ÄÃ’N Báº¨Y NHÃ‚N                   â”‚
  â”‚    â†’ Cache efficiency Ã— Thread parallelism Ã— SIMD width         â”‚
  â”‚    â†’ 5Ã— cache Ã— 8Ã— cores Ã— 4-8Ã— SIMD = ~160-320Ã— vs Mono     â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 3.2. ECS Memory Layout â€” Táº¡i sao DOTS nhanh?

```
â•â•â• VÃ­ dá»¥: 10,000 Entities cÃ³ Position + Velocity + Health â•â•â•


MonoBehaviour (AOS â€” Array of Structs):

  Má»—i Enemy object trÃªn Managed Heap:
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚ Object Header â”‚ vtable â”‚ pos.x â”‚ pos.y â”‚ pos.z â”‚ vel.x â”‚  â”‚
  â”‚  16 bytes     â”‚  8B    â”‚  4B   â”‚  4B   â”‚  4B   â”‚  4B   â”‚  â”‚
  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”¤â”€â”€â”€â”€â”€â”€â”€â”€â”¤  â”‚
  â”‚ vel.y â”‚ vel.z â”‚ health â”‚ name_ref â”‚ rb_ref â”‚ anim_ref â”‚  â”‚
  â”‚  4B   â”‚  4B   â”‚  4B    â”‚    8B    â”‚   8B   â”‚    8B    â”‚  â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
  Total: ~80 bytes per enemy (scattered on heap!)

  Äá»ƒ duyá»‡t position:
  â†’ Load 80 bytes nhÆ°ng chá»‰ cáº§n 12 bytes (pos) = 85% lÃ£ng phÃ­!
  â†’ Má»—i enemy á»Ÿ vá»‹ trÃ­ random trÃªn heap â†’ Cache Miss liÃªn tá»¥c


ECS (SOA â€” Struct of Arrays) â€” Archetype Chunk:

  Chunk A (Archetype: Position+Velocity+Health, 16 KB):
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚ Chunk Header: Entity count, Archetype info (256 bytes)       â”‚
  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
  â”‚ Entity IDs:                                                  â”‚
  â”‚ [E0][E1][E2][E3]...[E659]                                   â”‚
  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
  â”‚ Position Data (SOA):                                         â”‚
  â”‚ [pos0.x][pos0.y][pos0.z] [pos1.x][pos1.y][pos1.z] ...      â”‚
  â”‚  12B per entity Ã— 660 entities = 7,920 bytes                â”‚
  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
  â”‚ Velocity Data (SOA):                                         â”‚
  â”‚ [vel0.x][vel0.y][vel0.z] [vel1.x][vel1.y][vel1.z] ...      â”‚
  â”‚  12B per entity Ã— 660 entities = 7,920 bytes                â”‚
  â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
  â”‚ Health Data (SOA):                                           â”‚
  â”‚ [hp0][hp1][hp2][hp3]...[hp659]                               â”‚
  â”‚  4B per entity Ã— 660 entities = 2,640 bytes                  â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
  Total: ~18.7 KB per chunk â‰ˆ 660 entities / chunk

  Äá»ƒ duyá»‡t position:
  â†’ Äá»c liÃªn tá»¥c 7,920 bytes!
  â†’ Cache Line (64B) = ~5 entities â†’ Cache Hit 80%+
  â†’ KHÃ”NG cÃ³ dá»¯ liá»‡u thá»«a â†’ 0% lÃ£ng phÃ­ bandwidth


Sá»‘ liá»‡u thá»±c táº¿ (10,000 entities, position += velocity * dt):

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  MonoBehaviour:                                               â”‚
  â”‚    - 10,000 Ã— virtual call Update() overhead = ~1.5ms        â”‚
  â”‚    - 10,000 Ã— Cache Miss (scattered heap) = ~2.0ms           â”‚
  â”‚    - 10,000 Ã— managedâ†’native transition = ~1.0ms             â”‚
  â”‚    - Scalar math (no SIMD) = ~1.0ms                          â”‚
  â”‚    - Single thread only                                      â”‚
  â”‚    Total: ~5.5ms on 1 core                                   â”‚
  â”‚                                                               â”‚
  â”‚  DOTS (ECS + Burst + Jobs):                                   â”‚
  â”‚    - 0 virtual calls (ISystem direct dispatch)               â”‚
  â”‚    - ~16 chunks Ã— sequential iteration â†’ Cache Hit 95%+      â”‚
  â”‚    - No managedâ†’native (pure Burst) = 0ms overhead           â”‚
  â”‚    - AVX2 SIMD: 8 entities per instruction                   â”‚
  â”‚    - 8 cores parallel (ScheduleParallel)                     â”‚
  â”‚    Total: ~0.04ms on 8 cores                                  â”‚
  â”‚                                                               â”‚
  â”‚    Speedup: 5.5ms / 0.04ms = ~137Ã—                           â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

### 3.3. Burst Compiler â€” Xem mÃ£ mÃ¡y thá»±c táº¿

```
C# Job code:

  [BurstCompile]
  struct MoveJob : IJobParallelFor
  {
      public NativeArray<float3> positions;
      [ReadOnly] public NativeArray<float3> velocities;
      public float deltaTime;
      
      public void Execute(int i)
      {
          positions[i] += velocities[i] * deltaTime;
      }
  }


Burst Inspector output (x86-64, AVX2):

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  ; Burst-generated assembly (simplified)                       â”‚
  â”‚                                                                 â”‚
  â”‚  .loop:                                                         â”‚
  â”‚      vbroadcastss  ymm0, [deltaTime]       ; dt â†’ 8 copies     â”‚
  â”‚                                                                 â”‚
  â”‚      ; Load 8 velocities (x components) â†’ 1 register           â”‚
  â”‚      vmovups       ymm1, [velocities + rax]                     â”‚
  â”‚      ; Load 8 positions  (x components) â†’ 1 register           â”‚
  â”‚      vmovups       ymm2, [positions + rax]                      â”‚
  â”‚                                                                 â”‚
  â”‚      ; position.x += velocity.x * dt (for 8 entities at once!) â”‚
  â”‚      vfmadd231ps   ymm2, ymm1, ymm0                            â”‚
  â”‚      ;   â†‘ Fused Multiply-Add: ymm2 = ymm1 * ymm0 + ymm2      â”‚
  â”‚      ;     1 instruction does both multiply AND add!            â”‚
  â”‚                                                                 â”‚
  â”‚      vmovups       [positions + rax], ymm2  ; Store back        â”‚
  â”‚                                                                 â”‚
  â”‚      ; ... repeat for y, z components                           â”‚
  â”‚                                                                 â”‚
  â”‚      add           rax, 32                  ; Next 8 entities   â”‚
  â”‚      cmp           rax, rcx                 ; Loop bound        â”‚
  â”‚      jl            .loop                                        â”‚
  â”‚                                                                 â”‚
  â”‚  ; Total per iteration of 8 entities:                           â”‚
  â”‚  ;   - 3 loads (pos x,y,z)                                     â”‚
  â”‚  ;   - 3 loads (vel x,y,z)                                     â”‚
  â”‚  ;   - 3 FMA  (multiply + add)                                 â”‚
  â”‚  ;   - 3 stores (pos x,y,z)                                    â”‚
  â”‚  ;   = 12 instructions for 8 entities = 1.5 inst/entity!       â”‚
  â”‚  ;                                                              â”‚
  â”‚  ;   Mono would need ~12-15 instructions PER entity.            â”‚
  â”‚  ;   â†’ Burst: 8Ã— fewer instructions (SIMD width alone)         â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


CÃ¡ch má»Ÿ Burst Inspector trong Unity:
  Jobs â†’ Burst â†’ Open Inspector
  â†’ Chá»n Job hoáº·c System
  â†’ Tab "Assembly" â†’ xem mÃ£ mÃ¡y thá»±c táº¿
  â†’ Tab "Summary" â†’ xem safety checks, SIMD width
  â†’ CÃ”NG Cá»¤ MÃƒ Máº NH NHáº¤T Ä‘á»ƒ hiá»ƒu code Ä‘ang cháº¡y tháº¿ nÃ o!
```

### 3.4. Job System â€” PhÃ¢n chia cÃ´ng viá»‡c cho nhiá»u cores

```
VÃ­ dá»¥: IJobParallelFor chia 10,000 entities cho 8 cores:

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                                â”‚
  â”‚  Main Thread:                                                  â”‚
  â”‚    var job = new MoveJob { ... };                               â”‚
  â”‚    var handle = job.ScheduleParallel(10000, 64, dependency);   â”‚
  â”‚    //                                           â†‘               â”‚
  â”‚    //                               Batch Size = 64 entities   â”‚
  â”‚    //                           (má»—i "work item" xá»­ lÃ½ 64)    â”‚
  â”‚                                                                â”‚
  â”‚  Job System tá»± chia:                                           â”‚
  â”‚    10,000 Ã· 64 = 157 work items (batches)                     â”‚
  â”‚    ÄÆ°a 157 items vÃ o Work Stealing Queue                      â”‚
  â”‚                                                                â”‚
  â”‚  Worker Threads (7 threads + main thread):                     â”‚
  â”‚                                                                â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”                  â”‚
  â”‚  â”‚Core 0  â”‚ â”‚Core 1  â”‚ â”‚Core 2  â”‚ â”‚Core 3  â”‚                  â”‚
  â”‚  â”‚Batch   â”‚ â”‚Batch   â”‚ â”‚Batch   â”‚ â”‚Batch   â”‚                  â”‚
  â”‚  â”‚0-19    â”‚ â”‚20-39   â”‚ â”‚40-59   â”‚ â”‚60-79   â”‚                  â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”€â”€â”€â”€â”˜                  â”‚
  â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â” â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”                  â”‚
  â”‚  â”‚Core 4  â”‚ â”‚Core 5  â”‚ â”‚Core 6  â”‚ â”‚Core 7  â”‚                  â”‚
  â”‚  â”‚Batch   â”‚ â”‚Batch   â”‚ â”‚Batch   â”‚ â”‚Batch   â”‚                  â”‚
  â”‚  â”‚80-99   â”‚ â”‚100-119 â”‚ â”‚120-139 â”‚ â”‚140-156 â”‚                  â”‚
  â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”€â”€â”€â”€â”˜ â””â”€â”€â”€â”€â”€â”€â”€â”€â”˜                  â”‚
  â”‚                                                                â”‚
  â”‚  Work Stealing:                                                â”‚
  â”‚    Core 3 xong sá»›m â†’ "Äƒn trá»™m" batch tá»« Core 7 (cháº­m nháº¥t)  â”‚
  â”‚    â†’ Táº¥t cáº£ cores LUÃ”N Báº¬N â†’ hiá»‡u quáº£ tá»‘i Ä‘a!                â”‚
  â”‚                                                                â”‚
  â”‚  Safety System:                                                â”‚
  â”‚    - NativeArray cÃ³ safety handle â†’ detect race conditions     â”‚
  â”‚    - [ReadOnly] tag â†’ nhiá»u Jobs Ä‘á»c song song                â”‚
  â”‚    - KhÃ´ng [ReadOnly] â†’ exclusive access, enforce sequential   â”‚
  â”‚    - Safety checks = Editor only â†’ zero cost in build         â”‚
  â”‚                                                                â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## 4. Tá»•ng káº¿t â€” HÃ nh trÃ¬nh tá»« Transistor Ä‘áº¿n 1 Frame trong Unity

```
â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
  HÃ€NH TRÃŒNH Cá»¦A 1 FRAME GAME â€” Tá»ª ELECTRON Äáº¾N PIXEL
â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•

Báº¡n nháº¥n nÃºt di chuyá»ƒn nhÃ¢n váº­t. Trong 16.67ms (60 FPS), Ä‘iá»u gÃ¬ xáº£y ra?


  â”Œâ”€â”€ Táº¦NG 1: Váº¬T LÃ (Chapter 1) â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                                  â”‚
  â”‚  âš¡ Transistors (hÃ ng Tá»¶ trÃªn chip CPU + GPU)                    â”‚
  â”‚     â†’ ÄÃ³ng/Má»Ÿ theo tÃ­n hiá»‡u Ä‘iá»‡n Ã¡p (0V = 0, 3.3V = 1)        â”‚
  â”‚     â†’ Táº¡o thÃ nh Logic Gates (AND, OR, NOT, XOR)                 â”‚
  â”‚     â†’ Gates káº¿t há»£p â†’ ALU (phÃ©p cá»™ng, trá»«, so sÃ¡nh)            â”‚
  â”‚     â†’ ALU + Registers + Control Unit = CPU Core                 â”‚
  â”‚                                                                  â”‚
  â”‚  Táº¥t cáº£ diá»…n ra á»Ÿ tá»‘c Ä‘á»™ 5 GHz = 5 tá»· láº§n Ä‘Ã³ng/má»Ÿ má»—i giÃ¢y   â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                                    â”‚
                                    â–¼
  â”Œâ”€â”€ Táº¦NG 2: Bá»˜ NHá»š (Chapter 2) â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                                  â”‚
  â”‚  ðŸ“¦ Dá»¯ liá»‡u game (positions, velocities, health) náº±m trong:     â”‚
  â”‚     NativeArray<float3> â†’ Unmanaged Heap â†’ DDR5 RAM             â”‚
  â”‚                                                                  â”‚
  â”‚  Khi CPU Ä‘á»c position[0]:                                       â”‚
  â”‚     RAM (100ns) â†’ L3 (10ns) â†’ L2 (3ns) â†’ L1 (1ns) â†’ Register  â”‚
  â”‚     + Táº£i nguyÃªn Cache Line 64 bytes                            â”‚
  â”‚     â†’ positions[1..4] miá»…n phÃ­ (ECS contiguous layout!)         â”‚
  â”‚                                                                  â”‚
  â”‚  Archetype Chunk 16KB â†’ vá»«a váº·n trong L1 Cache (32-64 KB)      â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                                    â”‚
                                    â–¼
  â”Œâ”€â”€ Táº¦NG 3: CPU EXECUTION (Chapter 3) â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                                  â”‚
  â”‚  ðŸ”§ Burst Compiler Ä‘Ã£ compile C# MoveJob â†’ x86-64 native code   â”‚
  â”‚     â†’ Sá»­ dá»¥ng AVX2 registers (YMM0-YMM15): 256-bit wide        â”‚
  â”‚     â†’ VFMADD231PS: pos += vel Ã— dt cho 8 entities/instruction   â”‚
  â”‚     â†’ Pipeline 20+ stages, Out-of-Order execution               â”‚
  â”‚     â†’ No branches trong tight loop â†’ Pipeline khÃ´ng bá»‹ flush    â”‚
  â”‚                                                                  â”‚
  â”‚  Job System phÃ¢n chia:                                           â”‚
  â”‚     10,000 entities Ã· 8 cores Ã— 8 SIMD =                        â”‚
  â”‚     ~156 iterations per core â†’ hoÃ n thÃ nh trong ~0.04ms          â”‚
  â”‚                                                                  â”‚
  â”‚  Song song: CPU cÅ©ng cháº¡y AI, Physics, Audio trÃªn cÃ¡c cores     â”‚
  â”‚  khÃ¡c hoáº·c trong cÃ¡c Jobs khÃ¡c                                   â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                                    â”‚
                                    â–¼
  â”Œâ”€â”€ Táº¦NG 4: GPU RENDERING (Chapter 4) â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                                  â”‚
  â”‚  ðŸŽ¨ CPU submit Command Buffer â†’ GPU qua PCIe/shared memory      â”‚
  â”‚                                                                  â”‚
  â”‚  GPU Pipeline:                                                   â”‚
  â”‚  â‘  Vertex Shader:                                                â”‚
  â”‚     â†’ 500K vertices Ã— MVP matrix transform                      â”‚
  â”‚     â†’ 46 SM Ã— 128 cores = 5,888 vertices Ä‘á»“ng thá»i             â”‚
  â”‚                                                                  â”‚
  â”‚  â‘¡ Rasterizer:                                                   â”‚
  â”‚     â†’ Tam giÃ¡c â†’ Fragments (Fixed-function hardware)             â”‚
  â”‚     â†’ Barycentric interpolation cho UV, Normal                   â”‚
  â”‚                                                                  â”‚
  â”‚  â‘¢ Fragment Shader:                                              â”‚
  â”‚     â†’ PBR Lighting: Cook-Torrance BRDF                           â”‚
  â”‚     â†’ 4M fragments Ã— (albedo + normal + roughness + shadow)      â”‚
  â”‚     â†’ SIMT: 1 Warp = 32 pixels cÃ¹ng lÃºc                         â”‚
  â”‚     â†’ Branchless: step(), lerp() thay if/else                   â”‚
  â”‚     â†’ Half precision (16-bit) cho mobile bandwidth               â”‚
  â”‚                                                                  â”‚
  â”‚  â‘£ Post-Processing:                                              â”‚
  â”‚     â†’ Bloom + Tonemapping + FXAA                                 â”‚
  â”‚     â†’ Fullscreen passes trÃªn Compute Shaders                     â”‚
  â”‚                                                                  â”‚
  â”‚  Tá»•ng GPU time: ~6-8ms                                           â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                                    â”‚
                                    â–¼
  â”Œâ”€â”€ Táº¦NG 5: UNITY ENGINE (Chapter 5) â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                                                                  â”‚
  â”‚  ðŸŽ® Unity Runtime orchestrates:                                  â”‚
  â”‚                                                                  â”‚
  â”‚  C++ Backend:                                                    â”‚
  â”‚     â†’ SRP Core submit draw calls                                â”‚
  â”‚     â†’ PhysX collisions resolved                                 â”‚
  â”‚     â†’ Memory allocators manage pools                             â”‚
  â”‚                                                                  â”‚
  â”‚  C# Frontend (IL2CPP / Burst):                                  â”‚
  â”‚     â†’ Game logic â†’ IL â†’ C++ â†’ Native (IL2CPP)                   â”‚
  â”‚     â†’ DOTS Jobs â†’ IL â†’ LLVM â†’ SIMD Native (Burst)               â”‚
  â”‚     â†’ Zero GC: NativeArrays + struct components                  â”‚
  â”‚                                                                  â”‚
  â”‚  Frame complete: Framebuffer â†’ V-Sync â†’ Display                  â”‚
  â”‚  Total: CPU ~4ms + GPU ~8ms = 12ms â†’ 83 FPS âœ…                   â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


â•â•â• CHUá»–I LOGIC DUY NHáº¤T â•â•â•

  Electron â†’ Transistor â†’ Logic Gate â†’ ALU â†’ CPU Core
       â†’ Cache â†’ RAM â†’ Assembly â†’ C++ â†’ C# â†’ IL â†’ Burst/IL2CPP
            â†’ Native SIMD code â†’ Multi-core Jobs â†’ ECS Chunks
                 â†’ Command Buffer â†’ GPU Pipeline â†’ Pixels
                      â†’ Display â†’ Máº®T NGÆ¯á»œI (60 láº§n/giÃ¢y)

  ToÃ n bá»™ chuá»—i nÃ y â€” tá»« electron Ä‘Ã³ng/má»Ÿ transistor
  Ä‘áº¿n pixel sÃ¡ng trÃªn mÃ n hÃ¬nh â€” diá»…n ra trong

                    â˜… 16.67 MILLISECONDS â˜…

  Tá»©c lÃ  16.67 PHáº¦N NGHÃŒN cá»§a 1 giÃ¢y.
  Nhanh hÆ¡n 1 cÃ¡i chá»›p máº¯t (300-400ms) khoáº£ng 20 láº§n.
```

---

## 5. Báº£ng tá»•ng há»£p â€” Quick Reference

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚       UNITY DEVELOPER â€” HARDWARE KNOWLEDGE QUICK REFERENCE          â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ KhÃ¡i niá»‡m         â”‚ áº¢nh hÆ°á»Ÿng thá»±c táº¿ trong Unity                   â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚ Cache Line 64B    â”‚ ECS Chunks: data liÃªn tá»¥c â†’ Cache Hit 95%+      â”‚
â”‚ Branch Prediction â”‚ math.select() thay if/else trong Burst Jobs     â”‚
â”‚ SIMD (AVX2)       â”‚ Burst auto-vectorize: 8 entities/instruction    â”‚
â”‚ Pipeline Stall    â”‚ Avoid data dependency chains trong tight loops   â”‚
â”‚ False Sharing     â”‚ Má»—i Job nÃªn cÃ³ read/write set riÃªng biá»‡t       â”‚
â”‚ GC Stop-the-World â”‚ Zero alloc: NativeArray, struct, object pool    â”‚
â”‚ Branch Divergence â”‚ Branchless shader: step(), lerp(), smoothstep() â”‚
â”‚ Bandwidth (GPU)   â”‚ Tex compression (ASTC), half precision, LODs    â”‚
â”‚ Draw Calls        â”‚ SRP Batcher + GPU Instancing + Indirect         â”‚
â”‚ TBR (Mobile)      â”‚ Minimize render passes, MSAA free trÃªn mobile   â”‚
â”‚ Managedâ†”Native    â”‚ Cache GetComponent á»Ÿ Awake, prefer DOTS queries â”‚
â”‚ IL2CPP vs Mono    â”‚ Dev=Mono, Build=IL2CPP, HotPath=Burst           â”‚
â”‚ Occupancy (GPU)   â”‚ Giáº£m register pressure, shader Ä‘Æ¡n giáº£n hÆ¡n    â”‚
â”‚ Memory Hierarchy  â”‚ Allocator.Temp < TempJob < Persistent            â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

> **Káº¿t:** Hiá»ƒu pháº§n cá»©ng khÃ´ng pháº£i Ä‘á»ƒ trá»Ÿ thÃ nh ká»¹ sÆ° chip. MÃ  Ä‘á»ƒ khi báº¡n viáº¿t `position += velocity * deltaTime`, báº¡n biáº¿t chÃ­nh xÃ¡c:
> - **Dá»¯ liá»‡u náº±m á»Ÿ Ä‘Ã¢u** (Register? L1 Cache? RAM? VRAM?)
> - **CÃ¢u lá»‡nh cháº¡y tháº¿ nÃ o** (Scalar hay SIMD? Pipelined hay stalled?)
> - **Táº¡i sao cÃ¡ch nÃ y nhanh hÆ¡n cÃ¡ch kia** (Cache locality? No branching? Parallelism?)
>
> ÄÃ³ lÃ  sá»± khÃ¡c biá»‡t giá»¯a **viáº¿t code cháº¡y Ä‘Æ°á»£c** vÃ  **viáº¿t code cháº¡y NHANH**.

---
*Chapter 5 (Final) â€” NghiÃªn cá»©u cho Unity High-Performance Agent*
