# 📚 የቃላት መዝገበ ቃላት እና ፅንሰ-ሀሳቦች
> **"የዚህን ፕሮቶኮል ቋንቋ መረዳት ማለት ራዕዩን መረዳት ማለት ነው።"**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: ዋና መሰረተ ልማት

**PoArt Forensic Engine (PFE)** የ[PoArt] ፕሮቶኮል ዋና ሎጂክ እና ቴክኒካዊ አሰራርን የሚወክል ዋና ንብርብር ነው። ይህ "የፎረንሲክ ሞተር" የስነ-ጥበብ ስራዎችን ጥሬ የማምረት መረጃ ወስዶ ወደ ሊረጋገጥ እና ሊቀየር የማይችል **ዲጂታል ማስረጃ** የሚቀይር ቦታ ነው።

### 🧩 ለምን "PoArt Forensic"?

- **PoArt (Proof of Art):** የሞተሩ ትኩረት የዲጂታል ንብረት ዋጋን ከግምት ላይ ሳይሆን፣ **ሊረጋገጥ በሚችል የማምረት ሂደት** ላይ የተመሰረተ ማድረግ ነው።
- **Forensic (የፎረንሲክ ማረጋገጫ):**
  - **ቴክኒካዊ ትርጓሜ:** የማምረት ሂደት መረጃዎች (የብሩሽ ምቶች፣ timelapse፣ logs) እንዳልተጭበረበሩ ለማረጋገጥ የተነደፈ አልጎሪዝም እና የመዝገብ ሰንሰለት አቀራረብ።
  - **ፍልስፍናዊ ንብርብር:** ሰው ሰራሽ ብልህነት (AI) "ፈጣን ውጤት" ከሚያመርተው በተቃራኒ፤ የሰውን **ጊዜ፣ ጥረት እና የውሳኔ ዋጋ** ወደ ሊለካ የሚችል እውነታ የመቀየር ጥያቄ።

> ማስታወሻ፦ የብሎክቼይን (ለምሳሌ Solana) ውህደት የPFE ዋና አካል ሳይሆን፤ ለማረጋገጫ/ምዝገባ በተለየ **Chain Anchor Layer** ይታከላል።

### 🛠️ v1.0 ቴክኒካዊ ወሰን

**PoArt Forensic Engine (PFE) v1.0** ውስብስብ የፋይናንስ ሞዴሎች ሳይሆን በዚህ **3 ዋና ምሰሶዎች** ላይ የተገነባ ነው፡

1. **Hashing & Sealing (ማሸግ):**  
   PFE፣ Evidence Pack ውስጥ ያሉትን ሁሉንም ንጥረ ነገሮች (የስራ ፋይል፣ ቪዲዮ፣ JSON/log፣ ፊርማ ወዘተ) በዲተርሚኒስቲክ መንገድ አስሮ ልዩ **NotarySeal** ዋጋ ያመነጫል።

   **ዋና ፅንሰ-ሀሳቦች (v1.0):**
   - **FileHash (የስራ ጣት አሻራ):** ከስራ ፋይል ባይት የሚመነጭ hash።
   - **EvidenceRoot (የማስረጃ ፓኬጅ ስር):** የEvidence Pack ታማኝነትን የሚወክል ስር ማጠቃለያ (Merkle root ወይም canonical manifest hash)።
   - **NotarySeal (የመጨረሻ ማሸጊያ / PFE Output):** EvidenceRoot + ጊዜ + ፊርማ ጥምር የሚመነጭ የመጨረሻ ማሸጊያ።

   **ቀመሮች (ለባለሃብት ግልጽ በሆነ መንገድ):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload ትርጓሜዎች (v1.0):**
   
   - **EvidenceRootPayload:**
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
   
   - **NotarySealPayload:**
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
   
   > ማስታወሻ፦ እንደ PFE ውጤት የሚታሰበው ዋጋ **NotarySeal** ነው። **SignerSignature** ዘዴ በፋዝ 2 (ከSolana Wallet Adapter ጋር) ይሰራል፤ አሁን ባለው v1.0 ላይ የሲስተሙ ራሱ attestation ፊርማ ጥቅም ላይ ይውላል።

2. **Indexing (ማህደር):**  
   የትኛው ቦርሳ፣ በየትኛው ቀን፣ ለየትኛው ስራ **Labor Proof (የጉልበት ማስረጃ)** እንዳቀረበ፤ በግልጽ እና ሊፈለግ በሚችል የመዝገብ ንብርብር ላይ ይመዘግባል።

3. **Verification (ማረጋገጫ):**  
   የስራ ኦሪጂናልነት ሲጠየቅ PFE ጥሬ ማስረጃዎችን እንደገና ያስሰራል፤ የተሰላው **EvidenceRoot / NotarySeal** ዋጋዎች በማህደሩ ካለው መዝገብ ጋር የሚዛመዱ መሆናቸውን በሂሳብ እርግጠኝነት ይፈትሻል።

---

### 🧮 የPoArt ዋጋ ቲዎረም (The Value Theorem)

[PoArt] ፕሮቶኮል፣ የዲጂታል ንብረት ዋጋን (\$V\$) ከተገዢ የገበያ ግንዛቤ ሳይሆን፣ ከ**የማምረት ሂደት አካላዊ እውነታ** ጋር ያገናኛል።

ሰው ሰራሽ ብልህነት (AI)፣ ውጤቱን ወዲያውኑ በመስጠት (\$t \to 0\$) ሂደቱን ያጠፋል። [PoArt] ግን ዋጋን፣ **ጊዜ፣ ጉልበት እና ፈቃድ** አካላት ክምችት አድርጎ ይይዛል።

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### የተለዋዋጮች ትርጓሜ

- **\$\int dt\$ (የሂደት ክምችት):**  
  ዋጋ፣ ፈጣን "ውጤት" (output) ሳይሆን፤ በ\$t_{\text{start}}\$ እና \$t_{\text{end}}\$ መካከል የሚከማች **ሂደት** ነው።

- **\$P_{\text{labor}}(t)\$ (ፈጣን የጉልበት ኃይል):**  
  በማምረት ጊዜ የሚወጣውን የአዕምሮ እና አካላዊ ጥረት ጥግግት ይወክላል።

- **\$I_{\text{agency}}(t)\$ (የፈቃድ ቅንጅት):**  
  የአምራቹ አደጋ የመውሰድ እና ውሳኔ የመስጠት አቅም ነው። ከ\$0\$ እስከ \$1\$ ዋጋ ይወስዳል።
  - **AI (\$I \approx 0\$):** ትዕዛዞችን ያስፈጽማል፣ አደጋ አይወስድም።
  - **ሰው (\$I \to 1\$):** ውሳኔ ይቀይራል፣ ያመነታል፣ አደጋ ይወስዳል።

- **\$U_{\text{irreversible}}\$ (የማይመለስ ልዩነት):**  
  በዲጂታል ማምረት መመለስ (Ctrl+Z) ቢቻልም፤ በአካላዊ ማምረት መመለሻ የለም።

### 🔎 የጉዳይ ትንተና: AI vs. ሰው

#### ሁኔታ ሀ: በAI በ10 ሰኮንድ ምስል ማምረት

- **ጊዜ:** 10 ሰኮንድ
- **የጉልበት ኃይል:** 1 አሃድ
- **የፈቃድ ቅንጅት:** 0.01
- **የማይመለስ:** 0

**ውጤት:**
$$V_{\text{AI}} \approx 0.1$$

#### ሁኔታ ለ: በቀጥታ ስርጭት ለ6 ሰዓታት አካላዊ ማምረት

- **ጊዜ:** 6 ሰዓታት (21,600 ሰኮንድ)
- **የጉልበት ኃይል:** 0.5 አሃድ
- **የፈቃድ ቅንጅት:** 0.9
- **የማይመለስ:** >0

**ውጤት:**
$$V_{\text{Human}} \approx 9720 + U_{\text{irreversible}}$$

> **🔐 ማጠቃለያ:** በAI ዘመን ያልተለመደው "ምስል" ሳይሆን፤ **ሊረጋገጥ የሚችል ጉልበት፣ ጊዜ እና ፈቃድ** ነው።

---

## 🎨 [PoArt] የጉልበት ማስረጃ ፕሮቶኮል (Proof of Art Protocol v1.0)

> **"እውነተኛ አርቲስት፣ እውነተኛ ማምረት፣ እውነተኛ ዋጋ።"**

ይህ ፕሮቶኮል፤ የክሪፕቶ ስነ-ምህዳሩን የከበበውን ማንነታቸው ያልታወቁ አጭበርባሪዎች፣ በ5 ደቂቃ የሚመረቱ ሰው ሰራሽ ብልህነት ምስሎች እና "Pump & Dump" (አፍልቅ እና አውርድ) ባህል ላይ የተገነባ **ባዮሎጂያዊ እና አዕምሯዊ የመከላከያ ዘዴ** ነው።

---

## ሀ) [PoArt] ምንድን ነው?

**Proof of Art [PoArt];** በብሎክቼይን ላይ ያለ ንብረት ከኋላው ያለው ዋጋ፣ ከግምት ሳይሆን፤ ሊረጋገጥ በሚችል **የሰው ጉልበት**፣ **ጊዜ** እና **አካላዊ ሃይል** ላይ የተመሰረተ መሆኑን የሚያረጋግጥ ተቋማዊ የማረጋገጫ መስፈርት ነው።

Bitcoin *"ኤሌክትሪክ እና ፕሮሰሰር ኃይል"* **(Proof of Work)** ዋጋ እንደሚፈጥረው ሁሉ፤ [PoArt] ተኳሃኝ ፕሮጀክቶችም *"የወጣ ችሎታ እና የሰው ጊዜ"* ዋጋ ይፈጥራሉ።

> **[PoArt]፣ ለተሳታፊው "እመኑን" አይልም፤ "እነሆ ማስረጃዎች፣ በዐይንህ ተመልከት፣ በሂሳብህ አረጋግጥ" ይላል።**

---

## ለ) [PoArt] 5-ኛ መስፈርት (The 5 Pillars of Truth)

### 1) የቀጥታ ማንነት ማስረጃ (Live Identity Proof)

- **ችግር:** የክሪፕቶ ዓለም፣ ማንነታቸው ያልታወቁ መስራቾች ገንዘብ ሰብስበው ፕሮጀክቱን በመተው የተሞላ ነው።
- **[PoArt] መፍትሔ:** አምራች፣ **በማምረት ጊዜ መኖሩን** ያረጋግጣል በቀጥታ ስርጭት ክፍለ ጊዜዎች።
- **መፈክር:** *"ቦቶች ሥዕል መሳል ይችላሉ ግን ቦቶች አይለፉም እና በድንገት አይሰሩም።"*

### 2) የጉልበት እና ሂደት ማስረጃ (Labor & Process Proof)

- **ችግር:** በ2 ሰኮንድ የተመረቱ AI ምስሎች ከ2 ወር የተሰራ ዘይት ሥዕል ጋር ተመሳሳይ "jpeg" አያያዝ ማግኘት።
- **[PoArt] መፍትሔ:** የስራው "እርግዝና እና ልደት" ሂደት ይመዘገባል። ይህ ለtoken **"የጊዜ ወጪ" (Time Cost)** ይጨምራል።

### 3) የውበት ዋጋ ማስረጃ (Aesthetic Value Proof)

- **ችግር:** "Meme" ባህል ውበት እና ጥልቅ ጥበብን ቸል ብሎ ፈጣን ቀልድ ላይ ብቻ ማተኮር።
- **[PoArt] መፍትሔ:** ፕሮጀክት፣ የአካዳሚክ ስነ-ጥበብ መስፈርቶች፣ የቀለም ቲዎሪ፣ የቅንብር ህጎች ሊኖረው ይገባል።

### 4) ፅንሰ-ሀሳባዊ ፈጠራ (Conceptual Novelty)

- **ችግር:** እርስ በእርስ ቅጂ የሆኑ፣ ከፈጠራ የራቁ በሺዎች የሚቆጠሩ ውሻ/ድመት coins።
- **[PoArt] መፍትሔ:** ፕሮጀክት፤ ስነ-ጥበብ፣ ሳይንስ፣ ፍልስፍና ወይም ቴክኖሎጂን በትርጉም ያለው መዋቅር የሚያገናኝ አዲስ ድልድይ መገንባት አለበት።

> [!IMPORTANT]
> **ዋቢ ምሳሌ (Las Palmitas ውጤት):**  
> በሜክሲኮ Las Palmitas ሰፈር ውስጥ፣ ከ200 በላይ ቤቶች ወደ ግዙፍ ቀስተ ደመና ድግስ ተቀይረዋል። ይህ የውበት ጣልቃ ገብነት በኋላ በሰፈሩ ያለው የወንጀል ምጣኔ ቀንሷል።

### 5) አልጎሪዝም-ያልሆነ ፈቃድ (Non-Algorithmic Agency)

- **ችግር:** ፍጹም ግን ነፍስ-የሌላቸው፣ እርስ በእርስ የሚደጋገሙ ዲጂታል ማምረቶች።
- **[PoArt] መፍትሔ:** ስህተት መሥራት የሚችል፣ አደጋ የሚወስድ የሰው ልዩ ፈቃድ በስራው ላይ መሰማት አለበት - **ባዮሎጂያዊ ፊርማ**።

---

## ሐ) ማረጋገጫ እና ፀረ-ማጭበርበር ዘዴ

### 📦 የማስረጃ ፓኬጅ (Evidence Pack)

እያንዳንዱ [PoArt] ሰርተፊኬት ያለው ስራ ከኋላው፣ ባለሃብቶች ሊያወርዱት የሚችሉት የተመሰጠረ ዳታ ፓኬጅ አለ:

- **RAW ቪዲዮ መዝገቦች:** ያልተቋረጠ የማምረት ጊዜ ጥሬ ምስሎች።
- **Metadata ትንተና:** የፋይል ፍጥረት ቀን፣ መሳሪያ መረጃዎች እና የቦታ ዳታ።
- **አካላዊ ዋቢዎች:** ስራው በአካላዊ ዓለም ውስጥ መኖሩን የሚያረጋግጡ ማስረጃዎች።

### 🔄 የ365 ቀን ማደስ (The Sustainability Protocol)

- **ህግ:** "Verified Artist" ደረጃ **1 ዓመት** ብቻ ይሰራል።
- **አሰራር:** አርቲስት/ገንቢ፣ በየ365 ቀኑ፣ ለማህበረሰቡ **አዲስ፣ ትልቅ እና ሊረጋገጥ የሚችል ስራ** ማቅረብ አለበት።

### 🚩 ቀይ ባንዲራ (Red Flag Protocol)

**ማጭበርበር ከተገኘ:**

1. ሰርተፊኬት ወዲያውኑ **"ተሰርዟል" (VOID)** ተብሎ ይሰየማል።
2. የማስረጃ ፓኬጆች **"ሀሰተኛ"** ተብለው ይለጠፋሉ።
3. ፕሮጀክቱ በ[PoArt] ጥቁር ዝርዝር ላይ ይገባል።

---

## መ) ድምዳሜ: ካዚኖ ሳይሆን ሙዚየም

**[PoArt]፣ በካዚኖ መካከል የተገነባ ምሽግ ነው።**

- 🎰 ካዚኖ በወረቀት ጨዋታዎች ላይ የተመሰረተ ነው፤ እኛ **በአካላዊ እውነታ** ላይ ተመስርተናል።
- 🃏 ካዚኖ ለማጭበርበር ክፍት ነው፤ እኛ **ለግልጽ ማስረጃዎች** ክፍት ነን።
- ⏳ ካዚኖ ጊዜያዊ ነው፤ እኛ **የስነ-ጥበብ እና ሳይንስ ዘላለማዊነት** ላይ ነን።

**ይህን ፕሮቶኮል የሚጠቀም token፣ "coin" ብቻ ሳይሆን፤ ከኋላው ላብ፣ ቀለም፣ ኮድ እና ፍልስፍና የያዘ ዲጂታል የአክሲዮን ድርሻ ነው።**

---

## 🗳️ 6) አስተዳደር እና ሕዝባዊ መዝገብ

### 6.1 Public Registry (ሕዝባዊ መዝገብ)

ሁሉም የጸደቁ ዳታዎች ilhanart.org/registry ላይ ይመዘገባሉ።

**የመዝገብ ሜዳዎች:**

- **ማንነት እና ሁኔታ:** certificate_id, status, visibility, created_at
- **አውጭ ተቋም:** issuer.name, issuer.location, issuer.attestation_pubkey
- **የስራ መረጃ:** asset.title, asset.creator, asset.fingerprints.sha256/sha512
- **የፎረንሲክ ዳታ:** forensics.ip_masked, forensics.location, forensics.device, forensics.timestamp
- **ክሪፕቶግራፊክ ማስረጃዎች:** proof.evidence_root, proof.signer_sig, proof.notary_seal
- **አስተዳደር:** governance.decision, governance.review_notes

### 6.2 PoArt Verified ማመልከቻ ሂደት

**PoArt Verified ማመልከቻዎች፣ በኢልሃን አርት ጋለሪ በ5 PoArt መስፈርቶች ይገመገማሉ።**

**ሂደት:**
1. ማመልከቻ ማቅረብ
2. ምርመራ (30 ቀን)
3. የማህበረሰብ ምክክር
4. ውሳኔ (Approved / Rejected)

### 6.3 Token Utility

**ለ\$CULTURE token holder-ዎች የሚሰጡ ጥቅሞች:**

1. **የጋለሪ ዝግጅቶች ቅድሚያ መዳረሻ** - በዓመት 1 ሳምንት ኤግዚቢሽን
2. **PoArt Registry ሙሉ መዳረሻ** - Evidence Pack-ዎች ሙሉ ስሪቶች
3. **Advisory Voting** - በPoArt Verified ማመልከቻዎች ላይ የምክር መብት
4. **Exclusive Content** - Behind-the-scenes ይዘቶች

---

## 7) 🔐 ቴክኒካዊ ማሸጊያ (NOTARY SEAL)

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] ዲጂታል ኖተሪ እና የፎረንሲክ ማስረጃ ፕሮቶኮል (Beta v1.0)

> **"ባህል፣ ከካፒታል ይበልጣል። ስራዎቻችሁን ዛሬ ጠብቁ፣ ወደ ነገ ውሰዱ።"**

## ለምን ለሕዝብ ክፍት ነው?

እውነተኛ ደህንነት ከግልጽነት ይመጣል። **Public Registry** ስርዓታችን በመጠቀም፣ በዓለም ማንኛውም ቦታ ያለ ሰው በእጁ ያለው ፋይል ኦሪጂናል መሆኑን በሰኮንዶች ውስጥ ማረጋገጥ ይችላል።

---

## 🧩 Visibility Modules

### 🔒 ግላዊ (Private)
አርቲስት ስራውን ገና ማተም አልፈለገም ግን የጊዜ ማህተም አድርጎ ማረጋገጥ ይፈልጋል።

### 🕶️ ማስክ የተደረገ (Masked)
አርቲስት ግልጽነት ይፈልጋል ግን IP/ቦታ እንዳይገኝ ይፈራል። IP ወደ 88.241.*.** ቅርጽ ይቀየራል።

### 🌍 ለሁሉም ክፍት (Public)
ሙሉ ግልጽነት። ስራው የት፣ መቼ፣ ከየትኛው አውታረ መረብ እንደተመረተ በግልጽ ይገለጻል።

---

## 💡 ቴክኖሎጂያዊ ፈጠራ

### 1) Client-Side Hashing
የስራ ፋይሎቻችሁ ፈጽሞ ወደ ሰርቨር አይጫኑም። Hash በራሳችሁ ኮምፒውተር ላይ ይሰላል።

### 2) Forensic Data Fusion
- **ዲጂታል ማጠቃለያ (SHA-512):** የስራው አንድ ፒክሰል ቢቀየር እንኳ የሚበላሽ ጣት አሻራ
- **ቦታ እና ጊዜ:** በሚሊሰኮንድ ትክክለኛነት
- **የመሳሪያ ማንነት:** ኦፕሬቲንግ ሲስተም፣ አሳሽ እና የመሳሪያ አይነት

---

## ⚙️ የስርዓት አርክቴክቸር

| ንብርብር | ቴክኖሎጂ | ማብራሪያ |
|--------|-----------|----------|
| **ክሪፕቶግራፊ** | SHA-256 & SHA-512 | ድርብ ንብርብር ማጠቃለያ |
| **ዳታ ቤዝ** | Supabase (PostgreSQL) | JSONB + RLS policies |
| **የፎረንሲክ ዳታ** | ipapi.co API | IP/ቦታ/ጊዜ ሶስትዮሽ |
| **Rendering** | html2canvas + jsPDF | Client-side PNG/PDF |
| **Frontend** | Vanilla JavaScript | ዜሮ framework dependency |
| **ደህንነት** | Client-side hashing | ፋይል ወደ ሰርቨር አይጫንም |

---

## 🗺️ የጎዳና ካርታ

### ፋዝ 1: Beta v1.0 (አሁን)
- Cloud Database (Supabase)
- Off-chain registry
- Gallery self-attestation

### ፋዝ 2: Decentralized Authority (2026 Q2-Q4)
- Edge Function INSERT
- Wallet ፊርማ (Solana)
- IPFS/Arweave Backup
- OpenTimestamps

### ፋዝ 3: ሙሉ መብዛት ያልሆነ (2027+)
- On-Chain Registry (Solana)
- Multi-Chain Support
- DID Integration
- በቱርክ ፍርድ ቤቶች ተቀባይነት

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

## 🔬 ቴክኒካዊ ጥልቀት: ማሸጊያ አልጎሪዝም

```javascript
// Deterministic Hash ተግባራት
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// FileHash ስሌት
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// EvidenceRoot መፍጠር
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = 
    "file_sha512:" + fileHash512 + "\n" +
    "forensics:" + JSON.stringify(forensicsData);
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// NotarySeal ማምረት
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = 
    "evidence_root:" + evidenceRoot + "\n" +
    "signer_sig:" + signerSignature + "\n" +
    "timestamp:" + timestamp;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// ማስክ ማድረጊያ
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
    return { valid: true, message: "✅ ኦሪጂናል" };
  } else {
    return { valid: false, message: "❌ ሀሰተኛ" };
  }
}
```

### Full Verify
```javascript
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  const cert = await fetchFromRegistry(certificateId);

  // FileHash ቁጥጥር
  if (userFileHash !== cert.asset.fingerprints.sha512) {
    return { valid: false, message: "❌ ፋይል hash አይዛመድም" };
  }

  // EvidenceRoot እንደገና ማመንጨት
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ EvidenceRoot አይመሳሰልም" };
  }

  // NotarySeal እንደገና ማመንጨት
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ NotarySeal አይመሳሰልም" };
  }

  return { valid: true, message: "✅ Full Verify አለፈ" };
}
```

---

## 📊 የተፎካካሪ ትንተና

| ባህሪ | **PoArt** | OpenTimestamps | Verisart | OriginStamp |
|---------|:---------:|:---------------:|:---------:|:-----------:|
| **ወጪ** | 🆓 ነጻ | 🆓 | 💰 ክፍያ | ⚠️ Freemium |
| **Drag & Drop UI** | ✅ | ❌ CLI | ⚠️ | ⚠️ |
| **Privacy Controls** | ✅ 3 ሁነታ | ❌ | ❌ | ❌ |
| **Client-Side Hash** | ✅ | ✅ | ❌ | ⚠️ |
| **Forensic Metadata** | ✅ ሙሉ | ❌ | ❌ | ⚠️ |
| **አማርኛ ድጋፍ** | ✅ | ❌ | ❌ | ❌ |
| **ክፍት ምንጭ** | ✅ GitHub | ✅ | ❌ | ⚠️ |

---

## 🌍 ማህበረሰብ እና ድጋፍ

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **ድር:** [ilhanart.org](https://ilhanart.org)
- **ኢሜይል:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 አስተዋጽኦ

**አስተዋጽኦ ለማድረግ:**
1. Fork ያድርጉ
2. Feature branch ይፍጠሩ
3. Commit ያድርጉ
4. Push ያድርጉ
5. Pull Request ይክፈቱ

### የእርዳታ ጥሪ

* **Supabase Edge Functions**
* **Solana Web3.js**
* **IPFS / Arweave**
* **Community Tools**

---

## 💬 የመጨረሻ ማስታወሻዎች

### Pump.fun እና እውነታ

ይህ ፕሮጀክት በPump.fun ላይ ተጀምሯል ምክንያቱም:
- ✅ የLiquidity መዳረሻ
- ✅ ያለ ማህበረሰብ መዳረሻ
- ✅ ዝቅተኛ የጅምር ወጪ

**ሆኖም:**
- **Token ዋጋ** የጥበብ ስኬት አመልካች አይደለም
- **የስኬት ልኬቶች:** Authenticated artworks + community engagement + አካላዊ ጎብኚ

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // ባህል፣ ከካፒታል ይበልጣል*

## 🧾 ፍቃድ

MIT License © 2026 İlhan Art Gallery Initiative

---

## 💬 ክሬዲቶች

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) 
![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) 
![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) 
![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**ይህ ፕሮጀክት [İlhan Art Gallery] ተነሳሽነት ጋር የተገነባ ሲሆን፣ የምንጭ ኮዶች ለግልጽነት ለሕዝብ ክፍት ናቸው።**

**ፕሮቶኮል V1.0 // በSHA-512 ታሽጓል።**

*© 2026 İLHAN ART | የስራዎች፣ ምስሎች እና ሀሳቦች ሁሉም መብቶች የተጠበቁ ናቸው።*

---
- ሙሉ ግልጽነት ለማረጋገጫ

---

## 📈 የአጠቃቀም ስታቲስቲክስ (2026 Q1 ግቦች)

| ልኬት | ግብ | ሁኔታ |
|--------|-------|-------|
| **ጠቅላላ ሰርተፊኬት** | 1,000 | 🔄 በሂደት ላይ |
| **ንቁ ተጠቃሚ** | 500 | 🔄 በሂደት ላይ |
| **የማረጋገጫ ቁጥር** | 5,000 | 🔄 በሂደት ላይ |
| **Uptime** | %99.9 | ✅ ንቁ |
| **Avg Response Time** | <200ms | ✅ ተስማሚ |

---

## 🏛️ የ"Engine" ፅንሰ-ሀሳብ አስፈላጊነት

Pump.fun ወይም ተመሳሳይ መድረኮች ከሚወጡ token-ዎች ብዙዎቹ ብዙ ጊዜ **"የመዳረሻ ቲኬት"** ብቻ ናቸው። **PoArt Forensic Engine (PFE)** ግን ያ ቲኬት የትኞቹን መብቶች እንደሚጠብቅ፣ ጉልበት እንዴት እንደሚመዘገብ እና ስነ-ጥበብ/ሳይንስ/ቴክኖሎጂ እንዴት ዘላቂ እንደሚሆን የሚወስነው **ህገ መንግስታዊ ሎጂክ ንብርብር** ነው።

> **ማስታወሻ:** ይህን ፕሮጀክት በPump.fun ላይ የጀመርነው በቂ ሊኩዊዲቲ እና በቂ ተከታዮች ስላልነበረን ነው። ያለውን ዳታ መጠቀም ስልታዊ እንደ ምርጥ ባይሆንም ትክክለኛው እርምጃ ነበር ማለት እንችላለን። ከበጀት እና ግብዓቶች ውጪ የዚህን ሞተር ሎጂክ በGitHub ላይ መግለጽ፣ ፕሮጀክቱ የፋይናንስ ግምት ብቻ ሳይሆን የረጅም ጊዜ **የሶፍትዌር መሰረተ ልማት** እና **ዲጂታል ብሔራዊ ቤተ መጻሕፍት** ራዕይ መሆኑን ያረጋግጣል።

---

## 🎯 ድምዳሜ: ዋጋ በማስረጃ መቆለፍ (Proof-Bound Value)

ይህ ቲዎረም፣ የ[PoArt] ዋጋ ጥያቄን ከ"ውዴታ" ወይም "የገበያ ትረካ" አውጥቶ **ሊረጋገጥ በሚችል የማምረት እውነታ** ላይ ይሰኩታል።

### ዋና ነጥቦች

1. **ያለ ሂደት ዋጋ አይፈጠርም:**  
   AI፣ በፈጣን ውጤት (\$t \to 0\$) ሂደቱን ያጠፋል። የሂደት መስኮት ሲጠብ የintegral ውጤት በሂሳብ አስፈላጊነት ይቀንሳል።

2. **ፈቃድ እና አደጋ ማባዛት ነው:**  
   [PoArt]፣ "የወጣውን ጊዜ" ብቻ ሳይሆን፤ በዚያ ጊዜ ውስጥ ያለውን እውነተኛ ውሳኔ፣ አደጋ እና ዋጋ ንብርብርንም ይለካል።

3. **ልዩነት፣ ግብይት ሳይሆን አካላዊ ማስረጃ ነው:**  
   በአካላዊ ማምረት የማይመለሱ ምልክቶች (የጣላ ድብደባ፣ የእብነበረድ ስብራት)፣ በዲጂታሉ Ctrl+Z ሎጂክ ውጪ ናቸው።

> **🔐 ማጠቃለያ:** በAI ዘመን ያልተለመደው "ምስል" ሳይሆን፤ **ሊረጋገጥ የሚችል ጉልበት፣ ጊዜ እና ፈቃድ** ነው። [PoArt]፣ ይህን እጥረት ይለካል እና በ**Evidence Pack** ይመዘግባል።

---

## 📊 ተጨማሪ የተፎካካሪ ትንተና

### የተፎካካሪዎች ጉድለቶች፣ የPoArt ጥንካሬዎች

| ጉድለት | ተፎካካሪዎች | PoArt |
|------|----------|-------|
| **የአጠቃቀም ችግር** | CLI፣ API እውቀት፣ ቦርሳ ያስፈልጋል | ጎትት-ጣል፣ በ3 ጠቅታ ይጠናቀቃል |
| **የወጪ መሰናክል** | \$50-500/ወር ምዝገባ | %100 ነጻ |
| **ግላዊነት** | ፋይል ወደ ሰርቨር ይጫናል | Client-side፣ ፋይል ፈጽሞ አይሄድም |
| **Forensic ዳታ** | Timestamp ብቻ | IP፣ ቦታ፣ መሳሪያ፣ ጊዜ - ሁሉም |
| **አማርኛ ድጋፍ** | የለም ወይም በጣም የተገደበ | Native ቋንቋ ድጋፍ |
| **ክፍት ምንጭ** | ዝግ ሳጥን | በGitHub ላይ ሁሉም ኮድ ክፍት |

---

## 🔄 Token Governance Evolution

### v1.0 (2026)
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (ማዕከላዊ ግን ግልጽ)
- Governance: Advisory only (ባህል ጠባቂ የመጨረሻ ውሳኔ)
- Token utility: Gallery access + registry + NFT priority

### v2.0 (2027)
- Registry: On-chain (Solana)
- Signatures: Wallet-based (decentralized)
- Governance: Hybrid (community advisory + curatorial quality)
- Token utility: Enhanced features + advanced access

### v3.0+ (2028+)
- Full community governance (optional)
- ባህል ጠባቂ quality control ሁልጊዜ ይጠበቃል
- Multi-chain support ሙሉ በሙሉ

---

## 🛡️ የአጠቃቀም ቦታዎች እና ጥቅም ዝርዝር

አርቲስት፣ ጸሐፊ ወይም ዲዛይነር ከሆናችሁ፣ "ይህን ቀድሜ ሰርቻለሁ" ማለት በቂ አይደለም፣ ማረጋገጥ ያስፈልጋችኋል።

**በPoArt ያሸጋችሁት ስራ:**

- **የሂሳብ ማስረጃ:** የፋይላችሁ አንድ ፒክሰል እንኳ ቢቀየር ስርዓቱ ይረዳዋል። ማጭበርበር የማይቻል ነው።
- **ህጋዊ መሰረት:** ስራው በየትኛው ቀን፣ በየትኛው ከተማ፣ ከየትኛው መሳሪያ እንዳሸገ ተመዝግቧል።
- **ፈጣን ሰርተፊኬት:** በሰኮንዶች ውስጥ ልዩ የሆነ፣ QR ኮድ ያለው እና የታሸገ **"የንብረት ማንነት ሰርተፊኬት"** ያመነጫል።

---

## 📝 Canonical Encoding ዝርዝር

### v1.0 Canonicalization መስፈርት

- **ቋሚ ሜዳ ቅደም ተከተል:** ip_masked → location → device → timestamp
- **Encoding:** UTF-8
- **Delimiter:** `\n` (newline)

### ፋዝ 2 እቅድ

RFC 8785 (JCS - JSON Canonicalization Scheme) ጋር canonical JSON-ን መቀየር።

---

## 🎨 ባህላዊ አውድ

### "ባህል ከካፒታል ይበልጣል" ፍልስፍና

ይህ ፕሮጀክት በ"Culture > Capital" ፍልስፍና ላይ የተመሰረተ ነው። ይህ ማለት:

1. **የረጅም ጊዜ አስተሳሰብ:** ከ2025 እስከ 3000 CE ያለው 975-ዓመት ራዕይ
2. **ፀረ-ግምት መርህ:** Token ዋጋን ከማሳደግ ይልቅ ባህላዊ ዋጋን ማስቀደም
3. **ማህበረሰብ ተኮር:** Mercenary capital ሳይሆን የረጅም ጊዜ ተሳታፊዎች

### የኢትዮጵያ ባህል እና PoArt

የኢትዮጵያ ባህል በሺዎች ዓመታት የሚቆጠር የስነ-ጥበብ ቅርስ አለው። PoArt ይህን ቅርስ ለመጠበቅ እና ለማስተላለፍ ዘመናዊ ቴክኖሎጂ ይሰጣል:

- **ጥንታዊ ስነ-ጥበብ:** የLalibela አብያተ ክርስቲያናት፣ የአክሱም ሀውልቶች
- **ዘመናዊ ስነ-ጥበብ:** የኢትዮጵያ ሠዓሊዎች እና ቅርጻ ቅርጾች
- **ዲጂታል ማህደር:** ለወደፊት ትውልዶች የማይጠፋ መዝገብ

---

## 🌐 ዓለም አቀፍ ተደራሽነት

### የቋንቋ ድጋፍ

PoArt ፕሮቶኮል በብዙ ቋንቋዎች ይገኛል:

- 🇹🇷 Türkçe (ዋና)
- 🇬🇧 English
- 🇪🇸 Español
- 🇨🇳 中文
- 🇫🇷 Français
- 🇩🇪 Deutsch
- 🇷🇺 Русский
- 🇮🇹 Italiano
- 🇵🇱 Polski
- 🇰🇷 한국어
- 🇮🇩 Bahasa Indonesia
- 🇻🇳 Tiếng Việt
- 🇹🇭 ไทย
- 🇱🇦 ລາວ
- 🇳🇱 Nederlands
- 🇪🇹 አማርኛ (ይህ ሰነድ)

### ለምን ብዙ ቋንቋ?

PoArt ለዓለም አቀፍ የስነ-ጥበብ ማህበረሰብ የተነደፈ ነው። ማንም አርቲስት፣ በየትኛውም ቦታ፣ ስራውን መጠበቅ መቻል አለበት።

---

## 🔗 አስፈላጊ ሊንኮች

### ኦፊሴላዊ

- **ድር:** [ilhanart.org](https://ilhanart.org)
- **Registry:** [ilhanart.org/public-registry](https://ilhanart.org/public-registry)
- **GitHub:** [github.com/galeri-coder](https://github.com/galeri-coder)

### ማህበራዊ ሚዲያ

- **Twitter/X:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Instagram:** [ilhanartgaleri](https://instagram.com/ilhanartgaleri)

### ግንኙነት

- **ኢሜይል:** galeri@ilhanart.org

---

## ⚠️ አስፈላጊ ማስጠንቀቂያዎች

1. **Token ዋጋ:** Token ዋጋ የስነ-ጥበብ ጥራት አመልካች አይደለም
2. **የኢንቨስትመንት ምክር አይደለም:** ይህ ሰነድ የኢንቨስትመንት ምክር አይደለም
3. **Beta ስሪት:** ስርዓቱ አሁንም በልማት ላይ ነው
4. **ሃላፊነት:** ተጠቃሚዎች የራሳቸውን ምርምር ማድረግ አለባቸው

---

## 📜 የመጨረሻ ቃላት

> **"ባህል፣ ከካፒታል ይበልጣል።"**

ይህ ፕሮቶኮል የስነ-ጥበብን ዋጋ ከግምት ወደ ማስረጃ ለመቀየር የተነደፈ ነው። በAI ዘመን፣ የሰው ጉልበት፣ ጊዜ እና ፈቃድ ማረጋገጥ አስፈላጊ ሆኗል።

[PoArt] ይህን ችግር ይፈታል - **ሊረጋገጥ በሚችል ማስረጃ**።

---

**ፕሮቶኮል V1.0**  
**በSHA-512 ታሽጓል**  
**© 2026 İLHAN ART**  
**ሁሉም መብቶች የተጠበቁ ናቸው**

---

---

## 📖 ተጨማሪ ማብራሪያዎች

### የማረጋገጫ ስርዓት ዝርዝር

#### Quick Verify ሂደት

1. ተጠቃሚ ፋይል ያስገባል
2. Client-side SHA-512 hash ይሰላል
3. Registry ከተመዘገበው hash ጋር ይነጻጸራል
4. ውጤት ይመለሳል: ✅ ኦሪጂናል ወይም ❌ ሀሰተኛ

#### Full Verify ሂደት

1. Quick Verify ይሰራል
2. EvidenceRoot እንደገና ይሰላል
3. NotarySeal እንደገና ይሰላል
4. ሁሉም ዋጋዎች ይነጻጸራሉ
5. ሙሉ ማረጋገጫ ውጤት ይመለሳል

### የForensics ዳታ ዝርዝር

| ሜዳ | ትርጓሜ | ምሳሌ |
|------|---------|-------|
| ip_masked | የተደበቀ IP | 88.241.*.** |
| location | ቦታ | Istanbul/TR ወይም ***/TR |
| device | መሳሪያ | Brave (Windows) |
| timestamp | ጊዜ | 2026-01-09T12:34:56.000Z |

### Hash Algorithm ምርጫ

**ለምን SHA-512?**

1. **ደህንነት:** 512-bit output ከፍተኛ ደህንነት ይሰጣል
2. **Collision Resistance:** ሁለት የተለያዩ ፋይሎች ተመሳሳይ hash ማግኘት ፈጽሞ የማይቻል ነው
3. **ፍጥነት:** ዘመናዊ ኮምፒውተሮች ላይ በፍጥነት ይሰራል
4. **መስፈርት:** ዓለም አቀፍ ተቀባይነት ያለው algorithm

---

## 🧪 ቴክኒካዊ ዝርዝሮች

### Supabase Configuration

```sql
-- RLS Policy ምሳሌ
CREATE POLICY "Public read for public records"
ON certificates
FOR SELECT
USING (visibility = 'public');

-- Index ለፈጣን ፍለጋ
CREATE INDEX idx_certificates_hash 
ON certificates(asset_fingerprints_sha512);
```

### API Endpoints (ፋዝ 3)

| Endpoint | Method | ዓላማ |
|----------|--------|------|
| /verify/quick | POST | ፈጣን ማረጋገጫ |
| /verify/full | POST | ሙሉ ማረጋገጫ |
| /certificate/{id} | GET | ሰርተፊኬት ማግኘት |
| /registry/search | GET | Registry ፍለጋ |

---

## 📋 Checklist ለአርቲስቶች

### PoArt Verified ለማግኘት

- [ ] Evidence Pack ዝግጅት
  - [ ] RAW ቪዲዮ መዝገቦች
  - [ ] Metadata ሰነዶች
  - [ ] የቀጥታ ስርጭት ሊንኮች
- [ ] 5 PoArt መስፈርቶች ማሟላት
  - [ ] Live Identity Proof
  - [ ] Labor & Process Proof
  - [ ] Aesthetic Value Proof
  - [ ] Conceptual Novelty
  - [ ] Non-Algorithmic Agency
- [ ] ማመልከቻ ማስገባት
- [ ] 30 ቀን መጠበቅ
- [ ] ውሳኔ መቀበል

### የ365 ቀን ማደስ

- [ ] አዲስ ስራ ማዘጋጀት
- [ ] Evidence Pack ማዘመን
- [ ] ማመልከቻ ማስገባት
- [ ] Badge ማደስ

---

## 🌟 ምስጋና

ይህ ፕሮጀክት ለሚከተሉት ምስጋና ይደርሳል:

- **İlhan Art Gallery** - ለራዕይ እና አመራር
- **ክፍት ምንጭ ማህበረሰብ** - ለአስተዋጽኦ
- **የኢትዮጵያ አርቲስቶች** - ለመነሳሳት
- **ዓለም አቀፍ የስነ-ጥበብ ማህበረሰብ** - ለድጋፍ

---

## 📞 ድጋፍ

ጥያቄ ወይም ችግር ካለዎት:

1. **GitHub Issues:** ቴክኒካዊ ችግሮች
2. **ኢሜይል:** ለአጠቃላይ ጥያቄዎች
3. **Twitter DM:** ለፈጣን ምላሽ

---

## 🔄 Version History

| Version | ቀን | ለውጦች |
|---------|------|--------|
| v1.0-beta | 2026-01 | የመጀመሪያ ስሪት |
| v1.1 | TBD | Bug fixes |
| v2.0 | 2026-Q4 | Wallet integration |
| v3.0 | 2027-Q1 | On-chain registry |

---

## 📄 ፍቃድ ሙሉ ጽሁፍ

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
**ባህል፣ ከካፒታል ይበልጣል**

*ይህ ሰነድ ከቱርክኛ ምንጭ ወደ አማርኛ ተተርጉሟል።*  
*ሁሉም ቴክኒካዊ ዝርዝሮች፣ ኮዶች፣ JSON፣ LaTeX እና markdown ተጠብቀዋል።*

---
