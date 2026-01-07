# 📜 Terminologi & Glosari Teknik 🇸🇬

> **Versi Protokol:** 1.0 (Stabil)  
> **Visi Rangkaian:** 2025 → 3000 Arkib  
> **Ekosistem:** [PoArt] + [FPP] + [Michelangelo] + [Lapisan Budaya]  
> **Status:** **HARD_LOCKED** (Dokumentasi Aktif)  
> **Integriti:** SHA-512 Dimeterai (Serasi dengan Notari Digital)

---

## 🔰 Gambaran Umum Seni Bina Berlapis

| Lapisan | Tujuan | Protokol |
|:--|:--|:--|
| **L1** | Pengesahan usaha | **PoArt (Proof of Art)** |
| **L2** | Kesetiaan / ekonomi | **FPP (Foundational Pillar Protocol)** |
| **L3** | Tadbir urus | **Rangka Kerja Michelangelo (Enjin Meritokrasi)** |
| **L4** | Integrasi budaya | **Lapisan & Keistimewaan Budaya** |

Struktur ini merangkumkan keseluruhan kesatuan teknikal dan falsafah ekosistem dalam empat lapisan asas.  
Pengguna baharu boleh memahami seni bina keseluruhan ini dalam masa **2 minit** melalui jadual ini.

---

## 🧩 Tahap Keahlian — “Primer → Texture → Impasto”

| Tahap | Definisi | Asas Teknikal |
|:--|:--|:--|
| **Primer (Asas)** | Tahap permulaan. Telah melengkapkan pengesahan asas tetapi belum mengumpul geseran masa (TWAB). | `0 < TWAB ≤ 10⁰` |
| **Texture (Tekstur)** | Ahli aktif yang telah mengumpul baki dari masa ke masa. | `10⁰ < TWAB ≤ 10²` |
| **Impasto (Lapisan Tebal)** | Ahli teras dengan skor TWAB tertinggi, mengekalkan kitaran selama 365 hari. | `TWAB > 10²` |

### Formula Tahap

$$
\text{Tier}(u)=
\begin{cases}
\text{Primer},&0<\text{TWAB}_u\le10^0\\
\text{Texture},&10^0<\text{TWAB}_u\le10^2\\
\text{Impasto},&\text{TWAB}_u>10^2
\end{cases}
$$

---

## 📑 Kandungan

1. Tiang Protokol (Pillars of the Protocol)  
2. Peranan & Entiti (Roles & Entities)  
3. Metrik Ekonomi & Tadbir Urus (Economic & Governance Metrics)  
4. Keselamatan & Pengesahan (Security & Validation)  
5. Pengesahan & Ketekalan (Validation & Persistence)  
6. Penyeliaan Terdesentralisasi (Decentralized Supervision)  
7. Rangka Kerja Michelangelo (Meritocracy Engine)  
8. Pengganda Budaya & Tahap Kedudukan (Cultural Multipliers & Ranking Levels)  
9. Ambang & Metrik Rangkaian (Cut-off Thresholds & Network Metrics)  
10. Rangka Kerja Intelektual (Intellectual Framework)  
11. Rintangan Sybil Lanjutan (Advanced Sybil Resistance)  
12. Warisan Generasi & Tadbir Urus (Generational Legacy & Governance)  
13. Lapisan Keistimewaan Budaya & Integrasi Dunia Sebenar (Cultural Privilege Layers & Real-World Integration)  
14. Mesin Keadaan (State Machine)  
15. Minimum On-chain / Maksimum Off-chain (Model Rantaian Minimum / Luar Maksimum)  
16. Mekanisme Rayuan & Kepercayaan (Appeals / Mercii & Itiraz Mechanism)  
17. Model Ancaman (Threat Model & Counter Layers)  
18. Kata Akhir: Pelan Induk Tadbir Urus Global (Manifesto)  
19. Peta Jalan & Nota Masa Depan (Roadmap & Future Notes)

---

## 🏛️ 1) Tiang Protokol (Pillars of the Protocol)

### **[PoArt] Proof of Art (v1.0)**

* **Definisi:** Protokol utama yang mengesahkan bukan sahaja hasil akhir karya seni tetapi juga seluruh proses penciptaan menggunakan data teknikal.  
* **Masalah yang Diselesaikan:** Dengan peningkatan alat AI generatif, bukti usaha manusia dalam ruang digital menjadi sukar dibuktikan — menjadikan nilai seni jatuh.  
* **Cara Ia Berfungsi:** Semasa artis berkarya, mereka menyerahkan **Pek Bukti (Evidence Pack)** yang merangkumi setiap peringkat. Protokol menandakan data ini pada blockchain dengan cap masa.  
* **Contoh:** Jika seorang artis melukis selama 40 jam, log penstriman, rakaman timelapse, dan cap jari digital akan disahkan oleh [PoArt]. Ia bukan hanya "lukisan siap" tetapi "40 jam tenaga manusia" yang diarkibkan.

---

### **[FPP] Foundational Pillar Protocol (v1.0)**

* **Definisi:** Sistem utama yang membina tiang ekonomi, tadbir urus, dan sosial ekosistem — memberi ganjaran kepada kesetiaan dan penyertaan jangka panjang.  
* **Masalah yang Diselesaikan:** Menghapuskan ketidakadilan dalam ekosistem kripto di mana "siapa ada duit, dia berkuasa" dan menghalang spekulator daripada merosakkan sistem.  
* **Cara Ia Berfungsi:** Kuasa undian dan tadbir urus pengguna ditentukan oleh berapa lama mereka menyimpan aset, bukan hanya jumlahnya.  
* **Contoh:** “Ikan paus” dengan 1 juta token yang baru masuk mempunyai kuasa lebih rendah daripada ahli yang setia dengan 100 token selama setahun.

---

## 👥 2) Peranan & Entiti (Roles & Entities)

Protokol ini menetapkan dengan jelas “siapa boleh buat apa” untuk mengurangkan salah faham dan penyalahgunaan.

- **Artis:** Menghasilkan Evidence Pack untuk [PoArt], memulakan pendaftaran dan menandatangani denyut tahunan (heartbeat).  
- **Patron (Penyokong):** Mendapat status dalam [FPP] berdasarkan kesetiaan dan sumbangan; mempunyai kuasa dalam veto dan pengawasan.  
- **Validator (Pengesah Komuniti):** Menyemak Evidence Pack, menandakan percanggahan, dan menyertai proses veto/appeal.  
- **Notari Digital:** Mengesahkan bukti + konsensus + cap masa dan mengukuhkannya ke dalam Public Registry.  
- **Public Registry (Daftar Awam):** Lapisan identiti kekal bagi semua rekod yang disahkan (Verified/Legacy/Revoked).  
- **Penyimpanan Bukti (IPFS/Arweave/Arkib):** Menyimpan data mentah di luar rantaian; hanya akar kriptografi ditulis ke blockchain.

---

## 📊 3) Metrik Ekonomi & Tadbir Urus (Economic & Governance Metrics)

Bahagian ini mentakrifkan model matematik dan sekatan masa yang memastikan kestabilan ekonomi serta keadilan dalam tadbir urus.  
Tujuannya ialah mengekang pengaruh modal besar jangka pendek melalui **geseran masa** sambil menjadikan kesetiaan jangka panjang boleh diukur dan diaudit.

---

### 3.1) Tetingkap Masa (Time Windows) dan Takrif Epoch

Dalam protokol ini, masa tidak hanya ditakrifkan oleh satu “epoch” tetapi oleh **tiga tetingkap berbeza**, setiap satu mempunyai tujuan tertentu.

#### 3.1.1) Epoch Operasi (Operational Epoch)
Kitaran asas untuk laporan, log, dan kemas kini rutin.

- **Default:** **7 Hari**  
- **Fungsi:** Kemas kini berkala dan pelaporan.

#### 3.1.2) Tetingkap Perlindungan Undian Kritikal (Critical Vote Guard Window)
Menentukan tempoh sejarah yang diambil kira semasa mengira kuasa undian.

- **Lookback:** **30 Hari**  
- **Fungsi:** Menghalang pembelian undian secara tiba-tiba sebelum pengundian kritikal.

> **Peraturan:** Dalam undian kritikal, pengiraan kuasa undian menggunakan **30 hari Lookback**, bukan **7 hari Epoch Operasi**.

#### 3.1.3) Kitaran Integriti (Integrity Cycle)
- **Tempoh:** **365 Hari**  
- **Fungsi:** Pembaharuan tahunan melalui pengesahan Evidence Pack.  
> **Nota Kekal v1.0:** Parameter 7 & 30 hari dikodkan secara kekal (hard-coded).

---

### 3.2) TWAB (Time-Weighted Average Balance)

TWAB ialah metrik utama yang mengukur **kesetiaan** dan **kestabilan** sesebuah dompet dalam ekosistem.

$$
\text{TWAB}=\frac{\sum_{i=1}^{n}(\text{Baki}_i\times\Delta t_i)}{\sum_{i=1}^{n}\Delta t_i}
$$

$\Delta t_i$ mewakili tempoh masa baki itu dipegang.

**Opsyen Metrik Kasar:**

$$
\text{TWA}=\sum_{i=1}^{n}(\text{Baki}_i\times\Delta t_i)
$$

---

### 3.3) Kuasa Undian (Voting Power)

$$
\text{VotingPower}=f(\text{TWAB},\text{EpochRules},\text{StatusTier})
$$

**Kesan Guard Window:** Dalam undian kritikal, 30 hari lookback digunakan.

---

### 3.4) Skor Logaritma (Logarithmic Power Scoring)

$$
\text{Score}=\log_{10}(\text{TWAB}+1)
$$

$$
\text{VotingPower}=\text{Score}\times g(\text{EpochRules},\text{StatusTier})
$$

| Baki (TWAB) | Skor ($\log_{10}$) | Analisis Kuasa |
|:--|:--|:--|
| 10 | 1.04 | Tahap pengaruh awal |
| 1,000 | 3.00 | 100× peningkatan baki ≈ 3 skor |
| 1,000,000 | 6.00 | 100,000× peningkatan ≈ 6 skor |

> **Simulasi:**  
> Untuk melihat simulasi kuasa undian logaritma, lawati [PoArt Simulation Console](https://galeri-coder.github.io/ilhanart-protocol/[PoArt]/).

---

### 3.5) Keserasian FPP v1.0

- **Epoch Operasi:** 7 Hari  
- **Guard Window:** 30 Hari  
- **Kitaran Integriti:** 365 Hari  

Semakan tahunan wajib dilakukan melalui Evidence Pack.

---

## 🛡️ 4) Keselamatan & Pengesahan (Security & Validation)

### 4.1) Vault Milenium (Millennium Vault, Epoch 10 Tahun)

* **Definisi:** Aset dikunci dalam tempoh 1 tahun (epoch), menjadi peti reputasi tertinggi dalam sistem.  
* **Masalah Diselesaikan:** Perlindungan terhadap spekulasi jangka pendek yang merosakkan visi jangka panjang.  
* **Jawapan:** Hanya mereka yang mengunci aset selama ≥1 tahun dan mempunyai status “Pillar” boleh membuat keputusan kritikal.

---

### 4.2) Pek Bukti (Evidence Pack)

**Definisi:**  
Set data teknikal wajib untuk pengesahan oleh [PoArt].

#### Kandungan Wajib (Triniti Bukti)
1. **Log Langsung:** Rekod siaran langsung semasa proses penciptaan.  
2. **Timelapse Proses:** Rakaman video dari awal hingga akhir.  
3. **Cap Jari Digital:** Hash ditandatangani oleh dompet artis.

---

#### Pengukuhan v1.0 (Lapisan Integriti Rantaian)

Triniti sahaja tidak mencukupi; hubungan antara fail mesti dimeterai juga:

4. **Manifest Tangkap:**  
   Data kamera/peranti, resolusi, kadar bingkai, senarai fail, dan checksum.

5. **Merkle Root / Rantaian Hash:**  

$$
\text{EvidenceRoot} = \text{MerkleRoot}(\text{AllFiles})
$$

6. **Frame Cabaran Rawak (Pilihan):**  
   Ujian manusia rawak semasa siaran langsung.  
   Contoh: menunjukkan objek khas atau menulis perkataan tertentu.  
   Ini meningkatkan kos serangan AI/deepfake.

---

**Masalah Diselesaikan:**  
Memberi jawapan teknikal muktamad kepada soalan: *“Adakah karya ini benar-benar dibuat oleh manusia?”*

---

### 4.3) Perlindungan Sybil & Flash-loan

* **Definisi:** Perlindungan matematik terhadap akaun bot dan serangan pinjaman segera.  
* **Jawapan:** TWAB + Guard Window dalam [FPP] menjadikan gerakan modal jangka pendek tidak relevan secara tadbir urus.

---

### 4.4) Notari Digital (Digital Notary: Meterai Protokol)

* **Definisi:** Mekanisme kendiri yang mengesahkan data [PoArt] dan [FPP], kemudian memeterai hasilnya ke dalam **Daftar Awam**.

### Masalah yang Diselesaikan

1. **Autoriti Pusat & Bias:** Menghapuskan keperluan persetujuan subjektif.  
2. **Manipulasi Data:** Rekod yang disahkan tidak boleh diubah semula.  
3. **Gatekeeping:** Akses artis ke arkib global berdasarkan bukti, bukan citarasa.

### Kitaran Pengesahan (Penapis Tiga)

- **Kelengkapan Evidence Pack:** Triniti + Manifest + EvidenceRoot  
- **Penyeliaan Demokratik:** Veto / Quorum  
- **Tandatangan Kriptografik:** Pengesahan SHA-512

### Meterai Matematik

$$
\text{NotarySeal}=\text{Hash}(\text{EvidenceRoot}+\text{VoterConsensus}+\text{TimeStamp})
$$

### Hasil (2026–3000)
Karya yang mendapat meterai notari menjadi sebahagian daripada warisan budaya manusia sejagat.

---

## 🏛️ 5) Pengesahan & Ketekalan (Validation & Persistence)

### 5.1) Pengesahan 365 Hari Dompet Sejuk (Cold Wallet)

**Definisi:**  
Aset disimpan secara berterusan dalam dompet sejuk selama **365 hari**.

**Masalah yang Diselesaikan:**
1. Dagangan palsu (Wash Trading)  
2. Tekanan spekulatif  
3. Risiko keselamatan dompet panas  

---

#### Kemas Kini v1.0: “Penalty Ladder” menggantikan “Hard Reset”

Menetapkan semula sepenuhnya dengan satu pemindahan terlalu keras, maka sistem v1.0 memperkenalkan penalti bertingkat:

**Pelanggaran 1 (pemindahan sebelum 365 hari):**

$$
\text{EffectiveTWAB} = \text{TWAB} \times 0.20
$$

**Pelanggaran 2:**

$$
\text{EffectiveTWAB} = \text{TWAB} \times 0.05
$$

**Pelanggaran 3:**  
Status menjadi **Revoked** (dibatalkan).

> Tangga penalti ini menghalang manipulasi keluar masuk pantas tanpa menghukum pengguna sejati secara berlebihan.

---

## 🗳️ 6) Penyeliaan Terdesentralisasi (Decentralized Supervision)

### 6.1) Mekanisme Veto Komuniti (Ambang 40%)

* **Definisi:** Sistem demokratik yang membolehkan minoriti berkualiti menghentikan pendaftaran atau perubahan protokol baharu.

#### Kemas Kini v1.0: “Quorum + Veto” Kunci Berganda

- **Kuorum (Penyertaan Minimum):** Sekurang-kurangnya **25%** kuasa undian aktif mesti menyertai.  
- **Ambang Veto:** Veto hanya sah apabila mencapai **40% daripada jumlah kuasa aktif.**

**Masalah yang Diselesaikan:**
1. Serangan Sybil  
2. Rasuah undi dan kolusi  
3. Pembelian undi besar-besaran  

* **Contoh:** Jika karya AI dihantar sebagai “manusia sebenar”, komuniti boleh menggunakan veto 40% untuk menghalang pengesahan karya tersebut secara kekal.

---

### 6.2) Tadbir Urus Kecemasan / Majlis Fallback

**Tujuan:** Mengelakkan kebuntuan keputusan apabila penyertaan rendah.

**Definisi:**

$$
\text{Deadlock}=(\text{ParticipationRate}<25\%)\land(\text{ProposalTimeout}>7\text{ days})
$$

Apabila `Deadlock = TRUE`:

1. **Majlis Fallback** (10% ahli tertinggi Impasto) diberi kuasa sementara.  
2. Keputusan dibuat dengan `Council Consensus ≥ ⅔`.  
3. Jika tidak disahkan melalui referendum komuniti dalam 30 hari, keputusan dibatalkan secara automatik.  
4. Semua keputusan dimeterai dengan hash SHA-512 pada **Lejar Kecemasan**.

---

## ⚙️ 7) Rangka Kerja Michelangelo (Meritocracy Engine)

### 7.1) Falsafah Michelangelo

* **Definisi:** Enjin reputasi dan kedudukan ekosistem Ilhan Art.  
* **Slogan:** *“Anda tidak boleh membeli jalan ke puncak.”*  
* **Contoh:** Paus dengan jutaan token tidak akan mengatasi seseorang yang telah memberi sumbangan budaya selama bertahun-tahun.

---

### 7.2) Formula Status: Masa × Sumbangan

$$
\text{Status}=\text{HoldingTime}\times\text{CulturalContribution}
$$

* **HoldingTime:** Bilangan hari aset disimpan dalam dompet sejuk tanpa gangguan.  
* **CulturalContribution:** Sumbangan nyata seperti terjemahan, kurasi, pameran, atau pembangunan.  
* **Masalah yang Diselesaikan:** Menghapuskan “pemegang pasif” yang tidak menyumbang kepada komuniti.

---

## 📊 8) Pengganda Budaya & Tahap Kedudukan (Cultural Multipliers & Ranking Levels)

### 8.1) Pengganda Budaya (Cultural Multiplier)

* **Definisi:** Sistem ganjaran bonus tambahan untuk sumbangan budaya.  
* **Aplikasi:**
  - **Impasto (JP/TR/EN):** Terjemahan teks saintifik/falsafah/seni (+4,500 mata contoh)  
  - **Texture:** Kawalan kualiti pendaftaran & penyertaan veto  
  - **Infrastruktur:** Sumbangan kod, dokumentasi, sokongan indeks  

* **Contoh:** 1000 hari pegangan + satu terjemahan besar boleh mengatasi ribuan pengguna lain.

---

### 8.2) Tahap Kedudukan (Ranking Levels)

| Kedudukan | Julat / Mata | Peranan & Kuasa |
|:--|:--|:--|
| **Impasto (≥100k)** | Peringkat Perlembagaan | Menentukan strategi dan yuran jangka panjang |
| **Texture (50k–99k)** | Peringkat Kuratorial | Menyelia, mengundi, dan menyusun kandungan |
| **Primer (<50k)** | Peringkat Ahli | Menyertai cadangan kecil dan undian asas |

> Kedudukan dikemas kini secara dinamik mengikut aktiviti dan kestabilan sumbangan dalam [FPP].

---

## 📈 9) Ambang & Metrik Rangkaian (Cut-off Thresholds & Network Metrics)

### 9.1) Ambang Kemasukan (Entry Thresholds)

Ambang ditetapkan apabila sistem mencapai kestabilan.

- **Ambang Impasto:** **≥ 100,000 Mata**  
- **Kemasukan 100 Teratas:** **≥ 45,000 Mata**

* **Masalah yang Diselesaikan:** Mengekalkan kualiti sistem dengan mengelak limpahan peserta tanpa sumbangan sebenar.

---

### 9.2) TWAB Rangkaian (Network TWAB)

* **Definisi:** Kapasiti TWAB keseluruhan ekosistem (contohnya: 4.2M Network TWAB).  
* **Fungsi:** Semakin tinggi nilai ini, semakin sukar sistem dimanipulasi.  
* **Kemasukan 24 Jam:** Jumlah pendaftaran [PoArt] baharu dalam 24 jam terakhir.

---

## 🎨 10) Rangka Kerja Intelektual (Intellectual Framework)

### 10.1) IPOW: Bukti Kerja Intelektual (Intellectual Proof of Work)

* **Definisi:** Enjin reputasi yang memberi ganjaran berdasarkan sumbangan intelektual seperti seni, pendidikan, dan terjemahan — bukan semata-mata pegangan aset.  
* **Masalah yang Diselesaikan:** Mengatasi budaya staking pasif.  
* **Contoh:** Dompet dengan 1 juta token tetapi tanpa sumbangan intelektual akan dinilai lebih rendah daripada pengguna dengan 100 token yang menyumbang secara aktif.

---

### 10.2) Penapis Kejujuran Intelektual (Intellectual Honesty Filter)

* **Definisi:** Tahap pengesahan yang menilai sama ada pengguna benar-benar memahami topik sebelum mengundi.  
* **Masalah yang Diselesaikan:** Undian buta, spam AI, dan manipulasi automatik.

#### Kemas Kini v1.0: Bukti Pemahaman

Daripada kuiz klasik, sistem meminta pengguna menunjukkan pemahaman sebenar:

**Pilihan A (Ringkasan):** Ringkaskan cadangan dalam 100 perkataan.  
**Pilihan B (Analisis Risiko):** Tandakan dua risiko dan jelaskan satu sebab.  
**Pilihan C (Bantahan):** Sediakan alasan jika tidak bersetuju.  

Modul ini menguji pemahaman sebenar dan menghalang automasi bot.

---

## 🛡️ 11) Rintangan Sybil Lanjutan (Advanced Sybil Resistance)

### 11.1) Mekanisme Turnstile

* **Definisi:** Ambang penyertaan minimum (contohnya: 250 ILHAN Token).  
* **Falsafah:** “Bukan tembok, tetapi pintu berpusing.”  
* **Masalah yang Diselesaikan:** Menyekat ribuan akaun palsu yang dicipta secara automatik.  
* **Contoh:** Serangan 10,000 akaun bot menjadi tidak ekonomik kerana setiap akaun mesti menyimpan 250 token.

---

### 11.2) Penapis Dompet Zombie (Zombie Wallet Filter)

* **Definisi:** Keperluan aktiviti berkala bagi membuktikan bahawa dompet masih aktif.  
* **Peraturan:** Dompet tidak aktif dikeluarkan daripada Daftar Global walaupun skor tinggi.  
* **Matlamat:** Mengekalkan sistem yang terdiri daripada pengguna sebenar yang hidup dan menyumbang.

---

## 🧬 12) Warisan Generasi & Tadbir Urus (Generational Legacy & Governance)

* **Definisi:** Pemindahan reputasi dan hak kepada waris bagi ahli Impasto yang mengekalkan statusnya dalam jangka panjang.  
* **Masalah yang Diselesaikan:** Menjamin nilai budaya tidak hilang apabila seseorang meninggal dunia.  
* **Pelaksanaan:** Skrin warisan dibuka kepada mereka yang membuktikan kesetiaan ≥4 tahun dan dimeterai secara on-chain.

---

### 12.2) Hak Tadbir Urus Parlimen (Parliamentary Governance Rights)

| Tahap | Julat | Hak & Fungsi |
|:--|:--|:--|
| **Impasto (≥100k)** | Perlembagaan | Dasar, strategi, yuran |
| **Texture (50k–99k)** | Kuratorial | Kurasi, pengawasan, undian |
| **Primer (<50k)** | Asas | Cadangan kecil & keputusan minor |

* **Masalah yang Diselesaikan:** Menggantikan demokrasi rawak dengan sistem meritokrasi berasaskan kelayakan.

---
## 🌍 13) Lapisan Keistimewaan Budaya & Integrasi Dunia Sebenar  
(Cultural Privilege Layers & Real-World Integration)

> **Nota:** Keistimewaan berikut akan dilaksanakan secara berperingkat antara tahun 2026–2030 sebagai sebahagian daripada "Peta Jalan Masa Depan".

---

### 13.1) Hak Pameran Tahunan (The Annual Exhibition Right)

* **Definisi:** Hak tahunan kepada artis/patron yang disahkan oleh [PoArt] untuk mempamerkan karya mereka di Ilhan Art Gallery selama 1 minggu setiap tahun.  
* **Masalah yang Diselesaikan:** Kos tinggi bagi artis bebas untuk mengakses ruang fizikal.  
* **Pelaksanaan:** Peserta yang mencapai ambang kelayakan boleh menempah tarikh melalui kalendar dan menggunakan ruang berdasarkan mata reputasi budaya mereka.

---

### 13.2) Harga Seni Dinamik (Dynamic Art Pricing)

* **Definisi:** Sistem API yang menentukan kadar diskaun berdasarkan status budaya pengguna.  
* **Struktur:**  
  - **Impasto (≥100k)** → Diskaun 50%+  
  - **Texture (50k–99k)** → Diskaun 30%  
  - **Primer (<50k)** → Diskaun 10%  
* **Falsafah:** “Tiada rundingan — hanya nilai usaha yang menentukan harga.”  
* **Matlamat:** Menggalakkan keadilan melalui ketelusan algoritma dan penghargaan budaya.

---

### 13.3) Integrasi Ekosistem Fizikal (Physical Ecosystem Integration)

- Kedai buku, kafe, pusat budaya  
- Kod QR untuk pengesahan status & penebusan kod  

---

### 13.4) Tenaga Kerja Mengatasi Modal (Labor Over Capital: Meritocratic Access)

* **Definisi:** Keistimewaan sebenar tidak bergantung pada jumlah modal, tetapi pada **sumbangan budaya dan kestabilan masa**.  

**Model Matematik:**

$$
\text{ClaimRight} \propto \text{CulturalScore} + \log_{10}(\text{Balance})
$$

Maksudnya, hak seseorang meningkat seiring dengan sumbangan budaya mereka,  
sementara jumlah aset hanya memberi kesan logaritma — menjadikan **usaha manusia lebih bernilai daripada modal**.

**Contoh:**  
Seorang pengguna dengan 250 token yang aktif lebih layak berbanding pengguna dengan 100,000 token tetapi tidak menyumbang apa-apa.

---

## 🧩 14) Mesin Keadaan (State Machine)

Rekod [PoArt] dan status [FPP] melalui aliran berikut:

1. **Draft** (Deraf)  
2. **Submitted** (Dihantar)  
3. **Under Review** (Dalam Semakan)  
4. **Challenged** (Cabaran Dibuka)  
5. **Verified** (NotarySeal Diterapkan)  
6. **Renew Due** (Tarikh Pembaharuan Tiba)  
7. **Legacy Archive** (Arkib Legasi)  
8. **Revoked** (Dibatalkan / Tidak Sah / Ditarik Balik)

> Aliran ini memberikan pandangan jelas tentang status semasa setiap pendaftaran.

---

## 🔗 15) Minimum On-chain / Maksimum Off-chain

### Data On-chain

- EvidenceRoot (Merkle Root)  
- NotarySeal  
- TimeStamp  
- Signer (Artis/Pemilik)  
- Status (Verified/Legacy/Revoked)  
- Permit Records (seperti Move Permit)

### Data Off-chain

- Fail video mentah  
- Timelapse  
- Log teknikal  
- Butiran Manifest  
- Arkib besar (IPFS / Arweave)

**Matlamat:** Memaksimumkan kebolehkesahan tanpa membebankan blockchain.

---

## 🏛️ 16) Mekanisme Rayuan & Mercii (Appeals / Institutional Trust Layer)

Mekanisme rayuan berfungsi sebagai jaminan kepercayaan institusi dalam sistem ini.

- **Penapis Strategik:** Rayuan mesti berdasarkan bukti, bukan emosi.  
- **Veto Komuniti:** 40% veto + kuorum ganda.  
- **Anti-Bot / Anti-Sybil:** Pengesahan berasaskan stake atau identiti Solana.  
- **Pembekuan Pek Bukti:** Apabila rayuan dibuka, semua bukti dibekukan dengan “time-lock”.  
- **Ketelusan:** Setiap kes rayuan direkod secara awam dengan garis masa yang boleh disemak.

---

## 🧨 17) Model Ancaman (Threat Model & Counter Layers)

| Ancaman | Lapisan Pertahanan |
|:--|:--|
| **Serangan Sybil** | Turnstile + Penapis Zombie + Kuorum |
| **Pinjaman Segera (Flash-loan)** | TWAB + Guard Window + Pemarkahan Logaritma |
| **Dominasi Paus (Whale Domination)** | Skor Kuasa Logaritma + TWAB |
| **Dagangan Palsu (Wash Trading)** | Pengesahan Dompet Sejuk + Tangga Penalti |
| **Kolusi (Berkomplot)** | Veto + Semakan Evidence Pack + Ketelusan |
| **Pengubahsuaian Data** | EvidenceRoot + Tandatangan SHA-512 + NotarySeal |
| **Rasuah / Pembelian Undi** | Time-lock + Kuorum + Legitimitas Berdasarkan Sumbangan |
| **Pemalsuan Proses Deepfake** | Frame Cabaran Rawak + Manifest + Rantaian Hash |

---

## ⚖️ 18) Kata Akhir: Pelan Induk Tadbir Urus Global (Manifesto)

> **Nota Visi:** Struktur matematik yang dibangunkan oleh [FPP] dan [PoArt] bukan sekadar untuk seni — ia adalah **model tadbir urus baharu** yang boleh memperbaiki sistem politik global yang rosak.

---

### 18.1) Tamatnya Plutokrasi (The End of Plotocracy)

* **Definisi:** Plutokrasi = kuasa ditentukan oleh kekayaan.  
* **Jawapan Protokol:** Dengan pemarkahan logaritma, kekuatan modal dikurangkan — masa & usaha menjadi asas kuasa.  
* **Rasional:** Masa depan milik mereka yang menyumbang nilai intelektual, bukan mereka yang hanya kaya.

---

### 18.2) Parlimen Meritokratik (The Meritocratic Parliament)

Menggantikan populisme dan politik wang dengan struktur di mana hak suara diberikan kepada mereka yang memahami dokumentasi dan menyumbang secara intelektual melalui IPOW.

---

### 18.3) Keselamatan Pilihan Raya (Security Against Vote Rigging)

- **Turnstile:** Menyekat manipulasi bot.  
- **TWAB:** Menghapuskan pembelian undi saat akhir.  
- **40% Veto + Kuorum:** Menjamin suara minoriti tetap terwakili.

---

### 18.4) Kesimpulan: Menyelamatkan Masa Depan (Saving the Future)

Sistem ini memberi kemenangan kepada **usaha terbukti**, bukan penipuan.  
Kejayaan datang kepada mereka yang berfikir untuk berabad-abad, bukan yang bertindak untuk seketika.  
Ia mengurangkan kesilapan manusia melalui **tadbir urus yang sah secara matematik**.

---


## 📅 19) Peta Jalan & Nota Masa Depan (Roadmap & Future Notes)

Semua bahagian dalam dokumentasi ini membentuk asas kepada visi jangka panjang ekosistem **Ilhan Art** dari tahun **2026 hingga 3000**.  
Setiap kemas kini versi (cth. v1.1, v1.2 dan seterusnya) akan memperkenalkan sambungan teknikal baharu — termasuk **integrasi API**, **penghubungan POS fizikal**, dan **kerjasama dengan rakan dunia sebenar.**

---

### Garis Panduan Utama Masa Depan

1. **v1.1 (2027):**  
   - Integrasi awal sistem reputasi off-chain.  
   - Modul “Heartbeat” separa automatik untuk pembaharuan tahunan.  
   - Penetapan kadar penalti dinamik untuk TWAB.

2. **v1.2 (2028):**  
   - Pelancaran mekanisme **Pengesahan Budaya Dunia Sebenar** (RCV).  
   - Peluasan kerjasama antara galeri seni dan platform NFT hibrid.  
   - Pelaksanaan **kad pengesahan fizikal (Proof Card)** berasaskan QR.

3. **v1.3 (2029):**  
   - Integrasi “AI Assisted Verification” — sistem penilaian video dengan cap jari digital.  
   - Lapisan keselamatan SHA-512 berlapis untuk notari dan validator komuniti.

4. **v1.4 (2030):**  
   - Pengenalan **governance peringkat global** untuk keseragaman tadbir urus seni.  
   - Penambahan sistem merit dunia sebenar dan jaringan budaya antarabangsa.

---

### Nota Penutup (Legacy Vision)

> Ekosistem ini bukan hanya protokol — ia adalah **manifestasi kesedaran budaya manusia**.  
> Ia menulis semula cara kita mengukur nilai seni, integriti, dan sumbangan.

Sistem ini berjanji untuk mengekalkan prinsip bahawa:

- **Seni adalah bukti usaha, bukan ilusi.**  
- **Kuasa mesti datang dari masa dan integriti, bukan kekayaan.**  
- **Setiap lapisan budaya adalah kod yang hidup.**

---

## 🔐 Tandatangan Hash (v1.0 Hard-Locked)

SHA-512 | Metadata | Cap Masa | Notari Digital  

