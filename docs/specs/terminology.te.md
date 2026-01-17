# 📚 పదజాలం & భావనలు
> **"ఈ ప్రోటోకాల్ భాషను అర్థం చేసుకోవడం దాని దృష్టిని అర్థం చేసుకోవడం."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: కోర్ ఇన్‌ఫ్రాస్ట్రక్చర్

**PoArt Forensic Engine (PFE)** అనేది [PoArt] ప్రోటోకాల్ వెనుక ఉన్న కోర్ లాజిక్ మరియు టెక్నికల్ ఆపరేషన్‌ను సూచించే ప్రధాన పొర. కళాకృతి యొక్క ముడి ఉత్పత్తి డేటాను తీసుకుని, దానిని ధృవీకరించగల మరియు మార్చలేని **డిజిటల్ సాక్ష్యంగా** మార్చే "ఫోరెన్సిక్ ఇంజన్" ఇది.

### 🧩 ఎందుకు "PoArt Forensic"?

- **PoArt (Proof of Art):** ఇంజన్ యొక్క దృష్టి, డిజిటల్ ఆస్తి విలువను ఊహాగానాలపై కాకుండా; **నిరూపించగల ఉత్పత్తి ప్రక్రియపై** ఆధారపడేలా చేయడం.
- **Forensic (ఫోరెన్సిక్ ధృవీకరణ):**
  - **టెక్నికల్ నిర్వచనం:** ఉత్పత్తి ప్రక్రియ డేటా (బ్రష్ స్ట్రోక్‌లు, టైమ్‌ల్యాప్స్, లాగ్‌లు) మార్పు చేయబడలేదని ధృవీకరించడానికి రూపొందించిన అల్గారిథమ్ మరియు రికార్డ్ చైన్ విధానం.
  - **తాత్విక పొర:** కృత్రిమ మేధస్సు (AI) "తక్షణ అవుట్‌పుట్" ఉత్పత్తికి వ్యతిరేకంగా; మానవుని **సమయం, ప్రయత్నం మరియు నిర్ణయ వ్యయం** కలిగిన ఉత్పత్తిని కొలవగల వాస్తవికతగా మార్చడం.

> గమనిక: బ్లాక్‌చెయిన్ (ఉదా. Solana) ఇంటిగ్రేషన్ PFE కోర్ కాదు; ధృవీకరణ/రిజిస్ట్రీ కోసం విడిగా నిర్వచించబడే **Chain Anchor Layer** గా పరిగణించబడుతుంది.

### 🛠️ v1.0 టెక్నికల్ పరిధి

**PoArt Forensic Engine (PFE) v1.0** సంక్లిష్ట ఆర్థిక నమూనాలకు బదులుగా ఈ **3 ప్రధాన స్తంభాలపై** నిర్మించబడింది:

1. **Hashing & Sealing (సీలింగ్):**  
   PFE, Evidence Pack లోని అన్ని అంశాలను (కళాకృతి ఫైల్, వీడియో, JSON/log, సంతకం మొదలైనవి) డిటర్మినిస్టిక్‌గా ప్రాసెస్ చేసి ప్రత్యేక **NotarySeal** విలువను ఉత్పత్తి చేస్తుంది.

   **కోర్ భావనలు (v1.0):**
   - **FileHash (కళాకృతి వేలిముద్ర):** కళాకృతి ఫైల్ బైట్‌ల నుండి ఉత్పత్తి చేయబడిన hash.
   - **EvidenceRoot (సాక్ష్య ప్యాకేజ్ మూలం):** Evidence Pack యొక్క సమగ్రతను సూచించే మూల సారాంశం (Merkle root లేదా canonical manifest hash).
   - **NotarySeal (తుది సీల్ / PFE అవుట్‌పుట్):** EvidenceRoot + సమయం + సంతకం కలయిక నుండి ఉత్పత్తి చేయబడిన తుది సీల్.

   **సూత్రాలు (పెట్టుబడిదారునికి స్పష్టంగా):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload నిర్వచనాలు (v1.0):**
   
   - **EvidenceRootPayload:**
   ```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
   ```
   
   - **NotarySealPayload:**
   ```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
   ```
   
   > గమనిక: PFE అవుట్‌పుట్‌గా ఉద్దేశించిన విలువ **NotarySeal**. **SignerSignature** మెకానిజం ఫేజ్ 2లో (Solana Wallet Adapter తో) అమలు చేయబడుతుంది; ప్రస్తుత v1.0లో సిస్టమ్ యొక్క సొంత attestation సంతకం ఉపయోగించబడుతుంది.

2. **Indexing (ఆర్కైవింగ్):**  
   ఏ వాలెట్, ఏ తేదీన, ఏ కళాకృతికి **Labor Proof (శ్రమ సాక్ష్యం)** సమర్పించిందో; పారదర్శక మరియు ప్రశ్నించగల రికార్డ్ పొరలో నమోదు చేస్తుంది.

3. **Verification (ధృవీకరణ):**  
   కళాకృతి యొక్క అసలుతనం ప్రశ్నించబడినప్పుడు PFE ముడి సాక్ష్యాలను మళ్ళీ ప్రాసెస్ చేస్తుంది; లెక్కించిన **EvidenceRoot / NotarySeal** విలువలు ఆర్కైవ్‌లోని రికార్డ్‌తో సరిపోతాయా అని గణిత ఖచ్చితత్వంతో పరీక్షిస్తుంది.

---

### 🧮 PoArt విలువ సిద్ధాంతం (The Value Theorem)

[PoArt] ప్రోటోకాల్, డిజిటల్ ఆస్తి విలువను ($V$) ఆత్మాశ్రయ మార్కెట్ అవగాహనతో కాకుండా; **ఉత్పత్తి ప్రక్రియ యొక్క భౌతిక వాస్తవికతతో** సంబంధం కలిగిస్తుంది.

కృత్రిమ మేధస్సు (AI), ఫలితాన్ని వెంటనే అందించడం ద్వారా ($t \to 0$) ప్రక్రియను నాశనం చేస్తుంది. [PoArt] విలువను; **సమయం, శ్రమ మరియు సంకల్పం** భాగాల సంచితంగా పరిగణిస్తుంది.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### వేరియబుల్స్ నిర్వచనం

- **$\int dt$ (ప్రక్రియ సంచితం):**  
  విలువ, తక్షణ "అవుట్‌పుట్" కాదు; $t_{\text{start}}$ మరియు $t_{\text{end}}$ మధ్య పేరుకుపోయే **ప్రక్రియ**.

- **$P_{\text{labor}}(t)$ (తక్షణ శ్రమ శక్తి):**  
  ఉత్పత్తి సమయంలో ఖర్చు చేయబడిన మానసిక మరియు శారీరక ప్రయత్న సాంద్రతను సూచిస్తుంది.

- **$I_{\text{agency}}(t)$ (సంకల్ప గుణకం):**  
  ఉత్పత్తిదారుని రిస్క్ తీసుకునే మరియు నిర్ణయం తీసుకునే సామర్థ్యం. $0$ నుండి $1$ వరకు విలువ తీసుకుంటుంది.
  - **AI ($I \approx 0$):** ఆదేశాలను అమలు చేస్తుంది, రిస్క్ తీసుకోదు.
  - **మానవుడు ($I \to 1$):** నిర్ణయాన్ని మారుస్తారు, సందేహిస్తారు, రిస్క్ తీసుకుంటారు.

- **$U_{\text{irreversible}}$ (తిరిగి పొందలేని ప్రత్యేకత):**  
  డిజిటల్ ఉత్పత్తిలో అన్‌డూ (Ctrl+Z) సాధ్యమైనప్పటికీ; భౌతిక ఉత్పత్తిలో తిరిగి రావడం లేదు.

### 🔎 కేస్ అనాలిసిస్: AI vs. మానవుడు

#### సినారియో A: AI తో 10 సెకన్లలో చిత్రం ఉత్పత్తి

- **సమయం:** 10 సెకన్లు
- **శ్రమ శక్తి:** 1 యూనిట్
- **సంకల్ప గుణకం:** 0.01
- **తిరిగి పొందలేనిది:** 0

**ఫలితం:**
$$V_{\text{AI}} \approx 0.1$$

#### సినారియో B: లైవ్ స్ట్రీమ్‌లో 6 గంటల భౌతిక ఉత్పత్తి

- **సమయం:** 6 గంటలు (21,600 సెకన్లు)
- **శ్రమ శక్తి:** 0.5 యూనిట్
- **సంకల్ప గుణకం:** 0.9
- **తిరిగి పొందలేనిది:** >0

**ఫలితం:**
$$V_{\text{Human}} \approx 9720 + U_{\text{irreversible}}$$

> **🔐 సారాంశం:** AI యుగంలో అరుదైనది "చిత్రం" కాదు; **నిరూపించగల శ్రమ, సమయం మరియు సంకల్పం**.

---

## 🎨 [PoArt] శ్రమ సాక్ష్య ప్రోటోకాల్ (Proof of Art Protocol v1.0)

> **"నిజమైన కళాకారుడు, నిజమైన ఉత్పత్తి, నిజమైన విలువ."**

ఈ ప్రోటోకాల్; క్రిప్టో ఎకోసిస్టమ్‌ను చుట్టుముట్టిన అనామక మోసగాళ్ళు, 5 నిమిషాల్లో ఉత్పత్తి చేయబడిన కృత్రిమ మేధస్సు చిత్రాలు మరియు "Pump & Dump" (పంప్ అండ్ డంప్) సంస్కృతికి వ్యతిరేకంగా అభివృద్ధి చేయబడిన **జీవ మరియు మేధో రక్షణ యంత్రాంగం**.

---

## అ) [PoArt] అంటే ఏమిటి?

**Proof of Art [PoArt];** బ్లాక్‌చెయిన్‌పై ఆస్తి వెనుక ఉన్న విలువ, ఊహాగానాలపై కాకుండా; ధృవీకరించగల **మానవ శ్రమ**, **సమయం** మరియు **భౌతిక శక్తి** ఆధారంగా ఉందని హామీ ఇచ్చే సంస్థాగత ధృవీకరణ ప్రమాణం.

Bitcoin ఎలా *"విద్యుత్ మరియు ప్రాసెసర్ శక్తి"* **(Proof of Work)** ద్వారా విలువను ఉత్పత్తి చేస్తుందో; [PoArt] అనుకూల ప్రాజెక్ట్‌లు కూడా *"ఖర్చు చేయబడిన ప్రతిభ మరియు మానవ సమయం"* ద్వారా విలువను ఉత్పత్తి చేస్తాయి.

> **[PoArt], పాల్గొనేవారికి "మమ్మల్ని నమ్మండి" అని చెప్పదు; "ఇవిగో సాక్ష్యాలు, మీ కళ్ళతో చూడండి, మీ గణితంతో ధృవీకరించండి" అని చెబుతుంది.**

---

## ఆ) [PoArt] 5 ప్రమాణాలు (The 5 Pillars of Truth)

### 1) లైవ్ ఐడెంటిటీ ప్రూఫ్ (Live Identity Proof)

- **సమస్య:** క్రిప్టో ప్రపంచం, అనామక వ్యవస్థాపకులు డబ్బు సేకరించి ప్రాజెక్ట్‌ను వదిలివేయడంతో నిండి ఉంది.
- **[PoArt] పరిష్కారం:** ఉత్పత్తిదారు, **ఉత్పత్తి సమయంలో ఉనికిని** నిరూపిస్తారు లైవ్ స్ట్రీమ్ సెషన్లలో.
- **నినాదం:** *"బోట్లు పెయింటింగ్ చేయగలవు కానీ బోట్లు చెమటలు కారచవు మరియు మెరుగుపరచలేవు."*

### 2) శ్రమ మరియు ప్రక్రియ సాక్ష్యం (Labor & Process Proof)

- **సమస్య:** 2 సెకన్లలో ఉత్పత్తి చేయబడిన AI చిత్రాలు 2 నెలల్లో చేసిన ఆయిల్ పెయింటింగ్‌తో ఒకే "jpeg" ట్రీట్‌మెంట్ పొందడం.
- **[PoArt] పరిష్కారం:** కళాకృతి యొక్క "గర్భం మరియు జన్మ" ప్రక్రియ రికార్డ్ చేయబడుతుంది. ఇది టోకెన్‌కు **"సమయ వ్యయం" (Time Cost)** జోడిస్తుంది.

### 3) సౌందర్య విలువ సాక్ష్యం (Aesthetic Value Proof)

- **సమస్య:** "మీమ్" సంస్కృతి సౌందర్యాన్ని విస్మరించి తక్షణ హాస్యంపై మాత్రమే దృష్టి పెట్టడం.
- **[PoArt] పరిష్కారం:** ప్రాజెక్ట్, అకాడమిక్ కళా ప్రమాణాలు, రంగు సిద్ధాంతం, కూర్పు నియమాలు కలిగి ఉండాలి.

### 4) భావనాత్మక ఆవిష్కరణ (Conceptual Novelty)

- **సమస్య:** ఒకరి నకలుగా ఉన్న, సృజనాత్మకతకు దూరంగా ఉన్న వేలాది కుక్క/పిల్లి coins.
- **[PoArt] పరిష్కారం:** ప్రాజెక్ట్; కళ, సైన్స్, తత్వశాస్త్రం లేదా సాంకేతికతను అర్థవంతమైన నిర్మాణంలో కలిపే కొత్త వంతెనను నిర్మించాలి.

> [!IMPORTANT]
> **రిఫరెన్స్ ఉదాహరణ (Las Palmitas ఎఫెక్ట్):**  
> మెక్సికో యొక్క నేరంతో పోరాడుతున్న Las Palmitas ప్రాంతంలో, 200+ ఇళ్ళు భారీ ఇంద్రధనుస్సు ఉత్సవంగా మారాయి. ఈ సౌందర్య జోక్యం తర్వాత ప్రాంతంలో నేర రేట్లు తగ్గాయి.

### 5) అల్గారిథమిక్-కాని సంకల్పం (Non-Algorithmic Agency)

- **సమస్య:** సరైన కానీ ఆత్మ లేని, ఒకరినొకరు పునరావృతం చేసే డిజిటల్ ఉత్పత్తులు.
- **[PoArt] పరిష్కారం:** తప్పు చేయగల, రిస్క్ తీసుకునే మానవుని ప్రత్యేక సంకల్పం కళాకృతిలో అనుభవించబడాలి - **జీవ సంతకం**.

---

## ఇ) ధృవీకరణ & మోసం-వ్యతిరేక యంత్రాంగం

### 📦 సాక్ష్య ప్యాకేజ్ (Evidence Pack)

ప్రతి [PoArt] సర్టిఫికేట్ కలిగిన కళాకృతి వెనుక, పెట్టుబడిదారులు డౌన్‌లోడ్ చేయగల ఎన్‌క్రిప్టెడ్ డేటా ప్యాకేజ్ ఉంది:

- **RAW వీడియో రికార్డులు:** ఉత్పత్తి క్షణం యొక్క అంతరాయం లేని ముడి చిత్రాలు.
- **Metadata విశ్లేషణ:** ఫైల్ సృష్టి తేదీ, పరికర సమాచారం మరియు స్థాన డేటా.
- **భౌతిక రిఫరెన్స్‌లు:** కళాకృతి భౌతిక ప్రపంచంలో ఉందని నిరూపించే సాక్ష్యాలు.

### 🔄 365 రోజుల పునరుద్ధరణ (The Sustainability Protocol)

- **నియమం:** "Verified Artist" స్థితి **1 సంవత్సరం** మాత్రమే చెల్లుతుంది.
- **ప్రక్రియ:** కళాకారుడు/డెవలపర్, ప్రతి 365 రోజులకు, సమాజానికి **కొత్త, పెద్ద మరియు నిరూపించగల కళాకృతిని** సమర్పించాలి.

### 🚩 రెడ్ ఫ్లాగ్ (Red Flag Protocol)

**మోసం కనుగొనబడితే:**

1. సర్టిఫికేట్ వెంటనే **"రద్దు" (VOID)** గా గుర్తించబడుతుంది.
2. సాక్ష్య ప్యాకేజీలు **"నకిలీ"** గా పబ్లిక్‌గా లేబుల్ చేయబడతాయి.
3. ప్రాజెక్ట్ [PoArt] బ్లాక్‌లిస్ట్‌లో చేర్చబడుతుంది.

---

## ఈ) ముగింపు: జూదం కాదు, మ్యూజియం

**[PoArt], జూదశాల మధ్యలో నిర్మించబడిన కోట.**

- 🎰 జూదశాల కాగితపు ఆటలపై ఆధారపడి ఉంటుంది; మేము **భౌతిక వాస్తవికతపై** ఆధారపడి ఉన్నాము.
- 🃏 జూదశాల మోసానికి తెరిచి ఉంటుంది; మేము **పారదర్శక సాక్ష్యాలకు** తెరిచి ఉన్నాము.
- ⏳ జూదశాల తాత్కాలికం; మేము **కళ మరియు సైన్స్ యొక్క శాశ్వతత్వంపై** దృష్టి పెడుతున్నాము.

**ఈ ప్రోటోకాల్‌ను ఉపయోగించే టోకెన్, కేవలం "coin" కాదు; వెనుక చెమట, రంగు, కోడ్ మరియు తత్వశాస్త్రం కలిగిన డిజిటల్ షేర్ డాక్యుమెంట్.**

---

## 🗳️ 6) గవర్నెన్స్ & పబ్లిక్ రిజిస్ట్రీ

### 6.1 Public Registry (పబ్లిక్ రిజిస్ట్రీ)

అన్ని ఆమోదించబడిన డేటాలు ilhanart.org/registry లో నమోదు చేయబడతాయి.

**రిజిస్ట్రీ ఫీల్డ్‌లు:**

- **ఐడెంటిటీ & స్టేటస్:** certificate_id, status, visibility, created_at
- **జారీ చేసే సంస్థ:** issuer.name, issuer.location, issuer.attestation_pubkey
- **కళాకృతి సమాచారం:** asset.title, asset.creator, asset.fingerprints.sha256/sha512
- **ఫోరెన్సిక్ డేటా:** forensics.ip_masked, forensics.location, forensics.device, forensics.timestamp
- **క్రిప్టోగ్రాఫిక్ సాక్ష్యాలు:** proof.evidence_root, proof.signer_sig, proof.notary_seal
- **గవర్నెన్స్:** governance.decision, governance.review_notes

### 6.2 PoArt Verified దరఖాస్తు ప్రక్రియ

**PoArt Verified దరఖాస్తులు, İlhan Art Gallery ద్వారా 5 PoArt ప్రమాణాల ప్రకారం మూల్యాంకనం చేయబడతాయి.**

**ప్రక్రియ:**
1. దరఖాస్తు సమర్పణ
2. పరిశీలన (30 రోజులు)
3. సమాజ సంప్రదింపు
4. నిర్ణయం (Approved / Rejected)

### 6.3 Token Utility

**$CULTURE టోకెన్ హోల్డర్లకు అందించబడే ప్రయోజనాలు:**

1. **గ్యాలరీ ఈవెంట్‌లకు ప్రాథమ్యత యాక్సెస్** - సంవత్సరానికి 1 వారం ఎగ్జిబిషన్
2. **PoArt Registry పూర్తి యాక్సెస్** - Evidence Pack-ల పూర్తి వెర్షన్‌లు
3. **Advisory Voting** - PoArt Verified దరఖాస్తులలో సలహా హక్కు
4. **Exclusive Content** - Behind-the-scenes కంటెంట్‌లు

---

## 7) 🔐 టెక్నికల్ సీల్ (NOTARY SEAL)

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] డిజిటల్ నోటరీ & ఫోరెన్సిక్ సాక్ష్య ప్రోటోకాల్ (Beta v1.0)

> **"సంస్కృతి, మూలధనం కంటే గొప్పది. మీ కళాకృతులను ఈ రోజే రక్షించండి, రేపటికి తీసుకెళ్ళండి."**

## ఎందుకు పబ్లిక్‌గా తెరిచి ఉంది?

నిజమైన భద్రత పారదర్శకత నుండి వస్తుంది. **Public Registry** వ్యవస్థను ఉపయోగించి, ప్రపంచంలో ఎక్కడైనా ఉన్న వ్యక్తి చేతిలో ఉన్న ఫైల్ అసలు అని సెకన్లలో ధృవీకరించవచ్చు.

---

## 🧩 Visibility Modules

### 🔒 ప్రైవేట్ (Private)
కళాకారుడు కళాకృతిని ఇంకా ప్రచురించాలనుకోవడం లేదు కానీ టైమ్‌స్టాంప్ వేసి ధృవీకరించాలనుకుంటారు.

### 🕶️ మాస్క్ చేయబడిన (Masked)
కళాకారుడు పారదర్శకత కోరుకుంటారు కానీ IP/స్థానం కనుగొనబడటానికి భయపడతారు. IP 88.241.*.** ఫార్మాట్‌కు మారుతుంది.

### 🌍 అందరికీ తెరిచిన (Public)
పూర్తి పారదర్శకత. కళాకృతి ఎక్కడ, ఎప్పుడు, ఏ నెట్‌వర్క్ నుండి ఉత్పత్తి చేయబడిందో స్పష్టంగా ప్రకటించబడుతుంది.

---

## 💡 సాంకేతిక ఆవిష్కరణ

### 1) Client-Side Hashing
మీ కళాకృతి ఫైల్‌లు ఎప్పుడూ సర్వర్‌కు అప్‌లోడ్ చేయబడవు. Hash మీ కంప్యూటర్‌లోనే లెక్కించబడుతుంది.

### 2) Forensic Data Fusion
- **డిజిటల్ సారాంశం (SHA-512):** కళాకృతి యొక్క ఒక పిక్సెల్ మారినా విరిగిపోయే వేలిముద్ర
- **స్థానం & సమయం:** మిల్లీసెకన్ ఖచ్చితత్వంతో
- **పరికర ఐడెంటిటీ:** ఆపరేటింగ్ సిస్టమ్, బ్రౌజర్ మరియు పరికర రకం

---

## ⚙️ సిస్టమ్ ఆర్కిటెక్చర్

| పొర | టెక్నాలజీ | వివరణ |
|--------|-----------|----------|
| **క్రిప్టోగ్రఫీ** | SHA-256 & SHA-512 | డబుల్ లేయర్ సారాంశం |
| **డేటాబేస్** | Supabase (PostgreSQL) | JSONB + RLS policies |
| **ఫోరెన్సిక్ డేటా** | ipapi.co API | IP/స్థానం/సమయం త్రయం |
| **Rendering** | html2canvas + jsPDF | Client-side PNG/PDF |
| **Frontend** | Vanilla JavaScript | Zero framework dependency |
| **భద్రత** | Client-side hashing | ఫైల్ సర్వర్‌కు వెళ్ళదు |

---

## 🗺️ రోడ్‌మ్యాప్

### ఫేజ్ 1: Beta v1.0 (ప్రస్తుతం)
- Cloud Database (Supabase)
- Off-chain registry
- Gallery self-attestation

### ఫేజ్ 2: Decentralized Authority (2026 Q2-Q4)
- Edge Function INSERT
- Wallet సంతకం (Solana)
- IPFS/Arweave Backup
- OpenTimestamps

### ఫేజ్ 3: పూర్తి వికేంద్రీకరణ (2027+)
- On-Chain Registry (Solana)
- Multi-Chain Support
- DID Integration
- టర్కీ న్యాయస్థానాలలో చెల్లుబాటు
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

## 🔬 టెక్నికల్ డెప్త్: సీల్ అల్గారిథమ్

```javascript
// Deterministic Hash ఫంక్షన్లు
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// FileHash లెక్కింపు
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// EvidenceRoot సృష్టి
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = 
    "file_sha512:" + fileHash512 + "\n" +
    "forensics:" + JSON.stringify(forensicsData);
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// NotarySeal ఉత్పత్తి
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = 
    "evidence_root:" + evidenceRoot + "\n" +
    "signer_sig:" + signerSignature + "\n" +
    "timestamp:" + timestamp;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// మాస్కింగ్ ఫంక్షన్
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
    return { valid: true, message: "✅ అసలు" };
  } else {
    return { valid: false, message: "❌ నకిలీ" };
  }
}
```

### Full Verify
```javascript
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  const cert = await fetchFromRegistry(certificateId);

  // FileHash తనిఖీ
  if (userFileHash !== cert.asset.fingerprints.sha512) {
    return { valid: false, message: "❌ ఫైల్ hash సరిపోలడం లేదు" };
  }

  // EvidenceRoot మళ్ళీ సృష్టి
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ EvidenceRoot సరిపోలడం లేదు" };
  }

  // NotarySeal మళ్ళీ సృష్టి
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ NotarySeal సరిపోలడం లేదు" };
  }

  return { valid: true, message: "✅ Full Verify పాస్" };
}
```

---

## 📊 పోటీదారుల విశ్లేషణ

| ఫీచర్ | **PoArt** | OpenTimestamps | Verisart | OriginStamp |
|---------|:---------:|:---------------:|:---------:|:-----------:|
| **ఖర్చు** | 🆓 ఉచితం | 🆓 | 💰 చెల్లింపు | ⚠️ Freemium |
| **Drag & Drop UI** | ✅ | ❌ CLI | ⚠️ | ⚠️ |
| **Privacy Controls** | ✅ 3 మోడ్‌లు | ❌ | ❌ | ❌ |
| **Client-Side Hash** | ✅ | ✅ | ❌ | ⚠️ |
| **Forensic Metadata** | ✅ పూర్తి | ❌ | ❌ | ⚠️ |
| **తెలుగు మద్దతు** | ✅ | ❌ | ❌ | ❌ |
| **ఓపెన్ సోర్స్** | ✅ GitHub | ✅ | ❌ | ⚠️ |

---

## 📈 వినియోగ గణాంకాలు (2026 Q1 లక్ష్యాలు)

| మెట్రిక్ | లక్ష్యం | స్థితి |
|--------|-------|-------|
| **మొత్తం సర్టిఫికేట్లు** | 1,000 | 🔄 పురోగతిలో |
| **యాక్టివ్ యూజర్లు** | 500 | 🔄 పురోగతిలో |
| **ధృవీకరణ సంఖ్య** | 5,000 | 🔄 పురోగతిలో |
| **Uptime** | %99.9 | ✅ యాక్టివ్ |
| **Avg Response Time** | <200ms | ✅ ఆప్టిమల్ |

---

## 🏛️ "Engine" భావన యొక్క ప్రాముఖ్యత

Pump.fun లేదా సారూప్య ప్లాట్‌ఫారమ్‌ల నుండి వచ్చే token-లు, చాలా సార్లు కేవలం **"యాక్సెస్ టికెట్"** మాత్రమే. **PoArt Forensic Engine (PFE)** ఆ టికెట్ ఏ హక్కులను రక్షిస్తుందో, శ్రమ ఎలా రికార్డ్ చేయబడుతుందో, కళ/సైన్స్/టెక్నాలజీ ఎలా శాశ్వతంగా చేయబడుతుందో నిర్ణయించే **రాజ్యాంగ తర్క పొర**.

---

## 🎯 ముగింపు: సాక్ష్యంతో లాక్ చేయబడిన విలువ

ఈ సిద్ధాంతం, [PoArt] విలువ వాదనను "ఇష్టం" లేదా "మార్కెట్ కథ" స్థితి నుండి బయటకు తీసుకువచ్చి **నిరూపించగల ఉత్పత్తి వాస్తవికతలో** అమరుస్తుంది.

### ముఖ్య పాయింట్లు

1. **ప్రక్రియ లేకుండా విలువ ఏర్పడదు:**  
   AI, వేగవంతమైన అవుట్‌పుట్‌లో ($t \to 0$) ప్రక్రియను నాశనం చేస్తుంది.

2. **సంకల్పం మరియు రిస్క్ గుణకం:**  
   [PoArt], "ఖర్చు చేసిన సమయాన్ని" మాత్రమే కాకుండా; ఆ సమయంలో ఉన్న నిజమైన నిర్ణయం, రిస్క్ మరియు వ్యయ పొరను కూడా కొలుస్తుంది.

3. **ప్రత్యేకత, మార్కెటింగ్ కాదు భౌతిక సాక్ష్యం:**  
   భౌతిక ఉత్పత్తిలో తిరిగి పొందలేని గుర్తులు, డిజిటల్ Ctrl+Z తర్కానికి బయట ఉన్నాయి.

---

## 📊 అదనపు పోటీదారుల విశ్లేషణ

### పోటీదారుల లోపాలు, PoArt బలాలు

| లోపం | పోటీదారులు | PoArt |
|------|----------|-------|
| **వినియోగ కష్టం** | CLI, API జ్ఞానం, వాలెట్ అవసరం | డ్రాగ్-డ్రాప్, 3 క్లిక్‌లలో ముగింపు |
| **ఖర్చు అడ్డంకి** | $50-500/నెల సబ్‌స్క్రిప్షన్ | %100 ఉచితం |
| **ప్రైవసీ** | ఫైల్ సర్వర్‌కు అప్‌లోడ్ అవుతుంది | Client-side, ఫైల్ ఎప్పుడూ వెళ్ళదు |
| **Forensic డేటా** | Timestamp మాత్రమే | IP, స్థానం, పరికరం, సమయం - అన్నీ |
| **తెలుగు మద్దతు** | లేదు లేదా చాలా పరిమితం | Native భాష మద్దతు |
| **ఓపెన్ సోర్స్** | మూసిన బాక్స్ | GitHub లో అన్ని కోడ్ తెరిచి ఉంది |

---

## 🔄 Token Governance పరిణామం

### v1.0 (2026)
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (కేంద్రీకృత కానీ పారదర్శక)
- Governance: Advisory only (సంస్కృతి సంరక్షకుడు తుది నిర్ణయం)
- Token utility: Gallery access + registry + NFT priority

### v2.0 (2027)
- Registry: On-chain (Solana)
- Signatures: Wallet-based (decentralized)
- Governance: Hybrid (community advisory + curatorial quality)
- Token utility: Enhanced features + advanced access

### v3.0+ (2028+)
- Full community governance (optional)
- సంస్కృతి సంరక్షకుడు quality control ఎల్లప్పుడూ రక్షించబడుతుంది
- Multi-chain support పూర్తిగా

---

## 🛡️ వినియోగ ప్రదేశాలు & ప్రయోజనం వివరాలు

కళాకారుడు, రచయిత లేదా డిజైనర్ అయితే, "దీన్ని నేను ముందే చేశాను" అని చెప్పడం సరిపోదు, నిరూపించాలి.

**PoArt తో సీల్ చేసిన కళాకృతి:**

- **గణిత సాక్ష్యం:** మీ ఫైల్ యొక్క ఒక పిక్సెల్ కూడా మారితే సిస్టమ్ అర్థం చేసుకుంటుంది. మోసం సాధ్యం కాదు.
- **న్యాయ ఆధారం:** కళాకృతి ఏ తేదీన, ఏ నగరంలో, ఏ పరికరం నుండి సీల్ చేయబడిందో రికార్డ్ చేయబడింది.
- **తక్షణ సర్టిఫికేట్:** సెకన్లలో ప్రత్యేకమైన, QR కోడ్ కలిగిన మరియు సీల్ చేయబడిన **"ఆస్తి ఐడెంటిటీ సర్టిఫికేట్"** సృష్టిస్తుంది.

---

## 📝 Canonical Encoding వివరాలు

### v1.0 Canonicalization ప్రమాణం

- **స్థిర ఫీల్డ్ క్రమం:** ip_masked → location → device → timestamp
- **Encoding:** UTF-8
- **Delimiter:** `\n` (newline)

### ఫేజ్ 2 ప్రణాళిక

RFC 8785 (JCS - JSON Canonicalization Scheme) తో canonical JSON కి మారడం.

---

## 🎨 సాంస్కృతిక సందర్భం

### "సంస్కృతి మూలధనం కంటే గొప్పది" తత్వశాస్త్రం

ఈ ప్రాజెక్ట్ "Culture > Capital" తత్వశాస్త్రం ఆధారంగా ఉంది. దీని అర్థం:

1. **దీర్ఘకాలిక ఆలోచన:** 2025 నుండి 3000 CE వరకు 975-సంవత్సర దృష్టి
2. **ఊహాగాన వ్యతిరేక సూత్రం:** Token ధరను పెంచడం కంటే సాంస్కృతిక విలువకు ప్రాధాన్యత
3. **సమాజ కేంద్రీకృతం:** Mercenary capital కాకుండా దీర్ఘకాలిక పాల్గొనేవారు

### తెలుగు సంస్కృతి మరియు PoArt

తెలుగు సంస్కృతి వేల సంవత్సరాల పురాతన కళా వారసత్వం కలిగి ఉంది. PoArt ఈ వారసత్వాన్ని రక్షించడానికి మరియు బదిలీ చేయడానికి ఆధునిక సాంకేతికతను అందిస్తుంది:

- **పురాతన కళ:** కాకతీయ శిల్పాలు, తంజావూరు చిత్రాలు
- **ఆధునిక కళ:** తెలుగు చిత్రకారులు మరియు శిల్పులు
- **డిజిటల్ ఆర్కైవ్:** భవిష్యత్ తరాలకు నశించని రికార్డు

---

## 🌐 ప్రపంచవ్యాప్త ప్రాప్యత

### భాష మద్దతు

PoArt ప్రోటోకాల్ అనేక భాషలలో అందుబాటులో ఉంది:

- 🇹🇷 Türkçe (ప్రధాన)
- 🇬🇧 English
- 🇪🇸 Español
- 🇨🇳 中文
- 🇫🇷 Français
- 🇩🇪 Deutsch
- 🇷🇺 Русский
- 🇮🇳 తెలుగు (ఈ డాక్యుమెంట్)

### ఎందుకు అనేక భాషలు?

PoArt ప్రపంచవ్యాప్త కళా సమాజం కోసం రూపొందించబడింది. ఏ కళాకారుడైనా, ఎక్కడైనా, తమ కళాకృతిని రక్షించగలగాలి.

---

## 🔗 ముఖ్యమైన లింక్‌లు

### అధికారిక

- **వెబ్:** [ilhanart.org](https://ilhanart.org)
- **Registry:** [ilhanart.org/public-registry](https://ilhanart.org/public-registry)
- **GitHub:** [github.com/galeri-coder](https://github.com/galeri-coder)

### సోషల్ మీడియా

- **Twitter/X:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Instagram:** [ilhanartgaleri](https://instagram.com/ilhanartgaleri)

### సంప్రదింపు

- **ఇమెయిల్:** galeri@ilhanart.org

---

## ⚠️ ముఖ్యమైన హెచ్చరికలు

1. **Token ధర:** Token ధర కళా నాణ్యత సూచిక కాదు
2. **పెట్టుబడి సలహా కాదు:** ఈ డాక్యుమెంట్ పెట్టుబడి సలహా కాదు
3. **Beta వెర్షన్:** సిస్టమ్ ఇంకా అభివృద్ధిలో ఉంది
4. **బాధ్యత:** వినియోగదారులు తమ సొంత పరిశోధన చేయాలి

---

## 🌍 సమాజం & మద్దతు

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **వెబ్:** [ilhanart.org](https://ilhanart.org)
- **ఇమెయిల్:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 సహకారం

**సహకరించడానికి:**
1. Fork చేయండి
2. Feature branch సృష్టించండి
3. Commit చేయండి
4. Push చేయండి
5. Pull Request తెరవండి

### సహాయ పిలుపు

* **Supabase Edge Functions**
* **Solana Web3.js**
* **IPFS / Arweave**
* **Community Tools**

---

## 💬 చివరి గమనికలు

### Pump.fun & వాస్తవికత

ఈ ప్రాజెక్ట్ Pump.fun లో ప్రారంభించబడింది ఎందుకంటే:
- ✅ Liquidity యాక్సెస్
- ✅ ఇప్పటికే ఉన్న సమాజ యాక్సెస్
- ✅ తక్కువ ప్రారంభ ఖర్చు

**అయితే:**
- **Token ధర** కళా విజయ సూచిక కాదు
- **విజయ కొలమానాలు:** Authenticated artworks + community engagement + భౌతిక సందర్శకులు

---

## 📋 అదనపు టెక్నికల్ వివరాలు

### రిజిస్ట్రీ ఉదాహరణ (Registry JSON)

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

## 🔐 భద్రత గమనికలు

### Client-Side ప్రయోజనాలు

1. **ఫైల్ ప్రైవసీ:** కళాకృతి ఫైల్‌లు ఎప్పుడూ సర్వర్‌కు అప్‌లోడ్ చేయబడవు
2. **Hash లెక్కింపు:** అన్ని క్రిప్టోగ్రాఫిక్ పని బ్రౌజర్‌లో జరుగుతుంది
3. **సాక్ష్య సమగ్రత:** Deterministic అల్గారిథమ్‌లు reproducible ఫలితాలను నిర్ధారిస్తాయి

### Masked Mode ఫీచర్లు

- IP అడ్రస్: `88.241.123.45` → `88.241.***.***`
- స్థానం: `Istanbul, Turkey` → `***/TR`
- Forensics hash లెక్కింపు masked డేటాను ఉపయోగిస్తుంది

### Public Mode ఫీచర్లు

- పూర్తి IP అడ్రస్ చూపబడుతుంది
- పూర్తి స్థాన వివరాలు
- ధృవీకరణకు పూర్తి పారదర్శకత

---

## 📈 అదనపు వినియోగ గణాంకాలు

| కొలమానం | వివరాలు |
|--------|---------|
| **మద్దతు ఉన్న ఫైల్ రకాలు** | PNG, JPG, PDF, MP4, అన్నీ |
| **గరిష్ట ఫైల్ పరిమాణం** | అపరిమితం (client-side) |
| **Hash అల్గారిథమ్‌లు** | SHA-256, SHA-512 |
| **సర్టిఫికేట్ ఫార్మాట్‌లు** | PNG, PDF, JSON |
| **QR కోడ్** | ప్రతి సర్టిఫికేట్‌లో |

---

## 🔄 ధృవీకరణ ప్రక్రియ వివరాలు

### Quick Verify ప్రక్రియ

1. వినియోగదారు ఫైల్‌ను ఇన్‌పుట్ చేస్తారు
2. Client-side SHA-512 hash లెక్కించబడుతుంది
3. Registry లో నమోదు చేయబడిన hash తో పోల్చబడుతుంది
4. ఫలితం తిరిగి వస్తుంది: ✅ అసలు లేదా ❌ నకిలీ

### Full Verify ప్రక్రియ

1. Quick Verify చేయబడుతుంది
2. EvidenceRoot మళ్ళీ లెక్కించబడుతుంది
3. NotarySeal మళ్ళీ లెక్కించబడుతుంది
4. అన్ని విలువలు పోల్చబడతాయి
5. పూర్తి ధృవీకరణ ఫలితం తిరిగి వస్తుంది

---

## 📝 Forensics డేటా వివరాలు

| ఫీల్డ్ | వివరణ | ఉదాహరణ |
|------|---------|-------|
| ip_masked | మాస్క్ చేయబడిన IP | 88.241.*.** |
| location | స్థానం | Istanbul/TR లేదా ***/TR |
| device | పరికరం | Brave (Windows) |
| timestamp | సమయం | 2026-01-09T12:34:56.000Z |

---

## 🧪 Hash Algorithm ఎంపిక

**ఎందుకు SHA-512?**

1. **భద్రత:** 512-bit output అధిక భద్రతను అందిస్తుంది
2. **Collision Resistance:** రెండు వేర్వేరు ఫైల్‌లు ఒకే hash పొందడం సాధ్యం కాదు
3. **వేగం:** ఆధునిక కంప్యూటర్‌లలో వేగంగా పనిచేస్తుంది
4. **ప్రమాణం:** ప్రపంచవ్యాప్తంగా అంగీకరించబడిన algorithm

---

## 🌟 కృతజ్ఞతలు

ఈ ప్రాజెక్ట్ క్రింది వారికి కృతజ్ఞతలు తెలుపుతుంది:

- **İlhan Art Gallery** - దృష్టి మరియు నాయకత్వానికి
- **ఓపెన్ సోర్స్ సమాజం** - సహకారానికి
- **తెలుగు కళాకారులు** - ప్రేరణకు
- **ప్రపంచవ్యాప్త కళా సమాజం** - మద్దతుకు

---

## 📞 మద్దతు

ప్రశ్న లేదా సమస్య ఉంటే:

1. **GitHub Issues:** టెక్నికల్ సమస్యలు
2. **ఇమెయిల్:** సాధారణ ప్రశ్నలకు
3. **Twitter DM:** వేగవంతమైన స్పందనకు

---

## 🔄 Version History

| Version | తేదీ | మార్పులు |
|---------|------|--------|
| v1.0-beta | 2026-01 | మొదటి వెర్షన్ |
| v1.1 | TBD | Bug fixes |
| v2.0 | 2026-Q4 | Wallet integration |
| v3.0 | 2027-Q1 | On-chain registry |

---

## 📄 లైసెన్స్ పూర్తి టెక్స్ట్

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

## 📜 చివరి మాటలు

> **"సంస్కృతి, మూలధనం కంటే గొప్పది."**

ఈ ప్రోటోకాల్ కళ యొక్క విలువను ఊహాగానం నుండి సాక్ష్యానికి మార్చడానికి రూపొందించబడింది. AI యుగంలో, మానవ శ్రమ, సమయం మరియు సంకల్పాన్ని నిరూపించడం అవసరమైంది.

[PoArt] ఈ సమస్యను పరిష్కరిస్తుంది - **నిరూపించగల సాక్ష్యంతో**.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // సంస్కృతి, మూలధనం కంటే గొప్పది*

## 🧾 లైసెన్స్

MIT License © 2026 İlhan Art Gallery Initiative

---

## 💬 క్రెడిట్స్

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) 
![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) 
![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) 
![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**ఈ ప్రాజెక్ట్ [İlhan Art Gallery] చొరవతో అభివృద్ధి చేయబడింది, సోర్స్ కోడ్‌లు పారదర్శకత కోసం పబ్లిక్‌గా తెరిచి ఉన్నాయి.**

**ప్రోటోకాల్ V1.0 // SHA-512 తో సీల్ చేయబడింది.**

*© 2026 İLHAN ART | కళాకృతులు, చిత్రాలు మరియు ఆలోచనల అన్ని హక్కులు రక్షించబడ్డాయి.*

---

*ఈ డాక్యుమెంట్ టర్కిష్ మూలం నుండి తెలుగులోకి అనువదించబడింది.*  
*అన్ని టెక్నికల్ వివరాలు, కోడ్‌లు, JSON, LaTeX మరియు markdown రక్షించబడ్డాయి.*

---
