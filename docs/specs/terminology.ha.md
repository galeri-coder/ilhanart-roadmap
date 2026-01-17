# 📚 ƘAMUS NA KALMOMIN FASAHA & RA'AYOYI
> **"Fahimtar harshen wannan yarjejeniya, ita ce fahimtar manufarta."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Tushen Gine-ginen Fasaha

**PoArt Forensic Engine (PFE)**, shine mataki na asali wanda ke wakiltar dabarar aiki da tsarin fasaha na yarjejeniyar [PoArt]. Wannan shine "injin binciken shari'a" wanda ke canza bayanan asali na samar da fasaha zuwa **shaidar dijital** mai tabbatarwa da rashin iya canzawa.

### 🧩 Me Ya Sa "PoArt Forensic"?

- **PoArt (Proof of Art / Shaidar Fasaha):** Manufar injin ita ce danganta darajar kadarar dijital ba ga hasashe ba; sai dai ga **tsarin samarwa mai tabbatarwa**.
- **Forensic (Binciken Shari'a):**
  - **Ma'anar Fasaha:** Tsarin algorithm da silsilar rikodin da ke tabbatar da cewa bayanan da suka shafi tsarin samarwa (bugun goga, timelapse, log) ba a canza su ba.
  - **Matakin Falsafa:** Game da samar da "sakamakon nan take" na AI; **canza aikin ɗan adam wanda ya haɗa da lokaci, ƙoƙari da farashin yanke shawara** zuwa gaskiya mai aunawa.

> Lura: Haɗin blockchain (misali Solana) ba shine ainihin PFE ba; ana ɗaukarsa a matsayin **Chain Anchor Layer** daban don tabbatarwa/rijista.

### 🛠️ Ƙayyadaddun Fasaha na v1.0

**PoArt Forensic Engine (PFE) v1.0**, an gina shi akan **ginshiƙai 3 na asali** maimakon tsarin kuɗi masu rikitarwa:

1. **Hashing & Sealing (Hatimcewa):**  
   PFE yana sarrafa dukkan abubuwan da ke cikin Evidence Pack (fayilolin fasaha, bidiyo, JSON/log, sa hannu da sauransu) ta hanyar deterministic kuma yana samar da darajar **NotarySeal** ta musamman.

   **Ra'ayoyin ginshiƙi (v1.0):**
   - **FileHash (sawun yatsa na fasaha):** Hash da aka samar daga byte na fayilin fasaha.
   - **EvidenceRoot (tushen fakitin shaida):** Taƙaitaccen tushe wanda ke wakiltar dukkan Evidence Pack (Merkle root ko canonical manifest hash).
   - **NotarySeal (hatimin ƙarshe / Sakamakon PFE):** Hatimin ƙarshe da aka samar daga haɗin EvidenceRoot + lokaci + sa hannu.

   **Dabarun (an nuna wa mai zuba jari a sarari):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Ma'anonin Canonical Payload (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Lura: Darajar da ake nufi a matsayin sakamakon PFE ita ce **NotarySeal**. Za a fara amfani da tsarin **SignerSignature** a Faz 2 (tare da Solana Wallet Adapter); a halin yanzu v1.0 ana amfani da sa hannun attestation na tsarin. Ana buga maɓallin attestation a cikin rijista a filin `issuer.attestation_pubkey`.

2. **Indexing (Adana Bayanan):**  
   Yana rikodin wane walat, a wane kwanan wata, ya gabatar da **Labor Proof (Shaidar Aiki)** ga wane fasaha; cikin ɓangaren rikodin bayyane kuma mai iya bincikewa.  
   *(Wannan ɓangare na iya zama bayanai; ana ɗaukar haɗin sarkar daban a matsayin "Chain Anchor Layer".)*

3. **Verification (Tabbatarwa):**  
   Lokacin da aka tambayi sahihancin fasaha, PFE yana sake sarrafa shaidun asali; yana gwadawa da tabbacin lissafi ko darajoyin **EvidenceRoot / NotarySeal** da aka lissafa sun dace da rikodin da ke cikin tarihin.

---

### 🧮 Ka'idar Darajar PoArt (The Value Theorem)

Yarjejeniyar [PoArt] tana danganta darajar kadarar dijital ($V$) ba ga fahimtar kasuwa mai canzawa ba; sai dai ga **gaskiyar jiki na tsarin samarwa**.

AI (Artificial Intelligence), ta hanyar ba da sakamako nan take ($t \to 0$) tana lalata tsari. [PoArt] ta dauki daraja a matsayin; tarawa na **lokaci, aiki da niyya**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Ma'anonin Masu Canzawa

- **$\int dt$ (Tararrun Tsari):**  
  Daraja ba "sakamako" (output) na nan take ba ne; tsari ne mai tarawa tsakanin $t_{\text{start}}$ da $t_{\text{end}}$. Yayin da lokaci ya ragu (samarwa ta AI), sakamakon integral yana kusantar 0.

- **$P_{\text{labor}}(t)$ (Ƙarfin Aiki Na Lokacin):**  
  Yana wakiltar yawan ƙoƙarin tunani da na jiki da aka kashe a lokacin samarwa. Yayin da ƙoƙari mai tabbatarwa ya ƙaru, integrand yana ƙaruwa.  
  > Lura: Ana iya daidaita wannan magana ta hanyar "siginar aiki mai aunawa/tabbatarwa" a aikace.

- **$I_{\text{agency}}(t)$ (Masu Niyya):**  
  Ƙarfin mai samarwa na ɗaukar haɗari da yanke shawara. Yana ɗaukar daraja tsakanin $0$ da $1$.
  - **AI ($I \approx 0$):** Yana aiwatar da umarni, ba ya ɗaukar haɗari, ba ya biyan farashi.
  - **Ɗan adam ($I \to 1$):** Yana canza shawara, yana jira, yana ɗaukar haɗari.

- **$U_{\text{irreversible}}$ (Keɓantaccen Rashin Iya Komawa):**  
  A samarwa ta dijital ana iya komawa (`Ctrl+Z`); amma a samarwa ta jiki (fenti da aka shafa a kan zane, dutse da aka sassaƙa, alamar yanayi a cikin watsawa kai tsaye) babu komawa. Wannan **rashin iya komawa**, shi ne karin magana wanda ke haifar da "keɓantacce" (hali na non-fungible) a cikin fasaha.

### 🔎 Nazarin Lamari: AI "Sakamakon Nan Take" vs. Ɗan Adam "Tsarin Tabbatacce"

Wannan yanayin yana nuna yadda **Ka'idar Darajar PoArt** ke aiki a aikace da kuma dalilin da ya sa samar da AI ke samun ƙaramin maki a cikin ma'aunin [PoArt].

#### Yanayi A: Samar da Hoto tare da AI cikin Daƙiƙa 10

- **Lokaci ($\Delta t$):** Daƙiƙa $10$ (kusan babu tsari)
- **Ƙarfin Aiki ($P_{\text{labor}}$):** Raka'a $1$ (kawai rubuta umarni)
- **Masu Niyya ($I_{\text{agency}}$):** $0.01$ (babu haɗari, babu farashi)
- **Rashin Iya Komawa ($U_{\text{irreversible}}$):** $0$ (ana iya komawa / ana iya kwafi)

**Sakamako:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Sharhi:** Ko da sakamakon ya cika kyau; saboda babu tsari kuma babu niyya/haɗari, darajar [PoArt] tana kusantar $0$.

#### Yanayi B: Samarwa ta Jiki ta Sa'o'i 6 a Watsawa Kai Tsaye

- **Lokaci ($\Delta t$):** Sa'o'i $6$ (daƙiƙa $21{,}600$)
- **Ƙarfin Aiki ($P_{\text{labor}}$):** Raka'a $0.5$ (dawwamammen ƙoƙarin jiki da na tunani)
- **Masu Niyya ($I_{\text{agency}}$):** $0.9$ (canza shawara, ɗaukar haɗari, zaɓuɓɓuka marasa komawa)
- **Rashin Iya Komawa ($U_{\text{irreversible}}$):** $>0$ (ba za a iya komawa alamun jiki ba)

**Sakamako:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Sharhi:** Yayin da tsari ya tsawaita kuma niyya (haɗari) ya ƙaru, daraja tana ƙaruwa a tarare. Maganar $U_{\text{irreversible}}$ ita ce ƙarin gudummawa wanda ke haifar da "keɓantacce" (hali na non-fungible) a cikin fasaha.

---

### ✅ Ƙarshe: Ɗaure Daraja da Shaida (Proof-Bound Value)

Wannan ka'ida tana cire da'awar darajar [PoArt] daga zama "so" ko "labarin kasuwa" kuma tana haɗa ta da **gaskiyar samarwa mai tabbatarwa**.

1. **Babu Daraja Ba Tare da Tsari Ba:**  
   AI, tana lalata tsari a sakamakon nan take ($t \to 0$). Yayin da tagogin tsari ya ragu, sakamakon integral yana raguwa ta tilas:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Niyya da Haɗari Sune Masu Ninkawa:**  
   [PoArt] ba kawai tana auna "lokacin da aka kashe" ba; tana kuma auna matakin shawara na ainihi, haɗari da farashi a cikin wannan lokacin. Darajar samarwa mara ɗaukar haɗari (AI) ƙanƙantar da ita:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Keɓantacce, Ba Talla Ba Ne Shaida ta Jiki:**  
   A samarwa ta jiki, alamun da ba za a iya komawa ba (bugun zane, fashewar dutse), sun wuce dabara ta dijital na `Ctrl+Z`. Wannan rashin iya komawa ($U_{\text{irreversible}}$), yana sa fasaha ta zama keɓantacciya ta hanyar kasancewa.

> **🔐 TAƘAITAWA:** Ko da ka'idar daraja ta yi kama da rashin tabbas a matsayin aunawa (ko da kuwa ba za a iya aunawa %100 a rayuwar ainihi ba), manufar wannan dabara ita ce nuna tsarin da alkiblar masu canzawa. Abin da ke da wuya a zamanin AI ba "hoto" ba ne; **aiki, lokaci da niyya mai tabbatarwa**. [PoArt] tana auna wannan ƙarancin kuma tana yi masa rijista da **Evidence Pack**.

### 🏛️ Mahimmancin Ra'ayin "Engine" (Injin)

Token da ke fitowa daga dandamali kamar Pump.fun, yawancin lokaci kawai **"tikiti na shiga"** ne. **PoArt Forensic Engine (PFE)** shine **matakin dabara na tsarin mulki** wanda ke ƙayyade wane haƙƙoƙi wannan tikiti take karewa, yadda za a rikodin aiki da kuma yadda za a dawwama fasaha/kimiyya/fasaha.

> **Lura:** Dalilin da ya sa muka fara wannan aikin a Pump.fun shi ne saboda ba mu da isasshen kuɗin ruwa da isassun mabiya. Ko da amfani da bayanan da ake da su ba shine mafi kyawun dabara ba, za mu iya cewa shine mafi kyawun matakin. Ba tare da la'akari da kasafin kuɗi da damar ba, bayyana dabarar wannan injin a GitHub, yana tabbatar da cewa aikin ba kawai hasashe na kuɗi ba ne, amma **gine-ginen software na dogon lokaci** da hangen nesa na **ɗakin karatu na dijital na ƙasa**.

---

## 🎨 YARJEJENIYAR SHAIDAR AIKI TA [PoArt] (Proof of Art Protocol v1.0)

> **"Mai Fasaha na Ainihi, Samarwa ta Ainihi, Daraja ta Ainihi."**

Wannan yarjejeniya; tsarin kariya ne na **halittu da hankali** da aka tsara don yaƙi da masu zamba marasa suna da ke mamaye yanayin crypto, hotunan AI da aka samar cikin mintuna 5 da al'adar "Pump & Dump".

---

## a) Menene [PoArt]? (Ma'anar Falsafa da Fasaha)

**Proof of Art [PoArt];** tsarin tabbatarwa na hukuma ne wanda ke tabbatar da cewa darajar kadarar da ke kan blockchain ta dogara ne kan **aikin ɗan adam mai tabbatarwa**, **lokaci** da **makamashin jiki**, ba hasashe ba.

Kamar yadda Bitcoin ke samar da daraja tare da *"Wutar Lantarki da Ƙarfin Na'ura"* **(Proof of Work)**; ayyukan da suka dace da [PoArt] kuma suna samar da daraja tare da *"Basira da Lokacin Ɗan Adam da Aka Kashe"*. Tana "Stake" lokaci.

Tana kawar da haɗarin *"Mai tsara shirye-shirye (Dev) ya sayar, aikin ya ƙare"* a dandamali na Pump.fun da DEX; saboda a nan darajar ba ta cikin lambar ba, tana cikin **dawwamammen samarwa**.

> **[PoArt] ba ta ce wa mai shiga "Ka dogara da mu" ba; tana cewa "Ga shaidun, duba da idanunka, tabbatar da lissafinka".**

---

## b) Ma'aunin [PoArt] na 5 (The 5 Pillars of Truth)

Waɗannan sharuɗɗa 5 su ne tacewa marasa iya sarrafa waɗanda dole aikin ya wuce don samun hatimin [PoArt].

### 1) Shaidar Asali ta Kai Tsaye (Live Identity Proof)

- **Matsala:** Duniyar crypto cike take da wadanda suka kafa marasa suna (Devs) waɗanda suka tattara kuɗi kuma suka bar aikin.
- **Maganin [PoArt]:** Mai samarwa, ba kawai katunan shaida ba, yana tabbatar da **kasancewarsa a lokacin samarwa**. Wannan ya haɗa da zaman watsawa kai tsaye inda ake hulɗa da al'umma kuma ana cika buƙatun nan take na musamman, ba bidiyon da aka riga aka yi rikodin su ba.  
  (Misali: *"Rubuta kwanan yau da lambar block na yanzu a kusurwar dama na zane"*)
- **Taken:** *"Robots na iya yin zane amma robots ba sa gumi kuma ba sa iya yin abubuwa nan take."*

### 2) Shaidar Aiki & Tsari (Labor & Process Proof)

- **Matsala:** Hotunan AI da aka samar cikin daƙiƙa 2 da fentin mai da aka yi cikin watanni 2 suna karɓar magani iri ɗaya na "jpeg" a duniyar dijital.
- **Maganin [PoArt]:** Ana yin rikodin tsarin "ciki da haihuwa" na fasaha. Ana rubuta matakan zane, yaduddukan fenti, sa'o'in tarawa da aka kashe da kuma tsarin jiki da mai fasaha ya shiga yayin ƙirƙirar wannan fasahar. Wannan yana ƙara **"Farashin Lokaci" (Time Cost)** ga token. Mafi wahalar samar da kadara, mafi ƙarfin darajarta.

### 3) Shaidar Darajar Kyau (Aesthetic Value Proof)

- **Matsala:** Al'adar "Meme" da ke watsi da kyau da zurfin fasaha kuma kawai ta mai da hankali kan ban dariya na nan take da kuma ayyukan "Hype" masu ɗan gajeren lokaci da ya haifar.
- **Maganin [PoArt]:** Aikin dole ya sami ma'aunin fasaha na ilimi, ka'idar launi, ƙa'idodin tsari da ilimin kayan aiki (Impasto, Texture da sauransu). Abun ciki bai kamata ya sa dariya kawai ba; ya kamata ya tayar da sha'awa a cikin masu kallo kuma ya kasance da **darajar tarin**.

### 4) Ƙirƙira ta Ra'ayi (Conceptual Novelty)

- **Matsala:** Dubunnan coins na kare/kyanwa waɗanda ke kwafi juna, masu nisa da ƙirƙira.
- **Maganin [PoArt]:** Aikin dole ya gina sabon gada wanda ke haɗa fasaha, kimiyya, falsafa ko fasaha a cikin tsari mai ma'ana.  
  (Misali: Haɗa mutum-mutumin Dauda na gargajiya da bayanan kasuwancin crypto; aiki akan ra'ayin "juya fahimtar ɗan adam zuwa dutse" da kuma iya kafa wannan akan tushen kimiyya.)  
  Fasahar, ba kawai biki na gani ba; ya kamata ta zama ƙalubale na hankali wanda ke sa tunani game da **Kimiyya, Falsafa ko Fasaha**.

> [!IMPORTANT]
> **Misalin Tunani (Tasirin Las Palmitas):**  
> A unguwar Las Palmitas ta Mexico da ke fama da laifi, an canza gidaje fiye da 200 zuwa bikin bakan gizo mai girma. Bayan wannan tsoma bakin kyau, ƙimar laifi a unguwar ta ragu a wani ƙayyadadden adadin, kuma matasa sun fara sha'awar fasaha maimakon ƙungiyoyin masu laifi. Canjin kyau, ya sake shirya girmama mutane ga yanayi da juna (Social Cohesion).
>
> **Tsammani:** Aikin da zai shiga jerin [PoArt]; kamar misalin da ke sama, ya kamata ya ƙunshi alaƙar sanadin-sakamako na zamantakewa, kimiyya ko falsafa fiye da kyawun gani kawai. Tun da "Lokaci" shine kawai kadara da ba za a iya saya da kuɗi ba, ya kamata a stake lokaci a matsayin garanti kuma a tabbatar a cikin wannan yarjejeniya. Tushen ra'ayi na aikin ya kamata ya zama mai ƙarfi da duniya sosai cewa; ko a cikin yanayin CTO (Community Take Over) a nan gaba, al'umma za ta iya ɗaukar wannan gado kuma ta ci gaba da ƙarfin ƙirƙira na aikin ta hanya mai cin gashin kai.

### 5) Niyya Mara Algorithm (Non-Algorithmic Agency)

- **Matsala:** Samarwa ta dijital cikakkiya amma mara rai, masu maimaita juna.
- **Maganin [PoArt]:** Niyya ta musamman ta ɗan adam wanda zai iya yin kuskure, ɗaukar haɗari da fuskantar girgizar motsin zuciya ya kamata a ji a cikin fasaha. Rashin tabbas a cikin bugun goga, martanin abubuwan da ba a yi tsammani ba na kayan aiki da yanke shawarar nan take na mai fasaha, shine **Sa hannun Halittu** wanda ke raba fasaha daga "Samarwa ta Na'ura".

---

## c) Tsarin Tabbatarwa & Kariya daga Jabu

Wannan tsarin yana tabbatar da cewa aikin ba kawai "a farko" ba ne da ya kasance abin dogaro da rai, amma "har abada".

### 📦 Fakitin Shaida (Evidence Pack - The Digital Twin)

A bayan kowane fasaha mai takaddun shaida na [PoArt], akwai fakitin bayanan da aka ɓoye kuma aka yi masa alamar lokaci wanda masu zuba jari za su iya saukewa:

- **RAW Video Recordings:** Hotunan asali marasa yankewa na lokacin samarwa.
- **Metadata Analysis:** Kwanan ƙirƙirar fayil, bayanan na'urar da aka yi amfani da ita da bayanan wuri (Birni-Ƙasa).
- **Physical References:** Shaidun cewa fasahar tana wanzuwa a duniyar jiki  
  (Misali: Jaridar yau ko bayanan blockchain na lokacin tsaye kusa da fasaha).

> *Lura na daidaituwa:* Kalmar "fakitin shaida" tana haɗuwa da layin **Evidence Pack → EvidenceRoot → NotarySeal** a sassan da suka gabata; wato ana wakiltar dukkan fakitin da hatimi mai tabbatarwa.

### 🔄 Sabuntawa na Kwanaki 365 (The Sustainability Protocol)

- **Fasalin Juyin Halitta:** A ayyukan crypto "Dev" (Mai Tsarawa) yakan saki token a kasuwa kuma yawancin lokaci yana ɓacewa bayan watanni 1-2 (Soft Rug). [PoArt] tana sa wannan ya zama ba zai yiwu ba.
- **Ka'ida:** Matsayin "Verified Artist" (Mai Fasaha da Aka Tabbatar) ba har abada ba ne. Yana aiki **shekara 1** kawai.
- **Yadda Ake Aiki:** Dole ne mai fasaha/mai tsarawa ya gabatar ga al'umma **sabuwar babbar fasaha mai tabbatarwa** kowane kwanaki 365.
- **Misalin Yanayi:** Kun fara aikin a 2026. A watan Janairu 2027 tsarin yana ba da gargaɗi na "Lokacin Shaida Ya Ƙare". Idan mai fasaha bai gabatar da sabuwar nunawa, sabuwar fasaha ta jiki ko sabuwar haɗin fasaha ba, "Alamar Amincewa" ta aikin tana faɗuwa.
- **Sakamako:** Wannan tsarin yana tabbatar da cewa **abun ciki bai taɓa zama tsoho ba** kuma mai zuba jari ba ya fuskantar tsoron *"Shin mai tsarawa har yanzu yana nan?"*. Aikin ya zama studio mai rai.

### 🚩 Alamar Ja (Red Flag Protocol)

**A yanayin da al'umma ko algorithms suka gano duk wani zamba (amfani da AI, fasaha da aka sata, bidiyo da aka sarrafa):**

1. Takaddar nan da nan ana yi mata alamar **"SOKE" (VOID)**.
2. Ana yi wa fakitin shaida alamar **"Karya"** a fili.
3. Ana saka aikin a cikin jerin baƙin [PoArt]. Wannan yana ƙarfafa gaskiyar cewa **suna shine kaɗai kuɗin** a duniyar da ba ta da tsakiya.
4. Ba za a iya ambaton furucin [PoArt] a kowane watsa labaru ba, tushe guda ɗaya mai inganci shine https://www.ilhanart.org/public-registry

---

## d) Ƙarshe: Gidan Kayan Tarihi, Ba Gidan Caca Ba

**Pump.fun da Kasuwancin Da Ba Su Da Tsakiya (DEX) a halin yanzu abin takaici gidajen caca ne; fitilun suna yi ta haske, kowa yana neman samun kuɗi cikin sauri kuma gidan (masu zamba) kullum yana cin nasara. Dalilin da ya sa muka fara aikin a nan shi ne kuma saboda muna ƙoƙarin inganta nan kuma saboda muna da data da za mu iya amfani da ita don isa ga masu sauraro na yanzu ta hanyar watsawa kai tsaye.**

**[PoArt], ita ce kagara da aka gina a tsakiyar wannan gidan caca.**

- 🎰 Gidan caca yana dogara da wasannin takarda; muna dogara da **gaskiyar jiki**.
- 🃏 Gidan caca yana buɗe ga yaudara; muna buɗe ga **shaidun bayyane**.
- ⏳ Gidan caca na ɗan lokaci ne; muna mai da hankali kan **dawwamar fasaha da kimiyya**.

**Token da ke amfani da wannan yarjejeniya, ba kawai "coin" ba ne; hannun jari na dijital ne wanda ke ɗauke da gumi, fenti, lambar da falsafa a bayansa.**

---

## 🗳️ 6) SHUGABANCI & RIJISTAN JAMA'A (Governance & Public Registry)

**Manufar wannan sashe ita ce: cire ma'aunin [PoArt] daga matakin "amincewa da mutane" kuma canza shi zuwa gine-ginen jama'a mai ɗorewa tare da rijista + tabbatarwa + kula da al'umma.**

### 6.1 Public Registry (Rijistan Jama'a)

- **Public Registry:** Duk bayanan da aka amince ana rikodin su a `ilhanart.org/registry` (ko GitHub Registry).

**Dabarar rijista (ma'aunin da aka ba da shawara - a tsarin JSON path):**

Kowane rikodin da ya shiga rijista yana ɗauke da aƙalla waɗannan filayen ginshiƙi masu tabbatarwa:

- **Asali & Matsayi:**
  - `certificate_id` (tunani mai karantawa)
  - `status` (active / void)
  - `void_reason` (idan akwai)
  - `visibility` (private / masked / public)
  - `created_at` (alamar lokaci)

- **Hukuma Mai Bayarwa:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Bayanan Fasaha:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (idan zai yiwu; don ganewa token holder)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Bayanan Binciken Shari'a:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Shaidun Cryptographic:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Shugabanci:**
  - `governance.decision`
  - `governance.review_notes`

Rijista na iya samun yadudduka biyu:
- **1)** Index mai karantawa na ɗan adam (jerin yanar gizo / bincike / tace)
- **2)** Manifest mai karantawa na na'ura (rikodin JSON; don tabbatarwa ta PFE)

**"Rijista" a nan, za a iya tabbatarwa tare da sarkar Evidence Pack → EvidenceRoot → NotarySeal ta PFE. Rijista, ba "da'awa" ba amma tana ba da manufar tabbatarwa.**

---

### 6.2 Tsarin Neman PoArt Verified

**Ana kimanta aikace-aikacen PoArt Verified daga Ilhan Art Gallery bisa ma'aunin PoArt 5. Ana la'akari da ra'ayoyin al'umma, amma shawarar ƙarshe ta dogara ne akan ƙungiyar curator. Ana bayyana shawarwari a sarari kuma ana rikodin su a ilhanart.org/registry.**

#### Tsarin Aikace-aikace

**Aikace-aikace:**
- Mai fasaha/aikin yana neman PoArt Verified
- Ana shirya Evidence Pack (rikodin bidiyo, metadata, hanyoyin watsawa kai tsaye)
- Ana aika aikace-aikace zuwa Ilhan Art Gallery

**Bincike (Kwanaki 30):**
- Ƙungiyar gallery tana bincika Evidence Pack dalla-dalla
- Ana duba duk ma'aunin PoArt 5:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Ganawa da mai fasaha (na zaɓi)

**Tuntuɓar Al'umma:**
- Ana raba Evidence Pack a bayyane yayin tsarin aikace-aikace
- Al'umma na iya ba da ra'ayi ta ilhanart.org
- Token holders (mafi ƙarancin 10,000 $CULTURE) musamman za su iya ba da shawarwari
- **Ana la'akari da duk ra'ayoyi yayin tsarin bincike**
- **Duk da haka shawara ta ƙarshe ta dogara ne akan kimanta curator**

**Shawara:**
- Gallery tana amincewa ko kin aikace-aikace
- Ana bayyana dalilin shawara a sarari
- Idan an amince → PoArt Verified badge
- Idan an ƙi → Ana iya sake nema bayan watanni 6

**Nuna Gaskiya:**
- Ana rikodin duk aikace-aikace da shawarwari a ilhanart.org/registry
- Ana buga rikodin shawara a bayyane:
  - Kwanan aikace-aikace
  - Taƙaitaccen tsarin bincike
  - Shawara (Amincewa / Ƙin)
  - Dalilin shawara (ɗan gajeren bayani)
  - Taƙaitaccen ra'ayoyin al'umma (ba a sani ba)

#### Me Ya Sa Shawara ta Curator?

**Kula da Inganci:**  
Matsayin PoArt Verified shine badge mai ma'aunin sama. Kimanta curator yana tabbatar da kiyaye waɗannan ma'auni.

**Hana Sarrafa Hasashe:**  
Ba zai yiwu a fasaha tare da on-chain governance cikakke (misali: Realms, DAO voting) tare da token na Pump.fun ba. Tsarin voting na off-chain kuma yana buɗe ga sarrafa whale da hare-hare masu daidaitawa. Shawarar curator tana kawar da wannan haɗarin.

**Inganci na Aiki:**  
Maimakon tsarin voting masu rikitarwa, tsari mai sauri da bayyananne. Masu fasaha suna samun sakamako cikin kwanaki 30.

**Shigar Al'umma:**  
Ana la'akari da ra'ayoyin al'umma gaba ɗaya kuma yana shafar tsarin shawara. Amma shawara ta ƙarshe ta dogara ne akan ƙungiyar curator da aka karewa daga sarrafa.

**Gaba:**  
Sa'ad da aikin ya girma (2027+), ana iya ƙarfafa tsarin tuntuɓar al'umma. Duk da haka kariyar ma'aunin curator ta dawwama.

---

### 6.3 Token Utility (Wuraren Amfani da Token)

**Fa'idodin da aka ba wa masu riƙe $CULTURE token:**

**1. Fifikon Shiga Taron Gallery:**
- Haƙƙin yin nunawa na mako 1 a shekara a Ilhan Art Gallery (ana iya canja haƙƙi)
- Rangwamen zane mai ɗigowa
- Haƙƙin rangwame tsakanin 10% zuwa 30% akan zane-zane a gallery

**2. Cikakken Shiga PoArt Registry:**
- Cikakkun rikodin duk fasahohin da aka tabbatar
- Cikakkun sigogin Evidence Pack
- Kayan aikin tabbatarwa na binciken shari'a

**3. Advisory Voting:**
- Haƙƙin ba da shawara a aikace-aikacen PoArt Verified
- Shiga tashar ra'ayoyin al'umma
- Shiga tattaunawar shugabanci

**4. Exclusive Content:**
- Abun ciki na bayan fage na studio
- Hirarraki da bidiyon tsari na masu fasaha
- Shiga takaddun fasaha

**Lura:**  
Token holders suna ba da advisory vote (ƙuri'ar shawara). Shawara ta ƙarshe ta curator ce. An zaɓi wannan tsari don hana sarrafa whale da hare-haren hasashe. Babu ladan staking saboda muna neman masu shiga al'adu na dogon lokaci, ba jarin mercenary na ɗan gajeren lokaci ba.

---

### 6.4 Metadata Sync (Daidaita da Duniyar Jiki)

- **Metadata Sync:** Bayanan fasaha a rijista dole su dace 100% da kadarar jiki.

**Bayyana "daidaituwa 100%" a fasaha (ɗan sarari da aka ba da shawara):**

- **Ƙaramin daidaituwa (dole):**
  - `asset.fingerprints.sha256/sha512` a rijista da hash na fayil ɗin da ke hannu dole su zama **iri ɗaya**.
  - `proof.notary_seal` a rijista lokacin da aka sake samar da shi (idan akwai Evidence Pack) dole ya zama **iri ɗaya**.

- **Daidaitar tunani na jiki (nau'in shaida):**
  - Shaidun kamar fasaha ta jiki + tunani na kwanan wata/block da aka nuna a watsawa kai tsaye, dole su dace da Evidence Pack.

- **Daidaita sirri:**
  - A cikin ganuwar `masked` ana buga filayen kamar IP/wuri **bisa ma'aunin ɓoyewa**.

---

### 6.5 Ƙorafi, Bincike da Soke (Dispute & Revocation)

Rijista, ba kawai tsarin "amincewa" ba; tsarin **kula da rai game da zamba**.

- Lokacin da aka fara ƙorafi ana iya sanya rikodin cikin yanayin **"review"**.
- Idan an gano zamba ana yi masa alamar `status: void` kuma ana ƙara dalili:
  - `void_reason` (amfani da AI / sata / sarrafa da sauransu)
  - `revoked_at` (lokacin soke)
- Asalin shawara ta soke ya bayyana a sarari a rijista:
  - binciken curator / ƙorafin al'umma / bayanin nazari na binciken shari'a (wanda ya dace)

> **Wannan sashe shine daidai a rijista na ra'ayin VOID a sashe na "Red Flag Protocol".**

---

### 6.6 Misalin Rikodin Rijista (Mai karantawa na na'ura)
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
    "review_notes": "Met all 5 PoArt standards. Community feedback positive."
  }
}
```

> *Lura: `asset.fingerprints.sha512` da sauran darajoyin hash an taƙaita su don nuna; a aikace na ainihi ana amfani da cikakken jerin haruffan hexadecimal.*

---

## 7) 🔐 HATIMIN FASAHA (NOTARY SEAL)

**Algorithm hatimi mai ƙarfi da **PoArt Forensic Engine (PFE) v1.0** ya samar:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$
# [PoArt] Yarjejeniyar Notary na Dijital & Shaidar Binciken Shari'a (Beta v1.0)

> **"Al'ada, ta fi jari girma. Ku kare fasahohinku tun yau, ku kai su gobe."**

---

## Me Ya Sa A Bayyane?

Tsaro na ainihi yana zuwa daga nuna gaskiya. Ta hanyar tsarinmu na **Public Registry (Rijistan Jama'a)**, kowane mutum a ko'ina a duniya; zai iya tabbatar cikin daƙiƙu kaɗan ko fayil ɗin da ke hannunsa ya kasance na asali, ba tare da buƙatar kowane iko ba.

---

## 🧩 Me Ya Sa Akwai "Modules na Gani" Masu Yawa?

Wannan shine muhimmin sashen lambar (zaɓin menu na visibility). Waɗannan zaɓuɓɓuka suna barin masu amfani su daidaita **"Sirri vs. Nuna Gaskiya"**:

### 🔒 Sirri (Private)

- **Yanayi:** Mai fasaha har yanzu ba ya son buga fasaha amma yana son tabbatar da alamar lokaci kuma tabbatar da "Na yi wannan a wannan kwanan watan".
- **Abin da Lambar Take Yi:** Yana rubuta bayanai zuwa database amma yana sa alamar `visibility: "private"`. A nan gaba lokacin rubuta manufofin "Public Read" za ka iya ɓoye waɗannan rikodin daga jama'a ta hanyar cewa `WHERE visibility = 'public'`.

### 🕶️ Maskelanci (Masked)

- **Yanayi:** Mai fasaha yana son nuna gaskiya amma yana tsoron a gano adireshin gidansa (wurin IP).
- **Abin da Lambar Take Yi:** A gefen JavaScript ayyuka na `maskIP` da `maskLoc` suna aiki. Yana canja adireshin IP zuwa siffa `88.241.***.***`, wuri zuwa siffa `***/TR` kuma yana aika sigar da aka tantance zuwa database.
- **Bayanin Sirri:** Ana yin maskelanci a browser, Supabase ba ya ganin wurin ainihi. **Duk da haka:** Idan ana amfani da APIs na ɓangare na uku kamar ipapi.co don bayanan wuri, waɗannan masu samarwa suna ganin adireshin IP a lokacin buƙatar.
- **Hatimcewa a Yanayin Maskelanci:** Ana yin lissafin EvidenceRoot da NotarySeal tare da bayanan forensics da aka tantance; ta haka tabbatarwa ta kasance deterministic.

### 🌍 Bayyane ga Kowa (Public)

- **Yanayi:** Cikakken nuna gaskiya. Bisa ma'aunin [PoArt], ana bayyana a sarari inda, yaushe, daga wane hanyar sadarwa aka samar da fasaha.

---

## 💡 Sabuntawar Fasaha

PoArt, ba kawai tsarin loda fayil ba ne. Injin **"Sarkar Shaidar Binciken Shari'a" (Forensic Chain of Custody)** ne wanda ke kawo sabon ma'auni ta hanyar haɗa yadudduka fasaha daban-daban uku a cikin tukunya ɗaya.

**Yaduwa da aka bayyana a matsayin "injin" a wannan sashe, ya dace da ginshiƙin PoArt Forensic Engine (PFE) a cikin kalmomin da suka gabata.**

### 1) Client-Side Hashing (Mafi Girman Sirri)

Ba a taɓa loda fayilolin fasahohinku zuwa server ba. Injinmu mai aiki a browser (Client-side) yana lissafin hash (taƙaitaccen dijital) na fayil ɗin a kwamfutarku. Kawai wannan sawun yatsa da metadata ne aka aika zuwa server.

> **Bayanin Sirri:** Ba a loda fayilin fasaha zuwa server ba kuma ana karewa ta wannan hanyar. Amma ana raba bayanan forensics (IP/wuri) bisa yanayin ganuwa da aka zaɓa (private/masked/public).

### 2) Forensic Data Fusion (Ƙarfin Binciken Shari'a)

Ya fi alamar lokaci (Timestamp) ta yau da kullun. Tsarin yana haɗa waɗannan bayanan a cikin "Genesis Seal" guda ɗaya:

- **Taƙaitaccen Dijital (SHA-512):** Sawun yatsa na dijital da aka samar ta amfani da ma'aunin SHA-512 cryptographic wanda zai lalace ko da an canja pixel ɗaya na fasaha.
- **Wuri & Lokaci:** Kwanan wata mai daidaito na millisecond na aikin, bayanai na ƙasa, birni da yanki.
- **Asalin Na'ura:** Tsarin aiki, browser da nau'in na'ura (Nazarin User-Agent).

---

## 🛡️ Wuraren Amfani da Fa'ida

Idan kai mai fasaha ne, marubuci ko mai zane, cewa "Na yi wannan kafin" ba ya isa, dole ka tabbatar.

**Fasahar da kuka hatimce tare da PoArt:**

- **Shaidar Lissafi:** Ko da pixel ɗaya na fayil ɗinku ya canja tsarin zai gano. Sarrafa ba zai yiwu ba.
- **Tushen Shari'a:** An yi rikodin wane kwanan wata, wane birni, daga wane na'ura aka hatimce fasaha.
- **Takaddar Nan Take:** Cikin daƙiƙu kaɗan yana samar **"Takaddar Asalin Kadara"** na musamman, mai QR code da hatimtacce.

---

## ⚙️ Gine-ginen Tsari & Fasalin Fasaha

An tsara tsarin akan gine-ginen "Serverless" (Ba tare da Server ba), mai mai da hankali kan babban aiki da ƙarfin girma.

| Yaduwa | Fasaha | Bayani |
|--------|--------|--------|
| **Cryptography** | SHA-256 & SHA-512 | Taƙaitaccen cryptographic yadudduka biyu |
| **Database** | Supabase (PostgreSQL) | Tsarin bayanan JSONB, manufofin RLS |
| **Bayanan Binciken Shari'a** | ipapi.co API | Uku na IP/Wuri/Lokaci |
| **Rendering** | html2canvas + jsPDF | Samar PNG/PDF a gefen abokin ciniki |
| **Frontend** | Vanilla JavaScript | Babu dogaro da framework |
| **Tsaro** | Client-side hashing | Ba a taɓa loda fayil zuwa server ba |

### Fasalolin da Suka Fi Fice

| Fasali | Dalla-dalla | A Masu Fafatawa? |
|--------|-------------|------------------|
| **Drag & Drop UI** | Ja da saki fayil, nuna nan take | ❌ Yawanci babu |
| **Multi-Format Export** | PNG, JSON, PDF - danna ɗaya | ⚠️ Ƙuntatacce |
| **Real-Time Preview** | Nuna takadda a raye | ❌ Babu |
| **Privacy Controls** | Zaɓuɓɓukan Private/Masked/Public | ❌ Babu |
| **Client-Side Hashing** | Ba a taɓa aika fayil zuwa server ba | ✅ Kaɗan kawai suna da |
| **Forensic Metadata** | IP, wuri, na'ura, lokaci - duka tare | ❌ A sassa |
| **QR Verification** | QR code na tabbatarwa nan take | ⚠️ Ƙuntatacce |
| **Rate Limiting** | Kariyar spam (RLS + Client) | ❌ Yawanci babu |

---

## 🗺️ Taswira: Makowar "Ba Tare da Aminci Ba"

Sigar yanzu **(Beta v1.0)**, an inganta don ba ƙarshen mai amfani mafi girman sauri, sauƙin amfani da kyauta. Duk da haka hangen nesanmu na ƙarshe shine miƙawa zuwa tsarin da ko mai gudanar da database (mu) ba zai iya shiga tsakani ba.

### Faz 1: Beta v1.0 (Yanzu A Layi)

**Gine-gine:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + IPFS backup)
- Gallery self-attestation (tsakiya amma bayyane)

**Token:**
- Dandali: Pump.fun
- Kuɗin ruwa: Raydium (ta atomatik)
- Shugabanci: Advisory kawai (tuntuɓar al'umma)

**Manufa:**
- Sauri, kawar da shingen UX
- Ba da tsaro "mara gogayya"
- Gina al'umma

**Token Utility (v1.0):**
- Fifikon shiga taron gallery
- Kallon PoArt Registry
- Haƙƙin advisory voting

---

### 🚀 Faz 2: Ikon Mara Tsakiya (2026 Q2-Q4)

Wannan faz yana rufe miƙawa daga tsarin "Client-Side" cikakke zuwa tsari mafi aminci da mara tsakiya.

| Fasali | Menene Ya Bayar? | Tech Stack | ETA |
|--------|-----------------|------------|-----|
| **Edge Function INSERT** | Hanawa spam + tsaron API Key | Supabase Edge (Deno) | Q2 2026 |
| **Wallet Signature** | Asalin mara tsakiya | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | Tarihin mara tsakiya | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | Sokewar takaddar ƙarya | DB Schema Update | Q2 2026 |
| **Audit Log** | Rikodin tambayar binciken shari'a | Custom logs table | Q3 2026 |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain voting (x/web) + sa hannun walat
- Zaɓen wakilan al'umma (kwanaki 90 na farko)
- Multi-sig operations wallet control
- Weighted advisory voting (tare da iyakar whale)

**Immutability:**
- IPFS hashes tare da backup na registry
- Bitcoin timestamp anchoring
- Shirye-shiryen tabbatarwa ta cross-chain

---

### Faz 3: Cikakken Rashin Tsakiya (2027+)

| Fasali | Manufa | ETA |
|--------|--------|-----|
| **On-Chain Registry** | Rikodin on-chain na Solana | Q1 2027 |
| **Enhanced Token Utility** | NFT mint, fasalin ci gaba | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **DID Integration** | Asalin Mara Tsakiya | Q3 2027 |
| **Community Governance** | Tsarin shawara mai ƙarfi | Q4 2027 |
| **Legal Recognition** | Inganci a kotun Turkiyya | 2027-2028 |
| **API for Developers** | Public API endpoint | Q3 2027 |

**Juyin Shugabanci:**
- v3.0: Tsarin haɗe (curatoryal + al'umma mai nauyi)
- 2028+: Shugabancin al'umma cikakke (na zaɓi)
- Kariyar ingancin curatoryal koyaushe tana nan

---

## 🧬 Tsarin Bayanan Yarjejeniya (JSON Schema)

**Kowane takaddar [PoArt] yana da katunan asalin JSON mai ɗaukuwa kuma mai tabbatarwa wanda aka samar a wannan ma'auni.**

> **Lura:** Wannan tsarin Identity JSON shine tsarin takadda da aka ba mai amfani. A rikodin registry ana amfani da `registry.asset` maimakon `identity.asset_data` (taswirar: `identity.asset_data` == `registry.asset`).
```json
{
  "$schema": "https://raw.githubusercontent.com/galeri-coder/ilhanart-core/main/protocols/poart-identity-v1.json",
  "manifest": {
    "protocol": "[PoArt] Proof of Art",
    "version": "1.0",
    "status": "Production-Ready"
  },
  "identity": {
    "issuer": "Ilhan Art Gallery",
    "location": "Istanbul / Besiktas",
    "archive_vision": "2025 - 3000"
  },
  "asset_data": {
    "title": "Official Whitepaper",
    "fingerprints": {
      "sha256": "e4123f83b44a409d7a43f0897837876dfabb3320db63dadbb34c54281f38a6ba",
      "sha512": "41e5e0d007a2a77b6e0e3ebc548fbaa2788ea265193434f58d23e8c0f5bb20a0835aa850edbadbd8341969cf743fc69fa951f7ed275901fefe0fe7eb1fb83099"
    }
  },
  "official_links": {
    "registry": "https://www.ilhanart.org/public-registry",
    "evidence": "https://www.ilhanart.org/identity"
  },
  "forensics": {
    "ip_masked": "46.1.***.***",
    "device": "Brave (Windows;Monster,Tulpar)...",
    "location": "***/TR",
    "timestamp": "2026-01-09T12:34:56.000Z"
  }
}
```

---

## 🔬 Zurfin Fasaha: Algorithm Hatimi

### Ayyukan Hash Masu Ƙayyade
```javascript
// Ayyukan Taimakawa: Canja digest zuwa hex string
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Canja String zuwa byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Samar canonical forensics string (v1.0: tsayayyen tsarin filin + UTF-8 + \n delimiter)
// Bayanin Faz 2: Za a miƙa zuwa canonical JSON tare da RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Tsarin Samar NotarySeal (Cikakken Ƙayyade)
```javascript
// 1. Lissafin FileHash (gefen abokin ciniki)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Tara bayanan Forensic (amfani da timestamp ɗaya)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Samar timestamp guda ɗaya
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Timestamp iri ɗaya
  };
  
  return { forensics, timestamp };
}

// 3. Ƙirƙirar EvidenceRoot (tare da canonical encoding)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Samar NotarySeal (amfani da timestamp iri ɗaya)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Ayyukan taimakawa na maskelanci (goyon baya na IPv4 da IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Duba IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 ko tsari da ba a sani ba
  return "***";
}
```

### Tsarin Tabbatarwa (Matakai Biyu)

#### Quick Verify (Tabbatarwa ta Sauri)
```javascript
// Yana duba kawai hash na fayil (alamar ja mai sauri)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Jawo daga Registry
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Kwatanta hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Na Asali - Hash na fayil ya dace"
    };
  } else {
    return {
      valid: false,
      message: "❌ Ƙarya - An sarrafa fayil"
    };
  }
}
```

#### Full Verify (Cikakken Tabbatarwa)
```javascript
// Yana sake samar EvidenceRoot da NotarySeal kuma yana tabbatarwa
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Jawo daga Registry
  const cert = await fetchFromRegistry(certificateId);

  // 1) Dubawa FileHash (alamar ja mai sauri)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Ƙarya - Hash na fayil bai dace ba" };
  }

  // 2) Sake samar EvidenceRoot (tare da forensics da aka adana a registry)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Bai Dace Ba - EvidenceRoot bai yi ba" };
  }

  // 3) Sake samar NotarySeal (tare da timestamp ɗaya + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Bai Dace Ba - NotarySeal bai yi ba" };
  }

  // Zaɓi: A Faz 2 za a tabbatar da signer_sig tare da attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Sa hannu marar inganci" };

  return { valid: true, message: "✅ Na Asali - Full Verify ya wuce" };
}
```

> **Muhimman Bayanan:**
> - **Quick Verify:** Yana duba kawai hash na fayil don amfani mai sauri.
> - **Full Verify:** Yana tabbatar da duk yaduddukan yarjejeniya (EvidenceRoot + NotarySeal).
> - Ana yin duk ayyukan hash ta hanyar ƙayyade tare da encoding da delimiters tsayayyu.
> - **Ma'aunin canonicalization na v1.0:** Tsayayyen tsarin filin + UTF-8 encoding + `\n` delimiter.
> - **Shirin Faz 2:** Miƙawa zuwa canonical JSON tare da RFC 8785 (JCS - JSON Canonicalization Scheme).
> - A yanayin Masked, ana yin lissafin EvidenceRoot da NotarySeal tare da forensics da aka tantance.
> - Ana amfani da timestamp ɗaya a duk tsari (forensics + NotarySeal); an tabbatar da ƙayyade.
> - **Sunayen filayen Forensics:** `ip_masked`, `location`, `device`, `timestamp` (lambar da registry sun dace cikakke).
> - **Hanyar Registry:** `certificate.asset.fingerprints` (ya dace cikakke da lambar verify).
> - **signer_sig a Registry:** Ana buƙatar filin `proof.signer_sig` don Full Verify.
> - Za a fara amfani da tsarin SignerSignature a Faz 2 tare da Solana Wallet Adapter; a v1.0 ana iya tabbatarwa da `attestation_pubkey`.

---

## 📊 Nazarin Masu Fafatawa (An Sabunta)

PoArt, yana tsaye a "Sweet Spot" (Mafi kyawun wuri) wanda ke cike giɓin mafita na yanzu.

| Fasali | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|--------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Farashi** | 🆓 Kyauta | 🆓 | 💰 Biyan kuɗi | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Sauƙi Sosai | ❌ CLI | ⚠️ Matsakaici | ⚠️ Matsakaici | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Raye | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ Yanayi 3 | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Sirri | ✅ | ❌ Loda | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Cikakke | ❌ | ❌ | ⚠️ Ƙuntatacce | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Nan take | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Taswira | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Goyon Bayan Hausa** | ✅ Na Asali | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Bayani:**
- ✅ : Cikakken goyon baya / akwai
- ⚠️ : Ƙuntatacce / a cikin shirin biyan kuɗi
- ❌ : Babu / ba a goyan baya
- 🔄 : A taswira (ana haɓakawa)
- 🆓 : Cikakken kyauta
- 💰 : Biyan kuɗi / buƙatar biyan kuɗi

### Ƙarancin Masu Fafatawa, Ƙarfin PoArt

| Ƙaranci | Masu Fafatawa | PoArt |
|---------|---------------|-------|
| **Wahalar Amfani** | CLI, buƙatar ilimin API, buƙatar walat | Ja da saki, ya ƙare a danna 3 |
| **Shingen Farashi** | Biyan kuɗi na $50-500/wata | 100% kyauta |
| **Sirri** | Ana loda fayil zuwa server | Gefen abokin ciniki, ba a taɓa aika fayil ba |
| **Bayanan Forensic** | Kawai timestamp | IP, wuri, na'ura, lokaci - duka |
| **Goyon Bayan Hausa** | Babu ko ƙuntatacce sosai | Goyon bayan harshe na asali |
| **Bude Tushe** | Akwatin rufe | Duk lambar a buɗe a GitHub |

---

## 📈 Ƙididdiga na Amfani (Manufofin 2026 Q1)

| Ma'auni | Manufa | Matsayi |
|---------|--------|---------|
| **Jimlar Takaddun** | 1,000 | 🔄 Ana Ci Gaba |
| **Masu Amfani Masu Aiki** | 500 | 🔄 Ana Ci Gaba |
| **Yawan Tabbatarwa** | 5,000 | 🔄 Ana Ci Gaba |
| **Uptime** | 99.9% | ✅ Mai Aiki |
| **Lokacin Amsa ta Matsakaici** | <200ms | ✅ Mafi Kyau |

---

## 🌍 Al'umma & Goyon Baya

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Yanar Gizo:** [ilhanart.org](https://ilhanart.org)
- **Imel:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Masu Bayar da Gudummawa

Yarjejeniyar PoArt tana ci gaba da haɓakawa tare da gudummawar al'ummar bude tushe.

**Don bayar da gudummawa:**
1. Yi Fork
2. Ƙirƙiri feature branch (`git checkout -b feature/amazing-feature`)
3. Yi Commit (`git commit -m 'Add amazing feature'`)
4. Yi Push (`git push origin feature/amazing-feature`)
5. Buɗe Pull Request

### 🛠️ Menene Muke Buƙata Yanzu? (Kiran Taimako)

Muna jiran gudummawar masu haɓakawa masu kwarewa a waɗannan batutuwa don haɓakawa **Faz 2** na Yarjejeniyar PoArt:

* **Supabase Edge Functions:** Matsawa kariyar spam zuwa gefen server.
* **Solana Web3.js:** Haɗin sa hannun Walat (Wallet Signing).
* **IPFS / Arweave:** Haɗin sabis na tarihi da pinning.
* **Community Tools:** X voting, tsarin ƙuri'a, dashboard na nazari.

> Da fatan za ku fara tattaunawa a shafin "Issues" kafin ƙara fasali.

---

## 💬 Bayanan Ƙarshe

### Pump.fun da Gaskiya

An fara wannan aikin a Pump.fun saboda:
- ✅ Shiga kuɗin ruwa (Raydium automatic migration)
- ✅ Shiga al'umma da ake da ita
- ✅ Ƙaramin farashin farawa

Duk da haka bari mu fayyace:
- **Farashin token**, ba alamar nasarar fasaha ba ne
- **Kasafin kuɗi na aiki** daraja ta token tana da muhimmanci (gallery, nunawa, gine-gine)
- **Ma'aunin nasara:** Fasahohin da aka tabbatar + hulɗar al'umma + masu ziyartar jiki

### Shugabanci da Rashin Tsakiya

**Gaskiyar v1.0 (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (tsakiya amma bayyane)
- Shugabanci: Advisory kawai (shawarar ƙarshe ta curator)
- Token utility: Shiga gallery + registry + NFT fifiko

**Hangen Nesa na v2.0+ (2027+):**
- Registry: On-chain (Solana)
- Sa hannu: Mai tushe na Walat (mara tsakiya)
- Shugabanci: Haɗe (shawara ta al'umma + inganci na curatoryal)
- Token utility: Fasalin da aka ƙara + ci gaba shiga

Wannan tsari, yana ba da **ingancin aiki** da **kula da inganci** a mataki na farko, yayin da yake buɗe hanya don **ƙara shigar al'umma** a nan gaba.

---

**[PoArt] Yarjejeniyar Shaidar Fasaha v1.0**  
*"Culture > Capital" // Al'ada, Ta Fi Jari Girma*

## 🧾 Lasisin

MIT License © 2026 Ƙaddamar da İlhan Art Gallery

Duba [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) don cikakkun sharuɗɗa.

---

## 💬 Godiyar

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**An haɓaka wannan aikin tare da ƙaddamar [İlhan Art Gallery], kuma an buɗe lambar tushe ga jama'a don nuna gaskiya.**

**YARJEJENIYA V1.0 // AN HATIMCE DA SHA-512.**

*© 2026 İLHAN ART | AN KIYAYE DUKKAN HAƘƘOƘIN FASAHOHHI, HOTUNA DA RA'AYOYI.*

---
