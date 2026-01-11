# 📚 Glosarium Istilah dan Konsep Teknis
> **"Memahami bahasa protokol ini berarti memahami visinya."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Arsitektur Dasar

**PoArt Forensic Engine (PFE)** adalah lapisan pusat yang mewakili logika dan operasi teknis di balik protokol [PoArt]. Ini adalah "mesin forensik" yang mengambil data produksi seni mentah dan mengubahnya menjadi **bukti digital** yang dapat diverifikasi dan tidak dapat diubah.

### 🧩 Mengapa "PoArt Forensic"?

- **PoArt (Bukti Seni):** Tujuan mesin adalah menghubungkan nilai aset digital bukan dengan estimasi, tetapi dengan **proses produksi yang dapat diverifikasi**.
- **Forensic (Verifikasi Ilmiah):**
  - **Definisi Teknis:** Metode algoritmik dan urutan catatan untuk memverifikasi bahwa data proses produksi (sapuan kuas, video waktu, catatan) tidak dimanipulasi.
  - **Level Filosofis:** Klaim mengubah **biaya waktu manusia, tenaga kerja, dan keputusan** menjadi kebenaran yang dapat diukur, berlawanan dengan produksi "hasil instan" AI.

> Catatan: Integrasi blockchain (misalnya, Solana) bukan bagian inti dari PFE; akan dijelaskan secara terpisah sebagai **lapisan jangkar rantai** untuk tujuan verifikasi/registrasi.

### 🛠️ Ruang Lingkup Teknis v1.0

**PoArt Forensic Engine (PFE) v1.0** dibangun di atas **3 pilar utama** berikut ini alih-alih model keuangan yang kompleks:

1. **Hashing & Sealing (Penyegelan):**  
   PFE memproses semua elemen dalam paket bukti (file karya, video, JSON/catatan, tanda tangan, dll.) dengan cara deterministik dan menghasilkan nilai **NotarySeal** yang unik.

   **Konsep Kunci (v1.0):**
   - **FileHash (Sidik Jari Digital Karya):** Hash yang dihasilkan dari byte file karya.
   - **EvidenceRoot (Akar Paket Bukti):** Ringkasan akar yang mewakili integritas paket bukti (akar Merkle atau hash representasi kanonik).
   - **NotarySeal (Segel Akhir / Output PFE):** Segel akhir yang dihasilkan dari kombinasi EvidenceRoot + waktu + tanda tangan.

   **Rumus (ditampilkan dengan jelas untuk investor):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Definisi Payload Kanonik (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Catatan: Nilai yang disebutkan sebagai output PFE adalah **NotarySeal**. Proses **SignerSignature** akan diaktifkan di tahap 2 (dengan Solana Wallet Adapter); dalam versi v1.0 saat ini, tanda tangan atestasi sistem digunakan. Kunci publik atestasi dipublikasikan di registri di bawah field `issuer.attestation_pubkey`.

2. **Indexing (Penyimpanan):**  
   Menulis ke lapisan registri yang jelas dan dapat di-query dompet mana, pada tanggal berapa, mengirim **bukti kerja** untuk karya mana.  
   *(Lapisan ini dapat berupa database; integrasi rantai dijelaskan secara terpisah sebagai "lapisan jangkar rantai".)*

3. **Verification (Verifikasi):**  
   Ketika pertanyaan tentang validitas karya muncul, PFE memproses ulang bukti mentah; secara matematis memverifikasi bahwa nilai yang dihitung **EvidenceRoot / NotarySeal** cocok dengan catatan yang tersimpan.

---

### 🧮 Teorema Nilai PoArt (The Value Theorem)

Protokol [PoArt] tidak menghubungkan nilai ($V$) aset digital dengan persepsi pasar yang tidak jelas, tetapi dengan **realitas fisik proses produksi**.

Kecerdasan Buatan (AI) menghancurkan proses dengan memberikan hasil instan ($t \to 0$). [PoArt], bagaimanapun, mempertahankan nilai sebagai akumulasi elemen **waktu, tenaga kerja, dan agensi**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definisi Variabel

- **$\int dt$ (Akumulasi Proses):**  
  Nilai bukan "hasil instan"; ini adalah **proses** yang dikumpulkan antara $t_{\text{start}}$ dan $t_{\text{end}}$. Ketika periode menyusut (produksi AI), hasil integral mendekati 0.

- **$P_{\text{labor}}(t)$ (Daya Kerja Instan):**  
  Mewakili intensitas kerja mental dan fisik yang dikeluarkan selama produksi. Saat kerja yang dapat diverifikasi meningkat, integrand meningkat.  
  > Catatan: Istilah ini dapat digeneralisasi secara praktis dengan "sinyal kerja yang dapat diukur/dapat diverifikasi".

- **$I_{\text{agency}}(t)$ (Faktor Agensi):**  
  Kemampuan pencipta untuk mengambil risiko dan membuat keputusan. Mengambil nilai antara $0$ dan $1$.
  - **AI ($I \approx 0$):** Menjalankan perintah, tidak mengambil risiko, tidak membayar harga.
  - **Manusia ($I \to 1$):** Mengubah keputusan, ragu-ragu, mengambil risiko.

- **$U_{\text{irreversible}}$ (Keunikan Ireversibel):**  
  Meskipun dalam produksi digital pembatalan dimungkinkan (`Ctrl+Z`), dalam produksi fisik (cat yang diterapkan pada kanvas, batu yang dipahat, tindakan dalam siaran langsung) tidak ada cara untuk kembali. **Sifat ireversibel** ini adalah anggota tambahan yang menciptakan "keunikan" (karakteristik tidak dapat diubah) dalam karya.

### 🔎 Analisis Kasus: AI "Hasil Instan" vs Manusia "Proses Terverifikasi"

Skenario berikut menunjukkan bagaimana **Teorema Nilai PoArt** bekerja secara praktis dan mengapa produksi AI mendapat skor lebih rendah pada skala [PoArt].

#### Skenario A: Produksi Adegan 10 Detik dengan AI

- **Periode ($\Delta t$):** $10$ detik (proses singkat)
- **Daya Kerja ($P_{\text{labor}}$):** $1$ unit (hanya menulis perintah)
- **Faktor Agensi ($I_{\text{agency}}$):** $0.01$ (tidak ada risiko, tidak ada biaya)
- **Sifat Ireversibel ($U_{\text{irreversible}}$):** $0$ (dapat dibalik / dapat disalin)

**Hasil:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Komentar:** Meskipun hasilnya sempurna; nilai [PoArt] mendekati $0$ karena tidak ada proses yang bertahan dan tidak ada agensi/risiko yang terlibat.

#### Skenario B: Produksi Fisik 6 Jam dalam Siaran Langsung

- **Periode ($\Delta t$):** $6$ jam ($21{,}600$ detik)
- **Daya Kerja ($P_{\text{labor}}$):** $0.5$ unit (kerja fisik dan mental berkelanjutan)
- **Faktor Agensi ($I_{\text{agency}}$):** $0.9$ (keputusan yang berubah, pengambilan risiko, pilihan ireversibel)
- **Sifat Ireversibel ($U_{\text{irreversible}}$):** $>0$ (tanda fisik tidak dapat dikembalikan)

**Hasil:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Komentar:** Dengan perluasan proses dan peningkatan agensi (risiko), nilai dikumpulkan dalam bentuk kumulatif. Anggota $U_{\text{irreversible}}$ adalah kontribusi tambahan yang menciptakan "keunikan" (karakteristik tidak dapat diubah) dalam karya.

---

### ✅ Kesimpulan: Nilai Terikat-Bukti (Proof-Bound Value)

Teorema ini menarik klaim nilai [PoArt] dari "preferensi" atau "cerita pasar" dan menghubungkannya dengan **realitas produksi yang dapat diverifikasi**.

1. **Tanpa Proses, Tidak Ada Nilai:**  
   AI menghancurkan proses dengan hasil instan ($t \to 0$). Ketika jendela proses menyusut, hasil integral harus menurun:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Agensi dan Risiko adalah Pengali:**  
   [PoArt] tidak hanya mengukur "waktu yang dihabiskan" tetapi juga tingkat keputusan, risiko, dan harga aktual pada waktu itu. Produksi tanpa risiko (AI) kurang berharga:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Keunikan adalah Bukti Fisik, Bukan Pemasaran:**  
   Tanda ireversibel dalam produksi fisik (sapuan kanvas, potongan batu) berada di luar logika `Ctrl+Z` digital. Sifat ireversibel ini ($U_{\text{irreversible}}$) membuat karya menjadi unik melalui keberadaan.

> **🔐 Ringkasan:** Teorema nilai mungkin tampak sebagai pengukuran ketidakpastian (meskipun ekuivalen dunia nyata tidak dapat diukur sepenuhnya), tujuan formula ini adalah untuk menetapkan variabel dan menunjukkan arah. Di era AI, yang langka bukan "gambar" tetapi **kerja yang dapat diverifikasi, waktu, dan agensi**. [PoArt] mengukur kelangkaan ini dan menulisnya dengan **paket bukti**.

### 🏛️ Pentingnya Konsep "Mesin"

Token yang datang dari Pump.fun atau platform serupa sering kali hanya **"tiket masuk"**. **PoArt Forensic Engine (PFE)**, bagaimanapun, adalah **lapisan logika konstitusional** yang memutuskan hak apa yang dilindungi tiket ini, bagaimana karya akan ditulis, dan bagaimana seni/sains/teknologi akan dilestarikan.

> **Catatan:** Alasan kami memulai proyek ini di Pumpfun adalah karena kekurangan dana yang cukup dan tidak adanya lingkungan untuk menjangkau audiens saat ini melalui siaran langsung. Penggunaan data saat ini adalah langkah yang benar secara strategis, meskipun bukan kualitas tertinggi. Terlepas dari anggaran dan sumber daya, mendefinisikan logika mesin ini di GitHub membuktikan bahwa proyek ini bukan hanya evaluasi keuangan, tetapi visi jangka panjang dari **infrastruktur perangkat lunak** dan **perpustakaan digital nasional**.

---

## 🎨 Protokol [PoArt] Bukti Kerja (Proof of Art Protocol v1.0)

> **"Seniman sejati, produksi sejati, nilai sejati."**

Protokol ini adalah **proses perlindungan biologis dan intelektual** yang dikembangkan melawan penipu anonim yang mengelilingi ekosistem kripto, melawan gambar AI yang dibuat dalam 5 menit, dan melawan budaya "Pump & Dump".

---

## a) Apa itu [PoArt]? (Definisi Filosofis dan Teknis)

**Bukti Seni [PoArt];** adalah standar sertifikasi institusional yang menjamin bahwa nilai di balik aset di blockchain tidak berdasarkan estimasi, tetapi pada **kerja manusia**, **waktu**, dan **energi fisik yang dapat diverifikasi**.

Bitcoin *"dengan listrik dan daya prosesor"* **(bukti kerja)** menghasilkan nilai, demikian pula proyek yang terhubung dengan [PoArt] *"dengan keterampilan artistik dan waktu manusia"* menghasilkan nilai.

Ini menghilangkan risiko *"Developer menjual, proyek berakhir"* di platform Pump.fun dan DEX; karena di sini nilai bukan di kode tetapi di **kontinuitas produksi**.

> **[PoArt] tidak mengatakan kepada peserta "percayalah pada kami"; ia mengatakan "ini buktinya, lihat dengan mata Anda sendiri, verifikasi dengan matematika Anda."**

---

## b) Standar 5-Pilar [PoArt] (5 Pilar Kebenaran)

5 item ini adalah filter yang tidak dapat diubah yang harus dilalui proyek untuk menerima segel [PoArt].

### 1) Bukti Identitas Langsung

- **Masalah:** Dunia kripto penuh dengan pendiri anonim (Devs) dengan identitas yang tidak jelas yang mengumpulkan uang dan meninggalkan proyek.
- **Solusi [PoArt]:** Pencipta tidak hanya memverifikasi identitas tetapi juga **kehadiran selama produksi**. Ini termasuk sesi siaran langsung di mana percakapan dengan komunitas dilakukan dan permintaan spesifik diterapkan segera, bukan video yang direkam sebelumnya.  
  (Misalnya, *"Tulis tanggal hari ini dan nomor blok saat ini di sudut kanan kanvas"*)
- **Slogan:** *"Bot bisa menggambar tetapi bot tidak berkeringat dan tidak bisa berimprovisasi."*

### 2) Bukti Kerja dan Proses

- **Masalah:** Gambar AI (kecerdasan buatan) yang dibuat dalam 2 detik menerima perlakuan "jpeg" yang sama di dunia digital dengan lukisan minyak yang dibuat dalam 2 bulan.
- **Solusi [PoArt]:** Proses "kehamilan dan kelahiran" karya ditulis. Tahap sketsa, tahap lukisan, jam yang dikumpulkan yang dihabiskan, dan proses fisik yang dialami seniman saat membuat karya ditulis. Ini menambahkan **"harga waktu"** ke token. Produksi aset sulit, nilainya kuat.

### 3) Bukti Nilai Estetika

- **Masalah:** Budaya "meme" yang hanya fokus pada tawa instan sementara keindahan dan kedalaman artistik diabaikan, yang merupakan alasan proyek "Hype" jangka pendek.
- **Solusi [PoArt]:** Proyek harus memiliki standar seni akademik, teori warna, aturan komposisi, dan pengetahuan material (Impasto, Texture, dll.). Konten tidak hanya harus membuat Anda tertawa; itu harus menciptakan kekaguman pada pemirsa dan memiliki **nilai koleksi**.

### 4) Inovasi Konseptual

- **Masalah:** Ribuan salinan token anjing/kucing tanpa kreativitas.
- **Solusi [PoArt]:** Proyek harus menciptakan jembatan baru yang menghubungkan seni, sains, filsafat, atau teknologi dalam struktur yang bermakna.  
  (Misalnya, menghubungkan patung Daud kuno dengan data pasar kripto; memproses ide "transformasi manusia menjadi batu" melalui ini dan mendasarkannya dengan sumber ilmiah.)  
  Karya tidak hanya harus menjadi undangan visual tetapi juga **tantangan intelektual** yang merangsang pemikiran tentang sains, filsafat, atau teknologi.

> [!IMPORTANT]
> **Contoh Tak Terlupakan (Efek Las Palmitas):** Di wilayah Las Palmitas di Meksiko, yang menderita kejahatan, lebih dari 200 rumah berubah menjadi pameran pelangi raksasa. Sebagai hasil dari intervensi keindahan ini, tingkat kejahatan di wilayah tersebut menurun secara signifikan, dan kaum muda mulai berpartisipasi dalam seni alih-alih geng kriminal. Transformasi keindahan menulis ulang rasa hormat orang terhadap lingkungan dan satu sama lain (integrasi sosial).
>
> **Harapan:** Proyek yang masuk ke daftar [PoArt] harus, seperti contoh di atas, memiliki hubungan sebab-akibat sosial, ilmiah, atau filosofis di luar keindahan visual. Waktu adalah satu-satunya modal yang tidak dapat dibeli dengan uang oleh karena itu, dalam protokol ini harus diverifikasi dengan menempatkan waktu sebagai jaminan. Dasar konseptual proyek harus begitu kuat dan universal sehingga, bahkan bertahun-tahun kemudian, dalam situasi CTO (Community Takeover) yang mungkin, komunitas dapat melanjutkan kapasitas kreatif proyek secara independen sambil mewarisi warisan ini.

### 5) Bukan Algoritmik tapi Agensi

- **Masalah:** Produksi digital berulang yang sempurna tetapi tanpa jiwa.
- **Solusi [PoArt]:** Agensi unik manusia yang dapat membuat kesalahan, mengambil risiko, dan mengalami perubahan emosional harus dirasakan dalam karya. Ketidakpastian dalam sapuan kuas, reaksi mendadak material, dan keputusan segera seniman adalah **tanda tangan biologis** yang membedakan karya dari "produksi mekanis".

---

## c) Proses Verifikasi dan Pencegahan Penipuan

Sistem ini memastikan bahwa proyek tetap dapat dipercaya dan hidup tidak hanya "di awal" tetapi "selalu".

### 📦 Paket Bukti - Kembar Digital

Di balik setiap karya yang disetujui oleh [PoArt] ada paket data terenkripsi dan diberi stempel waktu yang dapat diunduh investor:

- **Rekaman Video RAW:** Film mentah berkelanjutan dari waktu produksi.
- **Analisis Metadata:** Tanggal pembuatan file, informasi tentang alat yang digunakan, dan data lokasi.
- **Referensi Fisik:** Bukti bahwa karya ada di dunia fisik  
  (Misalnya, koran saat ini atau data blockchain dari waktu itu di samping karya).

> *Catatan Kepatuhan:* Istilah "paket bukti" di bagian sebelumnya terhubung dengan rantai **paket bukti → EvidenceRoot → NotarySeal**; yaitu, integritas paket diwakili oleh segel yang dapat diverifikasi.

### 🔄 Perpanjangan 365 Hari (Protokol Keberlanjutan)

- **Fitur Revolusioner:** Dalam proyek kripto "Dev" (Developer) biasanya menerbitkan token dan biasanya menghilang setelah 1-2 bulan (soft rug). [PoArt] membuat ini tidak mungkin.
- **Aturan:** Status "seniman terverifikasi" bukan seumur hidup. Hanya **1 tahun** berlaku.
- **Operasi:** Seniman/developer harus mempresentasikan **karya baru yang signifikan dan dapat diverifikasi** kepada komunitas setiap 365 hari.
- **Contoh Skenario:** Memulai proyek pada 2026. Pada Januari 2027, sistem memberikan peringatan "bukti kedaluwarsa". Jika seniman tidak mempresentasikan pameran baru, karya fisik baru, atau integrasi teknis baru maka "lencana kepercayaan" proyek turun.
- **Hasil:** Sistem ini memastikan **konten tidak pernah kehilangan relevansi** dan investor tidak pernah takut *"Apakah Developer masih di sini?"*. Proyek menjadi studio yang hidup.

### 🚩 Protokol Bendera Merah

**Dalam setiap situasi penipuan yang terdeteksi oleh komunitas atau algoritma (penggunaan AI, karya yang dicuri, video yang dimanipulasi):**

1. Sertifikat segera ditandai sebagai **"VOID" (batal)**.
2. Paket bukti ditandai secara publik sebagai **"palsu"**.
3. Proyek ditempatkan di daftar hitam [PoArt]. Ini di dunia terdesentralisasi, **reputasi adalah mata uang** memperkuat.

---

## d) Kesimpulan: Bukan Kasino, tapi Museum

**Pump.fun dan bursa terdesentralisasi (DEX) sayangnya sekarang adalah kasino; lampu berkedip, semua orang mengejar keuntungan cepat, dan rumah (penipu) selalu menang. Alasan kami memulai proyek ini di sini adalah karena kekurangan dana yang cukup dan tidak adanya lingkungan untuk menjangkau audiens saat ini melalui siaran langsung.**

**[PoArt] adalah benteng yang dibangun di tengah kasino ini.**

- 🎰 Kasino berbasis permainan kartu; kami **berbasis realitas fisik**.
- 🃏 Kasino terbuka untuk penipuan; kami **terbuka untuk bukti yang jelas**.
- ⏳ Kasino bersifat sementara; kami **fokus pada keabadian seni dan sains**.

**Token yang menggunakan protokol ini bukan hanya "koin"; ini adalah modal digital dengan keringat, warna, kode, dan visi.**

---

## 🗳️ 6) Tata Kelola dan Registri Publik

**Tujuan bagian ini: Mengubah standar [PoArt] dari tingkat "kepercayaan pada orang" menjadi infrastruktur publik berkelanjutan dengan registri + verifikasi + pengawasan komunitas.**

### 6.1 Registri Publik

- **Registri Publik:** Semua data yang disetujui ditulis di `ilhanart.org/registry` (atau GitHub Registry).

**Logika Registri (standar yang diusulkan - dalam format jalur JSON):**

Setiap entri yang masuk ke registri memiliki bidang inti minimum yang dapat diverifikasi ini:

- **Identitas dan Status:**
  - `certificate_id` (referensi yang dapat dibaca)
  - `status` (active / void)
  - `void_reason` (jika berlaku)
  - `visibility` (private / masked / public)
  - `created_at` (stempel waktu)

- **Otoritas Penerbit:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informasi Karya:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (jika memungkinkan; untuk identifikasi dengan gerbang token)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Data Forensik:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Bukti Kriptografi:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Tata Kelola:**
  - `governance.decision`
  - `governance.veto_threshold`

Registri dapat memiliki dua tingkat:
- **1)** Indeks yang dapat dibaca manusia (daftar web / pencarian / filter)
- **2)** Representasi yang dapat dibaca mesin (catatan JSON; untuk verifikasi PFE)

**"Pendaftaran" ini menjadi dapat diverifikasi melalui rantai PFE paket bukti → EvidenceRoot → NotarySeal. Registri menyediakan target verifikasi, bukan "klaim".**

---

### 6.2 Veto Komunitas 40% (Tata Kelola Gerbang-Token)

- **Veto Komunitas 40%:** Pemungutan suara dimulai satu bulan sebelum pemberian status; **40% komunitas gerbang-token (diverifikasi dengan Solana)** veto membatalkan aplikasi.

**Alur Pemungutan Suara (proses yang jelas yang diusulkan):**
- **Jendela Aplikasi:** Proyek kandidat membuka "pendaftaran kandidat PoArt" (catatan kandidat muncul dengan status "pending").
- **Periode Peninjauan:** Komunitas meninjau bukti hingga 30 hari (paket bukti + catatan siaran langsung + metadata).
- **Verifikasi Gerbang-Token:** Pemungutan suara dilakukan dengan dompet Solana yang diverifikasi (misalnya kepemilikan token/NFT tertentu + tanda tangan dompet).
- **Aturan Veto:** Jika 40% suara adalah **oposisi (tidak / veto)** maka aplikasi dibatalkan.
- **Transparansi:** Hasil pemungutan suara disimpan di registri sebagai "catatan keputusan" (tanggal, rasio, ID gambar).

---

### 6.3 Sinkronisasi Metadata (Keselarasan dengan Dunia Fisik)

- **Sinkronisasi Metadata:** Data teknis di registri harus cocok 100% dengan entitas fisik.

**Definisi Teknis "100% Keselarasan" (transparansi yang diusulkan):**
- **Keselarasan Minimum (wajib):**
  - `asset.fingerprints.sha256/sha512` di registri harus **identik** dengan hash file yang dibahas.
  - `proof.notary_seal` di registri yang dibuat ulang (jika paket bukti ada), harus **identik**.
- **Keselarasan Referensi Fisik (jenis bukti):**
  - Karya fisik + tanggal/referensi blok yang ditampilkan dalam siaran langsung dan bukti yang sama harus cocok dengan paket bukti.
- **Kepatuhan Privasi:**
  - Bidang seperti IP/lokasi dalam visibilitas `masked` dipublikasikan **sesuai standar masking**.

---

### 6.4 Sengketa dan Pembatalan

Registri bukan hanya proses "persetujuan"; ini adalah **proses peninjauan hidup** melawan penipuan.

- Ketika sengketa dimulai, entri dapat ditempatkan dalam status **"review" (peninjauan)**.
- Ketika penipuan terdeteksi, ditandai sebagai `status: void` dan alasan ditambahkan:
  - `void_reason` (penggunaan AI / pencurian / manipulasi, dll.)
  - `revoked_at` (waktu pembatalan)
- Sumber keputusan pembatalan jelas di registri:
  - Pemungutan suara komunitas / komite resmi / catatan investigasi ilmiah (berlaku)

> **Bagian ini adalah kembar registri dari konsep VOID di bagian "Protokol Bendera Merah".**

---

### 6.5 Contoh Entri Registri (dapat dibaca mesin)
```json
{
  "certificate_id": "POART-AB12CD34",
  "status": "active",
  "visibility": "masked",
  "created_at": "2026-01-09T12:34:56.000Z",
  "issuer": {
    "name": "Ilhan Art Gallery",
    "location": "Istanbul / Besiktas",
    "attestation_pubkey": "PFE_ATTEST_PUBKEY_BASE58..."
  },
  "asset": {
    "title": "Untitled",
    "creator": "Anonymous",
    "fingerprints": {
      "sha256": "e4123f83b44a409d7a43f0897837876dfabb3320db63dadbb34c54281f38a6ba",
      "sha512": "41e5e0d007a2a77b6e0e3ebc548fbaa2788ea265193434f58d23e8c0f5bb20a0835aa850edbadbd8341969cf743fc69fa951f7ed275901fefe0fe7eb1fb83099"
    }
  },
  "forensics": {
    "ip_masked": "46.1.***.***",
    "device": "Brave (Windows;Monster,Tulpar)...",
    "location": "***/TR",
    "timestamp": "2026-01-09T12:34:56.000Z"
  },
  "proof": {
    "evidence_root": "7f8a9b2c3d4e5f6a7b8c9d0e1f2a3b4c...",
    "signer_sig": "PFE_ATTEST_SIG_BASE64...",
    "notary_seal": "9d3e5a1f2b3c4d5e6f7a8b9c0d1e2f3a..."
  },
  "governance": {
    "decision": "approved",
    "veto_threshold": 0.40
  }
}
```
> *Catatan: `asset.fingerprints.sha512` dan nilai hash lainnya disingkat untuk tujuan tampilan; dalam implementasi aktual, string heksadesimal panjang penuh digunakan.*

---

## 7) 🔐 Segel Teknis (NOTARY SEAL)

**Algoritma segel tidak dapat diubah yang dihasilkan oleh PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Protokol [PoArt] Notaris Digital dan Bukti Ilmiah (Beta v1.0)

> **"Budaya lebih besar dari modal. Lindungi karya Anda hari ini, transfer besok."**

---

## Mengapa Publik?

Keamanan sejati berasal dari transparansi. Berkat sistem **registri publik** kami, siapa pun di mana pun di dunia dapat memverifikasi dalam hitungan detik apakah file itu asli, tanpa memerlukan otoritas.

---

## 🧩 Mengapa Beberapa "Modul Visibilitas"?

Ini adalah bagian paling penting dari kode (menu opsi visibilitas). Opsi ini memungkinkan pengguna untuk membuat keseimbangan dalam **"privasi vs transparansi"**:

### 🔒 Pribadi

- **Skenario:** Seniman belum ingin mempublikasikan karya, tetapi ingin memberi stempel waktu untuk membuktikan "Saya melakukan ini pada tanggal ini".
- **Apa yang dilakukan kode:** Menulis data ke database tetapi menandai segel sebagai `visibility: "private"`. Nanti ketika Anda menulis kebijakan "baca publik", Anda dapat menyembunyikan catatan ini dari orang dengan `WHERE visibility = 'public'`.

### 🕶️ Bertopeng

- **Skenario:** Seniman menginginkan transparansi tetapi khawatir alamat rumahnya (lokasi IP) akan diketahui.
- **Apa yang dilakukan kode:** Fungsi `maskIP` dan `maskLoc` bekerja di sisi JavaScript. Ini mengubah alamat IP ke format `88.241.***.***`, lokasi ke format `***/TR`, dan mengirim versi yang disensor ke database.
- **Kebenaran Privasi:** Masking dilakukan di browser, Supabase tidak melihat lokasi sebenarnya. **Tetapi:** Jika API pihak ketiga seperti ipapi.co digunakan untuk data lokasi, penyedia ini melihat alamat IP pada saat permintaan.
- **Penyegelan dalam Mode Bertopeng:** Perhitungan EvidenceRoot dan NotarySeal dilakukan dengan data forensik bertopeng; oleh karena itu verifikasi tetap deterministik.

### 🌍 Publik

- **Skenario:** Transparansi penuh. Menurut standar [PoArt], di mana, kapan, dari jaringan mana karya dibuat dinyatakan secara publik.

---

## 💡 Inovasi Teknis

PoArt bukan hanya sistem unggah file. Ini adalah mesin **"rantai perawatan ilmiah"** yang mencampur tiga tingkat teknis berbeda dalam satu panci untuk membawa standar baru.

**Lapisan yang dijelaskan sebagai "mesin" di bagian ini sesuai dengan inti PoArt Forensic Engine (PFE) dalam istilah sebelumnya.**

### 1) Hashing Sisi-Klien (Privasi Maksimum)

File potongan seni Anda tidak diunggah ke server. Mesin berbasis browser (sisi-klien) kami menghitung hash file (ringkasan digital) di komputer Anda sendiri. Hanya sidik jari digital ini dan metadata yang dikirim ke server.

> **Kebenaran Privasi:** File karya tidak diunggah ke server dan dengan demikian aman. Namun, data forensik (IP/lokasi) dibagikan sesuai dengan mode visibilitas yang dipilih (pribadi/bertopeng/publik).

### 2) Fusi Data Forensik (Kekuatan Ilmiah)

Lebih dari stempel waktu sederhana. Sistem menghubungkan data ini dalam "segel akar":

- **Ringkasan Digital (SHA-512):** Sidik jari digital menggunakan standar ringkasan kriptografi (SHA-512) yang rusak jika satu piksel karya berubah.
- **Lokasi dan Waktu:** Mengkodekan data tanggal, negara, kota, dan wilayah dengan presisi milidetik.
- **Identifikasi Perangkat:** Sistem operasi, browser, dan jenis perangkat (analisis User-Agent).

---

## 🛡️ Kasus Penggunaan dan Manfaat

Jika Anda seorang seniman, penulis, atau desainer, mengatakan "Saya melakukan ini pertama kali" tidak cukup; Anda harus membuktikan.

**Karya Anda yang disegel dengan PoArt:**

- **Bukti Matematis:** Jika bahkan satu piksel file Anda berubah, sistem mengetahui. Manipulasi tidak mungkin.
- **Dasar Hukum:** Ditulis pada tanggal berapa, di kota mana, dari perangkat mana karya disegel.
- **Sertifikat Instan:** Menghasilkan **"sertifikat identitas aset"** khusus, kode QR, dan segel untuk Anda dalam hitungan detik.

---

## ⚙️ Arsitektur Sistem dan Fitur Teknis

Sistem dirancang pada arsitektur "serverless", dengan fokus pada kinerja tinggi dan skalabilitas.

| Lapisan | Teknologi | Deskripsi |
|--------|-----------|-------------|
| **Enkripsi** | SHA-256 & SHA-512 | Ringkasan kriptografi dua lapis |
| **Basis Data** | Supabase (PostgreSQL) | Struktur data JSONB, kebijakan RLS |
| **Data Forensik** | ipapi.co API | Segitiga IP/lokasi/waktu |
| **Presentasi** | html2canvas + jsPDF | Pembuatan PNG/PDF sisi-klien |
| **Frontend** | Vanilla JavaScript | Nol ketergantungan framework |
| **Keamanan** | Hashing Sisi-Klien | File tidak pernah ke server |

### Fitur yang Menonjol

| Fitur | Deskripsi | Di Pesaing? |
|---------|-------|-----------------|
| **UI Tarik dan Lepas** | Tarik dan lepas file, pratinjau instan | ❌ Di sebagian besar tidak ada |
| **Ekspor Multi-Format** | PNG, JSON, PDF - dengan satu klik | ⚠️ Terbatas |
| **Pratinjau Waktu Nyata** | Pratinjau sertifikat langsung | ❌ Tidak ada |
| **Kontrol Privasi** | Opsi pribadi/bertopeng/publik | ❌ Tidak ada |
| **Hash Sisi-Klien** | File tidak pernah ke server | ✅ Hanya di beberapa |
| **Metadata Forensik** | IP, lokasi, perangkat, waktu - semua bersama | ❌ Terpisah |
| **Verifikasi QR** | Verifikasi instan kode QR | ⚠️ Terbatas |
| **Pembatasan Laju** | Perlindungan spam (RLS + klien) | ❌ Di sebagian besar tidak ada |

---

## 🗺️ Peta Jalan: Masa Depan "Tanpa Kepercayaan"

Versi saat ini **(Beta v1.0)** dirancang untuk memberikan kecepatan maksimum, antarmuka mudah, dan akses gratis kepada pengguna akhir. Visi akhir kami, bagaimanapun, adalah transformasi ke struktur di mana administrator basis data (kami) bahkan tidak dapat campur tangan.

### Tahap 1: Beta (Sekarang langsung)

- **Infrastruktur:** Basis data cloud (Supabase).
- **Tujuan:** Kecepatan, penghapusan hambatan UX (pengalaman pengguna), dan kepatuhan. Memberikan keamanan "tanpa gesekan".

### 🚀 Tahap 2: (Persyaratan Backend / Edge Function)

Tahap ini melibatkan transformasi dari struktur manajemen penuh "sisi-klien" ke struktur "otoritas sisi-server" yang lebih aman dan dapat dikontrol.

| Item | Apa yang dibawa? | Stack Teknis | Prioritas |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Function** | Pencegahan spam + keamanan kunci API | Supabase Edge (Deno) | 🔴 Tinggi |
| **Tanda Tangan Dompet** | Verifikasi kriptografi | Solana Wallet Adapter | 🟡 Sedang |
| **Cadangan IPFS/Arweave** | Ketidakberubahan terdesentralisasi | IPFS SDK + Pinata | 🟢 Rendah |
| **Proses Pembatalan** | Batalkan sertifikat palsu | Pembaruan skema DB | 🔴 Tinggi |
| **Log Peninjauan** | Catatan investigasi ilmiah | Tabel catatan khusus | 🟡 Sedang |
| **OpenTimestamps** | Jangkar Bitcoin | OTS JavaScript | 🟢 Rendah |
| **Integrasi DID** | Identitas terdesentralisasi | ION/Ceramic | 🟢 Rendah |

### Tahap 3: Desentralisasi Penuh (Jangka Panjang)

| Fitur | Target | ETA |
|---------|------|-----|
| **Registri Blockchain** | Pendaftaran on-chain Ethereum/Solana | Q4 2026 |
| **Tata Kelola DAO** | Tata kelola komunitas | Q1 2027 |
| **Dukungan Multi-Rantai** | Polygon, Arbitrum, Base | Q2 2027 |
| **Pengakuan Hukum** | Validitas di pengadilan Turki | 2027-2028 |
| **API untuk Developer** | Titik akhir API publik | Q3 2026 |

---

## 📊 Analisis Pesaing (Diperbarui)

PoArt berdiri di "Sweet Spot" sambil mengisi kesenjangan solusi saat ini.

| Fitur | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Biaya** | 🆓 Gratis | 🆓 | 💰 Berbayar | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI Tarik & Lepas** | ✅ Sangat mudah | ❌ CLI | ⚠️ Sedang | ⚠️ Sedang | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Ekspor Multi-Format** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Pratinjau Real-Time** | ✅ Langsung | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Kontrol Privasi** | ✅ 3 mode | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Hash Sisi-Klien** | ✅ Privasi | ✅ | ❌ Unggah | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Metadata Forensik** | ✅ Penuh | ❌ | ❌ | ⚠️ Terbatas | ❌ | ⚠️ | ❌ | ⚠️ |
| **Verifikasi QR** | ✅ Instan | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Pembatasan Laju** | ✅ RLS+klien | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Jangkar Blockchain** | 🔄 Peta jalan | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Kode Terbuka** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Dukungan Indonesia** | ✅ Asli | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Kunci:**
- ✅ : Dukungan penuh / tersedia
- ⚠️ : Terbatas / dalam paket berbayar
- ❌ : Tidak ada / tidak didukung
- 🔄 : Dalam peta jalan (dalam pengembangan)
- 🆓 : Sepenuhnya gratis
- 💰 : Berbayar / pendaftaran diperlukan

---

**Protokol [PoArt] Bukti Seni v1.0**  
*"Budaya > Modal"*

## 🧾 Lisensi

Lisensi MIT © 2026 Ilhan Art Gallery Initiative

Untuk ketentuan lengkap lihat [![Lisensi](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE).

---

## 💬 Ucapan Terima Kasih

![Versi](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Keamanan](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![Lisensi](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Proyek ini dikembangkan oleh inisiatif [Ilhan Art Gallery], dan kode sumbernya tersedia untuk umum demi transparansi.**

**Protokol V1.0 // Disegel dengan SHA-512**

*© 2026 İLHAN ART | Semua hak dilindungi untuk karya seni, gambar, dan ide.*

---
