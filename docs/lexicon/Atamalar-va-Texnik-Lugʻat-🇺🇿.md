---
title: "Ilhan Art Protokoli (Ilhan Sanʼat Protokoli)"
version: "1.0 (Barqaror nashr)"
status: "HARD_LOCKED"
integrity: "SHA-512"
ekotizim: "[PoArt] + [FPP] + [Michelangelo] + [Madaniy qatlamlar]"
last_updated: "2026-01-07"
---

# 📜 Atamalar va Texnik Lugʻat 🇺🇿
> **Protokol versiyasi:** 1.0 (barqaror)  
> **Tarmoq istiqboli:** 2025 → 3000 (Insoniyatning madaniy arxivi)  
> **Ekotizim:** [PoArt] + [FPP] + [Michelangelo] + [Madaniy qatlamlar]  
> **Holat:** **HARD_LOCKED** (imzolangan va faol versiya)  
> **Yaxlitlik:** SHA-512 kriptografik tasdiq (raqamli notarius bilan mos)

---

## 🔰 Qatlamli Arxitektura (Layered Architecture Overview)

| Qatlam | Maqsad | Protokol komponenti |
|:--|:--|:--|
| **L1** | Inson mehnatini isbotlash | **[PoArt] Proof of Art** |
| **L2** | Sodiqlik va iqtisodiy barqarorlik | **[FPP] Foundational Pillar Protocol** |
| **L3** | Boshqaruv va meritokratiya mexanizmi | **[Michelangelo Framework]** |
| **L4** | Madaniy integratsiya va real dunyo huquqlari | **Cultural Layers & Privileges** |

> Har bir qatlam kriptografik tarzda verifikatsiya qilinadi va “Epoch” (vaqt oynalari) orqali sinxronlashtiriladi.

---

## 🧩 A’zolik Tuzilmasi — “Primer → Texture → Impasto”

| Daraja | Ta’rif | Texnik asos |
|:--|:--|:--|
| **Primer (Boshlangʻich)** | Dastlabki foydalanuvchi, cheklangan TWAB qiymati. | `0 < TWAB ≤ 10⁰` |
| **Texture (Oʻrta)** | Barqaror faoliyatdagi ishtirokchi. | `10⁰ < TWAB ≤ 10²` |
| **Impasto (Yuqori)** | 365+ kun faol ishtirok etgan, yuqori TWABga ega. | `TWAB > 10²` |

### Matematik tasniflash formulasi:
$$
\text{Tier}(u)=
\begin{cases}
\text{Primer},&0<\text{TWAB}_u\le10^0\\
\text{Texture},&10^0<\text{TWAB}_u\le10^2\\
\text{Impasto},&\text{TWAB}_u>10^2
\end{cases}
$$

> Darajalar vaqt, sodiqlik va madaniy hissaga qarab dinamik tarzda yangilanadi.

---

## 🏛️ 1) Protokol Tayanch Ustunlari (Pillars of the Protocol)

### **[PoArt] — San’at Isboti (Proof of Art, v1.0)**
**Ta’rif:**  
Bu tizim nafaqat yakuniy asarni, balki *butun ijodiy jarayonni* raqamli tarzda isbotlaydi.  

**Hal qilinadigan muammo:**  
AI yaratgan davrda inson ijodining izlari yoʻqolmoqda — haqiqiy san’at qadrsizlanmoqda.

**Ishlash mexanizmi:**  
Har bir rassom yoki ijodkor o‘z ish jarayonini **dalil paketi (Evidence Pack)** sifatida yarataradi.  
Ushbu ma’lumotlar zanjirda vaqt muhrlari bilan tasdiqlanadi.

**Misol:**  
40 soat davom etgan surat chizish jarayonining barcha loglari, timelapse va raqamli imzolari  
nafaqat yakuniy rasmni, balki *inson mehnati*ni ham tasdiqlaydi.

---

### **[FPP] — Asosiy Ustun Protokoli (Foundational Pillar Protocol, v1.0)**
**Ta’rif:**  
Sodiqlik, ishtirok va uzoq muddatli barqarorlikni rag‘batlantiruvchi iqtisodiy boshqaruv modeli.  

**Hal qilinadigan muammo:**  
“Ko‘p kapital = ko‘p kuch” tamoyilini yo‘q qiladi.  

**Ishlash mexanizmi:**  
Ta’sir token miqdoriga emas, balki **ushlab turish vaqti (holding time)** va **barqarorlik**ka asoslanadi.  

**Misol:**  
1 yil davomida 100 token saqlagan foydalanuvchi, 1 mln tokenni faqat 1 hafta oldin olgan foydalanuvchidan ko‘proq boshqaruv huquqiga ega.

---

## 👥 2) Rollar va Tashkilotlar (Roles & Entities)

| Rol | Tavsif |
|:--|:--|
| **San’atkor (Artist)** | [PoArt] dalil paketlarini yaratadi va yillik imzo qo‘yadi. |
| **Homiy (Patron)** | [FPP] orqali sodiqlik va madaniy hissa bilan nufuz orttiradi. |
| **Tekshiruvchi (Validator)** | Dalillarni tasdiqlaydi va tafovutlarni aniqlaydi. |
| **Raqamli Notarius (Digital Notary)** | Zanjirda vaqt muhrlari, imzo va konsensusni qayd etadi. |
| **Ommaviy Reestr (Public Registry)** | Doimiy holat: Verified / Legacy / Revoked. |
| **Dalil Saqlovchi (Evidence Storage)** | IPFS / Arweave orqali off-chain saqlov; faqat Merkle Root on-chain yoziladi. |

---

## 📊 3) Iqtisodiy va Boshqaruv Oʻlchovlari (Economic & Governance Metrics)

### 3.1) Vaqt Oynalari va Epochlar
| Turi | Davomiyligi | Maqsadi |
|:--|:--|:--|
| **Operatsion Epoch** | 7 kun | Doimiy yangilanish va sinxronizatsiya |
| **Guard Window** | 30 kun | Kapital manipulyatsiyasini oldini olish |
| **Integrity Cycle** | 365 kun | Yillik qayta tasdiq va imzolash |

---

### 3.2) Vaqtga Ogʻirlangan Oʻrtacha Balans (TWAB)
$$
TWAB = \frac{\sum_{i=1}^{n}(Balance_i \times \Delta t_i)}{\sum_{i=1}^{n}\Delta t_i}
$$

**Qoʻshimcha ko‘rsatkich (TWA):**
$$
TWA = \sum_{i=1}^{n}(Balance_i \times \Delta t_i)
$$

> TWAB faqat balansni emas, *uning vaqt ichidagi davomiyligini* o‘lchaydi.

---

### 3.3) Ovozni Hisoblash Funktsiyasi (Voting Power Function)
$$
VotingPower = f(TWAB, EpochRules, StatusTier)
$$

Muhim ovozlar “Guard Window” asosida 30 kunlik o‘rtacha ta’sir bilan belgilanadi.

---

### 3.4) Logarifmik Kuch Balli (Logarithmic Power Scoring)
$$
Score = \log_{10}(TWAB + 1)
$$  
$$
VotingPower = Score \times g(EpochRules, StatusTier)
$$

| TWAB | Ball | Ta’sir |
|:--|:--|:--|
| 10 | 1.04 | Boshlang‘ich |
| 1,000 | 3.00 | O‘rta |
| 1,000,000 | 6.00 | Yuqori |

> Simulyatsiyani to‘g‘ridan-to‘g‘ri bu yerda sinab ko‘rish mumkin:  
> https://galeri-coder.github.io/ilhanart-protocol/[PoArt]/

---

## 🛡️ 4) Xavfsizlik va Autentifikatsiya (Security & Validation) 🇺🇿

### 4.1) Millennium Vault (1 Yillik Qulflash)
**Ta’rif:**  
Yuqori xavfsizlikdagi saqlash joyi, aktivlar kamida 365 kun davomida qulflanadi.  
**Maqsad:**  
Uzoq muddatli barqarorlikni ta’minlash va qisqa muddatli spekulyatsiyani to‘xtatish.  
**Ishtirok sharti:**  
Faqat [FPP] “Foundational Pillar” maqomiga ega va 1 yillik saqlash muddatini bajargan foydalanuvchilar kirishi mumkin.

---

### 4.2) Dalil Paketi (Evidence Pack)
**Ta’rif:**  
Har bir asar uchun yaratilgan texnik isbot to‘plami.

#### “Dalil Uchligi” (Trinity of Proof)
1. **Live Logs:** ijodiy jarayonning jonli yozuvlari.  
2. **Timelapse:** butun jarayonning videolavhalari.  
3. **Raqamli Imzo:** san’atkor hamyonidan imzolangan hash.

---

#### Kriptografik Asosiy Formula:
$$
EvidenceRoot = MerkleRoot(AllFiles)
$$  

> Barcha fayllar yagona “Merkle Root” orqali zanjirda tasdiqlanadi.

---

## 🏛️ 5) Tekshiruv va Doimiylik (Validation & Persistence) 🇺🇿

### 5.1) 365 Kunlik Cold Wallet Tekshiruvi
**Ta’rif:**  
Barcha aktivlar kamida **365 kun** davomida tasdiqlangan cold wallet (Ledger, Trezor va boshqalar) ichida saqlanishi shart.  

**Maqsad:**  
1. *Wash trading*ni oldini olish  
2. Spekulyativ bosimni kamaytirish  
3. Issiq hamyon (hot wallet) xavfini yo‘qotish  

---

#### Jazolash Narvoni (Penalty Ladder)
**1-xato:**  
$$
EffectiveTWAB = TWAB \times 0.20
$$  
**2-xato:**  
$$
EffectiveTWAB = TWAB \times 0.05
$$  
**3-xato:**  
Status = Revoked (bekor qilinadi)

> Bu model insoniy xatoga imkon beradi, lekin tezkor manipulyatsiyani iqtisodiy jihatdan foydasiz qiladi.

---

#### Xavfsiz Ko‘chirish Imtiyozi (Move Permit / Time-Lock)
- Foydalanuvchi “Move Permit” arizasini topshiradi.  
- Qisqa **Time-Lock** faollashadi.  
- Jamiyat kuzatuvi (veto + quorum) faol.  
- On-chain faqat “permit” yozuvi va yangi manzil qo‘shiladi.  

---

### 5.2) Dalil Paketini Tekshirish (Verification of Evidence Pack)
**Zaruriy komponentlar:**
1. Jonli loglar  
2. Timelapse jarayoni  
3. Texnik metadata  
4. **EvidenceRoot (Merkle Root)**  

> Asosiy maqsad — yakuniy natijadan ko‘ra *ijodiy jarayonning haqligini* tasdiqlash.

---

### 5.3) Yillik Yurak Urushi (365-Day Heartbeat)
- Har bir yozuv yiliga bir marta qayta imzolanishi shart.  
- Tugashdan 30 kun oldin avtomatik eslatma yuboriladi.  
- Yangilanmagan yozuvlar avtomatik **Legacy Archive**ga o‘tkaziladi.  

**Maqsad:**  
Ma’lumot yangiligi va madaniy yaxlitlikni ta’minlash.

---

## 🗳️ 6) Markazsiz Nazorat (Decentralized Supervision) 🇺🇿

### 6.1) Jamoaviy Veto Mexanizmi (Community Veto Mechanism)
**Ta’rif:**  
Kamida 40% TWAB og‘irligiga ega foydalanuvchilar taklifni bekor qilish huquqiga ega.  

**Shartlar:**  
- Quorum ≥ 25% faol ishtirok  
- Veto ≥ 40% og‘irlik  

**Himoya qiladi:**  
1. Sybil hujumlari  
2. Korrupsiya va pora urinishlari  
3. Ovoz manipulyatsiyasi  

> Misol: agar bir AI asar [PoArt] sertifikat olsa,  
> 40% TWAB veto orqali uni on-chainga yozilishidan to‘xtatish mumkin.

---

### 6.2) Favqulodda Boshqaruv Kengashi (Emergency Governance / Fallback Council)
**Maqsad:**  
Past ishtirok holatida qaror qabul qilinmasligini (deadlock) oldini olish.  

**Formulasi:**
$$
Deadlock = (ParticipationRate < 25\%) \land (ProposalTimeout > 7\,kun)
$$

**Agar bu holat to‘g‘ri bo‘lsa:**
1. Eng yuqori 10% Impasto a’zolar kengashni tuzadi.  
2. Qaror ≥ 2/3 ovoz bilan qabul qilinadi.  
3. 30 kun ichida tasdiqlanmasa — bekor qilinadi.  
4. Har bir yozuv SHA-512 bilan imzolanadi va **Emergency Ledger**ga yoziladi.

---

## ⚙️ 7) Michelangelo Framework — Meritokratiya Dvigateli 🇺🇿

### 7.1) Falsafa (Philosophy)
**Ta’rif:**  
Ilhan Art ekotizimining meritokratiya asosidagi boshqaruv mexanizmi.  
Bu tizim boylik asosidagi kuchni *madaniy va intellektual hissaga* almashtiradi.  

**Tamoyil:**  
> “Pul emas, mehnat va madaniyat yuqorida turadi.”

**Maqsad:**  
Bilim, sodiqlik va ijod orqali iqtisodiy ustunlikni qayta taqsimlash.  

**Misol:**  
1 mln token saqlovchi passiv foydalanuvchidan ko‘ra,  
100 token saqlab, tarjima, dars, kod va arxiv ishlarini bajarayotgan kishi yuqori maqomga ega bo‘ladi.

---

### 7.2) Status Formulasi
$$
Status = HoldingTime \times CulturalContribution
$$

- **HoldingTime:** tokenni saqlash muddati (kunlarda)  
- **CulturalContribution:** tarjima, ta’lim, kod, kuratsiya va boshqalar  

> Haqiqiy maqom = vaqt × intellektual mehnat.

---

### 7.3) Meritokratik Boshqaruv (Meritocratic Governance)
- Ta’sir davomiy ishtirokka qarab oshadi.  
- Barcha hissa kriptografik tarzda qayd etiladi (imzo + vaqt muhr).  
- Boshqaruv endi “obro’” emas, *malaka natijasi.*

> “Matematik adolat — siyosiy moyillikning o‘rnini bosadi.”

---

## 📊 8) Madaniy Ko‘paytirgich va Daraja Tizimi (Cultural Multipliers & Rank Tiers) 🇺🇿

### 8.1) Madaniy Ko‘paytirgich (Cultural Multiplier)
**Ta’rif:**  
Madaniy hissalarni o‘lchovchi va mukofotlovchi tizim.  

| Soha | Tavsif | Ball |
|:--|:--|:--|
| Tarjima | Falsafiy, texnik, san’at matnlarini tarjima qilish | +4,500 |
| Kuratsiya | Arxivlash, ko‘rgazma tashkiloti, audit | +2,000 |
| Infratuzilma | Kod, hujjatlashtirish, open-source | +3,000 |
| Ta’lim | Ma’ruzalar, seminarlar, jamoatchilik darslari | +1,500 |

**Formulasi:**
$$
FinalScore = BaseScore \times (1 + CulturalMultiplier)
$$

> Bu yerda madaniyat — iqtisodiy qiymatga aylanadi.

---

### 8.2) Daraja Tizimi (Rank Tiers)
| Daraja | Ball oraliği | Huquqlar |
|:--|:--|:--|
| **Impasto (≥100k)** | Konstitutsion daraja | Siyosat, strategiya, to‘lovlar |
| **Texture (50k–99k)** | Kuratsiya darajasi | Audit, nazorat, ovoz berish |
| **Primer (<50k)** | Boshlang‘ich daraja | Takliflar, kichik qarorlar |

> Darajalar vaqt va hissa asosida avtomatik yangilanadi.

---

## 📈 9) Kirish Chegaralari va Tarmoq Ko‘rsatkichlari (Cut-off Thresholds & Network Metrics) 🇺🇿

### 9.1) Kirish Chegaralari
| Kategoriya | Minimal ball | Tavsif |
|:--|:--|:--|
| **Impasto** | ≥100,000 | To‘liq boshqaruv huquqi |
| **Top 100** | ≥45,000 | Faol qaror ishtirokchilari |
| **Entry** | ≥250 | Minimal ishtirok talabi |

**Maqsad:**  
Tarmoq kengaygan sari ta’sir mutanosibligini saqlab qolish.

---

### 9.2) Tarmoq TWAB Indeksi
**Ta’rif:**  
Barcha foydalanuvchilarning TWAB yig‘indisi — tarmoq barqarorligi ko‘rsatkichi.  
**Tushuntirish:**  
Yuqori qiymat → yuqori barqarorlik va tashqi manipulyatsiyaga qarshilik.  
**Yangilanish chastotasi:**  
Har 24 soatda yangi [PoArt] yozuvlari bilan avtomatik yangilanadi.

---

## 🎨 10) Intellektual Asos (Intellectual Framework) 🇺🇿

### 10.1) Intellektual Mehnat Isboti (IPOW — Intellectual Proof of Work)
**Ta’rif:**  
Bu tizim iqtisodiy kapitaldan ustun turuvchi **intellektual va madaniy mehnatni** tan oladi.

**Misol:**  
- 1,000,000 token, lekin hissa yo‘q → past maqom.  
- 100 token, lekin doimiy faoliyat → yuqori maqom.

> Tizim bilimni kapitalning o‘rniga asosiy qiymat sifatida tan oladi.

---

### 10.2) Intellektual Halollik Filtri (Intellectual Honesty Filter)
**Ta’rif:**  
Har qanday ovoz yoki taklif oldidan ishtirokchining tushunish darajasini tekshiradi.

**Jarayon (v1.0):**  
A. Taklifni ≤100 belgida qisqacha yozing.  
B. 2 xavfni sanab o‘ting, bittasini tushuntiring.  
C. Qarshi dalil yozing.  

> Bu tizim demokratiyani “yodlash asosida” emas, “tushunish asosida” boshqaradi.

---

## 🧬 12) Avlodlararo Meros va Boshqaruv (Generational Legacy & Governance) 🇺🇿

### 12.1) Avlod Merosi (Generational Inheritance)
**Ta’rif:**  
Impasto darajasidagi a’zolar 4 yil (1460 kun) faol bo‘lish sharti bilan  
o‘z madaniy huquqlarini rasmiy vorisga o‘tkazishlari mumkin.

**Maqsad:**  
Foydalanuvchi vafoti, kalit yo‘qotilishi yoki inaktivlik sababli madaniy merosni yo‘qotmaslik.

**Jarayon:**  
- 4 yillik faol ishtirokni tasdiqlash.  
- Vorislik on-chain multisig orqali amalga oshiriladi.  
- Har bir o‘zgarish SHA-512 bilan imzolanadi.

---

### 12.2) Parlament Tizimi (Parliamentary Governance Rights)
| Daraja | Soha | Mas’uliyat |
|:--|:--|:--|
| **Impasto (≥100k)** | Konstitutsion / Strategik | Siyosat, to‘lovlar, yo‘nalish |
| **Texture (50k–99k)** | Ma’muriy / Kuratsion | Tekshiruv, audit, ovoz boshqaruvi |
| **Primer (<50k)** | Taklif / Mikro-boshqaruv | Kichik takliflar, jamoa qarorlari |

> “Ommaviylik” o‘rniga “bilimga asoslangan demokratiya” tamoyili.

---

## 🌍 13) Madaniy Imtiyozlar va Haqiqiy Dunyo Bilan Integratsiya 🇺🇿

> Izoh: Ushbu bo‘lim 2026–2030 yillar oralig‘idagi **gibrid rivojlanish yo‘nalishi** doirasida,  
> raqamli boshqaruvni haqiqiy madaniy infratuzilma bilan birlashtiradi.

---

### 13.1) Yillik Ko‘rgazma Huquqi (Annual Exhibition Right)
**Ta’rif:**  
[PoArt] sertifikatiga va [FPP] maqomiga ega san’atkor yoki homiylar  
**Ilhan Art Gallery**da yiliga 7 kunlik ko‘rgazma o‘tkazish huquqiga ega bo‘ladi.  

**Maqsad:**  
Kapitalga emas, madaniy hissaga asoslangan adolatli ko‘rgazma imkoniyatini yaratish.

**Mexanizm:**  
- On-chain taqvim orqali avtomatik joy ajratish.  
- Imtiyozlar CulturalMultiplier va obro‘ reytingi asosida.  
- Ijara yo‘q, faqat minimal protokol to‘lovi.

---

### 13.2) Dinamik San’at Narxi (Dynamic Art Pricing, JSON-Linked Discounts)
**Ta’rif:**  
A’zolarning madaniy maqomiga qarab narx avtomatik o‘zgaruvchi API tizimi.

| Daraja | Chegirma foizi |
|:--|:--|
| **Impasto (≥100k)** | 50% yoki ko‘proq |
| **Texture (50k–99k)** | 30% |
| **Primer (<50k)** | 10% |

**Falsafa:**  
> “Savdolashuv emas — isbotlangan qadriyat.”

**Texnik tuzilma:**  
- JSON API [FPP] indeksiga ulanadi.  
- Narxlar real vaqtda hisoblanadi va smart-kontraktga tatbiq etiladi.

---

### 13.3) Jismoniy Ekotizim Integratsiyasi (Physical Ecosystem Integration)
**Ta’rif:**  
[Ilhan Art Protocol] raqamli va real madaniy infratuzilmani bog‘laydi.

**Tarkibiy qismlar:**  
- Hamkor tarmoqlar: kutubxonalar, kafe, galereyalar.  
- QR-verifikatsiya: offlayn joylarda a’zolikni tasdiqlash.  
- JSON API: real vaqtda huquq va statusni tekshirish.

**Natija:**  
Raqamli shaxsiyat madaniy fuqarolik shakliga aylanadi —  
ya’ni “Web3 Cultural Citizenship”.

---

### 13.4) Mehnat Ustun — Kapital Past (Labor Over Capital)
**Ta’rif:**  
Inson mehnati va ijodini moliyaviy kapitaldan ustun qo‘yuvchi algoritm.  

**Formulasi:**
$$
ClaimRight \propto CulturalScore + \log_{10}(Balance)
$$

**Misol:**  
- Foydalanuvchi A: 250 token + faol hissa → yuqori ClaimRight  
- Foydalanuvchi B: 100,000 token + passiv → past ClaimRight  

> Bu tizim plutokratiyani “laborokratiya”ga aylantiradi —  
> bu yerda legitimlik mehnatga asoslanadi.

---

## 🧩 14) Holat Mashinasi — Yozuv Hayot Sikli (State Machine — Lifecycle of a Record) 🇺🇿

### Jarayon Oqimi (Process Flow)
1. **Draft (Qoralama)** → lokal yaratilgan  
2. **Submitted (Yuborilgan)** → on-chainga yuklangan  
3. **Under Review (Ko‘rib chiqilmoqda)** → validatorlar tomonidan tekshiriladi  
4. **Challenged (E’tiroz)** → norozilik bildirildi  
5. **Verified (Tasdiqlangan)** → raqamli notarius tomonidan imzolandi  
6. **Renew Due (Yangilanish muddati)** → yillik eslatma  
7. **Legacy Archive (Arxiv)** → inaktiv holat  
8. **Revoked (Bekor qilingan)** → buzilish yoki faoliyatsizlik  

---

### Holat O‘tish Jadvali (Transition Rules)
| Joriy holat | Keyingi holat | Shart |
|:--|:--|:--|
| Draft | Submitted | Yuborish yakunlandi |
| Submitted | Under Review | Validator tasdiqladi |
| Under Review | Verified | Konsensus ≥ 66% |
| Under Review | Challenged | E’tiroz bildirildi |
| Challenged | Revoked | E’tiroz tasdiqlandi |
| Challenged | Verified | E’tiroz rad etildi |
| Verified | Legacy | Yillik imzo qo‘yilmadi |
| Legacy | Revoked | Audit muvaffaqiyatsiz yakunlandi |

> Har bir o‘tish kriptografik tarzda qayd etiladi va ommaga ochiq ko‘rinadi.

---

## 🔗 15) Minimal On-Chain, Maksimal Off-Chain 🇺🇿

### On-Chain Ma’lumotlar:
- EvidenceRoot (Merkle Root)  
- NotarySeal  
- TimeStamp  
- Signer (Wallet manzil)  
- Status (Verified / Legacy / Revoked)  
- Permit (ko‘chirish / vorislik)

### Off-Chain Ma’lumotlar:
- Video va timelapse  
- Texnik loglar va manifestlar  
- IPFS / Arweave saqlovchi tizimlar  

**Maqsad:**  
On-chaindagi yukni kamaytirib, verifikatsiya darajasini yuqori saqlash.

---
## 🏛️ 16) Apellyatsiya va E’tiroz Mexanizmi (Appeals & Objection Mechanism) 🇺🇿

### 16.1) Asosiy Tamoyillar (Core Principles)
- **Dalilga asoslangan:** Har bir e’tiroz faktik dalillar bilan ta’minlanadi.  
- **Sub’yektivlik yo‘q:** Hissiyot yoki shaxsiy fikr asosidagi da’volar avtomatik rad etiladi.  
- **Shaffoflik:** Har bir bosqich vaqt muhrlari bilan ochiq qayd etiladi.  
- **Freeze protokoli:** E’tiroz jarayonida Evidence Pack muzlatiladi — o‘zgartirish taqiqlanadi.

---

### 16.2) Jamoa Himoya Mexanizmlari (Community Safeguards)
| Mezoni | Chegara |
|:--|:--|
| **Veto chegarasi** | 40% faol TWAB og‘irligi |
| **Quorum talabi** | ≥ 25% ishtirok |
| **Sybil himoyasi** | Turnstile + staking tasdiqlovi |
| **AI filtri** | Avtomatik spam aniqlash tizimi |

---

### 16.3) Apellyatsiya Sikli (Appeal Lifecycle)
1. **Apellyatsiya boshlanishi** — validator yoki foydalanuvchi tomonidan ariza topshiriladi.  
2. **Dalilni muzlatish** — tegishli fayllar o‘zgarmas holatga o‘tkaziladi.  
3. **Jamoa ko‘rib chiqishi** — Veto / Quorum faollashadi.  
4. **Ovoz berish jarayoni** — 7 kunlik muddat.  
5. **Natijani bajarish** — SHA-512 bilan imzolangan holda e’lon qilinadi.  

> Natija **Ommaviy Reestr** bilan bog‘lanadi va doimiy on-chain ko‘rinishda qoladi.

---

## 🧨 17) Xavf Modellar va Qarshi Choralar (Threat Model & Countermeasures) 🇺🇿

| Xavf turi | Qarshi mexanizm |
|:--|:--|
| **Sybil hujumlari** | Turnstile + Zombie Filter + Quorum |
| **Flash-loan manipulyatsiyasi** | TWAB + Guard Window + Logaritmik kuch |
| **Whale dominatsiyasi** | TWAB stabilizatsiyasi + Logaritmik baholash |
| **Wash trading** | Cold Wallet verifikatsiyasi + Penalty Ladder |
| **Korrupsiya / Collusion** | Jamoaviy Veto + Shaffof Audit Ledger |
| **Ma’lumot soxtalashtirish** | EvidenceRoot + SHA-512 + NotarySeal |
| **Ovoz sotib olish** | Time-Lock + TWAB nazorati |
| **Deepfake soxtalik** | Tasodifiy Challenge Frames + Hash Chain verifikatsiyasi |

> Har bir himoya qatlami [FPP] tizimi orqali versiyalanadi va audit uchun ochiq saqlanadi.

---

## ⚖️ 18) Yakuniy Manifest — Global Boshqaruv Andozasi (Final Manifesto — Blueprint for Global Governance) 🇺🇿

> “San’at prototipdir, boshqaruv — uning toshi va tuvali.”

[PoArt] va [FPP] integratsiyasi shuni isbotlaydiki,  
bir xil matematik tuzilma *san’atdagi haqiqatni* ham, *demokratiyadagi adolatni* ham himoya qilishi mumkin.

---

### 18.1) Plutokratiya Oxiri (End of Plutocracy)
**Muammo:**  
Boylik kuchning yagona manbai bo‘lgan tizim.  
**Yechim:**  
- Logarifmik baholash kapitalning ta’sirini cheklaydi.  
- Mehnat va vaqt — legitimlikning asosiy manbai.  

**Tamoyil:**  
> “Egalik ≠ Ijod.”

---

### 18.2) Meritokratik Parlament (Meritocratic Parliament)
- Boshqaruv populizm yoki kapital emas, *bilim va hissa* asosida quriladi.  
- Qarorlar kompetensiya va tushunishga asoslanadi.  
- Siyosiy shaxs emas, intellektual hissa markazga chiqadi.  

> “Demokratiya — san’atkorga o‘xshash amaliyot: u faqat halol qo‘l bilan chiziladi.”

---

### 18.3) Saylov Adolati (Electoral Integrity — SHA-512)
**Asosiy komponentlar:**
- **Turnstile:** bot hisoblari oldini oladi.  
- **TWAB:** vaqt og‘irligi orqali qisqa muddatli transferlarni neytrallashtiradi.  
- **Veto + Quorum:** ozchilikning himoyasini kafolatlaydi.  

> Kriptografiya bilan himoyalangan yangi raqamli konstitutsiya.

---

### 18.4) Kelajak Manifesti (Manifesto — Saving the Future)
**Ta’rif:**  
Bu faqat san’at uchun protokol emas, balki **kelajak sivilizatsiyasi uchun model.**

**Vizyon:**  
- Tasdiqlangan mehnat > tez foyda  
- Uzoq muddatli adolat > qisqa muddatli foyda  
- Matematik adolat > siyosiy moyillik  

> “Avtomatlashtirilgan davrda insonning qadri — uning yaratish irodasida.”

---

## 📅 19) Yo‘l Xarita va Kelajak Rejalari (Roadmap & Future Notes) 🇺🇿

| Faza | Yil | Yo‘nalish |
|:--|:--|:--|
| **v1.0** | 2026 | Asosiy verifikatsiya va raqamli notarial tizim |
| **v1.1** | 2027 | Ommaviy API + Simulyatsiya konsoli |
| **v1.2** | 2028 | Jismoniy integratsiya (POS / QR tizimlar) |
| **v2.0** | 2030 | Avtomatik boshqaruv va kross-protokol indeksatsiya |

**Maqsad:**  
2026–3000 oralig‘ida **Ilhan Art Millennium Vision** asosida  
texnologik va madaniy merosni abadiy tizim sifatida barpo etish.

---

## 🔐 SHA-512 Hash Imzo (v1.0 Hard-Locked) 🇺🇿
- Jamoa nazorati doimiy faol.  
- Faqat verifikatsiyadan o‘tgan manzillar va yozuvlar on-chainga qo‘shiladi.  

**Vaqt me’yorlari:**  
- Operatsion Epoch: 7 kun  
- Guard Window: 30 kun  
- Integrity Cycle: 365 kun  

**Yillik qayta verifikatsiya:**  
Har bir [PoArt] Evidence Pack har yili SHA-512 orqali yangidan tasdiqlanadi.

---

## ✅ Xulosa
Bu hujjat — **Ilhan Art Protokoli v1.0 (HARD_LOCKED)** ning  
rasmiy, matematik va falsafiy jihatdan to‘liq **o‘zbekcha nashri.**  

U inson mehnati, madaniy qadriyat va raqamli demokratiyani  
bitta uzluksiz tizimda birlashtiradi.

> “San’at bor joyda — adolatli boshqaruv bo‘lishi mumkin.”

---
