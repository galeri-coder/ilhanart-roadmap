# 📜 Terminologi & Glosarium Teknis 🇮🇩

> **Versi Protokol:** 1.0 (Stabil)  
> **Visi Jaringan:** 2025 → 3000 Arsip  
> **Ekosistem:** [PoArt] + [FPP] + [Michelangelo] + [Lapisan Budaya]  
> **Status:** **HARD_LOCKED** (Dokumentasi Aktif)  
> **Integritas:** Disegel dengan SHA-512 (Kompatibel dengan Notaris Digital)

---

## 🔰 Gambaran Arsitektur Berlapis

| Lapisan | Tujuan | Protokol |
|:--|:--|:--|
| **L1** | Verifikasi kerja manusia | **PoArt (Proof of Art)** |
| **L2** | Loyalitas / ekonomi | **FPP (Foundational Pillar Protocol)** |
| **L3** | Tata kelola | **Kerangka Michelangelo (Mesin Meritokrasi)** |
| **L4** | Integrasi budaya | **Lapisan & Hak Istimewa Budaya** |

Struktur ini mencerminkan kesatuan teknis dan filosofis dari seluruh ekosistem dalam empat lapisan inti.  
Pengguna baru dapat memahami keseluruhan arsitektur ini hanya dalam **2 menit** melalui tabel di atas.

---

## 🧩 Tingkatan Keanggotaan — “Primer → Texture → Impasto”

| Tingkat | Definisi | Dasar Teknis |
|:--|:--|:--|
| **Primer (Dasar)** | Tingkat awal. Sudah menyelesaikan verifikasi dasar tetapi belum memiliki friksi waktu (TWAB). | `0 < TWAB ≤ 10⁰` |
| **Texture (Tekstur)** | Anggota aktif yang telah mengakumulasi saldo dari waktu ke waktu. | `10⁰ < TWAB ≤ 10²` |
| **Impasto (Lapisan Tebal)** | Anggota inti dengan TWAB tertinggi, mempertahankan siklus 365 hari. | `TWAB > 10²` |

### Rumus Tingkat Keanggotaan

$$
\text{Tier}(u)=
\begin{cases}
\text{Primer},&0<\text{TWAB}_u\le10^0\\
\text{Texture},&10^0<\text{TWAB}_u\le10^2\\
\text{Impasto},&\text{TWAB}_u>10^2
\end{cases}
$$

---

## 📑 Daftar Isi

1. Pilar Protokol (Pillars of the Protocol)  
2. Peran & Entitas (Roles & Entities)  
3. Metrik Ekonomi & Tata Kelola (Economic & Governance Metrics)  
4. Keamanan & Validasi (Security & Validation)  
5. Validasi & Persistensi (Validation & Persistence)  
6. Pengawasan Terdesentralisasi (Decentralized Supervision)  
7. Kerangka Michelangelo (Meritocracy Engine)  
8. Pengganda Budaya & Tingkat Peringkat (Cultural Multipliers & Ranking Levels)  
9. Ambang Batas & Metrik Jaringan (Cut-off Thresholds & Network Metrics)  
10. Kerangka Intelektual (Intellectual Framework)  
11. Resistansi Sybil Lanjutan (Advanced Sybil Resistance)  
12. Warisan Generasional & Tata Kelola (Generational Legacy & Governance)  
13. Lapisan Hak Istimewa Budaya & Integrasi Dunia Nyata (Cultural Privilege Layers & Real-World Integration)  
14. Mesin Keadaan (State Machine)  
15. Minimum On-chain / Maksimum Off-chain (Minimal On-chain / Maximal Off-chain)  
16. Mekanisme Banding & Kepercayaan (Appeals / Mercii & Trust Mechanism)  
17. Model Ancaman (Threat Model & Counter Layers)  
18. Pernyataan Akhir: Manifesto Tata Kelola Global (Manifesto)  
19. Peta Jalan & Catatan Masa Depan (Roadmap & Future Notes)

---

## 🏛️ 1) Pilar Protokol (Pillars of the Protocol)

### **[PoArt] Proof of Art (v1.0)**

* **Definisi:** Protokol utama yang memverifikasi tidak hanya hasil akhir karya seni, tetapi juga seluruh proses penciptaannya menggunakan data teknis.  
* **Masalah yang Diselesaikan:** Dengan munculnya alat AI generatif, membuktikan kerja manusia dalam dunia digital menjadi sulit — nilai seni pun menurun.  
* **Cara Kerja:** Saat artis berkarya, mereka mengirimkan **Paket Bukti (Evidence Pack)** yang mencatat setiap tahap. Protokol mencatat data ini ke blockchain dengan cap waktu.  
* **Contoh:** Jika seorang seniman melukis selama 40 jam, rekaman streaming, video timelapse, dan sidik jari digitalnya diverifikasi oleh [PoArt]. Bukan hanya “lukisan jadi” yang diakui, tetapi “40 jam tenaga manusia” yang diarsipkan.

---

### **[FPP] Foundational Pillar Protocol (v1.0)**

* **Definisi:** Sistem utama yang membangun pilar ekonomi, tata kelola, dan sosial dari ekosistem — memberi penghargaan pada loyalitas dan partisipasi jangka panjang.  
* **Masalah yang Diselesaikan:** Menghapus ketidakadilan dalam ekosistem kripto di mana “siapa punya modal, dia berkuasa”, serta mencegah spekulasi destruktif.  
* **Cara Kerja:** Hak suara dan tata kelola pengguna ditentukan oleh lamanya kepemilikan, bukan hanya jumlah aset.  
* **Contoh:** “Paus” dengan 1 juta token yang baru bergabung akan memiliki kekuatan lebih rendah daripada anggota setia yang menyimpan 100 token selama satu tahun.

---

## 👥 2) Peran & Entitas (Roles & Entities)

Protokol ini mendefinisikan secara jelas “siapa yang berhak melakukan apa” untuk mengurangi kesalahpahaman dan penyalahgunaan.

- **Seniman (Artist):** Menghasilkan Paket Bukti untuk [PoArt], memulai registrasi, dan menandatangani heartbeat tahunan.  
- **Patron (Penyokong):** Mendapat status dalam [FPP] berdasarkan loyalitas dan kontribusi; memiliki hak veto dan pengawasan.  
- **Validator (Pemeriksa Komunitas):** Memeriksa Evidence Pack, menandai ketidaksesuaian, dan ikut serta dalam proses veto/banding.  
- **Notaris Digital (Digital Notary):** Memverifikasi bukti + konsensus + cap waktu, lalu mengarsipkannya ke dalam Registri Publik.  
- **Registri Publik (Public Registry):** Lapisan identitas permanen untuk semua catatan yang diverifikasi (Verified / Legacy / Revoked).  
- **Penyimpanan Bukti (IPFS / Arweave / Arsip):** Menyimpan data mentah di luar rantai; hanya akar kriptografi yang ditulis ke blockchain.

---

## 📊 3) Metrik Ekonomi & Tata Kelola (Economic & Governance Metrics)

Bagian ini mendefinisikan model matematis dan batas waktu untuk menjamin stabilitas ekonomi dan keadilan dalam tata kelola.  
Tujuannya adalah menahan dominasi modal jangka pendek melalui **gesekan waktu (time friction)**, sambil membuat loyalitas jangka panjang dapat diukur dan diaudit.

---

### 3.1) Jendela Waktu (Time Windows) dan Definisi Epoch

Dalam protokol ini, waktu tidak hanya didefinisikan oleh satu “epoch”, tetapi oleh **tiga jendela waktu** dengan fungsi yang berbeda.

#### 3.1.1) Epoch Operasional (Operational Epoch)
Siklus dasar untuk laporan, log, dan pembaruan rutin.

- **Default:** **7 Hari**  
- **Fungsi:** Pembaruan mingguan dan pelaporan rutin.

#### 3.1.2) Jendela Perlindungan Suara Kritis (Critical Vote Guard Window)
Menentukan periode historis yang digunakan dalam menghitung kekuatan suara.

- **Lookback:** **30 Hari**  
- **Fungsi:** Mencegah pembelian suara mendadak sebelum pemungutan suara penting.

> **Aturan:** Dalam pemungutan suara kritis, perhitungan kekuatan suara menggunakan **lookback 30 hari**, bukan **epoch 7 hari**.

#### 3.1.3) Siklus Integritas (Integrity Cycle)
- **Durasi:** **365 Hari**  
- **Fungsi:** Verifikasi tahunan melalui Evidence Pack.  
> **Catatan Permanen v1.0:** Parameter 7 dan 30 hari bersifat hard-coded.

---

### 3.2) TWAB (Time-Weighted Average Balance)

TWAB adalah metrik utama yang mengukur **loyalitas** dan **stabilitas** suatu dompet dalam ekosistem.

$$
\text{TWAB}=\frac{\sum_{i=1}^{n}(\text{Saldo}_i\times\Delta t_i)}{\sum_{i=1}^{n}\Delta t_i}
$$

$\Delta t_i$ mewakili lamanya saldo tersebut dipegang.

**Opsi Metrik Mentah:**

$$
\text{TWA}=\sum_{i=1}^{n}(\text{Saldo}_i\times\Delta t_i)
$$

---

### 3.3) Kekuatan Suara (Voting Power)

$$
\text{VotingPower}=f(\text{TWAB},\text{EpochRules},\text{StatusTier})
$$

**Efek Guard Window:** Dalam pemungutan suara kritis, digunakan lookback 30 hari.

---

### 3.4) Skor Logaritmik (Logarithmic Power Scoring)

$$
\text{Score}=\log_{10}(\text{TWAB}+1)
$$

$$
\text{VotingPower}=\text{Score}\times g(\text{EpochRules},\text{StatusTier})
$$

| Saldo (TWAB) | Skor ($\log_{10}$) | Analisis Kekuatan |
|:--|:--|:--|
| 10 | 1.04 | Pengaruh awal |
| 1,000 | 3.00 | 100× peningkatan ≈ 3 skor |
| 1,000,000 | 6.00 | 100,000× peningkatan ≈ 6 skor |

> **Simulasi:**  
> Untuk melihat simulasi kekuatan suara logaritmik, kunjungi [PoArt Simulation Console](https://galeri-coder.github.io/ilhanart-protocol/[PoArt]/).

---

### 3.5) Kompatibilitas FPP v1.0

- **Epoch Operasional:** 7 Hari  
- **Guard Window:** 30 Hari  
- **Siklus Integritas:** 365 Hari  

Verifikasi tahunan wajib dilakukan melalui Evidence Pack.

---

## 🛡️ 4) Keamanan & Validasi (Security & Validation)

### 4.1) Vault Milenium (Millennium Vault, Epoch 10 Tahun)

* **Definisi:** Aset dikunci selama satu tahun (epoch), menjadi peti reputasi tertinggi dalam sistem.  
* **Masalah yang Diselesaikan:** Melindungi dari spekulasi jangka pendek yang merusak visi jangka panjang.  
* **Solusi:** Hanya mereka yang mengunci aset ≥1 tahun dan memiliki status “Pillar” yang dapat membuat keputusan kritis.

---

### 4.2) Paket Bukti (Evidence Pack)

**Definisi:**  
Kumpulan data teknis wajib untuk verifikasi oleh [PoArt].

#### Isi Wajib (Trinitas Bukti)
1. **Log Langsung:** Rekaman siaran langsung saat proses penciptaan.  
2. **Video Timelapse:** Perekaman dari awal hingga akhir.  
3. **Sidik Jari Digital:** Hash yang ditandatangani oleh dompet artis.

---

#### Penguatan v1.0 (Lapisan Integritas Rantai)

Trinitas saja tidak cukup; hubungan antar file juga harus disegel:

4. **Manifest Tangkapan:**  
   Data kamera/perangkat, resolusi, frame rate, daftar file, dan checksum.

5. **Merkle Root / Rantai Hash:**  

$$
\text{EvidenceRoot} = \text{MerkleRoot}(\text{SemuaFile})
$$

6. **Frame Tantangan Acak (Opsional):**  
   Uji keaslian manusia selama siaran langsung.  
   Contoh: menampilkan objek khusus atau menulis kata tertentu.  
   Ini meningkatkan biaya serangan AI/deepfake.

---

**Masalah yang Diselesaikan:**  
Memberikan jawaban teknis yang pasti terhadap pertanyaan:  
*“Apakah karya ini benar-benar dibuat oleh manusia?”*

---

### 4.3) Perlindungan Sybil & Flash-loan

* **Definisi:** Perlindungan matematis terhadap akun bot dan serangan pinjaman instan.  
* **Solusi:** Kombinasi TWAB + Guard Window membuat pergerakan modal jangka pendek tidak relevan secara tata kelola.

---

### 4.4) Notaris Digital (Digital Notary: Segel Protokol)

* **Definisi:** Mekanisme mandiri yang memverifikasi data dari [PoArt] dan [FPP], kemudian menuliskannya ke dalam **Registri Publik**.

### Masalah yang Diselesaikan

1. **Otoritas Terpusat & Bias:** Menghapus kebutuhan persetujuan subjektif.  
2. **Manipulasi Data:** Catatan yang diverifikasi tidak dapat diubah kembali.  
3. **Gatekeeping:** Akses seniman ke arsip global berdasarkan bukti, bukan selera pribadi.

### Siklus Verifikasi (Filter Tiga Lapisan)

- **Kelengkapan Evidence Pack:** Trinitas + Manifest + EvidenceRoot  
- **Pengawasan Demokratik:** Veto / Quorum  
- **Tanda Tangan Kriptografis:** Verifikasi SHA-512

### Segel Matematis

$$
\text{NotarySeal}=\text{Hash}(\text{EvidenceRoot}+\text{VoterConsensus}+\text{TimeStamp})
$$

### Hasil (2026–3000)
Karya yang memperoleh segel notaris menjadi bagian dari warisan budaya manusia universal.

---

## 🏛️ 5) Validasi & Persistensi (Validation & Persistence)

### 5.1) Validasi Dompet Dingin 365 Hari (Cold Wallet Validation)

**Definisi:**  
Aset disimpan secara berkelanjutan di dompet dingin selama **365 hari**.

**Masalah yang Diselesaikan:**
1. Perdagangan palsu (wash trading)  
2. Tekanan spekulatif  
3. Risiko keamanan dompet panas  

---

#### Pembaruan v1.0: “Tangga Penalti” menggantikan “Hard Reset”

Mengatur ulang total dengan satu transfer dianggap terlalu keras,  
sehingga sistem v1.0 memperkenalkan penalti bertingkat:

**Pelanggaran 1 (transfer sebelum 365 hari):**

$$
\text{EffectiveTWAB} = \text{TWAB} \times 0.20
$$

**Pelanggaran 2:**

$$
\text{EffectiveTWAB} = \text{TWAB} \times 0.05
$$

**Pelanggaran 3:**  
Status menjadi **Revoked** (dicabut).

> Tangga penalti ini mencegah manipulasi keluar-masuk cepat tanpa menghukum pengguna yang sah secara berlebihan.

## 🗳️ 6) Pengawasan Terdesentralisasi (Decentralized Supervision)

### 6.1) Mekanisme Veto Komunitas (Community Veto Mechanism, Ambang 40%)

* **Definisi:** Sistem demokratis yang memungkinkan minoritas berkualitas menghentikan pendaftaran atau perubahan protokol baru.

#### Pembaruan v1.0: “Quorum + Veto” Kunci Ganda

- **Quorum (Partisipasi Minimum):** Setidaknya **25%** kekuatan suara aktif harus berpartisipasi.  
- **Ambang Veto:** Hanya sah jika mencapai **40% dari total kekuatan suara aktif.**

**Masalah yang Diselesaikan:**
1. Serangan Sybil  
2. Pembelian suara & kolusi  
3. Intervensi modal besar  

* **Contoh:** Jika karya AI diajukan sebagai “buatan manusia”, komunitas dapat menggunakan hak veto 40% untuk menghentikan validasinya secara permanen.

---

### 6.2) Tata Kelola Darurat / Dewan Fallback (Emergency Governance / Fallback Council)

**Tujuan:** Mencegah kebuntuan keputusan ketika partisipasi rendah.

**Definisi:**

$$
\text{Deadlock}=(\text{ParticipationRate}<25\%)\land(\text{ProposalTimeout}>7\text{ days})
$$

Ketika `Deadlock = TRUE`:

1. **Dewan Fallback** (10% anggota tertinggi dari Impasto) memperoleh kekuasaan sementara.  
2. Keputusan dibuat dengan `Council Consensus ≥ ⅔`.  
3. Jika tidak disahkan melalui referendum komunitas dalam 30 hari, keputusan otomatis dibatalkan.  
4. Semua keputusan dicatat dengan hash SHA-512 dalam **Ledger Darurat (Emergency Ledger)**.

---

## ⚙️ 7) Kerangka Michelangelo (Meritocracy Engine)

### 7.1) Filsafat Michelangelo

* **Definisi:** Mesin reputasi dan peringkat dalam ekosistem Ilhan Art.  
* **Slogan:** *“Kamu tidak bisa membeli jalan ke puncak.”*  
* **Contoh:** Paus dengan jutaan token tidak akan melampaui seseorang yang telah berkontribusi secara budaya selama bertahun-tahun.

---

### 7.2) Rumus Status: Waktu × Kontribusi

$$
\text{Status}=\text{HoldingTime}\times\text{CulturalContribution}
$$

* **HoldingTime:** Jumlah hari aset disimpan dalam dompet dingin tanpa gangguan.  
* **CulturalContribution:** Kontribusi nyata seperti penerjemahan, kurasi, pameran, atau pengembangan.  
* **Masalah yang Diselesaikan:** Menghapus “pemegang pasif” yang tidak berkontribusi kepada komunitas.

---

## 📊 8) Pengganda Budaya & Tingkat Peringkat (Cultural Multipliers & Ranking Levels)

### 8.1) Pengganda Budaya (Cultural Multiplier)

* **Definisi:** Sistem bonus tambahan untuk kontribusi budaya.  
* **Penerapan:**
  - **Impasto (JP/TR/EN):** Penerjemahan karya ilmiah, filosofis, atau artistik (+4,500 poin contoh)  
  - **Texture:** Pengendalian kualitas pendaftaran & partisipasi veto  
  - **Infrastruktur:** Kontribusi kode, dokumentasi, atau dukungan sistem  

* **Contoh:** 1.000 hari penyimpanan + satu proyek penerjemahan besar dapat melampaui ribuan anggota lainnya.

---

### 8.2) Tingkat Peringkat (Ranking Levels)

| Peringkat | Rentang / Poin | Peran & Wewenang |
|:--|:--|:--|
| **Impasto (≥100k)** | Konstitusional | Menentukan strategi & biaya jangka panjang |
| **Texture (50k–99k)** | Kuratorial | Mengawasi, mengelola, dan mengedit konten |
| **Primer (<50k)** | Anggota | Mengajukan proposal kecil & pemungutan dasar |

> Peringkat diperbarui secara dinamis berdasarkan aktivitas dan stabilitas kontribusi dalam [FPP].

---

## 📈 9) Ambang & Metrik Jaringan (Cut-off Thresholds & Network Metrics)

### 9.1) Ambang Masuk (Entry Thresholds)

Ambang ditetapkan setelah sistem mencapai stabilitas.

- **Ambang Impasto:** **≥ 100.000 Poin**  
- **100 Teratas:** **≥ 45.000 Poin**

* **Masalah yang Diselesaikan:** Menjaga kualitas sistem dengan mencegah banjir peserta tanpa kontribusi nyata.

---

### 9.2) TWAB Jaringan (Network TWAB)

* **Definisi:** Total kapasitas TWAB seluruh ekosistem (contoh: 4.2M Network TWAB).  
* **Fungsi:** Semakin tinggi nilainya, semakin sulit sistem dimanipulasi.  
* **Registrasi 24 Jam:** Jumlah pendaftaran [PoArt] baru dalam 24 jam terakhir.

---

## 🎨 10) Kerangka Intelektual (Intellectual Framework)

### 10.1) IPOW: Bukti Kerja Intelektual (Intellectual Proof of Work)

* **Definisi:** Mesin reputasi yang memberi penghargaan berdasarkan kontribusi intelektual seperti seni, pendidikan, dan penerjemahan — bukan sekadar kepemilikan aset.  
* **Masalah yang Diselesaikan:** Mengatasi budaya staking pasif.  
* **Contoh:** Dompet dengan 1 juta token tanpa kontribusi intelektual akan mendapat skor lebih rendah daripada pengguna dengan 100 token yang aktif berkontribusi.

---

### 10.2) Filter Kejujuran Intelektual (Intellectual Honesty Filter)

* **Definisi:** Lapisan verifikasi untuk menilai apakah pengguna benar-benar memahami topik sebelum memberikan suara.  
* **Masalah yang Diselesaikan:** Pemungutan suara buta, spam AI, dan manipulasi otomatis.

#### Pembaruan v1.0: Bukti Pemahaman (Proof of Understanding)

Alih-alih kuis klasik, sistem meminta pengguna menunjukkan pemahaman sejati:

**Opsi A (Ringkasan):** Ringkas proposal dalam 100 kata.  
**Opsi B (Analisis Risiko):** Tandai dua risiko dan jelaskan salah satunya.  
**Opsi C (Keberatan):** Tulis alasan logis jika tidak setuju.  

Modul ini menguji pemahaman nyata dan mencegah otomasi bot.

---

## 🛡️ 11) Resistansi Sybil Lanjutan (Advanced Sybil Resistance)

### 11.1) Mekanisme Turnstile

* **Definisi:** Ambang partisipasi minimum (misalnya 250 ILHAN Token).  
* **Filosofi:** “Bukan tembok, tapi pintu berputar.”  
* **Masalah yang Diselesaikan:** Mencegah pembuatan ribuan akun bot otomatis.  
* **Contoh:** Serangan 10.000 akun bot menjadi tidak efisien karena setiap akun harus menyimpan 250 token.

---

### 11.2) Filter Dompet Zombie (Zombie Wallet Filter)

* **Definisi:** Kebutuhan aktivitas berkala untuk membuktikan dompet masih aktif.  
* **Aturan:** Dompet tidak aktif dihapus dari registri global meskipun memiliki skor tinggi.  
* **Tujuan:** Memastikan sistem hanya berisi pengguna hidup dan aktif.

---

## 🧬 12) Warisan Generasional & Tata Kelola (Generational Legacy & Governance)

* **Definisi:** Transfer reputasi dan hak kepada ahli waris anggota Impasto yang mempertahankan status jangka panjang.  
* **Masalah yang Diselesaikan:** Menjaga agar nilai budaya tidak hilang saat seseorang meninggal.  
* **Implementasi:** Hak ini dibuka bagi mereka yang menunjukkan loyalitas ≥ 4 tahun dan disegel secara on-chain.

---

### 12.2) Hak Tata Kelola Parlemen (Parliamentary Governance Rights)

| Tingkat | Rentang | Hak & Fungsi |
|:--|:--|:--|
| **Impasto (≥100k)** | Konstitusional | Menentukan kebijakan, strategi, dan biaya |
| **Texture (50k–99k)** | Kuratorial | Kurasi, pengawasan, dan pemungutan suara |
| **Primer (<50k)** | Dasar | Mengajukan & menyetujui proposal kecil |

* **Masalah yang Diselesaikan:** Menggantikan demokrasi acak dengan sistem meritokrasi berbasis kontribusi dan kemampuan.

---

## 🌍 13) Lapisan Hak Istimewa Budaya & Integrasi Dunia Nyata  
(Cultural Privilege Layers & Real-World Integration)

> **Catatan:** Hak-hak istimewa berikut akan diterapkan secara bertahap antara tahun 2026–2030 sebagai bagian dari “Peta Jalan Masa Depan”.

---

### 13.1) Hak Pameran Tahunan (Annual Exhibition Right)

* **Definisi:** Hak tahunan bagi artis/patron yang diverifikasi oleh [PoArt] untuk memamerkan karya mereka di Ilhan Art Gallery selama 1 minggu per tahun.  
* **Masalah yang Diselesaikan:** Biaya tinggi bagi seniman independen untuk mengakses ruang fisik.  
* **Implementasi:** Peserta yang mencapai ambang kelayakan dapat memesan tanggal sesuai skor reputasi budayanya.

---

### 13.2) Penetapan Harga Seni Dinamis (Dynamic Art Pricing)

* **Definisi:** Sistem API yang menyesuaikan diskon berdasarkan status budaya pengguna.  
* **Struktur:**  
  - **Impasto (≥100k):** Diskon 50%+  
  - **Texture (50k–99k):** Diskon 30%  
  - **Primer (<50k):** Diskon 10%  
* **Filosofi:** “Tidak ada negosiasi — hanya nilai usaha yang menentukan harga.”  
* **Tujuan:** Mendorong keadilan melalui transparansi algoritma dan penghargaan budaya.

---

### 13.3) Integrasi Ekosistem Fisik (Physical Ecosystem Integration)

- Toko buku, kafe, pusat budaya  
- Kode QR untuk verifikasi status & penebusan hak  

---

### 13.4) Tenaga Lebih Tinggi dari Modal (Labor Over Capital: Meritocratic Access)

* **Definisi:** Hak sejati tidak bergantung pada jumlah modal, tetapi pada **kontribusi budaya dan stabilitas waktu**.  

**Rumus Matematis:**

$$
\text{ClaimRight} \propto \text{CulturalScore} + \log_{10}(\text{Balance})
$$

Artinya, hak seseorang meningkat sesuai kontribusi budaya,  
sementara jumlah aset hanya memberi pengaruh logaritmik — menjadikan **tenaga manusia lebih bernilai daripada modal**.

**Contoh:**  
Pengguna dengan 250 token yang aktif lebih layak dibandingkan pemegang 100.000 token yang pasif.

---

## 🧩 14) Mesin Keadaan (State Machine)

Alur status [PoArt] dan [FPP] mengikuti urutan berikut:

1. **Draft** (Draf)  
2. **Submitted** (Dikirim)  
3. **Under Review** (Dalam Peninjauan)  
4. **Challenged** (Dipersoalkan)  
5. **Verified** (Tersertifikasi / NotarySeal diterapkan)  
6. **Renew Due** (Menunggu Perpanjangan)  
7. **Legacy Archive** (Arsip Warisan)  
8. **Revoked** (Dibatalkan / Tidak Sah)

> Alur ini memberikan transparansi penuh terhadap status setiap pendaftaran dalam sistem.

---

## 🔗 15) Minimum On-chain / Maksimum Off-chain  
(Minimal On-chain / Maximal Off-chain)

### Data On-chain

- EvidenceRoot (Merkle Root)  
- NotarySeal  
- TimeStamp  
- Signer (Seniman / Pemilik)  
- Status (Verified / Legacy / Revoked)  
- Catatan lisensi (misal: Move Permit)

### Data Off-chain

- File video asli  
- Rekaman timelapse  
- Catatan teknis  
- Detail Manifest  
- Penyimpanan permanen (IPFS / Arweave)

**Tujuan:**  
Meningkatkan kemampuan audit dan transparansi tanpa membebani blockchain secara berlebihan.

---

## 🏛️ 16) Mekanisme Banding & Kepercayaan  
(Appeals / Mercii & Trust Layer)

Lapisan ini berfungsi sebagai jaminan kepercayaan institusional dalam ekosistem.

- **Filter Strategis:** Banding harus berbasis bukti, bukan emosi.  
- **Hak Veto Komunitas:** 40% veto + quorum ganda.  
- **Anti-Bot / Anti-Sybil:** Verifikasi melalui staking atau identitas Solana.  
- **Penguncian Evidence Pack:** Saat banding dimulai, semua bukti dikunci dengan “time-lock”.  
- **Transparansi:** Semua kasus banding dicatat secara publik dengan garis waktu.

---

## 🧨 17) Model Ancaman & Lapisan Perlindungan  
(Threat Model & Counter Layers)

| Ancaman | Lapisan Perlindungan |
|:--|:--|
| **Serangan Sybil** | Turnstile + Zombie Filter + Quorum |
| **Flash-loan** | TWAB + Guard Window + Skor logaritmik |
| **Dominasi Paus (Whale Domination)** | Skor logaritmik + TWAB |
| **Perdagangan Palsu (Wash Trading)** | Validasi Dompet Dingin + Tangga Penalti |
| **Kolusi / Konspirasi** | Veto + Audit Evidence Pack + Transparansi Publik |
| **Manipulasi Data** | EvidenceRoot + Tanda SHA-512 + NotarySeal |
| **Pembelian Suara / Suap** | Time-lock + Quorum + Skor Berdasarkan Kontribusi |
| **Deepfake / AI Forgery** | Uji Frame Acak + Manifest + Rantai Hash |

---

## ⚖️ 18) Manifesto Tata Kelola Global  
(Global Governance Manifesto)

> **Catatan Visi:**  
> Struktur matematis yang dikembangkan oleh [FPP] dan [PoArt]  
> tidak hanya untuk seni — tetapi untuk **membangun model pemerintahan baru** yang dapat memperbaiki kegagalan sistem politik global.

---

### 18.1) Akhir dari Plutokrasi (End of Plutocracy)

* **Definisi:** Plutokrasi = Kekuasaan ditentukan oleh kekayaan.  
* **Solusi Protokol:** Skor logaritmik mengurangi dominasi modal — menjadikan waktu dan upaya sebagai dasar kekuasaan.  
* **Prinsip:** Masa depan milik pencipta nilai intelektual, bukan pemilik modal besar.

---

### 18.2) Parlemen Meritokratis (The Meritocratic Parliament)

Menggantikan politik populis dan berbasis uang  
dengan struktur yang memberi hak kepada mereka yang memahami dokumen dan berkontribusi secara intelektual melalui IPOW.

---

### 18.3) Keamanan Pemilihan (Election Security)

- **Turnstile:** Mencegah manipulasi bot.  
- **TWAB:** Menghilangkan pembelian suara menjelang pemungutan.  
- **40% Veto + Quorum Ganda:** Menjamin representasi minoritas.

---

### 18.4) Penutup: Menyelamatkan Masa Depan (Saving the Future)

Sistem ini memberikan kemenangan bagi **upaya yang dapat dibuktikan**,  
bukan ilusi atau oportunisme.  
Keberhasilan diperoleh oleh mereka yang merencanakan untuk abad, bukan minggu.  
Kesalahan manusia diminimalkan melalui **tata kelola yang dapat diaudit secara matematis**.

---

## 📅 19) Peta Jalan & Catatan Masa Depan  
(Roadmap & Future Notes)

Dokumen ini menyatukan visi jangka panjang ekosistem **Ilhan Art** dari tahun **2026 hingga 3000**.  
Setiap versi baru (misal: v1.1, v1.2, dst.) akan memperluas lapisan teknis, termasuk **integrasi API**, **titik POS nyata**, dan **kemitraan dunia nyata.**

---

### Arah Utama Masa Depan

1. **v1.1 (2027):**  
   - Integrasi sistem reputasi off-chain.  
   - Modul Heartbeat semi-otomatis untuk pembaruan tahunan.  
   - Penalti TWAB dinamis.

2. **v1.2 (2028):**  
   - Meluncurkan mekanisme **Validasi Budaya Dunia Nyata (RCV)**.  
   - Kolaborasi dengan galeri seni & platform NFT hibrida.  
   - Menambahkan **Kartu Bukti (Proof Card)** dengan kode QR.

3. **v1.3 (2029):**  
   - Integrasi **Verifikasi Berbantuan AI** untuk video & sidik jari digital.  
   - Lapisan keamanan SHA-512 bertingkat untuk Notaris & Validator.

4. **v1.4 (2030):**  
   - Peluncuran **Tata Kelola Global** untuk keseragaman sistem seni.  
   - Membentuk jaringan budaya & meritokrasi internasional.

---

### Visi Warisan (Legacy Vision)

> Sistem ini bukan hanya protokol —  
> tetapi **manifestasi kesadaran budaya manusia.**  
> Ia menulis ulang definisi nilai, kejujuran, dan seni.

Sistem ini berkomitmen pada prinsip:

- **Seni adalah bukti kerja, bukan ilusi.**  
- **Kekuasaan lahir dari waktu & kebajikan, bukan kekayaan.**  
- **Setiap lapisan budaya adalah kode yang hidup.**

---

## 🔐 Tanda Hash (v1.0 Hard-Locked)

SHA-512 | Metadata | TimeStamp | Digital Notary
