# 📚 ƘAMUS NA KALMOMI DA MANUFOFI
> **"Fahimtar harshen wannan yarjejeniya shine fahimtar manufarta."**

## ⚙️ Injin Bincike na Shari'a na PoArt (PFE) v1.0: Tushen Tsarin

**Injin Bincike na Shari'a na PoArt (PFE)**, shine babban Layer wanda ke wakiltar ainihin dabaru da aiki na fasaha na yarjejeniyar [PoArt]. Wannan shi ne "injin shari'a" wanda ke ɗaukar ɗanyen bayanan samar da aikin fasaha kuma ya mayar da shi zuwa **shaidar dijital** wadda za a iya tabbatarwa kuma ba za a iya canzawa ba.

### 🧩 Me yasa "PoArt Forensic"?

- **PoArt (Tabbacin Fasaha):** Manufar injin ita ce haɗa ƙimar kadara ta dijital ba ga hasashe ba; amma ga **tsarin samarwa wanda za a iya tabbatarwa**.
- **Forensic (Tabbatar da Shari'a):**
  - **Ma'anar Fasaha:** Hanyar algorithm da sarkar rajista don tabbatar da cewa bayanan da ke da alaƙa da tsarin samarwa (bugun goga, timelapse, log) ba a manne su ba.
  - **Layer na Falsafa:** Sabanin "sakamakon nan take" na AI; da'awar mai canza samarwar ɗan adam wanda ya ƙunshi **lokaci, ƙoƙari da farashin yanke shawara** zuwa gaskiyar da za a iya aunawa.

> Lura: Haɗin blockchain (misali Solana) ba shi ne tushen PFE ba; za a bayyana shi dabam a matsayin **Chain Anchor Layer** don tabbatarwa/rajista.

### 🛠️ Iyakar Fasaha ta v1.0

**Injin Bincike na Shari'a na PoArt (PFE) v1.0** an gina shi akan waɗannan **ginshiƙai 3 na asali** maimakon ƙirar kuɗi mai rikitarwa:

1. **Hashing & Sealing (Rufe da Hatimi):**  
   PFE tana sarrafa dukkan abubuwan da ke cikin Fakitin Shaida (fayil ɗin aikin, bidiyo, JSON/log, sa hannu da sauransu) ta hanyar ƙayyadaddun ƙayyadaddun ƙayyadaddun ƙayyadaddun ƙayyadaddun kuma ta samar da ƙimar **NotarySeal** ta musamman.

   **Manufofin asali (v1.0):**
   - **FileHash (sawun yatsa na aikin):** Hash da aka samar daga bytes na fayil ɗin aikin.
   - **EvidenceRoot (tushen fakitin shaida):** Taƙaitaccen tushe wanda ke wakiltar ingancin Fakitin Shaida (Merkle root ko canonical manifest hash).
   - **NotarySeal (hatimi na ƙarshe / Sakamakon PFE):** Hatimin ƙarshe da aka samar daga haɗuwa da EvidenceRoot + lokaci + sa hannu.

   **Dabaru (bayyananne ga masu saka hannun jari):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Ma'anoni na Canonical Payload (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
   > Lura: Ƙimar da ake nufi a matsayin sakamakon PFE ita ce **NotarySeal**. Hanyar **SignerSignature** za a kunna a Phase 2 (tare da Solana Wallet Adapter); a cikin v1.0 na yanzu, ana amfani da sa hannun tabbatar da tsarin. Ana buga makullin jama'a na tabbatarwa a cikin rajista a filin `issuer.attestation_pubkey`.

2. **Indexing (Adanawa):**  
   Yana shigar da bayanan wane jakar kuɗi, wanne kwanan wata, don wane aikin ya gabatar da **Tabbacin Aiki (Labor Proof)**; zuwa Layer na rajista mai bayyane kuma mai iya tambaya.  
   *(Wannan Layer na iya zama bayanai; haɗin sarkar yana bayyana dabam a matsayin "Chain Anchor Layer".)*

3. **Verification (Tabbatarwa):**  
   Lokacin da aka tambayi asalin aikin, PFE yana sake sarrafa shaidun ɗanye; yana gwada tare da tabbacin lissafi ko ƙimar da aka ƙididdige ta **EvidenceRoot / NotarySeal** ta yi daidai da rajista a cikin adana.

---

### 🧮 Ka'idar Ƙimar PoArt (The Value Theorem)

Yarjejeniyar [PoArt] tana haɗa ƙimar kadara ta dijital ($V$) ba ga fahimtar kasuwa ta mutum ba; amma ga **gaskiyar zahiri ta tsarin samarwa**.

Hankali na Wucin Gadi (AI) yana lalata tsari ta ba da sakamako nan take ($t \to 0$). [PoArt] yana ɗaukar ƙima a matsayin tarawa na abubuwan **lokaci, ƙoƙari da nufin**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Ma'anar Masu Canzawa

- **$\int dt$ (Tarawa na Tsari):**  
  Ƙima ba "sakamako" na nan take ba ne; **tsari** ne wanda aka tara tsakanin $t_{\text{start}}$ da $t_{\text{end}}$. Yayin da lokaci ke raguwa (samarwar AI), sakamakon integral yana kusantar sifili.

- **$P_{\text{labor}}(t)$ (Ƙarfin Aiki na Nan Take):**  
  Yana wakiltar ƙarfin ƙoƙarin tunani da jiki da aka kashe a lokacin samarwa. Yayin da ƙoƙarin da za a iya tabbatarwa ke ƙaruwa, integrand yana girma.  
  > Lura: Ana iya daidaita wannan kalma a aikace ta hanyar "siginar aiki da za a iya auna/tabbatarwa".

- **$I_{\text{agency}}(t)$ (Ma'aunin Nufin):**  
  Ikon mai samarwa na ɗaukar haɗari da yanke shawara. Yana ɗaukar ƙima tsakanin $0$ da $1$.
  - **AI ($I \approx 0$):** Yana aiwatar da umarni, ba ya ɗaukar haɗari, ba ya biyan farashi.
  - **Dan Adam ($I \to 1$):** Yana canza shawara, yana shakka, yana ɗaukar haɗari.

- **$U_{\text{irreversible}}$ (Keɓantaccen da ba za a iya dawo da shi ba):**  
  Yayin da a samarwa ta dijital komawa (`Ctrl+Z`) mai yiwuwa ne; a samarwa ta zahiri (fenti da aka shafa akan zane, dutse da aka sassaƙa, yanayi a watsa kai tsaye) babu komawa. Wannan **rashin dawo da baya** kalma ce ta ƙari wacce ke haifar da "keɓance" (halayen non-fungible) a cikin aikin.

### 🔎 Nazarin Sharadi: AI "Sakamakon Nan Take" da Dan Adam "Tsarin da aka Tabbatar"

Yanayin da ke gaba yana nuna yadda **Ka'idar Ƙimar PoArt** ke aiki a aikace da kuma dalilin da ya sa samarwar AI ke samun maki kaɗan a cikin ma'aunin [PoArt].

#### Sharadi A: Samar da Hoto ta AI a cikin Daƙiƙa 10

- **Lokaci ($\Delta t$):** Daƙiƙa $10$ (tsarin kusan sifili)
- **Ƙarfin Aiki ($P_{\text{labor}}$):** Raka'a $1$ (rubuta umarni kawai)
- **Ma'aunin Nufin ($I_{\text{agency}}$):** $0.01$ (babu haɗari, babu farashi)
- **Rashin Dawo da Baya ($U_{\text{irreversible}}$):** $0$ (ana iya dawo da shi / ana iya kwafi)

**Sakamako:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Sharhi:** Ko da yake sakamakon cikakke ne; saboda ba a yi tsarin ba kuma ba ya ɗauke haɗari/nufin, ƙimar [PoArt] tana kusantar sifili.

#### Sharadi B: Samarwa ta Zahiri na Sa'o'i 6 a Watsa Kai Tsaye

- **Lokaci ($\Delta t$):** Sa'o'i $6$ (daƙiƙa $21{,}600$)
- **Ƙarfin Aiki ($P_{\text{labor}}$):** Raka'a $0.5$ (ci gaba da ƙoƙarin zahiri da tunani)
- **Ma'aunin Nufin ($I_{\text{agency}}$):** $0.9$ (canza shawara, ɗaukar haɗari, zaɓuɓɓuka marasa dawo da baya)
- **Rashin Dawo da Baya ($U_{\text{irreversible}}$):** $>0$ (alamun zahiri ba za a iya dawo da su ba)

**Sakamako:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Sharhi:** Yayin da tsari ke tsawaitawa kuma nufin (haɗari) ke ƙaruwa, ƙimar tana ƙaruwa da tarawa. Kalmar $U_{\text{irreversible}}$ ita ce ƙari wanda ke haifar da "keɓance" (halayen non-fungible) a cikin aikin.

---

### ✅ Ƙarshe: Kulle Ƙimar da Tabbaci (Proof-Bound Value)

Wannan ka'idar tana fitar da da'awar ƙimar [PoArt] daga "abin so" ko "labarin kasuwa" kuma tana haɗa shi zuwa **gaskiyar samarwa da za a iya tabbatarwa**.

1. **Ba Tare da Tsari Babu Ƙima:**  
   AI yana lalata tsari a cikin sakamakon nan take ($t \to 0$). Yayin da tagar tsari ke raguwa, sakamakon integral yana raguwa da wajibi na lissafi:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Nufin da Haɗari Su ne Masu Ƙarawa:**  
   [PoArt] ba yana auna "lokacin da aka kashe" kawai ba; amma kuma ainihin Layer na yanke shawara, haɗari da farashi a cikin lokacin. Ƙimar samarwar da ba ta ɗaukar haɗari (AI) tana da ƙasa:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Keɓance, Ba Tallan Ba Amma Tabbacin Zahiri:**  
   Alamun da ba za a iya dawo da su a samarwa ta zahiri (bugun zane, fashewar dutse), suna waje da dabaru na `Ctrl+Z` na dijital. Wannan **rashin dawo da baya** ($U_{\text{irreversible}}$), yana sanya aikin ya zama na musamman a ilimin halittar duniya.

> **🔐 TAKAITACCEN:** Ko da yake ka'idar ƙima tana ganin kamar ba ta da tabbas a matsayin awo (ko da yake a rayuwa ba za a iya auna daidai 100% ba) manufar wannan dabaru ita ce nuna tsarin da alkiblar masu canzawa. Abin da yake da wuya a zamanin AI ba "hoto" ba ne; **ƙoƙari, lokaci da nufin da za a iya tabbatarwa.** [PoArt] yana auna wannan ƙaranci kuma yana tabbatar da shi tare da **Fakitin Shaida**.

### 🏛️ Muhimmancin Manufar "Injin" (Engine)

Alamun da suka fito daga dandamali kamar Pump.fun, galibi suna kasancewa kawai **"tikitin shiga"**. **Injin Bincike na Shari'a na PoArt (PFE)** shi ne **Layer na dabaru na tsarin mulki** wanda ke ƙayyade waɗanne haƙƙoƙi tikitin ke kiyayewa, yadda ake rikodin aiki da kuma yadda fasaha/kimiyya/fasaha ke dawwama.

> **Lura:** Dalilin da ya sa muka fara wannan aikin a Pump.fun shine saboda ba mu da isasshen kuɗi da isasshen masu bi. Amfani da bayanan da ake da su a matsayin dabaru ba shi ne mafi inganci ba amma za mu iya cewa ya kasance matakin da ya dace. Bayyana dabaru na wannan injin a GitHub, ba tare da dogara ga kasafin kuɗi da kayan aiki ba, yana tabbatar da cewa aikin ba hasashe na kuɗi kawai ba ne, amma hangen nesa na dogon lokaci na **tsarin software** da **ɗakin karatu na ƙasa na dijital**.

---

## 🎨 YARJEJENIYAR TABBACIN AIKI NA [PoArt] (Proof of Art Protocol v1.0)

> **"Mai Fasaha na Gaske, Samarwa ta Gaske, Ƙima ta Gaske."**

Wannan yarjejeniya; **tsarin kariya na halittar halitta da hankali** ne da aka ƙera don mayar da martani ga masu zamba marasa sananniya waɗanda ke kewaye da yanayin crypto, hotuna na hankali na wucin gadi da aka samar a cikin mintuna 5 da al'adar "Pump & Dump" (Ƙara da Zubar).

---

## a) [PoArt] Menene? (Ma'ana ta Falsafa da Fasaha)

**Tabbacin Fasaha [PoArt];** ma'auni ne na tabbatarwa na hukuma wanda ke tabbatar da cewa ƙimar da ke bayan kadara akan blockchain tana dogara akan **aikin ɗan adam** da za a iya tabbatarwa, **lokaci** da **kuzarin zahiri**, ba hasashe ba.

Kamar yadda Bitcoin ke samar da ƙima ta *"Wutar Lantarki da Ƙarfin Processor"* **(Tabbacin Aiki)**; ayyukan da suka dace da [PoArt] suma suna samar da ƙima ta *"Baiwar Gwaninta da Lokacin Dan Adam da aka Kashe"*. Suna "Stake" lokaci.

Yana kawar da haɗarin *"Mai Tsara Shirye-shirye (Dev) ya sayar, aikin ya ƙare"* a cikin dandamali na Pump.fun da DEX; domin a nan ƙima ba ta cikin lambar ba ce, tana cikin **ci gaba da samarwa**.

> **[PoArt] ba ya ce wa mahalarta "Ku amince da mu"; yana cewa "Ga shaidun, ga shi da idanunka, tabbatar da lissafinka."**

---

## b) Ma'auni na Ginshiƙai 5 na [PoArt] (Ginshiƙai 5 na Gaskiya)

Waɗannan abubuwa 5 ne masu tacewa marasa iya lalacewa waɗanda aikin dole ne ya wuce don samun hatimin [PoArt].

### 1) Tabbacin Suna na Kai Tsaye (Live Identity Proof)

- **Matsala:** Duniyar crypto tana cike da masu ƙaddamarwa marasa sananniya (Dev) waɗanda ke tattara kuɗi kuma suka bar ayyuka.
- **Maganin [PoArt]:** Mai samarwa yana tabbatar da ba kawai katin shaida ba, amma **kasancewarsa a lokacin samarwa**. Wannan ya haɗa da zaman watsa kai tsaye inda ake hulɗa da al'umma kuma ana cika buƙatun musamman na nan take, ba bidiyo da aka riga aka yi rikodin ba.  
  (Misali: *"Rubuta kwanan yau da lambar shinge na yanzu a kusurwar dama na zane"*)
- **Taken:** *"Robots na iya zana amma robots ba su gumi kuma ba su yi improvisation."*

### 2) Tabbacin Aiki da Tsari (Labor & Process Proof)

- **Matsala:** Hotunan AI (Hankali na Wucin Gadi) da aka samar a cikin daƙiƙa 2 da zanen mai mai wanda aka yi a cikin watanni 2 ana ɗaukar su a matsayin "jpeg" iri ɗaya a duniyar dijital.
- **Maganin [PoArt]:** Tsarin "ciki da haihuwa" na aikin ana rikodin shi. Matakan sketch, yadudduka na fenti, sa'o'in da aka tara da aka kashe da kuma tsarin zahiri wanda mai fasaha ya fuskanta yayin ƙirƙirar aikin ana rubuta su. Wannan yana ƙara **"Farashin Lokaci" (Time Cost)** ga alama. Yayin da samarwar kadara ke da wahala, ƙimarta tana da ƙarfi.

### 3) Tabbacin Ƙimar Kyakkyawa (Aesthetic Value Proof)

- **Matsala:** Al'adar "Meme" tana yin watsi da kyakkyawa da zurfi na fasaha kuma tana mai da hankali kawai kan wasan kwaikwayo na nan take kuma sakamakonsa ayyukan gajere na "Hype".
- **Maganin [PoArt]:** Aikin dole ne ya kasance yana da ma'auni na fasaha na ilimi, ka'idar launi, ƙa'idodin tsari da ilimin kayan aiki (Impasto, Texture da dai sauransu). Abun ciki bai kamata ya ba da dariya kawai ba; ya kamata ya tayar da mamaki a cikin mai kallo kuma ya kasance yana da **ƙimar tarin**.

### 4) Sabbin Tunani (Conceptual Novelty)

- **Matsala:** Dubban saraƙun kare/cat waɗanda suke kwafin juna, marasa ƙirƙira.
- **Maganin [PoArt]:** Aikin dole ne ya gina sabuwar gada wacce ke haɗa fasaha, kimiyya, falsafa ko fasaha a cikin tsari mai ma'ana.  
  (Misali: Haɗa mutum-mutumin gargajiya na David da bayanan kasuwar crypto; sarrafa ra'ayin "zama dutse" na fahimtar ɗan adam ta hanyar wannan kuma kafa shi da tushe na kimiyya.)  
  Aikin bai kamata ya zama biki na gani kawai ba; amma kuma dole ne ya zama **ƙalubale na hankali** wanda ke sa mutane su yi tunani akan **Kimiyya, Falsafa ko Fasaha**.

> [!IMPORTANT]
> **Misalin Tunani (Tasirin Las Palmitas):**  
> A unguwar Las Palmitas ta Mexico wadda ke fama da laifuka, gidaje sama da 200 an mayar da su zuwa babban bikin bakan gizo. Sakamakon wannan shiga tsakani na ƙawa, adadin laifuka a unguwar ya ragu zuwa wani mataki, matasa sun fara sha'awar fasaha maimakon ƙungiyoyin laifi. Canjin ƙawa ya sake tsara girmama mutane ga muhallinsu da juna (Haɗin Kai na Zamantakewa).
>
> **Tsammani:** Aikin da zai shiga jerin [PoArt]; kamar misalin da ke sama, dole ne ya ƙunshi alaƙar sanadi-sakamako ta zamantakewa, kimiyya ko falsafa, fiye da ƙawa na gani kawai. Tun da dukiyar da ba za a iya saya da kuɗi ba "Lokaci" ne, a wannan yarjejeniya lokaci dole ne a yi stake a matsayin jingina kuma a tabbatar. Tushen tunani na aikin dole ne ya kasance mai ƙarfi da duniya har cewa; shekaru bayan haka ko da a yanayin CTO (Ɗaukar Jama'a), al'umma za ta iya gado wannan gado kuma ta ci gaba da yuwuwar ƙirƙira ta aikin ta hanyar mai zaman kanta.

### 5) Nufin Ba Na Algorithm Ba (Non-Algorithmic Agency)

- **Matsala:** Samarwa ta dijital cikakke amma maras ruhu, mai maimaitawa.
- **Maganin [PoArt]:** Nufin musamman na ɗan adam wanda ke iya kuskure, ɗaukar haɗari da fuskantar canje-canje na motsin rai dole ne a ji shi a cikin aikin. Rashin tabbas a cikin bugun goga, martanin kayan aiki marasa tsammani da shawaran nan take na mai fasaha, su ne **Sa Hannun Halitta** wanda ke bambanta aikin da "Samarwar Injin".

---

## c) Tsarin Tabbatarwa da Hana Karya

Wannan tsari yana tabbatar da cewa aikin yana kasancewa abin dogara kuma mai rai ba kawai "a farko" ba amma "har abada".

### 📦 Fakitin Shaida (Evidence Pack - The Digital Twin)

A bayan kowane aikin da aka tabbatar da [PoArt], akwai fakitin bayanai da aka ɓoye kuma mai alamar lokaci wanda masu saka hannun jari za su iya sauke:

- **Rikodin Bidiyo na RAW:** Hotunan ɗanye marasa katsewa na lokacin samarwa.
- **Nazarin Metadata:** Ranar ƙirƙirar fayil, bayanan na'urar da aka yi amfani da ita da bayanan wuri (Birni-Ƙasa).
- **Tunani na Zahiri:** Shaidu cewa aikin yana wanzuwa a duniyar zahiri  
  (Misali: Jarida ta yanzu ko bayanan blockchain na lokacin a kusa da aikin).

> *Bayanin daidaitawa:* Kalmar "fakitin shaida" tana haɗuwa zuwa layin **Evidence Pack → EvidenceRoot → NotarySeal** a cikin sassan da suka gabata; wato ingancin fakitin ana wakilta shi da hatimin da za a iya tabbatarwa.

### 🔄 Sabuntawa na Kwanaki 365 (Yarjejeniyar Dorewa)

- **Fasalin Juyin Juya Hali:** A cikin ayyukan crypto "Dev" (Mai Tsara Shirye-shirye), yana fitar da alama zuwa kasuwa kuma yawanci yana bace bayan watanni 1-2 (Soft Rug). [PoArt] yana sa wannan ya zama ba zai yiwu ba.
- **Doka:** Matsayin "Mai Fasaha da aka Tabbatar" (Verified Artist) ba na rayuwa ba ne. Yana aiki **shekara 1** kawai.
- **Aiki:** Mai fasaha/Mai Tsara Shirye-shirye, kowane kwanaki 365, dole ne ya gabatar da **sabon aiki babba wanda za a iya tabbatarwa** ga al'umma.
- **Misalin Sharadi:** Kun fara aikin a 2026. A watan Janairu 2027 tsarin yana ba da faɗakarwa "Lokacin Tabbatarwa Ya Ƙare". Idan mai fasaha bai gabatar da sabon nuni, sabon aikin zahiri ko sabon haɗin fasaha ba, "Badge na Aminci" na aikin yana faɗuwa.
- **Sakamako:** Wannan tsari yana tabbatar da cewa **abun ciki ba zai taɓa rasa muhimmancin ba** kuma mai saka hannun jari ba ya fuskanci tsoron *"Shin Mai Tsara Shirye-shirye har yanzu yana nan?"*. Aikin yana zama studio mai rai.

### 🚩 Yarjejeniyar Tuta Ja (Red Flag Protocol)

**A cikin kowane yanayin karya da al'umma ko algorithms suka gano (amfani da AI, aikin sata, bidiyo da aka manne):**

1. Shaida nan da nan ana sanya shi alama a matsayin **"BATALA" (VOID)**.
2. Fakitin shaidu ana sanya su alama a fili a matsayin **"Karya"**.
3. Aikin ana sanya shi a jerin baƙi na [PoArt]. Wannan yana ƙarfafa gaskiyar cewa a duniyar da ba ta da cibiya **suna shine kuɗin kawai**.
4. A cikin kowace wallafa ba za a iya amfani da kalmomi na [PoArt] ba, tushe mai inganci kawai shine https://www.ilhanart.org/public-registry

---

## d) Ƙarshe: Ba Gidan Caca Ba, Gidan Tarihi

**Pump.fun da Kasuwannin Ba tare da Cibiya (DEX) a halin yanzu abin baƙin ciki gidajen caca ne; fitilu suna kunna da kashewa, kowa yana neman riba mai sauri kuma akwatin (masu zamba) koyaushe yana cin nasara. Dalilin fara aikin a nan shi ne kuma ƙoƙarinmu na inganta wannan wuri kuma saboda bayananmu da muke da su da muhalli don isa ga jama'a ta yanzu ta hanyar watsa kai tsaye.**

**[PoArt], katanga ce da aka gina a tsakiyar wannan gidan caca.**

- 🎰 Gidan caca yana dogara akan wasannin takarda; mu muna dogara akan **gaskiyar zahiri**.
- 🃏 Gidan caca yana buɗe ga yaudara; mu muna buɗe ga **shaidu masu haske**.
- ⏳ Gidan caca na ɗan lokaci ne; mu muna mai da hankali kan **har abada na fasaha da kimiyya**.

**Alamar da ke amfani da wannan yarjejeniya ba "coin" kawai ba ce; hannun jarin dijital ne wanda ke ɗauke da gumi, fenti, lambar da falsafa a bayansa.**

---
## 🗳️ 6) MULKI DA RAJISTAR JAMA'A (Governance & Public Registry)

**Manufar wannan sashe ita ce: Fitar da ma'aunin [PoArt] daga matakin "amincewa da mutane" kuma mayar da shi zuwa tsarin jama'a mai dorewa ta hanyar rajista + tabbatarwa + sa ido na al'umma.**

### 6.1 Rajistar Jama'a (Public Registry)

- **Rajistar Jama'a:** Ana rubuta dukkan bayanan da aka amince da su a `ilhanart.org/registry` (ko GitHub Registry).

**Dabaru na rajista (ma'auni da aka ba da shawara - tsarin hanyar JSON):**

Kowane rikodin da ya shiga rajista yana ɗauke da aƙalla waɗannan filayen tushe da za a iya tabbatarwa:

- **Suna & Matsayi:**
  - `certificate_id` (tunani mai karantawa)
  - `status` (active / void)
  - `void_reason` (idan akwai)
  - `visibility` (private / masked / public)
  - `created_at` (hatimin lokaci)

- **Hukumar Mai Bayarwa:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Bayanan Aikin:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (idan zai yiwu; don gano mai riƙe alama)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Bayanan Shari'a:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Shaidun Cryptographic:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Mulki:**
  - `governance.decision`
  - `governance.review_notes`

Rajista na iya samun yadudduka biyu:
- **1)** Fihirisar karanta-mutum (lissafi/bincike/tacewa wavuti)
- **2)** Bayanan karanta-injin (rikodin JSON; don tabbatar da PFE)

**"Rajistar" a nan yana zama mai yiwuwar tabbatarwa ta hanyar sarkar Evidence Pack → EvidenceRoot → NotarySeal na PFE. Rajista tana ba da manufar tabbatarwa, ba da'awa ba.**

---

### 6.2 Tsarin Neman PoArt Verified

**Ana kimanta bukatar PoArt Verified ta İlhan Art Gallery bisa ga ma'auni 5 na PoArt. Ana la'akari da ra'ayin al'umma, amma yanke shawara na ƙarshe yana dogara ga ƙungiyar curate. Ana bayyana yanke shawara a fili kuma ana rubuta su a ilhanart.org/registry.**

#### Tsarin Nema

**Nema:**
- Mai fasaha/aikin yana yin neman PoArt Verified
- Ana shirya Fakitin Shaida (rikodin bidiyo, metadata, hanyoyin haɗi na watsa kai tsaye)
- Ana aika neman zuwa İlhan Art Gallery

**Bincike (Kwanaki 30):**
- Ƙungiyar galeri tana nazarin Fakitin Shaida dalla-dalla
- Ana duba dukkan ma'auni 5 na PoArt:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Tattaunawa da mai fasaha (na zaɓi)

**Shawarar Al'umma:**
- Ana raba Fakitin Shaida a fili yayin tsarin nema
- Al'umma za ta iya ba da ra'ayi ta hanyar ilhanart.org
- Masu riƙe alama (mafi ƙaranci 10,000 $CULTURE) na iya ba da shawarwari musamman
- **Ana la'akari da duk ra'ayoyi a cikin tsarin bincike**
- **Amma yanke shawara na ƙarshe yana dogara ga kimantawa ta curate**

**Yanke Shawara:**
- Galeri tana yarda ko ƙin neman
- Ana bayyana dalilin yanke shawara a fili
- Idan an yarda → badge na PoArt Verified
- Idan an ƙi → Ana iya sake nema bayan watanni 6

**Gaskiya:**
- Ana rubuta dukkan buƙatu da yanke shawara a ilhanart.org/registry
- Ana buga rikodin yanke shawara a fili:
  - Ranar nema
  - Taƙaitaccen tsarin bincike
  - Yanke shawara (An Yarda / An Ƙi)
  - Dalilin yanke shawara (bayani gajere)
  - Taƙaitaccen ra'ayoyin al'umma (marasa suna)

#### Me yasa Yanke Shawara ta Curate?

**Sarrafa Inganci:**  
Matsayin PoArt Verified badge ne mai ƙa'idodi masu girma. Kimantawa ta curate tana tabbatar da cewa ana kiyaye waɗannan ƙa'idodi.

**Hana Ɓarna ta Hasashe:**  
Cikakken mulkin kan-sarkar (misali: Realms, ƙuri'ar DAO) da alamun Pump.fun ba zai yiwu ba ta fuskar fasaha. Tsarin ƙuri'a na waje-sarkar suma suna buɗe ga ɓarna na whale da hare-hare masu haɗin kai. Yanke shawara ta curate yana kawar da wannan haɗarin.

**Ingancin Aiki:**  
Maimakon hanyoyin ƙuri'a masu rikitarwa, tsarin yanke shawara mai sauri da bayyananne. Masu fasaha suna samun sakamako a cikin kwanaki 30.

**Shigar da Al'umma:**  
Ana la'akari da ra'ayin al'umma gabaɗaya kuma yana shafar tsarin yanke shawara. Amma yanke shawara na ƙarshe yana dogara ga ƙungiyar curate da aka kare daga ɓarna.

**Gaba:**  
Sa'ad da aikin ya balaga (2027+), za a iya ƙarfafa tsarin shawarar al'umma. Amma kariyar ma'auni ta curate tana dawwama.

---

### 6.3 Amfanin Alama (Token Utility)

**Fa'idodin da ake bayarwa ga masu riƙe alamar $CULTURE:**

**1. Samun Damar Farko ga Ayyukan Galeri:**
- Haƙƙin yin nuni na mako 1 a shekara a İlhan Art Gallery (haƙƙin ana iya canjawa)
- Rangwame na Drop painting
- Haƙƙin rangwame na 10% zuwa 30% akan hotuna a galeri

**2. Cikakken Samun Damar PoArt Registry:**
- Cikakkun rikodin dukkan ayyukan fasaha da aka tabbatar
- Cikakkun sigogin Fakitin Shaida
- Kayan aikin tabbatar da shari'a

**3. Ƙuri'ar Shawara:**
- Haƙƙin shawara a buƙatun PoArt Verified
- Samun damar hanyoyin ra'ayin al'umma
- Shiga cikin tattaunawar mulki

**4. Abun Ciki na Musamman:**
- Abun ciki na bayan-labule na studio
- Hirar masu fasaha da bidiyoyin tsari
- Samun damar takaddun fasaha

**Lura:**  
Masu riƙe alama suna ba da ƙuri'ar shawara (advisory vote). Yanke shawara na ƙarshe na ƙungiyar curate ne. An zaɓi wannan tsarin don hana ɓarna na whale da hare-hare na hasashe. Babu ladan staking saboda muna neman mahalarta al'ada na dogon lokaci, ba jarin soja na ɗan lokaci ba.

---

### 6.4 Daidaita Metadata (Metadata Sync)

- **Daidaita Metadata:** Bayanan fasaha a cikin rajista dole su yi daidai 100% da kadara ta zahiri.

**Ma'anar fasaha ta "daidaitawa 100%" (haske da aka ba da shawara):**

- **Mafi ƙarancin daidaitawa (wajibi):**
  - `asset.fingerprints.sha256/sha512` a cikin rajista da hash na fayil ɗin da ake da shi dole su kasance **daidai-daidai**.
  - `proof.notary_seal` a cikin rajista lokacin da aka sake samarwa (idan akwai Fakitin Shaida) dole ya kasance **daidai-daidai**.

- **Daidaitawa da tunani na zahiri (nau'in shaida):**
  - Shaidu kamar aikin zahiri da aka nuna a watsa kai tsaye + tunani na kwanan wata/shinge dole su yi daidai da Fakitin Shaida.

- **Daidaituwa da sirri:**
  - Filayen kamar IP/wuri a gani na `masked` dole a buga su **bisa ga ma'aunin rufewa**.

---

### 6.5 Ƙin Yarda, Bincike da Soke (Dispute & Revocation)

Rajista ba tsarin "amincewa" kawai ba ne; **tsarin sa ido mai rai ne** akan karya.

- Lokacin da aka fara ƙin yarda, ana iya shigar da rikodin zuwa yanayin **"bincike"**.
- Idan aka gano karya, ana sanya shi alama a matsayin `status: void` kuma ana ƙara dalili:
  - `void_reason` (amfani da AI / sata / ɓarna da dai sauransu)
  - `revoked_at` (lokacin sokewa)
- Tushen yanke shawara na sokewa yana bayyana a fili a cikin rajista:
  - binciken curate / ƙin yarda na al'umma / bayanin nazarin shari'a (duk abin da ake amfani da shi)

> **Wannan sashe shine daidai da manufar VOID a kan rajista daga sashin "Yarjejeniyar Tuta Ja".**

---

### 6.6 Misalin Rikodin Rajista (Mai Karantawa-Injin)
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

> *Lura: An taƙaita `asset.fingerprints.sha512` da sauran ƙimar hash don nuni; a aikace na gaske, ana amfani da cikakken tsawon jerin haruffan hexadecimal.*

---

## 7) 🔐 HATIMI NA FASAHA (NOTARY SEAL)

**Algorithm na hatimi maras girgiza da Injin Bincike na Shari'a na PoArt (PFE) v1.0 ya samar:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Yarjejeniyar [PoArt] ta Dijital Notary & Shaidar Shari'a (Beta v1.0)

> **"Al'ada ta fi jari girma. Kiyaye ayyukanku yau, kai su gobe."**

---

## Me yasa A Fili?

Tsaro na gaske yana fitowa daga gaskiya. Saboda tsarin **Rajistar Jama'a (Public Registry)** namu, mutum a ko'ina a duniya zai iya; tabbatar da ko fayil ɗin da yake da shi asali ne, a cikin daƙiƙa kaɗan, ba tare da buƙatar kowace hukuma ba.

---

## 🧩 Me yasa Akwai "Modular Gani" da Yawa?

Wannan shi ne mafi mahimmancin sashe na lambar (menu na zaɓi na visibility). Waɗannan zaɓuɓɓuka suna ba masu amfani damar kafa ma'auni na **"Sirri da Gaskiya"**:

### 🔒 Sirri (Private)

- **Sharadi:** Mai fasaha har yanzu ba ya son buga aikin amma yana so ya buga hatimin kwanan wata ya tabbatar "na yi wannan a wannan kwanan wata".
- **Abin da Lambar ke Yi:** Tana rubuta bayanai zuwa bayanai amma tana buga alamar `visibility: "private"`. A nan gaba lokacin rubuta manufar "Karanta Jama'a" za ku iya faɗi `WHERE visibility = 'public'` don ɓoye waɗannan rikodin daga jama'a.

### 🕶️ Mai Rufi (Masked)

- **Sharadi:** Mai fasaha yana son gaskiya amma yana jin tsoron gano adireshin gida (wurin IP).
- **Abin da Lambar ke Yi:** Ayyukan `maskIP` da `maskLoc` suna aiki a gefen JavaScript. Yana canza adireshin IP zuwa siffar `88.241.***.***`, wurin zuwa siffar `***/TR` kuma yana aika sigar da aka danna zuwa bayanai.
- **Bayanin Sirri:** Ana yin rufewa a cikin burauzar, Supabase ba ya ganin ainihin wurin. **Amma:** Idan ana amfani da API na ɓangare na uku kamar ipapi.co don bayanan wurin, waɗannan masu bayarwa suna ganin adireshin IP a lokacin buƙata.
- **Rufewa a Yanayin Masked:** Ana yin ƙididdigar EvidenceRoot da NotarySeal tare da bayanan forensics da aka rufe; don haka tabbatarwa tana kasancewa deterministic.

### 🌍 Ga Kowa (Public)

- **Sharadi:** Cikakken gaskiya. Bisa ga ma'aunin [PoArt], ana bayyana a fili inda aikin aka samar, lokacin da kuma daga wane hanyar sadarwa.

---

## 💡 Sabon Fasaha

PoArt ba tsarin loda fayil kawai ba ne. Injini ne na **"Sarkar Kiyaye Shaidar Shari'a" (Forensic Chain of Custody)** wanda ke narkar da yadudduka uku daban-daban na fasaha a cikin tukunya ɗaya kuma yana kawo sabon ma'auni.

**Layer da ake bayyana a cikin wannan sashe a matsayin "injini" yayi daidai da tushen Injin Bincike na Shari'a na PoArt (PFE) a cikin kalmomi na farko.**

### 1) Hashing na Gefen Abokin Ciniki (Client-Side Hashing) - Mafi Girman Sirri

Fayilolin aikinku ba a loda su zuwa sabar ba. Injin mu wanda ke aiki a cikin burauzar (Client-side), yana ƙididdige hash (taƙaitaccen dijital) na fayil a cikin kwamfutarka. Ana aika wannan sawun yatsa da metadata kawai zuwa sabar.

> **Bayanin Sirri:** Ba a loda fayil ɗin aikin zuwa sabar ba kuma ana kiyaye shi ta wannan hanya. Amma bayanan forensics (IP/wurin) ana raba su bisa ga yanayin gani da aka zaɓa (private/masked/public).

### 2) Haɗuwa da Bayanan Shari'a (Forensic Data Fusion) - Ƙarfin Shari'a

Ya wuce hatimin lokaci na yau da kullun (Timestamp). Tsarin yana haɗa waɗannan bayanan zuwa cikin "Hatimin Farawa" ɗaya:

- **Taƙaitaccen Dijital (SHA-512):** Sawun yatsan dijital ta amfani da ma'aunin taƙaitaccen cryptographic (SHA-512) wanda zai lalace ko da pikseli ɗaya na aikin ya canza.
- **Wurin & Lokaci:** Kwanan wata mai daidaiton millisecond, ƙasa, birni da bayanan gundumar inda aka yi aikin.
- **Shaida na Na'ura:** Tsarin aiki, burauzar da nau'in na'ura (nazarin User-Agent).

---

## 🛡️ Wuraren Amfani da Fa'ida

Idan kai mai fasaha ne, marubuci ko mai zane, ba ya isa ka ce "Na yi wannan a baya", dole ne ka tabbatar.

**Aikin da ka buga hatimi da PoArt:**

- **Tabbacin Lissafi:** Ko da pikseli ɗaya na fayilinka ya canza, tsarin yana gane. Ɓarna ba zai yiwu ba.
- **Tushen Shari'a:** An rubuta aikin lokacin da aka buga hatimi kwanan wata, birni, daga wacce na'ura.
- **Shaida ta Nan Take:** A cikin daƙiƙa kaɗan tana samar da **"Shaidar Shaida na Kadara"** ta musamman gare ka, mai lambar QR da hatimi.

---

## ⚙️ Tsarin Tsari da Halayen Fasaha

An tsara tsarin akan tsarin "Serverless" (Ba Sabar), tare da mai da hankali kan babban aiki da ikon faɗaɗa.

| Layer | Fasaha | Bayani |
|-------|--------|--------|
| **Cryptography** | SHA-256 & SHA-512 | Taƙaitaccen cryptographic mai yadudduka biyu |
| **Bayanai** | Supabase (PostgreSQL) | Tsarin bayanai na JSONB, manufofin RLS |
| **Bayanan Shari'a** | ipapi.co API | Uku na IP/Wurin/Lokaci |
| **Rendering** | html2canvas + jsPDF | Samar da PNG/PDF na gefen abokin ciniki |
| **Frontend** | Vanilla JavaScript | Babu dogaro da tsari |
| **Tsaro** | Client-side hashing | Fayil ba ya taɓa zuwa sabar |

### Halayen da Suka Fito

| Halaye | Bayani | A cikin Masu Fafatawa? |
|---------|---------|----------------------|
| **Ja & Sauke UI** | Ja fayil ka sauke, nunin nan take | ❌ A yawancin su babu |
| **Fitowa ta Nau'ikan da Yawa** | PNG, JSON, PDF - da dannawa ɗaya | ⚠️ Ƙananan |
| **Nunin Lokaci Mai Aiki** | Nunin kai tsaye na shaida | ❌ Babu |
| **Sarrafa Sirri** | Zaɓuɓɓukan Private/Masked/Public | ❌ Babu |
| **Hashing na Gefen Abokin Ciniki** | Fayil ba ya taɓa zuwa sabar | ✅ A kaɗan kawai |
| **Metadata na Shari'a** | IP, wurin, na'ura, lokaci - duka tare | ❌ Guntun-guntun |
| **Tabbatar da QR** | Lambar QR na tabbatarwa na nan take | ⚠️ Ƙananan |
| **Iyakance Ƙimar** | Kariyar spam (RLS + Client) | ❌ A yawancin su babu |

---

## 🗺️ Taswiran Hanya: Makomar "Ba tare da Amana"

Sigar yanzu **(Beta v1.0)** an inganta ta don ba da mafi girman gudu, sauƙin mai amfani da damar kyauta ga mai amfani na ƙarshe. Amma makon mu na ƙarshe, matsayin da har ma da mai sarrafa bayanai (mu) ba zai iya shiga ba.

### Awamu na 1: Beta v1.0 (Yanzu A Layi)

**Tsari:**
- Bayanai na Girgije (Supabase)
- Rajistar waje-sarkar (PostgreSQL + madadin IPFS)
- Tabbatar da galeri ta kai (cibiya amma bayyananne)

**Alama:**
- Dandamali: Pump.fun
- Kuɗi: Raydium (kai-tsaye)
- Mulki: Shawara kawai (shawarar al'umma)

**Manufa:**
- Gudu, kawar da shingaye na UX
- Ba da tsaro "ba tare da juzu'i"
- Ƙirƙirar al'umma

**Amfanin Alama (v1.0):**
- Samun damar farko ga ayyukan galeri
- Kallon PoArt Registry
- Haƙƙin ƙuri'ar shawara

---

### 🚀 Awamu na 2: Ikon da Ba ta da Cibiya (Decentralized Authority) (2026 Q2-Q4)

Wannan awamu yana ɗaukar canjin tsarin daga tsarin da ke aiki gabaɗayan "Gefen Abokin Ciniki", zuwa tsarin mafi aminci da rashin cibiya.

| Halaye | Menene Yana Kawo? | Tech Stack | ETA |
|---------|------------------|------------|-----|
| **Edge Function INSERT** | Shingen spam + tsaron makullin API | Supabase Edge (Deno) | Q2 2026 |
| **Sa Hannun Jakar Kuɗi** | Shaida maras cibiya | Solana Wallet Adapter | Q2 2026 |
| **Madadin IPFS/Arweave** | Adana maras cibiya | IPFS SDK + Pinata | Q3 2026 |
| **Tsarin Sokewa** | Soke shaidar karya | Sabunta Schema na DB | Q2 2026 |
| **Log na Bincike** | Rikodin tambaya na shari'a | Tebur na log na al'ada | Q3 2026 |
| **OpenTimestamps** | Ƙulla zuwa Bitcoin | OTS JavaScript | Q4 2026 |

**Mulkin Alama (v2.0):**
- Ƙuri'a ta waje-sarkar (x/web) + sa hannun jakar kuɗi
- Zaɓin wakilin al'umma (kwanaki 90 na farko)
- Sarrafa jakar kuɗi na ayyuka masu sa-hannu da yawa
- Ƙuri'ar shawara mai nauyi (tare da shingen whale)

**Rashin Canzawa:**
- Madadin rajista da hash na IPFS
- Ƙulla hatimin lokaci na Bitcoin
- Shirye-shiryen tabbatar da tsakanin-sarƙoƙi

---

### Awamu na 3: Cikakken Rashin Cibiya (2027+)

| Halaye | Manufa | ETA |
|---------|--------|-----|
| **Rajistar Kan-Sarkar** | Rikodin kan-sarkar Solana | Q1 2027 |
| **Ƙara Amfanin Alama** | Buga NFT, halaye masu girma | Q1 2027 |
| **Goyan Bayan Sarƙoƙi da Yawa** | Ethereum, Polygon, Base | Q2 2027 |
| **Haɗin DID** | Shaida Maras Cibiya | Q3 2027 |
| **Mulkin Al'umma** | Tsarin shawara da aka ƙarfafa | Q4 2027 |
| **Sanin Shari'a** | Inganci a kotunan Turkiyya | 2027-2028 |
| **API don Masu Tsarawa** | Wurin API na jama'a | Q3 2027 |

**Ci Gaban Mulki:**
- v3.0: Misali na haɗe-haɗe (curate + al'umma mai nauyi)
- 2028+: Cikakken mulkin al'umma (na zaɓi)
- Sarrafa ingancin curate koyaushe ana kiyaye shi

---

**[PoArt] Yarjejeniyar Tabbacin Fasaha v1.0**  
*"Al'ada > Jari" // Culture > Capital // Kültür, Sermayeden Büyüktür*

## 🧾 Lasisi

Lasisi na MIT © 2026 Shirin İlhan Art Gallery

Duba [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) don cikakken sharuɗɗa.

---

## 💬 Ƙima

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**An ƙera wannan aikin tare da shirin [İlhan Art Gallery] kuma lambar tushe na buɗe don gaskiya.**

**YARJEJENIYA V1.0 // AN BUGA HATIMI DA SHA-512.**

*© 2026 İLHAN ART | DUKKAN HAƘƘOƘIN AYYUKA, HOTUNA DA TUNANI AN AJIYE SU.*

---
