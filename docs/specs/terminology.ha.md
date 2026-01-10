# 📚 ƘAMUS NA KALMOMIN FASAHA DA MANUFA
> **"Fahimtar harshen wannan yarjejeniya yana nufin fahimtar hangen nesanta."**

## ⚙️ Injin Bincike na PoArt (PFE) v1.0: Tushen Ababen More Rayuwa

**Injin Bincike na PoArt (PFE)** shine babban matakin da ke wakiltar tsakiyar dabaru da ayyukan fasaha a bayan yarjejeniyar [PoArt]. Wannan shine "injin bincike" wanda ke ɗaukar bayanan samarwa na ɗanyen aikin fasaha kuma yana mai da su zuwa **shaidun dijital** waɗanda za a iya tabbatarwa kuma ba za a canza su ba.

### 🧩 Me yasa "PoArt Forensic"?

- **PoArt (Tabbacin Fasaha):** Manufar injin ita ce haɗa ƙimar kadara ta dijital ba ga hasashe ba, amma ga **tsarin samarwa mai iya tabbatarwa**.
- **Forensic (Tabbatarwa ta Kimiyya):**
  - **Ma'anar Fasaha:** Hanyar algorithm da tsarin rubutawa don tabbatar da cewa bayanan tsarin samarwa (zanen goga, video na lokaci, rajista) ba a dame su ba.
  - **Matakin Falsafa:** Da'awar canza **lokacin ɗan adam, ƙoƙari, da farashin yanke shawara** zuwa gaskiyar da za a iya auna, a kan samar da "sakamako nan take" na AI.

> Lura: Haɗin blockchain (misali, Solana) ba tushen PFE ba ne; za a siffanta shi daban a matsayin **Matakin Anka na Sarkar** don dalilan tabbatarwa/rajista.

### 🛠️ Iyakar Fasaha v1.0

**Injin Bincike na PoArt (PFE) v1.0** an gina shi akan **ginshiƙai 3 masu mahimmanci** masu zuwa maimakon ƙirar kuɗi masu rikitarwa:

1. **Hashing & Sealing (Hatimewa):**  
   PFE yana sarrafa dukkan abubuwa a cikin Kunshin Shaida (fayil ɗin aikin, bidiyo, JSON/rajista, sa hannu, da sauransu) ta hanyar da za a iya tantancewa kuma yana haifar da ƙimar **NotarySeal** ta musamman.

   **Mahimman ra'ayoyi (v1.0):**
   - **FileHash (tambarin yatsa na aikin):** Hash da aka samar daga bytes na fayil ɗin aikin.
   - **EvidenceRoot (tushen kunshin shaida):** Taƙaitaccen tushe wanda ke wakiltar amincin Kunshin Shaida (tushen Merkle ko hash na bayani na asali).
   - **NotarySeal (hatimi na ƙarshe / fitarwa ta PFE):** Hatimi na ƙarshe da aka samar daga haɗin EvidenceRoot + lokaci + sa hannu.

   **Dabarun (masu ganin sauƙi ga masu zuba jari):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Ma'anar Kaya na Asali (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Lura: Ƙimar da ake kiranta a matsayin fitarwar PFE ita ce **NotarySeal**. Za a kunna tsarin **SignerSignature** a Mataki na 2 (tare da Solana Wallet Adapter); a cikin v1.0 na yanzu, ana amfani da sa hannun shaidar tsarin. Ana buga maɓallin jama'a na shaidar a cikin rajista a ƙarƙashin filin `issuer.attestation_pubkey`.

2. **Indexing (Ajiya):**  
   Yana rubuta wace jakata, a wane kwanan wata, ta ƙaddamar da **Tabbacin Aiki** don wane aiki zuwa matakin rajista mai bayyana kuma za a iya tambaya.  
   *(Wannan matakin na iya zama bayanan adana; an siffanta haɗin sarkar daban a matsayin "Matakin Anka na Sarkar".)*

3. **Verification (Tabbatarwa):**  
   Lokacin da aka yi tambaya game da sahihancin aikin, PFE yana sake sarrafa shaidun ɗanyen; yana gwada a lissafi ko ƙimar **EvidenceRoot / NotarySeal** da aka ƙididdige suna daidai da bayanan ajiya.

---

### 🧮 Ka'idar Daraja ta PoArt (The Value Theorem)

Yarjejeniyar [PoArt] tana haɗa ƙimar ($V$) kadara ta dijital ba ga fahimtar kasuwa ta zahiri ba, amma ga **gaskiyar zahiri ta tsarin samarwa**.

Hankali na Wucin Gadi (AI) yana lalata tsarin ta hanyar ba da sakamako nan take ($t \to 0$). [PoArt], duk da haka, yana ɗaukar ƙimar a matsayin tarin abubuwan **lokaci, aiki, da niyya**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Ma'anar Ma'auni

- **$\int dt$ (Tarin Tsari):**  
  Daraja ba "sakamako" na nan take ba ne; **tsari** ne da aka tara tsakanin $t_{\text{start}}$ da $t_{\text{end}}$. Yayin da tsawon lokaci yake raguwa (samarwa ta AI), sakamakon haɗewa yana kusantar 0.

- **$P_{\text{labor}}(t)$ (Ƙarfin Aiki na Nan Take):**  
  Yana wakiltar ƙarfin ƙoƙarin hankali da na jiki da aka kashe a lokacin samarwa. Yayin da ƙoƙarin da za a iya tabbatarwa yake ƙaruwa, integrand yana girma.  
  > Lura: Za a iya daidaita wannan kalmar a aikace ta hanyar "alamun aiki mai iya aunawa/tabbatarwa".

- **$I_{\text{agency}}(t)$ (Ma'aunin Niyya):**  
  Ikon mai samarwa na ɗaukar haɗari da yanke shawara. Yana ɗaukar ƙima tsakanin $0$ da $1$.
  - **AI ($I \approx 0$):** Yana aiwatar da umarni, ba ya ɗaukar haɗari, ba ya biyan farashi.
  - **Mutum ($I \to 1$):** Yana canza yanke shawara, yana shakka, yana ɗaukar haɗari.

- **$U_{\text{irreversible}}$ (Keɓancewar da Ba za a Iya Juyawa ba):**  
  Yayin da warwarewa (`Ctrl+Z`) yana yiwuwa a cikin samarwa ta dijital, a cikin samarwa ta zahiri (fentin da aka shafa a kan zane, marmara da aka sassaka, motsin hannu a yaɗuwar kai tsaye) babu hanyar komawa. Wannan **rashin juyawa** kalma ce ta ƙari da ke haifar da "keɓantacce" (halayen da ba za a iya musanya ba) a cikin aikin.

### 🔎 Nazarin Lamari: AI "Sakamako na Nan Take" da Mutum "Tsarin da aka Tabbatar"

Yanayin da ke zuwa yana nuna yadda **Ka'idar Daraja ta PoArt** ke aiki a aikace kuma me yasa samarwa ta AI ke samun maki ƙanƙanta a ma'aunin [PoArt].

#### Yanayi A: Samarwar Gani na Daƙiƙa 10 da AI

- **Tsawon lokaci ($\Delta t$):** $10$ daƙiƙa (tsari kaɗan)
- **Ƙarfin Aiki ($P_{\text{labor}}$):** $1$ naúrar (kawai rubuta umarni)
- **Ma'aunin Niyya ($I_{\text{agency}}$):** $0.01$ (babu haɗari, babu farashi)
- **Rashin Juyawa ($U_{\text{irreversible}}$):** $0$ (ana iya juyawa / ana iya kwafewa)

**Sakamako:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Sharhi:** Ko da sakamakon ya yi kyau; ƙimar [PoArt] tana kusantar $0$ saboda ba a rayar da kowane tsari kuma ba a shigar da niyya/haɗari ba.

#### Yanayi B: Samarwar Zahiri na Awa 6 a Yaɗuwar Kai Tsaye

- **Tsawon lokaci ($\Delta t$):** $6$ awa ($21{,}600$ daƙiƙa)
- **Ƙarfin Aiki ($P_{\text{labor}}$):** $0.5$ naúrar (ci gaba da ƙoƙarin jiki da na hankali)
- **Ma'aunin Niyya ($I_{\text{agency}}$):** $0.9$ (canza yanke shawara, ɗaukar haɗari, zaɓin da ba za a iya juyawa ba)
- **Rashin Juyawa ($U_{\text{irreversible}}$):** $>0$ (alamun zahiri ba za a iya warwarewa ba)

**Sakamako:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Sharhi:** Yayin da tsari yake tsawaita kuma niyya (haɗari) yana ƙaruwa, daraja tana tarawa. Kalmar $U_{\text{irreversible}}$ gudummawa ce ta ƙari da ke haifar da "keɓantacce" (halayen da ba za a iya musanya ba) a cikin aikin.

---

### ✅ Ƙarshe: Darajar da aka Haɗa da Shaida (Proof-Bound Value)

Wannan ka'idar tana fitar da da'awar darajar [PoArt] daga kasancewa "so" ko "labarin kasuwa" kuma tana haɗa shi da **gaskiyar samarwa mai iya tabbatarwa**.

1. **Babu Tsari, Babu Daraja:**  
  AI yana lalata tsarin da sakamakon nan take ($t \to 0$). Yayin da tagar tsari ke kunkuntar, sakamakon haɗewa dole ne ya ragu:
   
   $$\Delta t \downarrow \ Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Niyya da Haɗari sune Masu Haɓakawa:**  
   [PoArt] ba kawai yana auna "lokacin da aka kashe ba" har ma da matakin ainihin yanke shawara, haɗari, da farashi a cikin wannan lokacin. Samarwar da ba ta ɗaukar haɗari ba (AI) tana da ƙimar ƙanƙanta:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Keɓantacce Shaida ce ta Zahiri, Ba Tallace-tallace Ba:**  
   Alamun da ba za a iya juyawa a cikin samarwa ta zahiri (bugun zane, guntun marmara) suna waje da dabarun `Ctrl+Z` na dijital. Wannan rashin juyawa ($U_{\text{irreversible}}$) yana keɓanta aikin ta hanyar ontology.

> **🔐 TAKAITACCEN BAYANI:** Ko da yake ka'idar daraja na iya zama marar tabbas a matsayin ma'auni (ko da yake abin da ya dace da shi a duniyar gaske ba za a iya auna shi gaba ɗaya ba), manufar wannan dabara ita ce nuna tsarin da alkiblar ma'auni. A zamanin AI, abin da yake da wuyar samu ba "hoto" ba ne amma **aiki mai iya tabbatarwa, lokaci, da niyya.** [PoArt] yana auna wannan karancin kuma yana rubuta shi da **Kunshin Shaida**.

### 🏛️ Mahimmancin Manufar "Injin"

Alamun da suka fito daga Pump.fun ko dandamali makamantan galibi **"tikiti na shiga"** ne kawai. **Injin Bincike na PoArt (PFE)**, duk da haka, shine **matakin dabaru na tsarin mulki** wanda ke ƙayyade wane hakki wannan tikiti ke karewa, yadda za a rubuta aiki kuma yadda za a dawwama da fasaha/kimiyya/fasaha.

> **Lura:** Dalilin da muka ƙaddamar da wannan aikin a Pumpfun shi ne cewa ba mu da isasshen kuɗi ko masu bi da yawa. Amfani da bayanan da ake da su ya kasance dabarun dabara mai kyau, ko da ba na mafi kyawun inganci ba. Ba tare da la'akari da kasafin kuɗi da albarkatu ba, ma'anar dabarun wannan injin a kan GitHub yana tabbatar da cewa aikin ba kawai hasashen kuɗi ba ne, amma hangen nesa na dogon lokaci na **kayan aikin software** da **ɗakin karatu na ƙasa na dijital**.

---

## 🎨 YARJEJENIYAR [PoArt] NA TABBACIN AIKI (Proof of Art Protocol v1.0)

> **"Mai Fasaha na Gaske, Samarwa ta Gaske, Daraja ta Gaske."**

Wannan yarjejeniya tsarin kariya ne na **halitta da hankali** wanda aka ƙera a kan maƙaryata marasa suna waɗanda ke kewaye da yanayin crypto, hotunan AI da aka samar kwa mintuna 5, da al'adar "Pump & Dump".

---

## a) Menene [PoArt]? (Ma'anar Falsafa da Fasaha)

**Tabbacin Fasaha [PoArt];** ma'auni ne na tabbatarwa na hukuma wanda ke tabbatar da cewa ƙimar bayan kadara akan blockchain ba ta dogara ne akan hasashe ba, amma akan **aikin ɗan adam**, **lokaci**, da **makamashi na zahiri** waɗanda za a iya tabbatarwa.

Kamar yadda Bitcoin ke samar da daraja da *"Wutar Lantarki da Ƙarfin Processor"* **(Tabbacin Aiki)**, ayyukan da suka dace da [PoArt] suna samar da daraja da *"Ƙwarewar Fasaha da Lokacin Ɗan adam"*.

Yana kawar da haɗarin *"Mai haɓakawa ya sayar, aikin ya ƙare"* akan dandamali na Pump.fun da DEX; saboda anan daraja ba ta cikin lambar ba ce, amma a cikin **ci gaba da samarwa**.

> **[PoArt] ba ya gaya wa mahalarta "Ka yarda da mu"; yana cewa "Ga shaida, gani da idanunka, tabbatar da lissafinka."**

---

## b) Ma'aunin Ginshiƙai 5 na [PoArt] (Ginshiƙai 5 na Gaskiya)

Waɗannan abubuwa 5 sune masu tacewa waɗanda ba za a iya sarrafa su ba waɗanda aikin dole ne ya wuce don samun hatimin [PoArt].

### 1) Tabbacin Ainihin Kai Tsaye

- **Matsala:** Duniyar crypto cike take da waɗanda suka kafa marasa suna (Masu Haɓakawa) waɗanda ba a san su ba waɗanda ke tara kuɗi suna barin ayyuka.
- **Maganin [PoArt]:** Mai samarwa ba kawai yana tabbatar da takardar shedar ba, amma **kasancewa a lokacin samarwa**. Wannan ya haɗa da zaman yaɗuwa kai tsaye inda ake mu'amala da al'umma kuma ana cika takamaiman buƙatun nan take, ba bidiyon da aka riga aka yi rikodin ba.  
  (Misali, *"Rubuta ranar yau da lambar toshe na yanzu a kusurwar dama na zane"*)
- **Taken:** *"Bots na iya yin zane amma bots ba sa fitar da gumi kuma ba za su iya yin tsarin gaggawa ba."*

### 2) Tabbacin Aiki da Tsari

- **Matsala:** Hotunan AI (Hankali na Wucin Gadi) da aka samar kwa daƙiƙa 2 suna samun kulawar "jpeg" iri ɗaya kamar zanen mai a cikin watanni 2 a duniyar dijital.
- **Maganin [PoArt]:** Ana rubuta tsarin "ciki da haihuwa" na aikin. Ana rubuta matakan zane, yadudduka na fenti, awanni da aka tara da aka kashe da tsarin zahiri da mai fasaha ya samu yayin ƙirƙirar aikin. Wannan yana ƙara **"Farashin Lokaci"** ga alamar. Yawan wahalar samar da kadara, ƙarfin darajar ta.

### 3) Tabbacin Darajar Kyawawan Abubuwa

- **Matsala:** Al'adar "Meme" mai mai da hankali kan barkwanci na nan take yayin watsi da kyawawan abubuwa da zurfin fasaha, wanda ke haifar da ayyukan "Hype" masu gajeren lokaci.
- **Maganin [PoArt]:** Aikin dole ne ya kasance da ƙa'idodin fasaha na ilimi, ka'idar launuka, ƙa'idodin tsari, da ilimin kayan aiki (Impasto, Texture, da sauransu). Abun ciki bai kamata ya sa ka yi dariya kawai ba; ya kamata ya motsa sha'awar masu kallo kuma ya kasance da **ƙimar tattarawa**.

### 4) Sabon Ra'ayi

- **Matsala:** Dubbai na tsabar kare/cat kwafi marasa ƙirƙira.
- **Maganin [PoArt]:** Aikin dole ne ya gina sabuwar gada mai haɗa fasaha, kimiyya, falsafa ko fasaha a cikin tsari mai ma'ana.  
  (Misali, Haɗa hoton gargajiya na David da bayanan kasuwar crypto; sarrafa ra'ayin cewa fahimtar ɗan adam "tana zama dutse" ta haka kuma tushe shi da tushen kimiyya.)  
  Aikin bai kamata ya zama biki na gani kawai ba amma kuma ƙalubale na hankali wanda ke motsa tunani game da **Kimiyya, Falsafa ko Fasaha**.

> [!IMPORTANT]
> **Misali na Tunani (Tasirin Las Palmitas):** A unguwar Las Palmitas a Mexico, wadda laifuka ke damunta, sama da gidaje 200 an mayar da su zuwa babban bakan gizo. Sakamakon wannan shiga tsakani na kyawawan abubuwa, yawan laifuka a unguwar sun ragu kaɗan, kuma matasa sun fara shiga cikin fasaha maimakon ƙungiyoyin laifuka. Canjin kyawawan abubuwa ya sake tsara girmaman mutane ga muhallinsu da juna (Haɗin Kai na Zamantakewa).
>
> **Tsammanin:** Aikin da ya shiga jerin [PoArt] dole ne, kamar a cikin misalin sama, ya ƙunshi alaƙar dalili da sakamako na zamantakewa, kimiyya ko falsafa fiye da kyawawan abubuwa na gani kawai. Tunda lokaci shine kadara ɗaya ba za a iya sayewa da kuɗi ba, a cikin wannan yarjejeniya dole ne a tabbatar da lokaci ta hanyar ajiye shi azaman jingina. Tushen ra'ayi na aikin dole ne ya kasance mai ƙarfi da na duniya duka ta yadda ko a cikin yanayin da zai yiwu na CTO (Ɗaukar Al'umma) shekaru bayan haka, al'umma za ta iya ci gaba da kai tsaye damar ƙirƙira ta aikin ta hanyar gado wannan gado.

### 5) Niyya Ba ta Algorithm ba

- **Matsala:** Samarwa ta dijital cikakke amma mara ruhu waɗanda ke maimaita juna.
- **Maganin [PoArt]:** Dole ne a ji keɓancewar niyyar ɗan adam wanda zai iya yin kuskure, ɗaukar haɗari da samun canje-canjen tunani a cikin aikin. Rashin tabbas a bugun goga, martanin kayan aiki da ba a zata ba, da yanke shawara na nan take na mai fasaha sune **Sa hannun Halitta** wanda ke raba aikin daga "Samarwar Inji".

---

## c) Tsarin Tabbatarwa da Hana Zamba

Wannan tsarin yana tabbatar da cewa aikin yana kasancewa abin dogaro kuma yana raye ba kawai "a farkon" ba amma "har abada".

### 📦 Kunshin Shaida - Tagwayen Dijital

A bayan kowane aikin da aka tabbatar da [PoArt] akwai kunshin bayanai mai ɓoyewa kuma mai hatimin lokaci wanda masu zuba jari za su iya saukewa:

- **Rikodin Bidiyo RAW:** Hoton ɗanyen da ba a katse ba na lokacin samarwa.
- **Nazarin Metadata:** Ranar ƙirƙirar fayil, bayanan na'urar da aka yi amfani da ita da bayanan wuri.
- **Maganganun Zahiri:** Shaida cewa aikin yana wanzu a duniyar zahiri  
  (Misali, Jarida na yanzu ko bayanan blockchain na wannan lokacin kusa da aikin).

> *Lura ta daidaito:* Kalmar "kunshin shaida" tana haɗuwa da sarkar **Kunshin Shaida → EvidenceRoot → NotarySeal** a cikin sassan da suka gabata; wato, amincin kunshin yana wakilta da hatimi mai iya tabbatarwa.

### 🔄 Sabuntawa na Kwanaki 365 (Yarjejeniyar Dorewa)

- **Fasalin Juyin Juya Hali:** A cikin ayyukan crypto, "Dev" (Mai Haɓakawa) yana fitar da alamar kuma galibi yana ɓacewa bayan watanni 1-2 (Ja Mai Laushi). [PoArt] yana sa wannan ya zama ba zai yiwu ba.
- **Ƙa'ida:** Matsayin "Mai Fasaha da aka Tabbatar" ba na rayuwa bane. **Shekara 1** kawai ce mai inganci.
- **Aiki:** Mai fasaha/mai haɓakawa dole ne ya gabatar wa al'umma **sabon aiki mai mahimmanci kuma mai iya tabbatarwa** kowane kwanaki 365.
- **Misali na Yanayi:** Ka ƙaddamar da aikin a 2026. A cikin Janairu 2027, tsarin yana ba da gargaɗi "Lokacin Shaida ya Ƙare". Idan mai fasaha bai gabatar da sabon nuni, sabon aikin zahiri ko sabon haɗin fasaha ba, "Alamar Amincewa" na aikin tana faɗuwa.
- **Sakamako:** Wannan tsarin yana tabbatar da cewa **abun ciki ba ya taɓa rasa dacewa** kuma cewa mai zuba jari ba ya taɓa fuskantar tsoron *"Mai haɓakawa yana nan har yanzu?"*. Aikin ya zama studio mai rai.

### 🚩 Yarjejeniyar Tuta Mai Ja

**A yanayin kowane zamba da al'umma ko algorithms suka gano (amfani da AI, aikin da aka sata, bidiyo da aka sarrafa):**

1. Ana yi wa takardar shedar alama nan take a matsayin **"VOID" (BA SHI DA AMFANI)**.
2. Ana yiwa kunshin shaida alamar jama'a a matsayin **"Karya"**.
3. Ana sanya aikin a cikin jerin baki na [PoArt]. Wannan yana ƙarfafa cewa a duniyar da ba ta da mulki na tsakiya, **suna shi ne kuɗin kawai**.

---

## d) Ƙarshe: Ba Casino Ba, Amma Gidan Kayan Gargajiya

**Pump.fun da Musayar Rashin Mulki na Tsakiya (DEX) abin takaici casino ne a yanzu; fitilu suna walƙiya, kowa yana bin riba mai sauri, kuma gidan (maƙaryata) koyaushe yana cin nasara. Dalilin da muka fara aikin a nan shi ne rashin isasshen kasafin kuɗi kuma samun yanayi don isa ga masu sauraro da ke akwai ta hanyar yaɗuwa kai tsaye.**

**[PoArt] katanga ce da aka gina a tsakiyar wannan casino.**

- 🎰 Casino ta dogara ne akan wasannin kati; mu muna dogara akan **gaskiyar zahiri**.
- 🃏 Casino yana buɗe ga zamba; mu muna buɗe ga **shaida mai bayyana**.
- ⏳ Casino na ɗan lokaci ne; muna mai da hankali ga **dawwamammen fasaha da kimiyya**.

**Alamar da ke amfani da wannan yarjejeniya ba "tsabar kuɗi" kawai ba ne; jarin dijital ne mai ɗauke da gumi, fenti, lambar, da falsafa.**

---

## 🗳️ 6) MULKI DA RAJISTAR JAMA'A

**Manufar wannan sashe ita ce: canza ma'aunin [PoArt] daga matakin "amincewa da mutane" zuwa kayan aikin jama'a mai dorewa tare da rajista + tabbatarwa + kulawa ta al'umma.**

### 6.1 Rajistar Jama'a

- **Rajistar Jama'a:** Ana rubuta duk bayanan da aka amince da su a `ilhanart.org/registry` (ko GitHub Registry).

**Dabarun rajista (ma'auni da aka ba da shawara - a cikin tsarin hanyar JSON):**

Kowane shigarwa da ke shiga rajista yana ɗauke da waɗannan filayen masu mahimmanci masu iya tabbatarwa:

- **Ainihi da Matsayi:**
  - `certificate_id` (tunani mai iya karantawa)
  - `status` (active / void)
  - `void_reason` (idan ya dace)
  - `visibility` (private / masked / public)
  - `created_at` (hatimin lokaci)

- **Hukumar Bayarwa:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Bayanan Aikin:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (idan zai yiwu; don ainihin ƙofar alamar)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Bayanan Bincike:**
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
  - `governance.veto_threshold`

Rajista na iya samun matakan 2:
- **1)** Fihrisa mai iya karantawa ga mutane (jerin gidan yanar gizo / bincike / tacewa)
- **2)** Bayani mai iya karantawa ga inji (rikodin JSON; don tabbatarwa ta PFE)

**Wannan "shigarwa" yana zama mai iya tabbatarwa ta hanyar sarkar Kunshin Shaida → EvidenceRoot → NotarySeal na PFE. Rajista yana ba da manufofin tabbatarwa, ba "da'awa" ba.**

---

### 6.2 Kini na Al'umma na 40% (Mulki Mai Ƙofar Alama)

- **Kini na Al'umma na 40%:** Ƙuri'a tana farawa wata ɗaya kafin ba da matsayi; kinin 40% na al'umma **mai Ƙofar Alama (da aka tabbatar da Solana)** yana soke buƙatar.

**Hanyar ƙuri'a (tsari mai bayyana da aka ba da shawara):**
- **Tagar aikace-aikace:** Aikin ɗan takarar yana buɗe "rijistar ɗan takara na PoArt" (rikodin ɗan takara suna bayyana a cikin matsayin "jiran gani").
- **Lokacin bita:** Al'umma tana bincika shaida na kwanaki 30 (Kunshin Shaida + rikodin yaɗuwa kai tsaye + metadata).
- **Tabbatarwa mai ƙofar alama:** Ana yin ƙuri'a tare da jakatu da aka tabbatar da Solana (misali mallakar alama/NFT na musamman + sa hannun jakata).
- **Ƙa'idar kini:** Idan 40% na ƙuri'u ne **ƙin yarda (A'A / KINI)**, ana ƙin buƙatar.
- **Bayyananne:** Ana adana sakamakon ƙuri'a a cikin rajista a matsayin "rikodin yanke shawara" (kwanan wata, rabo, ID na hoto).

---

### 6.3 Daidaitawa ta Metadata (Daidaitawa da Duniyar Zahiri)

- **Daidaitawa ta Metadata:** Bayanan fasaha a cikin rajista dole ne su yi daidai 100% da huluki ta zahiri.

**Ma'anar fasaha ta "daidaituwa 100%" (bayyananne da aka ba da shawara):**
- **Mafi ƙarancin daidaituwa (tilas):**
  - `asset.fingerprints.sha256/sha512` a cikin rajista dole ne ya kasance **iri ɗaya** da hash na fayil ɗin da ake magana akai.
  - Lokacin da aka sake samar da `proof.notary_seal` a cikin rajista (idan Kunshin Shaida yana wanzu), dole ne ya kasance **iri ɗaya**.
- **Daidaitawar tunani na zahiri (nau'in shaida):**
  - Aikin zahiri + tunanin kwanan wata/toshe da aka nuna a yaɗuwa kai tsaye da shaida iri ɗaya dole ne su yi daidai da Kunshin Shaida.
- **Yarda da sirri:**
  - Filayen kamar IP/wuri a ganuwa ta `masked` ana buga su **bisa ga ma'aunin rufewa**.

---

### 6.4 Rigima da Sokewa

Rajista ba tsarin "amincewa" kawai ba ne; tsarin **bita mai rai ne a kan zamba**.

- Lokacin da aka fara rigima, ana iya sanya shigarwar a yanayin **"review" (bita)**.
- Idan an gano zamba, ana yiwa alama a matsayin `status: void` tare da ƙara dalili:
  - `void_reason` (amfani da AI / sata / sarrafa, da sauransu)
  - `revoked_at` (lokacin sokewa)
- Tushen yanke shawarar sokewa yana bayyana a fili a cikin rajista:
  - ƙuri'ar al'umma / kwamitin da aka ba izini / bayanin bincike na kimiyya (abin da ya dace)

> **Wannan sashe shine takwaror rajista na manufar VOID a cikin sashen "Yarjejeniyar Tuta Mai Ja".**

---

### 6.5 Misalin Shigarwar Rajista (Mai Iya Karantawa ga Inji)
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
> *Lura: `asset.fingerprints.sha512` da sauran ƙimar hash an taƙaita su don nuna; a cikin aiwatar da gaske, ana amfani da cikakkun igiyoyin haruffa na hexadecimal.*

---

## 7) 🔐 HATIMI NA FASAHA (NOTARY SEAL)

Algorithm na hatimi maras girgiza wanda **Injin Bincike na PoArt (PFE) v1.0** ya samar:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Yarjejeniyar [PoArt] ta Notary na Dijital da Shaida ta Kimiyya (Beta v1.0)

> **"Al'ada ta fi babba fiye da jari. Ka kare ayyukanka yau, ka ɗauke su zuwa gobe."**

---

## Me yasa Jama'a?

Tsaro na gaske yana fitowa daga bayyananne. Godiya ga tsarin **Rajistar Jama'a** namu, kowa a ko'ina a duniya zai iya tabbatar da cewa fayil asali ne cikin daƙiƙa, ba tare da bukatar kowace hukuma ba.

---

## 🧩 Me yasa "Ƙananan Gani" da Yawa?

Wannan shine sashi mafi mahimmanci na lambar (menu na zaɓin gani). Waɗannan zaɓuɓɓukan suna ba masu amfani damar daidaita **"Sirri da Bayyananne"**:

### 🔒 Mai Zaman Kansa

- **Yanayi:** Mai fasaha har yanzu baya son buga aikin, amma yana son hatimi shi da lokaci don tabbatar da "na yi wannan a wannan kwanan wata".
- **Abin da Lambar Take yi:** Yana rubuta bayani a cikin bayanan adana amma yana buga hatimi `visibility: "private"`. Daga baya lokacin rubuta manufar "Karanta ta Jama'a", zaka iya ɓoye waɗannan rajista daga jama'a tare da `WHERE visibility = 'public'`.

### 🕶️ An Rufe

- **Yanayi:** Mai fasaha yana son bayyananne amma yana tsoron adireshin gidansa (wurin IP) za a samo shi.
- **Abin da Lambar Take yi:** Ayyukan `maskIP` da `maskLoc` suna aiki a gefen JavaScript. Yana juyar da adireshin IP zuwa tsarin `88.241.***.***`, wurin zuwa tsarin `***/TR`, kuma yana aika sigar da aka tantance zuwa bayanan adana.
- **Lura ta Sirri:** Ana yin rufewa a mai bincike, Supabase ba ta ganin ainihin wurin. **Duk da haka:** Idan aka yi amfani da APIs na wasu kamar ipapi.co don bayanan wuri, waɗannan masu samar da sabis suna ganin adireshin IP a lokacin buƙatar.
- **Hatimewa a Yanayin Rufewa:** Ana yin ƙididdigar EvidenceRoot da NotarySeal tare da bayanan bincike da aka rufe; saboda haka tabbatarwa tana kasancewa mai iya tantancewa.

### 🌍 Jama'a

- **Yanayi:** Cikakken bayyananne. Bisa ga ma'aunin [PoArt], a fili ana bayyana inda, lokacin da, daga wane cibiyar sadarwa aka samar da aikin.

---

## 💡 Ƙirƙira ta Fasaha

PoArt ba tsarin ɗora fayil kawai ba ne. Injin **"Sarkar Kulawa ta Kimiyya"** ne wanda ke kawo sabon ma'auni ta hanyar haɗa matakan fasaha 3 daban-daban a cikin tukunya guda.

**Matakin da aka bayyana a matsayin "injin" a wannan sashe ya dace da tushen Injin Bincike na PoArt (PFE) a cikin kalmomin farko.**

### 1) Hashing na Gefen Abokin Ciniki (Mafi Girman Sirri)

Ba a ɗora fayilolinku na fasaha zuwa uwar garken. Injin mu na tushen mai bincike (gefen abokin ciniki) yana ƙididdige hash (taƙaitaccen dijital) na fayil ɗin akan kwamfutarku. Wannan tambarin yatsa da metadata kawai ake aikawa zuwa uwar garken.

> **Lura ta Sirri:** Ba a ɗora fayil ɗin aikin zuwa uwar garken kuma an kare shi ta wannan hanyar. Duk da haka, bayanan bincike (IP/wuri) ana raba su bisa ga yanayin gani da aka zaɓa (mai zaman kansa/an rufe/jama'a).

### 2) Haɗakar Bayanan Bincike (Ƙarfin Kimiyya)

Da yawa fiye da hatimin lokaci na yau da kullun. Tsarin yana haɗa waɗannan bayani a cikin "Hatimin Asali" guda:

- **Taƙaitaccen Dijital (SHA-512):** Tambarin yatsa ta amfani da ma'aunin taƙaitaccen cryptographic (SHA-512) wanda zai karye idan har pixel ɗaya na aikin ya canja.
- **Wuri da Lokaci:** Kwanan wata mai daidaitattun milliseconds, ƙasa, birni da bayanan gundumomi na ciniki.
- **Ainihin Na'ura:** Tsarin aiki, mai bincike da nau'in na'ura (nazarin User-Agent).

---

## 🛡️ Abubuwan Amfani da Amfani

Idan kai mai fasaha ne, marubuci ko mai zane, cewa "Na yi wannan a baya" ba ya isa; kana bukatar tabbatarwa.

**Aikin da kake hatimewa da PoArt:**

- **Shaida ta Lissafi:** Idan har pixel ɗaya na fayilinka ya canja, tsarin ya sani. Sarrafa ba zai yiwu ba.
- **Tushen Doka:** An rubuta kwanan watan da, birnin da, daga wace na'ura aka hatimi aikin.
- **Takardar Shedar Nan Take:** Yana samar da **"Takardar Shedar Ainihin Kadara"** na musamman a gare ka cikin daƙiƙa, mai lambar QR kuma an hatimewa.

---

## ⚙️ Gine-ginen Tsarin da Fasalolin Fasaha

An tsara tsarin akan gine-ginen "Serverless", mai mai da hankali ga babban aiki da ƙarfin haɓakawa.

| Mataki | Fasaha | Bayani |
|--------|-----------|-------------|
| **Rufewa** | SHA-256 & SHA-512 | Taƙaitaccen cryptographic mai mataki biyu |
| **Bayanan Adana** | Supabase (PostgreSQL) | Tsarin bayanan JSONB, manufofin RLS |
| **Bayanan Bincike** | ipapi.co API | Uku na IP/Wuri/Lokaci |
| **Bayyanawa** | html2canvas + jsPDF | Samar da PNG/PDF na gefen abokin ciniki |
| **Gaban gida** | Vanilla JavaScript | Dogaro da tsari sifili |
| **Tsaro** | Hashing na gefen abokin ciniki | Fayil ba ya taba zuwa uwar garken |

### Fasalolin da Suka Bayyana

| Fasali | Bayani | A Masu Fafatawa? |
|---------|-------|-----------------|
| **UI Jawo & Sauke** | Jawo da sauke fayil, gani nan take | ❌ Babu a mafi yawa |
| **Fitar da Tsari da Yawa** | PNG, JSON, PDF - danna ɗaya | ⚠️ Iyakance |
| **Ganin Lokaci Mai Sauri** | Ganin takardar shedar kai tsaye | ❌ Babu |
| **Sarrafa Sirri** | Zaɓuɓɓukan Mai Zaman Kansa/An Rufe/Jama'a | ❌ Babu |
| **Hash na Gefen Abokin Ciniki** | Fayil ba ya taba zuwa uwar garken | ✅ Kawai a wasu |
| **Metadata na Bincike** | IP, wuri, na'ura, lokaci - duk tare | ❌ An rabu |
| **Tabbatarwa ta QR** | Lambar QR ta tabbatarwa nan take | ⚠️ Iyakance |
| **Iyakance Saurin** | Kariya daga spam (RLS + Abokin Ciniki) | ❌ Babu a mafi yawa |

---

## 🗺️ Taswirar Hanya: Makomar "Ba tare da Amincewa"

Sigar yanzu **(Beta v1.0)** an tsara ta don ba masu amfani na ƙarshe mafi girman sauri, mai sauƙin amfani da shiga kyauta. Duk da haka, hangen nesa na ƙarshe shine canji zuwa tsarin da har ma da mai kula da bayanan adana (mu) ba zai iya shiga ba.

### Mataki na 1: Beta (Yana Raye A Yanzu)

- **Kayan Aikin:** Bayanan Adana na Gajimare (Supabase).
- **Manufa:** Sauri, kawar da shingayen UX (Gwanin Amfani) da daidaitawa. Samar da tsaro "ba tare da juriya ba".

### 🚀 Mataki na 2: (Buƙatun Baya / Aikin Edge)

Wannan mataki ya ƙunshi canji daga tsarin aiki "gefen abokin ciniki" gaba ɗaya zuwa tsarin "Ikon Gefen Uwar Garken" mafi tsaro da kulawa.

| Abu | Me Yake Kawo? | Tarin Fasaha | Fifiko |
|-------|---------------|------------|---------|
| **`INSERT` → Aikin Edge** | Hana spam + tsaron maɓallin API | Supabase Edge (Deno) | 🔴 Babba |
| **Sa Hannun Jakata** | Tabbatarwa ta cryptographic | Solana Wallet Adapter | 🟡 Matsakaita |
| **Madadin IPFS/Arweave** | Rashin canzawa ba tare da mulki na tsakiya ba | IPFS SDK + Pinata | 🟢 Ƙasa |
| **Tsarin Sokewa** | Soke takardar shedar karya | Sabunta Tsarin DB | 🔴 Babba |
| **Rajistar Bita** | Rikodin tambaya na kimiyya | Tebur na rajista na musamman | 🟡 Matsakaita |
| **OpenTimestamps** | Anka na Bitcoin | OTS JavaScript | 🟢 Ƙasa |
| **Haɗin DID** | Ainihi Ba tare da Mulki na Tsakiya | ION/Ceramic | 🟢 Ƙasa |

### Mataki na 3: Cikakken Rashin Mulki na Tsakiya (Dogon Lokaci)

| Fasali | Manufa | ETA |
|---------|------|-----|
| **Rajistar Blockchain** | Rajista akan sarkar Ethereum/Solana | Q4 2026 |
| **Mulkin DAO** | Gudanarwa ta al'umma | Q1 2027 |
| **Tallafin Sarkokin da Yawa** | Polygon, Arbitrum, Base | Q2 2027 |
| **Amincewa ta Doka** | Inganci a kotunan Turkiyya | 2027-2028 |
| **API don Masu Haɓakawa** | Manufar API ta jama'a | Q3 2026 |

---

## 📊 Nazarin Gasa (An Sabunta)

PoArt yana a "Sweet Spot" wanda ke cika rashi na hanyoyin da ake da su.

| Fasali | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Farashi** | 🆓 Kyauta | 🆓 | 💰 Kuɗi | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI Jawo & Sauke** | ✅ Mai Sauƙi Sosai | ❌ CLI | ⚠️ Matsakaita | ⚠️ Matsakaita | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Fitar da Tsari da Yawa** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Ganin Lokaci Mai Sauri** | ✅ Kai Tsaye | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Sarrafa Sirri** | ✅ Yanayi 3 | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Hash na Gefen Abokin Ciniki** | ✅ Sirri | ✅ | ❌ Ɗora | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Metadata na Bincike** | ✅ Cikakke | ❌ | ❌ | ⚠️ Iyakance | ❌ | ⚠️ | ❌ | ⚠️ |
| **Tabbatarwa ta QR** | ✅ Nan Take | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Iyakance Saurin** | ✅ RLS+Abokin Ciniki | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Anka na Blockchain** | 🔄 Taswirar Hanya | ✅ Bitcoin | ✅ Ethereum | ✅ Da Yawa | ✅ | ✅ | ✅ | ✅ |
| **Buɗe Tushe** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Tallafin Turkiyya** | ✅ Asali | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Maganin:**
- ✅ : Cikakken tallafi / akwai
- ⚠️ : Iyakance / a cikin tsare-tsaren kuɗi
- ❌ : Babu / ba a tallafawa
- 🔄 : A cikin taswirar hanya (ana haɓakawa)
- 🆓 : Gaba ɗaya kyauta
- 💰 : Kuɗi / ana buƙatar rajista

### Rashi na Masu Fafatawa, Ƙarfin PoArt

| Rashi | Masu Fafatawa | PoArt |
|-------|-------------|-------|
| **Matsalolin Amfani** | CLI, ilimin API, jakata ana buƙata | Jawo da sauke, shirye cikin dannawa 3 |
| **Shinge Farashi** | Rajista $50-500/wata | 100% kyauta |
| **Sirri** | Ana ɗora fayil zuwa uwar garken | Gefen abokin ciniki, fayil ba ya taba zuwa |
| **Bayanan Bincike** | Hatimin lokaci kawai | IP, wuri, na'ura, lokaci - duk |
| **Tallafin Turkiyya** | Babu ko iyakance sosai | Tallafin harshe na asali |
| **Buɗe Tushe** | Akwatin rufaffiya | Duk lambar a buɗe akan GitHub |

---

## 🧬 Tsarin Bayanan Yarjejeniya (JSON Schema)

**Kowane takardar shedar [PoArt] tana da katin ainihi na JSON mai ɗaukarwa kuma mai iya tabbatarwa wanda aka samar da shi a ma'auni mai zuwa.**

> **Lura:** Wannan tsarin JSON na ainihi tsarin takardar shedar da ake gabatar wa masu amfani. A cikin rikodin rajista, ana amfani da `registry.asset` maimakon `identity.asset_data` (taswira: `identity.asset_data` == `registry.asset`).
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

## 🔬 Zurfin Fasaha: Algorithm na Hatimi

### Ayyukan Hash Mai Tantancewa
```javascript
// Ayyukan Taimako: Canza taƙaitawa zuwa igiyar hexadecimal
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Canza igiya zuwa jerin bytes
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Samar da igiyar bincike ta asali (v1.0: tsarin fili mai ƙayyadaddun + UTF-8 + mai rabu \n)
// Lura ta Mataki na 2: Canji zuwa JSON na asali tare da RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Tsarin Samar da NotarySeal (Cikakken Mai Tantancewa)
```javascript
// 1. Ƙididdige FileHash (gefen abokin ciniki)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Tattara bayanan bincike (amfani da hatimin lokaci ɗaya)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Samar da hatimin lokaci ɗaya
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Iri ɗaya hatimin lokaci
  };
  
  return { forensics, timestamp };
}

// 3. Ƙirƙirar EvidenceRoot (tare da rufewa na asali)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Samar da NotarySeal (amfani da iri ɗaya hatimin lokaci)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Ayyukan taimako na rufewa (tallafin IPv4 da IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Bincike IPv4
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

### Hanyar Tabbatarwa (Matakan Biyu)

#### Quick Verify (Tabbatarwa Mai Sauri)
```javascript
// Tabbatar da hash na fayil kawai (tuta mai ja mai sauri)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Samu daga rajista
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Kwatanta hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Asali - Hash na fayil ya dace"
    };
  } else {
    return {
      valid: false,
      message: "❌ Karya - An sarrafa fayil"
    };
  }
}
```

#### Full Verify (Cikakken Tabbatarwa)
```javascript
// Sake samar kuma tabbatar da EvidenceRoot da NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Samu daga rajista
  const cert = await fetchFromRegistry(certificateId);

  // 1) Tabbatar da FileHash (tuta mai ja mai sauri)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Karya - Hash na fayil bai dace ba" };
  }

  // 2) Sake samar da EvidenceRoot (da bayanan bincike da aka adana a cikin rajista)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Bai dace ba - EvidenceRoot bai tsaya ba" };
  }

  // 3) Sake samar da NotarySeal (da iri ɗaya hatimin lokaci + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Bai dace ba - NotarySeal bai tsaya ba" };
  }

  // Zaɓi: A Mataki na 2, kuma tabbatar da signer_sig tare da attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Sa hannu mara inganci" };

  return { valid: true, message: "✅ Asali - Cikakken tabbatarwa ya wuce" };
}
```

> **Mahimman Bayanai:**
> - **Quick Verify:** Yana tabbatar da hash na fayil kawai don amfani mai sauri.
> - **Full Verify:** Yana tabbatar da duk matakan yarjejeniya (EvidenceRoot + NotarySeal).
> - Ana aiwatar da dukkan ayyukan hash ta hanyar da za a iya tantancewa tare da rufewa da masu rabu masu ƙayyadaddun.
> - **Ma'aunin kawaida v1.0:** Tsarin fili mai ƙayyadaddun + rufewa na UTF-8 + mai rabu `\n`.
> - **Tsarin Mataki na 2:** Canji zuwa JSON na asali tare da RFC 8785 (JCS - JSON Canonicalization Scheme).
> - A yanayin rufewa, ana yin ƙididdigar EvidenceRoot da NotarySeal tare da bayanan bincike da aka rufe; saboda haka tabbatarwa tana kasancewa mai iya tantancewa.
> - Ana amfani da hatimin lokaci ɗaya a duk tsarin (bincike + NotarySeal); an tabbatar da tantancewa.
> - **Sunayen filayen bincike:** `ip_masked`, `location`, `device`, `timestamp` (lambar da rajista sun dace gaba ɗaya).
> - **Hanyar rajista:** `certificate.asset.fingerprints` (tana daidaitawa gaba ɗaya da lambar tabbatarwa).
> - **signer_sig a cikin rajista:** Filin `proof.signer_sig` yana buƙata don Cikakken Tabbatarwa.
> - Za a kunna tsarin SignerSignature a Mataki na 2 tare da Solana Wallet Adapter; a v1.0, ana iya yin tabbatarwa tare da `attestation_pubkey`.

---

## 📈 Ƙididdiga na Amfani (Maƙasudin Q1 2026)

| Ma'auni | Maƙasudi | Matsayi |
|--------|--------|--------|
| **Jimlar Takardun Shedar** | 1,000 | 🔄 Ci gaba |
| **Masu Amfani Masu Rai** | 500 | 🔄 Ci gaba |
| **Adadin Tabbatarwa** | 5,000 | 🔄 Ci gaba |
| **Lokacin Kasancewa** | 99.9% | ✅ Mai Rai |
| **Matsakaicin Lokacin Amsawa** | <200ms | ✅ Mafi Kyau |

---

## 🌍 Al'umma da Tallafi

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Yanar Gizo:** [ilhanart.org](https://ilhanart.org)
- **Imel:** galeri@ilhanart.org

---

## 🙏 Masu Bayarwa

Yarjejeniyar PoArt tana ci gaba da bunƙasawa tare da gudummawar al'ummar buɗaɗɗen tushe.

**Don bayarwa:**
1. Fork ma'ajin
2. Ƙirƙiri reshe na fasali (`git checkout -b feature/amazing-feature`)
3. Ƙaddamarwa (`git commit -m 'Add amazing feature'`)
4. Tura (`git push origin feature/amazing-feature`)
5. Buɗe Buƙatar Ja

### 🛠️ Me Muke Buƙata Yanzu? (Kiran Taimako)

Yarjejeniyar PoArt tana neman ƙwararrun masu haɓakawa a fannoni masu zuwa don ci gaban **Mataki na 2**:

* **Ayyukan Edge na Supabase:** Matsar da kariya daga spam zuwa gefen uwar garken.
* **Solana Web3.js:** Haɗin sa hannun jakata.
* **IPFS / Arweave:** Haɗin sabis na ajiya da ƙafawa.

> Don Allah fara tattaunawa a shafin "Issues" kafin ƙara fasali.

---

**Yarjejeniyar [PoArt] Proof of Art v1.0**  
*"Al'ada > Jari"*

## 🧾 Lasisi

Lasisi na MIT © 2026 Ilhan Art Gallery Initiative

Duba [![Lasisi](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) don cikakkun sharuɗɗa.

---

## 💬 Yabo

![Sigar](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Tsaro](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Dandamali](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![Lasisi](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Ana haɓaka wannan aikin ta hanyar ƙungiyar [Ilhan Art Gallery], kuma lambobin tushe na suna bayyane ga jama'a don bayyananne.**

**YARJEJENIYA V1.0 // AN HATIMEWA DA SHA-512**

*© 2026 İLHAN ART | DUKKAN HAƘƘOƘIN AN AJIYE DON AYYUKAN FASAHA, HOTUNA DA RA'AYOYI.*

---
