# 📚 சொற்களஞ்சியம் & கருத்துக்கள்
> **"இந்த நெறிமுறையின் மொழியைப் புரிந்துகொள்வது அதன் பார்வையைப் புரிந்துகொள்வதாகும்."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: முக்கிய உள்கட்டமைப்பு

**PoArt Forensic Engine (PFE)** என்பது [PoArt] நெறிமுறையின் பின்னணியில் உள்ள முக்கிய தர்க்கம் மற்றும் தொழில்நுட்ப செயல்பாட்டைக் குறிக்கும் முக்கிய அடுக்கு ஆகும். கலைப்படைப்பின் மூல உற்பத்தி தரவை எடுத்து, சரிபார்க்கக்கூடிய மற்றும் மாற்ற முடியாத **டிஜிட்டல் ஆதாரமாக** மாற்றும் "தடயவியல் இயந்திரம்" இதுவாகும்.

### 🧩 ஏன் "PoArt Forensic"?

- **PoArt (Proof of Art):** இயந்திரத்தின் கவனம், டிஜிட்டல் சொத்தின் மதிப்பை ஊகத்தின் அடிப்படையில் அல்லாமல், **நிரூபிக்கக்கூடிய உற்பத்தி செயல்முறையின்** அடிப்படையில் அமைப்பதாகும்.
- **Forensic (தடயவியல் சரிபார்ப்பு):**
  - **தொழில்நுட்ப வரையறை:** உற்பத்தி செயல்முறை தரவுகள் (தூரிகை அடிகள், timelapse, logs) மாற்றப்படவில்லை என்பதை சரிபார்க்க வடிவமைக்கப்பட்ட அல்காரிதம் மற்றும் பதிவு சங்கிலி அணுகுமுறை.
  - **தத்துவ அடுக்கு:** செயற்கை நுண்ணறிவு (AI) "உடனடி வெளியீடு" உற்பத்தி செய்வதற்கு மாறாக; மனிதனின் **நேரம், முயற்சி மற்றும் முடிவின் விலை** என்பதை அளவிடக்கூடிய யதார்த்தமாக மாற்றும் கோரிக்கை.

> குறிப்பு: பிளாக்செயின் (எ.கா. Solana) ஒருங்கிணைப்பு PFE-யின் மையம் அல்ல; சரிபார்ப்பு/பதிவேட்டிற்கு தனியாக வரையறுக்கப்படும் **Chain Anchor Layer** ஆக கருதப்படுகிறது.

### 🛠️ v1.0 தொழில்நுட்ப வரம்பு

**PoArt Forensic Engine (PFE) v1.0** சிக்கலான நிதி மாதிரிகள் இல்லாமல் இந்த **3 முக்கிய தூண்களின்** மீது கட்டமைக்கப்பட்டுள்ளது:

1. **Hashing & Sealing (முத்திரையிடுதல்):**  
   PFE, Evidence Pack-ல் உள்ள அனைத்து உருப்படிகளையும் (படைப்பு கோப்பு, வீடியோ, JSON/log, கையொப்பம் போன்றவை) தீர்மானிப்புக்குரிய முறையில் செயலாக்கி தனித்துவமான **NotarySeal** மதிப்பை உருவாக்குகிறது.

   **முக்கிய கருத்துக்கள் (v1.0):**
   - **FileHash (படைப்பு விரல்ரேகை):** படைப்பு கோப்பின் பைட்டுகளிலிருந்து உருவாக்கப்பட்ட hash.
   - **EvidenceRoot (ஆதார தொகுப்பு வேர்):** Evidence Pack-ன் ஒருமைப்பாட்டைக் குறிக்கும் வேர் சுருக்கம் (Merkle root அல்லது canonical manifest hash).
   - **NotarySeal (இறுதி முத்திரை / PFE வெளியீடு):** EvidenceRoot + நேரம் + கையொப்பம் சேர்க்கையிலிருந்து உருவாக்கப்பட்ட இறுதி முத்திரை.

   **சூத்திரங்கள் (முதலீட்டாளருக்கு தெளிவாக):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload வரையறைகள் (v1.0):**
   
   - **EvidenceRootPayload:**
   ```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
   ```
   
   - **NotarySealPayload:**
   ```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
   ```
   
   > குறிப்பு: PFE வெளியீடாக கருதப்படும் மதிப்பு **NotarySeal** ஆகும். **SignerSignature** வழிமுறை கட்டம் 2-ல் (Solana Wallet Adapter உடன்) செயல்படுத்தப்படும்; தற்போதைய v1.0-ல் கணினியின் சொந்த attestation கையொப்பம் பயன்படுத்தப்படுகிறது.

2. **Indexing (காப்பகம்):**  
   எந்த வாலெட், எந்த தேதியில், எந்த படைப்புக்கு **Labor Proof (உழைப்பு ஆதாரம்)** சமர்ப்பித்தது என்பதை; வெளிப்படையான மற்றும் வினவக்கூடிய பதிவு அடுக்கில் பதிவு செய்கிறது.

3. **Verification (சரிபார்ப்பு):**  
   ஒரு படைப்பின் அசல் தன்மை கேள்விக்குள்ளாக்கப்படும்போது PFE மூல ஆதாரங்களை மீண்டும் செயலாக்குகிறது; கணக்கிடப்பட்ட **EvidenceRoot / NotarySeal** மதிப்புகள் காப்பகத்தில் உள்ள பதிவுடன் பொருந்துகிறதா என்பதை கணித உறுதியுடன் சோதிக்கிறது.

---

### 🧮 PoArt மதிப்பு தேற்றம் (The Value Theorem)

[PoArt] நெறிமுறை, டிஜிட்டல் சொத்தின் மதிப்பை ($V$) அகநிலை சந்தை புரிதலுடன் அல்லாமல்; **உற்பத்தி செயல்முறையின் இயற்பியல் யதார்த்தத்துடன்** தொடர்புபடுத்துகிறது.

செயற்கை நுண்ணறிவு (AI), முடிவை உடனடியாக வழங்குவதன் மூலம் ($t \to 0$) செயல்முறையை அழிக்கிறது. [PoArt] மதிப்பை; **நேரம், உழைப்பு மற்றும் விருப்பம்** கூறுகளின் திரட்சியாக கருதுகிறது.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### மாறிகளின் வரையறை

- **$\int dt$ (செயல்முறை திரட்சி):**  
  மதிப்பு, உடனடி "வெளியீடு" (output) அல்ல; $t_{\text{start}}$ மற்றும் $t_{\text{end}}$ இடையே திரளும் **செயல்முறை** ஆகும்.

- **$P_{\text{labor}}(t)$ (உடனடி உழைப்பு சக்தி):**  
  உற்பத்தி தருணத்தில் செலவழிக்கப்படும் மன மற்றும் உடல் முயற்சி அடர்த்தியைக் குறிக்கிறது.

- **$I_{\text{agency}}(t)$ (விருப்ப குணகம்):**  
  உற்பத்தியாளரின் ஆபத்து எடுக்கும் மற்றும் முடிவெடுக்கும் திறன் ஆகும். $0$ முதல் $1$ வரை மதிப்பு எடுக்கும்.
  - **AI ($I \approx 0$):** கட்டளைகளை செயல்படுத்துகிறது, ஆபத்து எடுக்காது.
  - **மனிதன் ($I \to 1$):** முடிவை மாற்றுகிறார், தயங்குகிறார், ஆபத்து எடுக்கிறார்.

- **$U_{\text{irreversible}}$ (மீள முடியாத தனித்துவம்):**  
  டிஜிட்டல் உற்பத்தியில் செயல்தவிர்ப்பு (Ctrl+Z) சாத்தியமாக இருக்கும்போது; இயற்பியல் உற்பத்தியில் திரும்ப வழி இல்லை.

### 🔎 வழக்கு பகுப்பாய்வு: AI vs. மனிதன்

#### காட்சி அ: AI-யுடன் 10 நொடியில் படம் உற்பத்தி

- **நேரம்:** 10 நொடிகள்
- **உழைப்பு சக்தி:** 1 அலகு
- **விருப்ப குணகம்:** 0.01
- **மீள முடியாதது:** 0

**முடிவு:**
$$V_{\text{AI}} \approx 0.1$$

#### காட்சி ஆ: நேரடி ஒளிபரப்பில் 6 மணி நேர இயற்பியல் உற்பத்தி

- **நேரம்:** 6 மணி நேரம் (21,600 நொடிகள்)
- **உழைப்பு சக்தி:** 0.5 அலகு
- **விருப்ப குணகம்:** 0.9
- **மீள முடியாதது:** >0

**முடிவு:**
$$V_{\text{Human}} \approx 9720 + U_{\text{irreversible}}$$

> **🔐 சுருக்கம்:** AI காலத்தில் அரிதானது "படம்" அல்ல; **நிரூபிக்கக்கூடிய உழைப்பு, நேரம் மற்றும் விருப்பம்** ஆகும்.

---

## 🎨 [PoArt] உழைப்பு ஆதார நெறிமுறை (Proof of Art Protocol v1.0)

> **"உண்மையான கலைஞர், உண்மையான உற்பத்தி, உண்மையான மதிப்பு."**

இந்த நெறிமுறை; கிரிப்டோ சூழலமைப்பைச் சுற்றியுள்ள அநாமதேய மோசடி செய்பவர்கள், 5 நிமிடத்தில் உற்பத்தி செய்யப்படும் செயற்கை நுண்ணறிவு படங்கள் மற்றும் "Pump & Dump" (ஊதி விடு) கலாச்சாரத்திற்கு எதிராக உருவாக்கப்பட்ட **உயிரியல் மற்றும் அறிவார்ந்த பாதுகாப்பு வழிமுறை** ஆகும்.

---

## அ) [PoArt] என்றால் என்ன?

**Proof of Art [PoArt];** பிளாக்செயினில் உள்ள சொத்தின் பின்னணி மதிப்பு, ஊகத்தின் அடிப்படையில் அல்லாமல்; சரிபார்க்கக்கூடிய **மனித உழைப்பு**, **நேரம்** மற்றும் **இயற்பியல் ஆற்றல்** அடிப்படையில் இருப்பதை உறுதிசெய்யும் நிறுவன சரிபார்ப்பு தரநிலை ஆகும்.

Bitcoin எப்படி *"மின்சாரம் மற்றும் செயலி சக்தி"* **(Proof of Work)** மூலம் மதிப்பை உருவாக்குகிறதோ; [PoArt] இணக்கமான திட்டங்களும் *"செலவழிக்கப்பட்ட திறமை மற்றும் மனித நேரம்"* மூலம் மதிப்பை உருவாக்குகின்றன.

> **[PoArt], பங்கேற்பாளருக்கு "எங்களை நம்புங்கள்" என்று சொல்வதில்லை; "இதோ ஆதாரங்கள், உங்கள் கண்களால் பாருங்கள், உங்கள் கணிதத்தால் சரிபார்க்கவும்" என்று சொல்கிறது.**

---

## ஆ) [PoArt] 5-வது தரநிலை (The 5 Pillars of Truth)

### 1) நேரடி அடையாள ஆதாரம் (Live Identity Proof)

- **பிரச்சனை:** கிரிப்டோ உலகம், அடையாளம் தெரியாத நிறுவனர்கள் பணத்தை சேகரித்து திட்டத்தை கைவிடுவதால் நிறைந்துள்ளது.
- **[PoArt] தீர்வு:** உற்பத்தியாளர், **உற்பத்தி நேரத்தில் இருப்பை** நிரூபிக்கிறார் நேரடி ஒளிபரப்பு அமர்வுகளில்.
- **குறிக்கோள்:** *"போட்கள் ஓவியம் வரைய முடியும் ஆனால் போட்கள் வியர்க்காது மற்றும் மேம்பாடு செய்ய முடியாது."*

### 2) உழைப்பு மற்றும் செயல்முறை ஆதாரம் (Labor & Process Proof)

- **பிரச்சனை:** 2 நொடியில் உற்பத்தி செய்யப்பட்ட AI படங்கள் 2 மாதத்தில் செய்யப்பட்ட எண்ணெய் ஓவியத்துடன் ஒரே "jpeg" நடத்தை பெறுவது.
- **[PoArt] தீர்வு:** படைப்பின் "கர்ப்பம் மற்றும் பிறப்பு" செயல்முறை பதிவு செய்யப்படுகிறது. இது டோக்கனுக்கு **"நேர செலவு" (Time Cost)** சேர்க்கிறது.

### 3) அழகியல் மதிப்பு ஆதாரம் (Aesthetic Value Proof)

- **பிரச்சனை:** "மீம்" கலாச்சாரம் அழகியலை புறக்கணித்து உடனடி நகைச்சுவையில் மட்டுமே கவனம் செலுத்துவது.
- **[PoArt] தீர்வு:** திட்டம், கல்வி கலை தரநிலைகள், வண்ண கோட்பாடு, இசையமைப்பு விதிகளைக் கொண்டிருக்க வேண்டும்.

### 4) கருத்தியல் புதுமை (Conceptual Novelty)

- **பிரச்சனை:** ஒருவருக்கொருவர் நகலான, படைப்பாற்றலற்ற ஆயிரக்கணக்கான நாய்/பூனை coins.
- **[PoArt] தீர்வு:** திட்டம்; கலை, அறிவியல், தத்துவம் அல்லது தொழில்நுட்பத்தை அர்த்தமுள்ள கட்டமைப்பில் இணைக்கும் புதிய பாலத்தை உருவாக்க வேண்டும்.

> [!IMPORTANT]
> **குறிப்பு உதாரணம் (Las Palmitas விளைவு):**  
> மெக்சிகோவின் குற்றத்துடன் போராடும் Las Palmitas பகுதியில், 200+ வீடுகள் மாபெரும் வானவில் விழாவாக மாற்றப்பட்டன. இந்த அழகியல் தலையீட்டிற்குப் பிறகு பகுதியில் குற்ற விகிதங்கள் குறைந்தன.

### 5) அல்காரிதம்-அல்லாத விருப்பம் (Non-Algorithmic Agency)

- **பிரச்சனை:** சரியான ஆனால் ஆன்மா இல்லாத, ஒருவருக்கொருவர் மீண்டும் மீண்டும் வரும் டிஜிட்டல் உற்பத்திகள்.
- **[PoArt] தீர்வு:** தவறு செய்யக்கூடிய, ஆபத்து எடுக்கும் மனிதனின் தனித்துவமான விருப்பம் படைப்பில் உணரப்பட வேண்டும் - **உயிரியல் கையொப்பம்**.

---

## இ) சரிபார்ப்பு & போலி-தடுப்பு வழிமுறை

### 📦 ஆதார தொகுப்பு (Evidence Pack)

ஒவ்வொரு [PoArt] சான்றிதழ் கொண்ட படைப்பின் பின்னணியில், முதலீட்டாளர்கள் பதிவிறக்கக்கூடிய மறைகுறியாக்கப்பட்ட தரவு தொகுப்பு உள்ளது:

- **RAW வீடியோ பதிவுகள்:** உற்பத்தி தருணத்தின் இடையூறில்லா மூல படங்கள்.
- **Metadata பகுப்பாய்வு:** கோப்பு உருவாக்க தேதி, சாதன தகவல்கள் மற்றும் இருப்பிட தரவு.
- **இயற்பியல் குறிப்புகள்:** படைப்பு இயற்பியல் உலகில் இருப்பதை நிரூபிக்கும் ஆதாரங்கள்.

### 🔄 365 நாள் புதுப்பித்தல் (The Sustainability Protocol)

- **விதி:** "Verified Artist" நிலை **1 வருடம்** மட்டுமே செல்லுபடியாகும்.
- **செயல்முறை:** கலைஞர்/டெவலப்பர், ஒவ்வொரு 365 நாளிலும், சமூகத்திற்கு **புதிய, பெரிய மற்றும் நிரூபிக்கக்கூடிய படைப்பை** சமர்ப்பிக்க வேண்டும்.

### 🚩 சிவப்பு கொடி (Red Flag Protocol)

**மோசடி கண்டறியப்பட்டால்:**

1. சான்றிதழ் உடனடியாக **"ரத்து" (VOID)** என குறிக்கப்படும்.
2. ஆதார தொகுப்புகள் **"போலி"** என்று பொதுவில் முத்திரையிடப்படும்.
3. திட்டம் [PoArt] கருப்பு பட்டியலில் சேர்க்கப்படும்.

---

## ஈ) முடிவு: சூதாட்டம் அல்ல, அருங்காட்சியகம்

**[PoArt], சூதாட்டத்தின் நடுவில் கட்டப்பட்ட கோட்டை.**

- 🎰 சூதாட்டம் காகித விளையாட்டுகளை அடிப்படையாகக் கொண்டது; நாங்கள் **இயற்பியல் யதார்த்தத்தை** அடிப்படையாகக் கொண்டுள்ளோம்.
- 🃏 சூதாட்டம் ஏமாற்றத்திற்கு திறந்திருக்கிறது; நாங்கள் **வெளிப்படையான ஆதாரங்களுக்கு** திறந்திருக்கிறோம்.
- ⏳ சூதாட்டம் தற்காலிகமானது; நாங்கள் **கலை மற்றும் அறிவியலின் நித்தியத்தில்** கவனம் செலுத்துகிறோம்.

**இந்த நெறிமுறையைப் பயன்படுத்தும் டோக்கன், வெறும் "coin" அல்ல; பின்னணியில் வியர்வை, வண்ணம், குறியீடு மற்றும் தத்துவம் கொண்ட டிஜிட்டல் பங்கு ஆவணம்.**

---

## 🗳️ 6) நிர்வாகம் & பொது பதிவேடு

### 6.1 Public Registry (பொது பதிவேடு)

அனைத்து அங்கீகரிக்கப்பட்ட தரவுகளும் ilhanart.org/registry இல் பதிவு செய்யப்படுகின்றன.

**பதிவு புலங்கள்:**

- **அடையாளம் & நிலை:** certificate_id, status, visibility, created_at
- **வழங்கும் நிறுவனம்:** issuer.name, issuer.location, issuer.attestation_pubkey
- **படைப்பு தகவல்:** asset.title, asset.creator, asset.fingerprints.sha256/sha512
- **தடயவியல் தரவு:** forensics.ip_masked, forensics.location, forensics.device, forensics.timestamp
- **கிரிப்டோகிராஃபிக் ஆதாரங்கள்:** proof.evidence_root, proof.signer_sig, proof.notary_seal
- **நிர்வாகம்:** governance.decision, governance.review_notes

### 6.2 PoArt Verified விண்ணப்ப செயல்முறை

**PoArt Verified விண்ணப்பங்கள், İlhan Art Gallery-ஆல் 5 PoArt தரநிலைகளின்படி மதிப்பீடு செய்யப்படுகின்றன.**

**செயல்முறை:**
1. விண்ணப்பம் சமர்ப்பித்தல்
2. ஆய்வு (30 நாட்கள்)
3. சமூக ஆலோசனை
4. முடிவு (Approved / Rejected)

### 6.3 Token Utility

**$CULTURE டோக்கன் வைத்திருப்பவர்களுக்கு வழங்கப்படும் நன்மைகள்:**

1. **கேலரி நிகழ்வுகள் முன்னுரிமை அணுகல்** - வருடத்திற்கு 1 வார கண்காட்சி
2. **PoArt Registry முழு அணுகல்** - Evidence Pack-களின் முழு பதிப்புகள்
3. **Advisory Voting** - PoArt Verified விண்ணப்பங்களில் ஆலோசனை உரிமை
4. **Exclusive Content** - Behind-the-scenes உள்ளடக்கங்கள்

---

## 7) 🔐 தொழில்நுட்ப முத்திரை (NOTARY SEAL)

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] டிஜிட்டல் நோட்டரி & தடயவியல் ஆதார நெறிமுறை (Beta v1.0)

> **"கலாச்சாரம், மூலதனத்தை விட பெரியது. உங்கள் படைப்புகளை இன்றே பாதுகாங்கள், நாளைக்கு கொண்டு செல்லுங்கள்."**

## ஏன் பொதுவில் திறந்திருக்கிறது?

உண்மையான பாதுகாப்பு வெளிப்படைத்தன்மையிலிருந்து வருகிறது. **Public Registry** அமைப்பைப் பயன்படுத்தி, உலகின் எந்த இடத்திலும் உள்ள நபர் கையில் உள்ள கோப்பு அசல் என்பதை நொடிகளில் சரிபார்க்க முடியும்.

---

## 🧩 Visibility Modules

### 🔒 தனிப்பட்ட (Private)
கலைஞர் படைப்பை இன்னும் வெளியிட விரும்பவில்லை ஆனால் நேர முத்திரை போட்டு சரிபார்க்க விரும்புகிறார்.

### 🕶️ மறைக்கப்பட்ட (Masked)
கலைஞர் வெளிப்படைத்தன்மை விரும்புகிறார் ஆனால் IP/இருப்பிடம் கண்டுபிடிக்கப்படுவதை அஞ்சுகிறார். IP 88.241.*.** வடிவத்திற்கு மாற்றப்படுகிறது.

### 🌍 அனைவருக்கும் திறந்த (Public)
முழு வெளிப்படைத்தன்மை. படைப்பு எங்கே, எப்போது, எந்த நெட்வொர்க்கிலிருந்து உற்பத்தி செய்யப்பட்டது என்று தெளிவாக அறிவிக்கப்படுகிறது.

---

## 💡 தொழில்நுட்ப புதுமை

### 1) Client-Side Hashing
உங்கள் படைப்பு கோப்புகள் ஒருபோதும் சேவையகத்திற்கு பதிவேற்றப்படாது. Hash உங்கள் கணினியிலேயே கணக்கிடப்படுகிறது.

### 2) Forensic Data Fusion
- **டிஜிட்டல் சுருக்கம் (SHA-512):** படைப்பின் ஒரு பிக்சல் மாறினாலும் உடையும் விரல்ரேகை
- **இருப்பிடம் & நேரம்:** மில்லி நொடி துல்லியத்தில்
- **சாதன அடையாளம்:** இயங்குதளம், உலாவி மற்றும் சாதன வகை

---

## ⚙️ கணினி கட்டமைப்பு

| அடுக்கு | தொழில்நுட்பம் | விளக்கம் |
|--------|-----------|----------|
| **கிரிப்டோகிராஃபி** | SHA-256 & SHA-512 | இரட்டை அடுக்கு சுருக்கம் |
| **தரவுத்தளம்** | Supabase (PostgreSQL) | JSONB + RLS policies |
| **தடயவியல் தரவு** | ipapi.co API | IP/இருப்பிடம்/நேரம் மூவகை |
| **Rendering** | html2canvas + jsPDF | Client-side PNG/PDF |
| **Frontend** | Vanilla JavaScript | Zero framework dependency |
| **பாதுகாப்பு** | Client-side hashing | கோப்பு சேவையகத்திற்கு போகாது |

---

## 🗺️ வழி வரைபடம்

### கட்டம் 1: Beta v1.0 (தற்போது)
- Cloud Database (Supabase)
- Off-chain registry
- Gallery self-attestation

### கட்டம் 2: Decentralized Authority (2026 Q2-Q4)
- Edge Function INSERT
- Wallet கையொப்பம் (Solana)
- IPFS/Arweave Backup
- OpenTimestamps

### கட்டம் 3: முழு பரவலாக்கம் (2027+)
- On-Chain Registry (Solana)
- Multi-Chain Support
- DID Integration
- துருக்கி நீதிமன்றங்களில் செல்லுபடியாகும்
---

## 🧬 JSON Schema

```json
{
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
      "sha256": "e4123f83b44a409d7a43f0897837876dfabb3320...",
      "sha512": "41e5e0d007a2a77b6e0e3ebc548fbaa2788ea265..."
    }
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

## 🔬 தொழில்நுட்ப ஆழம்: முத்திரை அல்காரிதம்

```javascript
// Deterministic Hash செயல்பாடுகள்
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// FileHash கணக்கீடு
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// EvidenceRoot உருவாக்கம்
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = 
    "file_sha512:" + fileHash512 + "\n" +
    "forensics:" + JSON.stringify(forensicsData);
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// NotarySeal உற்பத்தி
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = 
    "evidence_root:" + evidenceRoot + "\n" +
    "signer_sig:" + signerSignature + "\n" +
    "timestamp:" + timestamp;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// மறைத்தல் செயல்பாடு
function maskIP(ip) {
  if (!ip) return "***";
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return parts[0] + "." + parts[1] + ".***.***";
    }
  }
  return "***";
}
```

### Quick Verify
```javascript
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  const cert = await fetchFromRegistry(certificateId);
  
  if (userFileHash === cert.asset.fingerprints.sha512) {
    return { valid: true, message: "✅ அசல்" };
  } else {
    return { valid: false, message: "❌ போலி" };
  }
}
```

### Full Verify
```javascript
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  const cert = await fetchFromRegistry(certificateId);

  // FileHash சோதனை
  if (userFileHash !== cert.asset.fingerprints.sha512) {
    return { valid: false, message: "❌ கோப்பு hash பொருந்தவில்லை" };
  }

  // EvidenceRoot மீண்டும் உருவாக்கம்
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ EvidenceRoot பொருந்தவில்லை" };
  }

  // NotarySeal மீண்டும் உருவாக்கம்
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ NotarySeal பொருந்தவில்லை" };
  }

  return { valid: true, message: "✅ Full Verify தேர்ச்சி" };
}
```

---

## 📊 போட்டியாளர் பகுப்பாய்வு

| அம்சம் | **PoArt** | OpenTimestamps | Verisart | OriginStamp |
|---------|:---------:|:---------------:|:---------:|:-----------:|
| **செலவு** | 🆓 இலவசம் | 🆓 | 💰 கட்டணம் | ⚠️ Freemium |
| **Drag & Drop UI** | ✅ | ❌ CLI | ⚠️ | ⚠️ |
| **Privacy Controls** | ✅ 3 முறை | ❌ | ❌ | ❌ |
| **Client-Side Hash** | ✅ | ✅ | ❌ | ⚠️ |
| **Forensic Metadata** | ✅ முழு | ❌ | ❌ | ⚠️ |
| **தமிழ் ஆதரவு** | ✅ | ❌ | ❌ | ❌ |
| **திறந்த மூலம்** | ✅ GitHub | ✅ | ❌ | ⚠️ |

---

## 📈 பயன்பாட்டு புள்ளிவிவரங்கள் (2026 Q1 இலக்குகள்)

| அளவீடு | இலக்கு | நிலை |
|--------|-------|-------|
| **மொத்த சான்றிதழ்** | 1,000 | 🔄 முன்னேற்றத்தில் |
| **செயலில் பயனர்** | 500 | 🔄 முன்னேற்றத்தில் |
| **சரிபார்ப்பு எண்ணிக்கை** | 5,000 | 🔄 முன்னேற்றத்தில் |
| **Uptime** | %99.9 | ✅ செயலில் |
| **Avg Response Time** | <200ms | ✅ சிறந்தது |

---

## 🏛️ "Engine" கருத்தின் முக்கியத்துவம்

Pump.fun அல்லது ஒத்த தளங்களிலிருந்து வெளிவரும் token-கள், பெரும்பாலும் **"அணுகல் டிக்கெட்"** மட்டுமே. **PoArt Forensic Engine (PFE)** அந்த டிக்கெட் எந்த உரிமைகளை பாதுகாக்கிறது, உழைப்பு எப்படி பதிவு செய்யப்படும், கலை/அறிவியல்/தொழில்நுட்பம் எப்படி நிரந்தரமாக்கப்படும் என்பதை தீர்மானிக்கும் **அரசியலமைப்பு தர்க்க அடுக்கு** ஆகும்.

---

## 🎯 முடிவு: ஆதாரத்தால் பூட்டப்பட்ட மதிப்பு

இந்த தேற்றம், [PoArt] மதிப்பு கோரிக்கையை "விருப்பம்" அல்லது "சந்தை கதை" நிலையிலிருந்து வெளியே கொண்டு வந்து **நிரூபிக்கக்கூடிய உற்பத்தி யதார்த்தத்தில்** பொருத்துகிறது.

### முக்கிய புள்ளிகள்

1. **செயல்முறை இல்லாமல் மதிப்பு உருவாகாது:**  
   AI, வேகமான வெளியீட்டில் ($t \to 0$) செயல்முறையை அழிக்கிறது.

2. **விருப்பமும் ஆபத்தும் பெருக்கி:**  
   [PoArt], "செலவழித்த நேரத்தை" மட்டுமல்லாமல்; அந்த நேரத்தில் உள்ள உண்மையான முடிவு, ஆபத்து மற்றும் விலை அடுக்கையும் அளவிடுகிறது.

3. **தனித்துவம், சந்தைப்படுத்துதல் அல்ல இயற்பியல் ஆதாரம்:**  
   இயற்பியல் உற்பத்தியில் மீள முடியாத அடையாளங்கள், டிஜிட்டலின் Ctrl+Z தர்க்கத்திற்கு வெளியே உள்ளன.

---

## 📊 கூடுதல் போட்டியாளர் பகுப்பாய்வு

### போட்டியாளர்களின் குறைபாடுகள், PoArt-ன் பலங்கள்

| குறைபாடு | போட்டியாளர்கள் | PoArt |
|------|----------|-------|
| **பயன்பாட்டு சிரமம்** | CLI, API அறிவு, வாலெட் தேவை | இழுத்து-போடு, 3 கிளிக்கில் முடிவு |
| **செலவு தடை** | $50-500/மாதம் சந்தா | %100 இலவசம் |
| **தனியுரிமை** | கோப்பு சேவையகத்திற்கு பதிவேற்றப்படுகிறது | Client-side, கோப்பு ஒருபோதும் போகாது |
| **Forensic தரவு** | Timestamp மட்டும் | IP, இருப்பிடம், சாதனம், நேரம் - அனைத்தும் |
| **தமிழ் ஆதரவு** | இல்லை அல்லது மிகக் குறைவு | Native மொழி ஆதரவு |
| **திறந்த மூலம்** | மூடிய பெட்டி | GitHub-ல் அனைத்து குறியீடும் திறந்தது |

---

## 🔄 Token Governance பரிணாமம்

### v1.0 (2026)
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (மையமான ஆனால் வெளிப்படையான)
- Governance: Advisory only (கலாச்சார பாதுகாவலர் இறுதி முடிவு)
- Token utility: Gallery access + registry + NFT priority

### v2.0 (2027)
- Registry: On-chain (Solana)
- Signatures: Wallet-based (decentralized)
- Governance: Hybrid (community advisory + curatorial quality)
- Token utility: Enhanced features + advanced access

### v3.0+ (2028+)
- Full community governance (optional)
- கலாச்சார பாதுகாவலர் quality control எப்போதும் பாதுகாக்கப்படும்
- Multi-chain support முழுமையாக

---

## 🛡️ பயன்பாட்டு இடங்கள் & நன்மை விவரம்

கலைஞர், எழுத்தாளர் அல்லது வடிவமைப்பாளராக இருந்தால், "இதை நான் முன்பே செய்தேன்" என்று சொல்வது போதாது, நிரூபிக்க வேண்டும்.

**PoArt-ல் முத்திரையிட்ட படைப்பு:**

- **கணித ஆதாரம்:** உங்கள் கோப்பின் ஒரு பிக்சல் கூட மாறினால் கணினி அதை புரிந்துகொள்ளும். மோசடி சாத்தியமில்லை.
- **சட்ட அடிப்படை:** படைப்பு எந்த தேதியில், எந்த நகரத்தில், எந்த சாதனத்திலிருந்து முத்திரையிடப்பட்டது என்று பதிவு செய்யப்பட்டுள்ளது.
- **உடனடி சான்றிதழ்:** நொடிகளில் தனித்துவமான, QR குறியீடு கொண்ட மற்றும் முத்திரையிடப்பட்ட **"சொத்து அடையாள சான்றிதழ்"** உருவாக்குகிறது.

---

## 📝 Canonical Encoding விவரம்

### v1.0 Canonicalization தரநிலை

- **நிலையான புல வரிசை:** ip_masked → location → device → timestamp
- **Encoding:** UTF-8
- **Delimiter:** `\n` (newline)

### கட்டம் 2 திட்டம்

RFC 8785 (JCS - JSON Canonicalization Scheme) உடன் canonical JSON-க்கு மாற்றம்.

---

## 🎨 கலாச்சார சூழல்

### "கலாச்சாரம் மூலதனத்தை விட பெரியது" தத்துவம்

இந்த திட்டம் "Culture > Capital" தத்துவத்தின் அடிப்படையில் அமைந்துள்ளது. இதன் பொருள்:

1. **நீண்ட கால சிந்தனை:** 2025 முதல் 3000 CE வரையிலான 975-ஆண்டு பார்வை
2. **ஊக எதிர்ப்பு கொள்கை:** Token விலையை உயர்த்துவதை விட கலாச்சார மதிப்பை முன்னிலைப்படுத்துதல்
3. **சமூகம் மையமானது:** Mercenary capital அல்லாமல் நீண்ட கால பங்கேற்பாளர்கள்

### தமிழ் கலாச்சாரமும் PoArt-உம்

தமிழ் கலாச்சாரம் ஆயிரக்கணக்கான ஆண்டுகள் பழமையான கலை மரபு கொண்டது. PoArt இந்த மரபை பாதுகாக்க மற்றும் கடத்த நவீன தொழில்நுட்பம் வழங்குகிறது:

- **பழங்கால கலை:** சோழர் சிற்பங்கள், தஞ்சாவூர் ஓவியங்கள்
- **நவீன கலை:** தமிழ் ஓவியர்கள் மற்றும் சிற்பிகள்
- **டிஜிட்டல் காப்பகம்:** எதிர்கால தலைமுறைகளுக்கு அழியாத பதிவு

---

## 🌐 உலகளாவிய அணுகல்

### மொழி ஆதரவு

PoArt நெறிமுறை பல மொழிகளில் கிடைக்கிறது:

- 🇹🇷 Türkçe (முக்கிய)
- 🇬🇧 English
- 🇪🇸 Español
- 🇨🇳 中文
- 🇫🇷 Français
- 🇩🇪 Deutsch
- 🇷🇺 Русский
- 🇮🇳 தமிழ் (இந்த ஆவணம்)

### ஏன் பல மொழிகள்?

PoArt உலகளாவிய கலை சமூகத்திற்காக வடிவமைக்கப்பட்டது. எந்த கலைஞரும், எந்த இடத்திலும், தங்கள் படைப்பை பாதுகாக்க முடிய வேண்டும்.

---

## 🔗 முக்கிய இணைப்புகள்

### அதிகாரப்பூர்வ

- **இணையம்:** [ilhanart.org](https://ilhanart.org)
- **Registry:** [ilhanart.org/public-registry](https://ilhanart.org/public-registry)
- **GitHub:** [github.com/galeri-coder](https://github.com/galeri-coder)

### சமூக ஊடகம்

- **Twitter/X:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Instagram:** [ilhanartgaleri](https://instagram.com/ilhanartgaleri)

### தொடர்பு

- **மின்னஞ்சல்:** galeri@ilhanart.org

---

## ⚠️ முக்கிய எச்சரிக்கைகள்

1. **Token விலை:** Token விலை கலை தரத்தின் குறிகாட்டி அல்ல
2. **முதலீட்டு ஆலோசனை அல்ல:** இந்த ஆவணம் முதலீட்டு ஆலோசனை அல்ல
3. **Beta பதிப்பு:** கணினி இன்னும் மேம்பாட்டில் உள்ளது
4. **பொறுப்பு:** பயனர்கள் தங்கள் சொந்த ஆராய்ச்சி செய்ய வேண்டும்

---

## 🌍 சமூகம் & ஆதரவு

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **இணையம்:** [ilhanart.org](https://ilhanart.org)
- **மின்னஞ்சல்:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 பங்களிப்பு

**பங்களிக்க:**
1. Fork செய்யுங்கள்
2. Feature branch உருவாக்குங்கள்
3. Commit செய்யுங்கள்
4. Push செய்யுங்கள்
5. Pull Request திறக்கவும்

### உதவி அழைப்பு

* **Supabase Edge Functions**
* **Solana Web3.js**
* **IPFS / Arweave**
* **Community Tools**

---

## 💬 இறுதி குறிப்புகள்

### Pump.fun & யதார்த்தம்

இந்த திட்டம் Pump.fun-ல் தொடங்கப்பட்டது ஏனெனில்:
- ✅ Liquidity அணுகல்
- ✅ ஏற்கனவே உள்ள சமூக அணுகல்
- ✅ குறைந்த தொடக்க செலவு

**ஆனால்:**
- **Token விலை** கலை வெற்றியின் குறிகாட்டி அல்ல
- **வெற்றி அளவீடுகள்:** Authenticated artworks + community engagement + இயற்பியல் பார்வையாளர்

---

## 📜 இறுதி வார்த்தைகள்

> **"கலாச்சாரம், மூலதனத்தை விட பெரியது."**

இந்த நெறிமுறை கலையின் மதிப்பை ஊகத்திலிருந்து ஆதாரத்திற்கு மாற்ற வடிவமைக்கப்பட்டது. AI காலத்தில், மனித உழைப்பு, நேரம் மற்றும் விருப்பத்தை நிரூபிப்பது அவசியமாகிவிட்டது.

[PoArt] இந்த சிக்கலை தீர்க்கிறது - **நிரூபிக்கக்கூடிய ஆதாரத்துடன்**.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // கலாச்சாரம், மூலதனத்தை விட பெரியது*

## 🧾 உரிமம்

MIT License © 2026 İlhan Art Gallery Initiative

---

## 💬 கடன்கள்

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) 
![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) 
![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) 
![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**இந்த திட்டம் [İlhan Art Gallery] முன்முயற்சியுடன் உருவாக்கப்பட்டது, மூல குறியீடுகள் வெளிப்படைத்தன்மைக்காக பொதுவில் திறந்தவை.**

**நெறிமுறை V1.0 // SHA-512 உடன் முத்திரையிடப்பட்டது.**

*© 2026 İLHAN ART | படைப்புகள், படங்கள் மற்றும் கருத்துக்களின் அனைத்து உரிமைகளும் பாதுகாக்கப்பட்டவை.*

---

*இந்த ஆவணம் துருக்கிய மூலத்திலிருந்து தமிழுக்கு மொழிபெயர்க்கப்பட்டது.*  
*அனைத்து தொழில்நுட்ப விவரங்கள், குறியீடுகள், JSON, LaTeX மற்றும் markdown பாதுகாக்கப்பட்டுள்ளன.*

---

---

## 📋 கூடுதல் தொழில்நுட்ப விவரங்கள்

### பதிவு உதாரணம் (Registry JSON)

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

---

## 🔐 பாதுகாப்பு குறிப்புகள்

### Client-Side நன்மைகள்

1. **கோப்பு தனியுரிமை:** படைப்பு கோப்புகள் ஒருபோதும் சேவையகத்திற்கு பதிவேற்றப்படாது
2. **Hash கணக்கீடு:** அனைத்து கிரிப்டோகிராஃபிக் வேலையும் உலாவியில் நடக்கிறது
3. **ஆதார ஒருமைப்பாடு:** Deterministic அல்காரிதங்கள் reproducible முடிவுகளை உறுதி செய்கின்றன

### Masked Mode அம்சங்கள்

- IP முகவரி: `88.241.123.45` → `88.241.***.***`
- இருப்பிடம்: `Istanbul, Turkey` → `***/TR`
- Forensics hash கணக்கீடு masked தரவைப் பயன்படுத்துகிறது

### Public Mode அம்சங்கள்

- முழு IP முகவரி காட்டப்படுகிறது
- முழு இருப்பிட விவரம்
- சரிபார்ப்புக்கு முழு வெளிப்படைத்தன்மை

---

## 📈 கூடுதல் பயன்பாட்டு புள்ளிவிவரங்கள்

| அளவீடு | விவரம் |
|--------|---------|
| **ஆதரிக்கப்படும் கோப்பு வகைகள்** | PNG, JPG, PDF, MP4, எல்லாம் |
| **அதிகபட்ச கோப்பு அளவு** | வரம்பற்றது (client-side) |
| **Hash அல்காரிதங்கள்** | SHA-256, SHA-512 |
| **சான்றிதழ் வடிவங்கள்** | PNG, PDF, JSON |
| **QR குறியீடு** | ஒவ்வொரு சான்றிதழிலும் |

---

## 🔄 சரிபார்ப்பு செயல்முறை விவரம்

### Quick Verify செயல்முறை

1. பயனர் கோப்பை உள்ளிடுகிறார்
2. Client-side SHA-512 hash கணக்கிடப்படுகிறது
3. Registry-ல் பதிவு செய்யப்பட்ட hash-உடன் ஒப்பிடப்படுகிறது
4. முடிவு திரும்பும்: ✅ அசல் அல்லது ❌ போலி

### Full Verify செயல்முறை

1. Quick Verify செய்யப்படுகிறது
2. EvidenceRoot மீண்டும் கணக்கிடப்படுகிறது
3. NotarySeal மீண்டும் கணக்கிடப்படுகிறது
4. அனைத்து மதிப்புகளும் ஒப்பிடப்படுகின்றன
5. முழு சரிபார்ப்பு முடிவு திரும்பும்

---

## 📝 Forensics தரவு விவரம்

| புலம் | விளக்கம் | உதாரணம் |
|------|---------|-------|
| ip_masked | மறைக்கப்பட்ட IP | 88.241.*.** |
| location | இருப்பிடம் | Istanbul/TR அல்லது ***/TR |
| device | சாதனம் | Brave (Windows) |
| timestamp | நேரம் | 2026-01-09T12:34:56.000Z |

---

## 🧪 Hash Algorithm தேர்வு

**ஏன் SHA-512?**

1. **பாதுகாப்பு:** 512-bit output உயர் பாதுகாப்பு வழங்குகிறது
2. **Collision Resistance:** இரண்டு வெவ்வேறு கோப்புகள் ஒரே hash பெறுவது சாத்தியமில்லை
3. **வேகம்:** நவீன கணினிகளில் வேகமாக இயங்குகிறது
4. **தரநிலை:** உலகளாவிய ஏற்றுக்கொள்ளப்பட்ட algorithm

---

## 🌟 நன்றி

இந்த திட்டம் பின்வருவோருக்கு நன்றி தெரிவிக்கிறது:

- **İlhan Art Gallery** - பார்வை மற்றும் தலைமைக்காக
- **திறந்த மூல சமூகம்** - பங்களிப்புக்காக
- **தமிழ் கலைஞர்கள்** - உத்வேகத்திற்காக
- **உலகளாவிய கலை சமூகம்** - ஆதரவுக்காக

---

## 📞 ஆதரவு

கேள்வி அல்லது சிக்கல் இருந்தால்:

1. **GitHub Issues:** தொழில்நுட்ப சிக்கல்கள்
2. **மின்னஞ்சல்:** பொதுவான கேள்விகளுக்கு
3. **Twitter DM:** விரைவான பதிலுக்கு

---

## 🔄 Version History

| Version | தேதி | மாற்றங்கள் |
|---------|------|--------|
| v1.0-beta | 2026-01 | முதல் பதிப்பு |
| v1.1 | TBD | Bug fixes |
| v2.0 | 2026-Q4 | Wallet integration |
| v3.0 | 2027-Q1 | On-chain registry |

---

## 📄 உரிம முழு உரை

MIT License

Copyright (c) 2026 İlhan Art Gallery Initiative

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

**[PoArt] Proof of Art Protocol**  
**"Culture > Capital"**  
**கலாச்சாரம், மூலதனத்தை விட பெரியது**

*இந்த ஆவணம் துருக்கிய மூலத்திலிருந்து தமிழுக்கு மொழிபெயர்க்கப்பட்டது.*  
*அனைத்து தொழில்நுட்ப விவரங்கள், குறியீடுகள், JSON, LaTeX மற்றும் markdown பாதுகாக்கப்பட்டுள்ளன.*

---
