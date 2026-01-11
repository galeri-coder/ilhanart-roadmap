# 📚 ဝေါဟာရနှင့် အယူအဆများ အဘိဓာန်
> **"ဤပရိုတိုကော၏ ဘာသာစကားကို နားလည်ခြင်းသည် ၎င်း၏ အမြင်ကို နားလည်ခြင်းဖြစ်သည်"**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: အဓိက အခြေခံအဆောက်အအုံ

**PoArt Forensic Engine (PFE)** သည် [PoArt] ပရိုတိုကော၏ နောက်ကွယ်ရှိ အဓိက ယုတ္တိဗေဒနှင့် နည်းပညာဆိုင်ရာ လုပ်ဆောင်ချက်များကို ကိုယ်စားပြုသော အဓိက အလွှာဖြစ်သည်။ ၎င်းသည် အနုပညာလက်ရာ၏ မူရင်းထုတ်လုပ်မှုဒေတာကို လက်ခံပြီး အတည်ပြုနိုင်ပြီး ပြောင်းလဲ၍မရသော **ဒစ်ဂျစ်တယ် သက်သေအထောက်အထား** အဖြစ် ပြောင်းလဲပေးသည့် "forensic engine" တစ်ခုဖြစ်သည်။

### 🧩 အဘယ်ကြောင့် "PoArt Forensic" ဟုခေါ်သနည်း။

- **PoArt (Proof of Art - အနုပညာသက်သေ):** Engine ၏ အဓိကအာရုံမှာ ဒစ်ဂျစ်တယ်ပိုင်ဆိုင်မှု၏ တန်ဖိုးကို ရောင်းဝယ်ဖောက်ကားမှုနှင့် မချိတ်ဆက်ဘဲ **သက်သေပြနိုင်သော ထုတ်လုပ်မှုလုပ်ငန်းစဉ်** နှင့် ချိတ်ဆက်ခြင်းဖြစ်သည်
- **Forensic (မှုခင်းစုံစမ်းစစ်ဆေးမှု):**
  - **နည်းပညာဆိုင်ရာ အဓိပ္ပာယ်:** ထုတ်လုပ်မှုလုပ်ငန်းစဉ်နှင့်သက်ဆိုင်သော ဒေတာ (စုတ်ချက်များ၊ timelapse၊ logs) များကို ပြုပြင်ပြောင်းလဲခြင်းမရှိကြောင်း အတည်ပြုရန် ရည်ရွယ်သော algorithm များနှင့် record chain ချဉ်းကပ်နည်း
  - **ဒဿနိကအလွှာ:** ထုတ်လုပ်မှုတွင် **အချိန်၊ ကြိုးစားအားထုတ်မှုနှင့် လူသား၏ ဆုံးဖြတ်ချက်ကုန်ကျစရိတ်** ကို တိုင်းတာနိုင်သော လက်တွေ့အဖြစ် ပြောင်းလဲရန် တောင်းဆိုချက်၊ AI ၏ "ချက်ချင်းရလဒ်" နှင့် ဆန့်ကျင်ဘက်

> မှတ်ချက်: Blockchain ပေါင်းစည်းမှု (ဥပမာ Solana) ကို အတည်ပြုခြင်း/registry အတွက် သီးခြား **Chain Anchor Layer** အဖြစ် ကိုင်တွယ်မည်ဖြစ်ပြီး PFE ၏ အဓိကအစိတ်အပိုင်းမဟုတ်ပါ

### 🛠️ နည်းပညာဆိုင်ရာ နယ်ပယ် v1.0

**PoArt Forensic Engine (PFE) v1.0** ကို ရှုပ်ထွေးသော ဘဏ္ဍာရေးပုံစံအစား **မဏ္ဍိုင် ၃ ခု** ပေါ်တွင် တည်ဆောက်ထားသည်:

1. **Hashing & Sealing (တံဆိပ်ခတ်ခြင်း):**  
   PFE သည် Evidence Pack ရှိ အစိတ်အပိုင်းအားလုံး (လက်ရာဖိုင်၊ ဗီဒီယို၊ JSON/log၊ လက်မှတ် စသည်) ကို deterministic ပုံစံဖြင့် လုပ်ဆောင်ပြီး ထူးခြားသော **NotarySeal** တန်ဖိုးကို ထုတ်လုပ်သည်။

   **အဓိက အယူအဆများ (v1.0):**
   - **FileHash (လက်ရာလက်ဗွေ):** လက်ရာဖိုင်၏ bytes မှ ထုတ်လုပ်သော hash
   - **EvidenceRoot (သက်သေအထောက်အထားအစုံ၏ အမြစ်):** Evidence Pack ၏ ခိုင်မာမှုကို ကိုယ်စားပြုသော root summary (Merkle root သို့မဟုတ် canonical manifest hash)
   - **NotarySeal (နောက်ဆုံးတံဆိပ် / PFE Output):** EvidenceRoot + အချိန် + လက်မှတ် ပေါင်းစပ်မှုမှ ထုတ်လုပ်သော နောက်ဆုံးတံဆိပ်

   **ဖော်မြူလာ (ရင်းနှီးမြှုပ်နှံသူများအတွက် ရှင်းလင်းစွာပြသထားသည်):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload အဓိပ္ပာယ်ဖွင့်ဆိုချက် (v1.0):**
   
   - **EvidenceRootPayload:**
   ```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
   ```
   
   - **NotarySealPayload:**
   ```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
   ```
   
   > မှတ်ချက်: PFE output အဖြစ် ရည်ညွှန်းသော တန်ဖိုးမှာ **NotarySeal** ဖြစ်သည်။ **SignerSignature** ယန္တရားကို Phase 2 (Solana Wallet Adapter နှင့်အတူ) တွင် အသက်သွင်းမည်ဖြစ်သည်။ လက်ရှိ v1.0 တွင် system ၏ ကိုယ်ပိုင် attestation signature ကို အသုံးပြုသည်။ Attestation public key ကို registry ရှိ `issuer.attestation_pubkey` field တွင် ထုတ်ဝေမည်ဖြစ်သည်

2. **Indexing (မှတ်တမ်းတင်ခြင်း):**  
   မည်သည့် wallet က မည်သည့်နေ့တွင် မည်သည့်လက်ရာအတွက် **Labor Proof (အလုပ်သက်သေ)** ကို ပွင့်လင်းပြီး ရှာဖွေနိုင်သော record layer သို့ တင်သွင်းကြောင်း မှတ်တမ်းတင်သည်။  
   *(ဤအလွှာသည် database ဖြစ်နိုင်သည်။ chain integration ကို "Chain Anchor Layer" အဖြစ် သီးခြားသတ်မှတ်မည်)*

3. **Verification (အတည်ပြုခြင်း):**  
   လက်ရာ၏ မူရင်းဖြစ်မှုကို မေးခွန်းထုတ်သောအခါ PFE သည် မူရင်းသက်သေကို ပြန်လည်လုပ်ဆောင်သည်။ တွက်ချက်ထားသော **EvidenceRoot / NotarySeal** တန်ဖိုးသည် archive ရှိ record နှင့် ကိုက်ညီမှုရှိမရှိကို သင်္ချာဆိုင်ရာ သေချာမှုဖြင့် စမ်းသပ်သည်။

---

### 🧮 PoArt တန်ဖိုးသီအိုရမ် (The Value Theorem)

[PoArt] ပရိုတိုကောသည် ဒစ်ဂျစ်တယ်ပိုင်ဆိုင်မှု၏ တန်ဖိုး ($V$) ကို ပုဂ္ဂလိကစျေးကွက်အမြင်နှင့် မချိတ်ဆက်ဘဲ **ထုတ်လုပ်မှုလုပ်ငန်းစဉ်၏ ရုပ်ပိုင်းဆိုင်ရာအမှန်တရား** နှင့် ချိတ်ဆက်သည်။

AI သည် ချက်ချင်းရလဒ် ($t \to 0$) ပေးခြင်းဖြင့် လုပ်ငန်းစဉ်ကို ဖျက်ဆီးသည်။ [PoArt] သည် တန်ဖိုးကို **အချိန်၊ အလုပ်နှင့် ဆန္ဒ** အစိတ်အပိုင်းများ၏ စုဆောင်းမှုအဖြစ် သတ်မှတ်သည်။

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### ကိန်းရှင်များ၏ အဓိပ္ပာယ်ဖွင့်ဆိုချက်

- **$\int dt$ (လုပ်ငန်းစဉ်စုဆောင်းမှု):**  
  တန်ဖိုးသည် ချက်ချင်း "ရလဒ်" မဟုတ်ပါ။ ၎င်းသည် $t_{\text{start}}$ နှင့် $t_{\text{end}}$ အကြား စုဆောင်းသော **လုပ်ငန်းစဉ်** ဖြစ်သည်။ ကြာချိန်လျော့သောအခါ (AI ထုတ်လုပ်မှု) integral ရလဒ်သည် 0 သို့ ချဉ်းကပ်သည်။

- **$P_{\text{labor}}(t)$ (ချက်ချင်းအလုပ်စွမ်းအား):**  
  ထုတ်လုပ်မှုကာလအတွင်း အသုံးပြုသော စိတ်ပိုင်းဆိုင်ရာနှင့် ရုပ်ပိုင်းဆိုင်ရာ ကြိုးစားအားထုတ်မှု ပြင်းထန်မှုကို ကိုယ်စားပြုသည်။ သက်သေပြနိုင်သော ကြိုးစားမှု တိုးလာသောအခါ integrand ကြီးထွားသည်။  
  > မှတ်ချက်: လက်တွေ့တွင် ဤအချက်ကို "တိုင်းတာနိုင်သော/သက်သေပြနိုင်သော အလုပ်အချက်ပြမှုများ" မှတစ်ဆင့် normalize လုပ်နိုင်သည်

- **$I_{\text{agency}}(t)$ (ဆန္ဒကိန်းဆ):**  
  ထုတ်လုပ်သူ၏ အန္တရာယ်ယူနိုင်မှုနှင့် ဆုံးဖြတ်ချက်ချနိုင်မှု စွမ်းရည်။ $0$ နှင့် $1$ အကြား တန်ဖိုးယူသည်။
  - **AI ($I \approx 0$):** ညွှန်ကြားချက်လုပ်ဆောင်သည်၊ အန္တရာယ်မယူ၊ ကုန်ကျစရိတ်မပေး
  - **လူသား ($I \to 1$):** ဆုံးဖြတ်ချက်ပြောင်းလဲသည်၊ ဆွံ့ဆိုင်းသည်၊ အန္တရာယ်ယူသည်

- **$U_{\text{irreversible}}$ (ပြန်လှည့်၍မရသော ထူးခြားမှု):**  
  ဒစ်ဂျစ်တယ်ထုတ်လုပ်မှုတွင် ပြန်လှည့်ခြင်း (`Ctrl+Z`) ဖြစ်နိုင်သော်လည်း ရုပ်ပိုင်းဆိုင်ရာထုတ်လုပ်မှုတွင် ပြန်လမ်းမရှိပါ (canvas ပေါ်သုတ်သော ဆေးရောင်၊ ထွင်းထားသော ကျောက်ဖြူ၊ live broadcast တွင် ကိုယ်ဟန်အမူအရာ)။ ဤ **ပြန်လှည့်၍မရနိုင်မှု** သည် လက်ရာတွင် "ထူးခြားမှု" (non-fungible characteristic) ကို ဖန်တီးသော ထပ်ဆောင်းအချက်ဖြစ်သည်။

### 🔎 Case ခွဲခြမ်းစိတ်ဖြာမှု: AI "ချက်ချင်းရလဒ်" vs. လူသား "သက်သေပြနိုင်သောလုပ်ငန်းစဉ်"

အောက်ပါအခြေအနေများသည် **PoArt တန်ဖိုးသီအိုရမ်** လက်တွေ့တွင် မည်သို့အလုပ်လုပ်ကြောင်းနှင့် AI ထုတ်လုပ်မှုသည် [PoArt] စံနှုန်းတွင် အဘယ်ကြောင့် အမှတ်နည်းကြောင်း ပြသသည်။

#### အခြေအနေ A: စက္ကန့် ၁၀ အတွင်း AI ပုံထုတ်လုပ်မှု

- **ကြာချိန် ($\Delta t$):** $10$ စက္ကန့် (လုပ်ငန်းစဉ်မရှိသလောက်)
- **အလုပ်စွမ်းအား ($P_{\text{labor}}$):** $1$ ယူနစ် (ညွှန်ကြားချက်ရိုက်ထည့်ရုံသာ)
- **ဆန္ဒကိန်းဆ ($I_{\text{agency}}$):** $0.01$ (အန္တရာယ်မရှိ၊ ကုန်ကျစရိတ်မရှိ)
- **ပြန်လှည့်၍မရနိုင်မှု ($U_{\text{irreversible}}$):** $0$ (ပြန်လှည့်နိုင်/ကူးယူနိုင်)

**ရလဒ်:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **မှတ်ချက်:** ရလဒ်ပြည့်စုံသော်လည်း လုပ်ငန်းစဉ်မရှိခြင်းနှင့် ဆန္ဒ/အန္တရာယ်မရှိခြင်းကြောင့် [PoArt] တန်ဖိုးသည် $0$ သို့ ချဉ်းကပ်သည်။

#### အခြေအနေ B: Live Broadcast တွင် နာရီ ၆ ကြာ ရုပ်ပိုင်းဆိုင်ရာ ဖန်တီးမှု

- **ကြာချိန် ($\Delta t$):** $6$ နာရီ ($21{,}600$ စက္ကန့်)
- **အလုပ်စွမ်းအား ($P_{\text{labor}}$):** $0.5$ ယူနစ် (ရုပ်ပိုင်းဆိုင်ရာနှင့် စိတ်ပိုင်းဆိုင်ရာ ကြိုးစားမှု အဆက်မပြတ်)
- **ဆန္ဒကိန်းဆ ($I_{\text{agency}}$):** $0.9$ (ဆုံးဖြတ်ချက်ပြောင်းလဲမှု၊ အန္တရာယ်ယူမှု၊ ပြန်လှည့်၍မရသော ရွေးချယ်မှုများ)
- **ပြန်လှည့်၍မရနိုင်မှု ($U_{\text{irreversible}}$):** $>0$ (ရုပ်ပိုင်းဆိုင်ရာ ခြေရာများ ပြန်လှည့်၍မရ)

**ရလဒ်:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **မှတ်ချက်:** လုပ်ငန်းစဉ်ရှည်လာပြီး ဆန္ဒ (အန္တရာယ်) တိုးလာသောအခါ စုဆောင်းတန်ဖိုး တိုးလာသည်။ $U_{\text{irreversible}}$ အချက်သည် လက်ရာတွင် "ထူးခြားမှု" (non-fungible characteristic) ကို ဖန်တီးသော ထပ်ဆောင်းပံ့ပိုးမှုဖြစ်သည်။

---

### ✅ နိဂုံး: သက်သေချိတ်ဆက်တန်ဖိုး (Proof-Bound Value)

ဤသီအိုရမ်သည် [PoArt] ၏ တန်ဖိုးတောင်းဆိုမှုကို "နှစ်သက်မှု" သို့မဟုတ် "စျေးကွက်ဇာတ်လမ်း" အစား **သက်သေပြနိုင်သော ထုတ်လုပ်မှုအမှန်တရား** နှင့် ချိတ်ဆက်သည်။

1. **လုပ်ငန်းစဉ်မရှိလျှင် တန်ဖိုးမရှိ:**  
   AI သည် ချက်ချင်းရလဒ် ($t \to 0$) ဖြင့် လုပ်ငန်းစဉ်ကို ဖျက်ဆီးသည်။ လုပ်ငန်းစဉ်ဝင်းဒိုး ကျဉ်းလာသောအခါ integral ရလဒ်သည် သင်္ချာအရ သေးငယ်လာသည်:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **ဆန္ဒနှင့် အန္တရာယ်သည် မြှောက်ကိန်းများဖြစ်သည်:**  
   [PoArt] သည် "အသုံးပြုသောအချိန်" သာမက ထိုကာလအတွင်း အမှန်တကယ် ဆုံးဖြတ်ချက်များ၊ အန္တရာယ်များနှင့် ကုန်ကျစရိတ်အလွှာများကိုပါ တိုင်းတာသည်။ အန္တရာယ်မယူသော ထုတ်လုပ်မှု (AI) ၏ တန်ဖိုးနည်းသည်:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **ထူးခြားမှုသည် ရုပ်ပိုင်းဆိုင်ရာသက်သေဖြစ်သည်၊ စျေးကွက်ရေးမဟုတ်:**  
   ရုပ်ပိုင်းဆိုင်ရာထုတ်လုပ်မှုတွင် ပြန်လှည့်၍မရသော ခြေရာများ (canvas ပေါ် စုတ်ချက်၊ ကျောက်ဖြူအက်ကွဲခြင်း) သည် ဒစ်ဂျစ်တယ် `Ctrl+Z` ယုတ္တိဗေဒကို ကျော်လွန်သည်။ ဤ ပြန်လှည့်၍မရနိုင်မှု ($U_{\text{irreversible}}$) သည် လက်ရာကို ontologically ထူးခြားစေသည်။

> **🔐 အကျဉ်းချုပ်:** တန်ဖိုးသီအိုရမ်သည် တိုင်းတာမှုအရ မသေချာဟု ထင်နိုင်သော်လည်း (လက်တွေ့ဘဝတွင်ပင် ၁၀၀% တိုင်းတာ၍မရ) ဤဖော်မြူလာ၏ ရည်ရွယ်ချက်မှာ ကိန်းရှင်များ၏ ဖွဲ့စည်းပုံနှင့် ဦးတည်ချက်ကို ပြသခြင်းဖြစ်သည်။ AI ခေတ်တွင် ရှားပါးသည်မှာ "ပုံ" မဟုတ်ပါ။ **သက်သေပြနိုင်သော အလုပ်၊ အချိန်နှင့် ဆန္ဒ** ဖြစ်သည်။ [PoArt] သည် ဤရှားပါးမှုကို တိုင်းတာပြီး **Evidence Pack** ဖြင့် မှတ်ပုံတင်သည်။

### 🏛️ "Engine" အယူအဆ၏ အရေးပါမှု

Pump.fun သို့မဟုတ် အလားတူပလက်ဖောင်းများမှ ထုတ်ဝေသော token များသည် မကြာခဏ **"ဝင်ခွင့်လက်မှတ်"** သာဖြစ်သည်။ **PoArt Forensic Engine (PFE)** သည် ထိုလက်မှတ်က မည်သည့်အခွင့်အရေးများကို ကာကွယ်ကြောင်း၊ အလုပ်ကို မည်သို့မှတ်တမ်းတင်ကြောင်းနှင့် အနုပညာ/သိပ္ပံ/နည်းပညာကို မည်သို့အမြဲတမ်းထားရှိကြောင်း သတ်မှတ်သော **ဖွဲ့စည်းပုံယုတ္တိဗေဒအလွှာ** ဖြစ်သည်။

> **မှတ်ချက်:** Pumpfun တွင် ဤပရောဂျက်ကို စတင်ရသည့်အကြောင်းရင်းမှာ ကျွန်ုပ်တို့တွင် လုံလောက်သော liquidity နှင့် follower များမရှိခြင်းကြောင့်ဖြစ်သည်။ ရှိပြီးသားဒေတာကို အသုံးပြုခြင်းသည် အရည်အသွေးအမြင့်ဆုံး မဟာဗျူဟာမဟုတ်နိုင်သော်လည်း budget နှင့် resource မည်မျှပင်ရှိစေ အမှန်ကန်ဆုံးလှုပ်ရှားမှုဖြစ်ကြောင်း ပြောနိုင်သည်။ ဤ engine ၏ ယုတ္တိဗေဒကို GitHub တွင် သတ်မှတ်ခြင်းသည် ပရောဂျက်သည် ငွေကြေးရောင်းဝယ်ဖောက်ကားမှုသာမက ရေရှည် **software infrastructure** နှင့် **အမျိုးသားဒစ်ဂျစ်တယ်စာကြည့်တိုက်** အမြင်ဖြစ်ကြောင်း သက်သေပြသည်။

---

## 🎨 [PoArt] အလုပ်သက်သေ ပရိုတိုကော (Proof of Art Protocol v1.0)

> **"တကယ့်အနုပညာရှင်၊ တကယ့်ထုတ်လုပ်မှု၊ တကယ့်တန်ဖိုး"**

ဤပရိုတိုကောသည် crypto ecosystem ကို ဖြည့်နေသော အမည်ဝှက်လိမ်လည်သူများ၊ မိနစ် ၅ အတွင်း ထုတ်လုပ်သော AI ပုံများနှင့် "Pump & Dump" (တင်ပြီးချ) ယဉ်ကျေးမှုကို တန်ပြန်ရန် ဖွံ့ဖြိုးထားသော **ဇီဝနှင့် ဥာဏ်ရည်ဆိုင်ရာ ကာကွယ်ရေးယန္တရား** ဖြစ်သည်။

---

## a) [PoArt] ဆိုသည်မှာ အဘယ်နည်း။ (ဒဿနိကနှင့် နည်းပညာဆိုင်ရာ အဓိပ္ပာယ်ဖွင့်ဆိုချက်)

**Proof of Art [PoArt]:** သည် blockchain ပေါ်ရှိ ပိုင်ဆိုင်မှု၏ နောက်ကွယ်တန်ဖိုးသည် ရောင်းဝယ်ဖောက်ကားမှုမဟုတ်ဘဲ အတည်ပြုနိုင်သော **လူသားအလုပ်**၊ **အချိန်**နှင့် **ရုပ်ပိုင်းဆိုင်ရာစွမ်းအင်** အပေါ် မူတည်ကြောင်း အာမခံသော အဖွဲ့အစည်းဆိုင်ရာ အတည်ပြုမှုစံနှုန်းဖြစ်သည်။

Bitcoin သည် *"လျှပ်စစ်စွမ်းအင်နှင့် လုပ်ဆောင်မှုစွမ်းအား"* **(Proof of Work)** ဖြင့် တန်ဖိုးဖန်တီးသကဲ့သို့ [PoArt] နှင့် ကိုက်ညီသော ပရောဂျက်များသည် *"အနုပညာစွမ်းရည်နှင့် လူသားအချိန်"* ဖြင့် တန်ဖိုးဖန်တီးသည်။

၎င်းသည် Pump.fun နှင့် DEX platform များတွင် *"Dev (developer) ရောင်းသွားသည်၊ ပရောဂျက်ပြီးသွားသည်"* အန္တရာယ်ကို ဖယ်ရှားသည်။ ဤနေရာတွင် တန်ဖိုးကို code တွင်မဟုတ်ဘဲ **ထုတ်လုပ်မှု အဆက်မပြတ်မှု** တွင် သိမ်းဆည်းထားသည်။

> **[PoArt] သည် ပါဝင်သူများကို "ကျွန်ုပ်တို့ကို ယုံကြည်ပါ" မပြောပါ။ "ဤသည်မှာ သက်သေဖြစ်သည်၊ မင်းမျက်လုံးနဲ့ ကြည့်၊ မင်းသင်္ချာနဲ့ အတည်ပြုပါ" ဟု ပြောသည်**

---

## b) [PoArt] ၏ စံနှုန်း ၅ ချက် (The 5 Pillars of Truth)

ဤ ၅ ချက်သည် [PoArt] တံဆိပ်ရရန် ပရောဂျက်သည် ဖြတ်သန်းရမည့် ကိုင်တွယ်၍မရသော စစ်ထုတ်စနစ်များဖြစ်သည်။

### 1) Live အထောက်အထားသက်သေ (Live Identity Proof)

- **ပြဿနာ:** Crypto လောကသည် ငွေစုပြီး ပရောဂျက်ကိုစွန့်ခွာသွားသော အမည်ဝှက်တည်ထောင်သူများ (Devs) ဖြင့် ပြည့်နှက်နေသည်
- **[PoArt] အဖြေ:** ထုတ်လုပ်သူသည် ID ကဒ်သာမက **ထုတ်လုပ်မှုကာလအတွင်း ၎င်းတို့၏ တည်ရှိမှု** ကိုလည်း သက်သေပြသည်။ ၎င်းတွင် အသိုက်အဝန်းနှင့် အပြန်အလှန်ဆက်ဆံပြီး သီးခြားတောင်းဆိုမှုများကို ချက်ချင်းတုံ့ပြန်သော live broadcast session များပါဝင်သည်၊ ကြိုတင်ရိုက်ကူးထားသော ဗီဒီယိုမဟုတ်ပါ။  
  (ဥပမာ: *"canvas ၏ ညာဘက်ထောင့်တွင် ယနေ့ရက်စွဲနှင့် လက်ရှိ block number ကို ရေးပါ"*)
- **ဆောင်ပုဒ်:** *"Bot သည် ပုံဆွဲနိုင်သည်၊ သို့သော် bot သည် ချွေးမထွက်ပြီး improvise လုပ်၍မရ"*

### 2) အလုပ်နှင့် လုပ်ငန်းစဉ် သက်သေ (Labor & Process Proof)

- **ပြဿနာ:** စက္ကန့် ၂ အတွင်း ထုတ်လုပ်သော AI ပုံများကို ဒစ်ဂျစ်တယ်လောကတွင် လ ၂ ကြာဆွဲသော ဆီဆေးပန်းချီနှင့် တူညီသော "jpeg" အဖြစ် သဘောထားသည်
- **[PoArt] အဖြေ:** လက်ရာ၏ "ပဋိသန္ဓေယူပြီး မွေးဖွားခြင်း" လုပ်ငန်းစဉ်ကို မှတ်တမ်းတင်သည်။ Sketch အဆင့်များ၊ အရောင်အလွှာများ၊ ကုန်ဆုံးသော စုဆောင်းနာရီများနှင့် အနုပညာရှင်သည် ဖန်တီးနေစဉ် ကြုံတွေ့သော ရုပ်ပိုင်းဆိုင်ရာလုပ်ငန်းစဉ်ကို မှတ်တမ်းတင်သည်။ ၎င်းသည် token သို့ **"Time Cost" (အချိန်ကုန်ကျစရိတ်)** ထည့်သွင်းသည်။ ပိုင်ဆိုင်မှုထုတ်လုပ်ရန် ပိုခက်ခဲလေ တန်ဖိုးပိုခိုင်မာလေဖြစ်သည်။

### 3) အလှအပတန်ဖိုး သက်သေ (Aesthetic Value Proof)

- **ပြဿနာ:** Aesthetics နှင့် အနုပညာအနက်ကို လျစ်လျူရှုပြီး ချက်ချင်းဟာသသာ အာရုံစိုက်သော "Meme" ယဉ်ကျေးမှုနှင့် ရလဒ်အဖြစ် တိုတောင်းသော "Hype" ပရောဂျက်များ
- **[PoArt] အဖြေ:** ပရောဂျက်သည် ပညာရေးဆိုင်ရာ အနုပညာစံနှုန်းများ၊ အရောင်သီအိုရီ၊ ဖွဲ့စည်းပုံစည်းမျဉ်းများနှင့် ပစ္စည်းဗဟုသုတ (Impasto၊ Texture စသည်) ရှိရမည်။ အကြောင်းအရာသည် ရယ်စရာသာမကဘဲ ပရိသတ်ကို အထင်ကြီးစေပြီး **စုဆောင်းတန်ဖိုး** ရှိရမည်။

### 4) အယူအဆဆိုင်ရာ ဆန်းသစ်မှု (Conceptual Novelty)

- **ပြဿနာ:** တစ်ခုနှင့်တစ်ခု ကူးယူသော ဖန်တီးရည်မရှိသော dog/cat coin ထောင်ပေါင်းများစွာ
- **[PoArt] အဖြေ:** ပရောဂျက်သည် အနုပညာ၊ သိပ္ပံ၊ ဒဿန သို့မဟုတ် နည်းပညာကို အဓိပ္ပာယ်ရှိသော ဖွဲ့စည်းပုံဖြင့် ပေါင်းစပ်သော တံတားအသစ်များ တည်ဆောက်ရမည်။  
  (ဥပမာ: ဂန္တဝင် David ရုပ်တုကို crypto market data နှင့် ပေါင်းစပ်ခြင်း၊ လူသားအမြင်၏ "ကျောက်ဖြစ်ခြင်း" အယူအဆဖြင့် လုပ်ဆောင်ပြီး သိပ္ပံဆိုင်ရာ အရင်းအမြစ်များဖြင့် ထောက်ပံ့နိုင်ခြင်း)  
  လက်ရာသည် visual feast သာမကဘဲ **သိပ္ပံ၊ ဒဿန သို့မဟုတ် နည်းပညာ** အကြောင်း စဉ်းစားမှုကို နှိုးဆွသော ဥာဏ်ရည်ဆိုင်ရာ စိန်ခေါ်မှုလည်း ဖြစ်ရမည်။

> [!IMPORTANT]
> **ကိုးကားနမူနာ (Las Palmitas Effect):** မက္ကဆီကိုရှိ ရာဇဝတ်မှုနှင့် တိုက်ပွဲဝင်နေသော Las Palmitas ရပ်ကွက်တွင် အိမ် ၂၀၀ ကျော်ကို ကြီးမားသော သက်တံရောင်ပွဲတော်အဖြစ် ပြောင်းလဲခဲ့သည်။ ဤ aesthetic ဝင်ရောက်စွက်ဖက်မှု၏ ရလဒ်အဖြစ် ရပ်ကွက်၏ ရာဇဝတ်မှုနှုန်း အတိုင်းအတာတစ်ခုအထိ ကျဆင်းခဲ့ပြီး လူငယ်များသည် ဂိုဏ်းများအစား အနုပညာကို စိတ်ဝင်စားလာခဲ့သည်။ Aesthetic ပြောင်းလဲမှုသည် လူများ၏ ပတ်ဝန်းကျင်နှင့် တစ်ဦးချင်းအပေါ် လေးစားမှု (Social Cohesion) ကို ပြန်လည်ကုဒ်ထုတ်ခဲ့သည်။
>
> **မျှော်လင့်ချက်:** [PoArt] တွင် စာရင်းသွင်းမည့် ပရောဂျက်များသည် အထက်ပါနမူနာကဲ့သို့ visual aesthetics သက်သက်ထက် ကျော်လွန်သော လူမှုဗေဒ၊ သိပ္ပံ သို့မဟုတ် ဒဿနဆိုင်ရာ အကြောင်းအကျိုး ဆက်စပ်မှုရှိရမည်။ ငွေဖြင့် မဝယ်နိုင်သော တစ်ခုတည်းသော ပိုင်ဆိုင်မှုမှာ "အချိန်" ဖြစ်သောကြောင့် အချိန်ကို ဤပရိုတိုကောတွင် အာမခံအဖြစ် stake ထားပြီး သက်သေပြရမည်။ ပရောဂျက်၏ conceptual foundation သည် လာမည့်နှစ်များတွင် ဖြစ်နိုင်သော CTO (Community Take Over) အခြေအနေတွင် အသိုက်အဝန်းသည် ဤအမွေအနှစ်ကို ဆက်ခံပြီး ပရောဂျက်၏ ဆန်းသစ်မှု အလားအလာကို လွတ်လပ်စွာ ဆက်လက်လုပ်ဆောင်နိုင်လောက်အောင် ခိုင်မာပြီး universal ဖြစ်ရမည်။

### 5) Algorithm မဟုတ်သော ဆန္ဒ (Non-Algorithmic Agency)

- **ပြဿနာ:** ပြည့်စုံသော်လည်း ဝိညာဉ်မဲ့၊ ထပ်ခါတလဲလဲ ဒစ်ဂျစ်တယ်ထုတ်လုပ်မှု
- **[PoArt] အဖြေ:** မှားနိုင်သော၊ အန္တရာယ်ယူနိုင်သောနှင့် စိတ်ခံစားမှု အတက်အကျကြုံနိုင်သော လူသား၏ ထူးခြားသော ဆန္ဒကို လက်ရာတွင် ခံစားရရမည်။ စုတ်ချက်တွင် မသေချာမှု၊ ပစ္စည်း၏ မမျှော်လင့်သော တုံ့ပြန်မှုနှင့် အနုပညာရှင်၏ ချက်ချင်းဆုံးဖြတ်ချက်များသည် လက်ရာကို "စက်ထုတ်လုပ်မှု" မှ ခွဲခြားသော **ဇီဝလက်မှတ်** ဖြစ်သည်။

---

## c) အတည်ပြုခြင်းနှင့် အတုဆန့်ကျင်ယန္တရား

ဤစနစ်သည် ပရောဂျက်ကို "အစတွင်" သာမက "အမြဲတမ်း" ယုံကြည်စိတ်ချရပြီး အသက်ရှင်နေစေကြောင်း အာမခံသည်။

### 📦 သက်သေအထောက်အထား Pack (Evidence Pack - The Digital Twin)

[PoArt] အသိအမှတ်ပြု လက်ရာတိုင်း၏ နောက်ကွယ်တွင် ရင်းနှီးမြှုပ်နှံသူများ download လုပ်နိုင်သော encrypted နှင့် timestamp ပါသော ဒေတာအစု ရှိသည်:

- **RAW ဗီဒီယို ရိုက်ကူးမှု:** ထုတ်လုပ်မှုကာလ၏ မပြတ်မလပ် raw footage
- **Metadata ခွဲခြမ်းစိတ်ဖြာမှု:** ဖိုင်ဖန်တီးရက်စွဲ၊ အသုံးပြုသော device အချက်အလက်နှင့် တည်နေရာဒေတာ
- **ရုပ်ပိုင်းဆိုင်ရာ ကိုးကား:** လက်ရာသည် ရုပ်ပိုင်းဆိုင်ရာလောကတွင် ရှိကြောင်း သက်သေ  
  (ဥပမာ: လက်ရာဘေးရှိ ယနေ့သတင်းစာ သို့မဟုတ် ထိုအချိန်က blockchain data)

> *အညီညွတ်မှု မှတ်ချက်:* "evidence pack" ဖော်ပြချက်သည် ယခင်အပိုင်းရှိ **Evidence Pack → EvidenceRoot → NotarySeal** chain နှင့် ချိတ်ဆက်သည်။ ဆိုလိုသည်မှာ set ၏ ခိုင်မာမှုကို အတည်ပြုနိုင်သော တံဆိပ်ဖြင့် ကိုယ်စားပြုသည်။

### 🔄 ရက် ၃၆၅ သက်တမ်းတိုး (The Sustainability Protocol)

- **တော်လှန်ရေးဆန်သော အင်္ဂါရပ်:** Crypto ပရောဂျက်များတွင် "Dev" (developer) သည် token ကို စျေးကွက်သို့ မိတ်ဆက်ပြီး လ ၁-၂ အကြာ ပျောက်ကွယ်သွားလေ့ရှိသည် (Soft Rug)။ [PoArt] သည် ၎င်းကို မဖြစ်နိုင်အောင် လုပ်သည်။
- **စည်းမျဉ်း:** "Verified Artist" (အတည်ပြုပြီး အနုပညာရှင်) အဆင့်သည် တစ်သက်တာမဟုတ်ပါ။ **၁ နှစ်** သာ အကျုံးဝင်သည်။
- **အကောင်အထည်ဖော်မှု:** အနုပညာရှင်/developer သည် ရက် ၃၆၅ တိုင်း အသိုက်အဝန်းသို့ **အသစ်၊ ကြီးမားပြီး သက်သေပြနိုင်သော လက်ရာ** တင်ပြရမည်။
- **နမူနာအခြေအနေ:** သင်သည် 2026 တွင် ပရောဂျက်စတင်သည်။ 2027 ဇန်နဝါရီတွင် စနစ်သည် "Proof Period Expired" သတိပေးမည်။ အနုပညာရှင်သည် ပြပွဲအသစ်၊ ရုပ်ပိုင်းဆိုင်ရာ လက်ရာအသစ် သို့မဟုတ် နည်းပညာပေါင်းစည်းမှုအသစ် မတင်ပြပါက ပရောဂျက်၏ "Trust Badge" ကျဆင်းမည်။
- **ရလဒ်:** ဤစနစ်သည် **အကြောင်းအရာ မည်သည့်အခါမှ မဟောင်းနွမ်း** ကြောင်းနှင့် ရင်းနှီးမြှုပ်နှံသူများ *"Dev ရှိသေးလား?"* ကြောက်ရွံ့မှု မကြုံရကြောင်း အာမခံသည်။ ပရောဂျက်သည် အသက်ရှင်နေသော studio ဖြစ်လာသည်။

### 🚩 အနီရောင်အလံ ပရိုတိုကော (Red Flag Protocol)

**အသိုက်အဝန်း သို့မဟုတ် algorithm မှ စစ်ဆေးတွေ့ရှိသော အတုပြုလုပ်မှု (AI အသုံးပြုခြင်း၊ ခိုးယူထားသော လက်ရာ၊ ပြုပြင်ထားသော ဗီဒီယို) တစ်ခုခုရှိပါက:**

1. လက်မှတ်ကို ချက်ချင်း **"VOID" (ပျက်ပြယ်)** အဖြစ် အမှတ်အသားပြုသည်
2. Evidence pack ကို **"အတု"** အဖြစ် အများသိ label တပ်သည်
3. ပရောဂျက်ကို [PoArt] blacklist သို့ ထည့်သည်။ ၎င်းသည် decentralized လောကတွင် **ဂုဏ်သတင်းသည် တစ်ခုတည်းသော ငွေကြေး** ဖြစ်သည်ဟူသော အချက်ကို အားဖြည့်သည်။

---

## d) နိဂုံး: ပြတိုက်၊ ကာစီနိုမဟုတ်

**Pump.fun နှင့် Decentralized Exchanges (DEX) များသည် ယခုအခါ ဝမ်းနည်းစရာကောင်းစွာ ကာစီနိုများဖြစ်နေသည်။ မီးတောက်များလက်နေသည်၊ လူတိုင်း အမြန်အမြတ်ကို လိုက်စားနေသည်၊ banker (လိမ်လည်သူ) အမြဲနိုင်သည်။ ဤနေရာတွင် ပရောဂျက်စတင်ရသည့် အကြောင်းရင်းမှာ ကျွန်ုပ်တို့တွင် live broadcast မှတစ်ဆင့် ရှိပြီးသား ပရိသတ်ထံ ရောက်ရှိရန် လုံလောက်သော budget နှင့် network မရှိသောကြောင့်ဖြစ်သည်။**

**[PoArt] သည် ဤကာစီနိုအလယ်တွင် တည်ဆောက်ထားသော ခံတပ်ဖြစ်သည်။**

- 🎰 ကာစီနိုသည် ဖဲဂိမ်းကို အားကိုးသည်။ ကျွန်ုပ်တို့သည် **ရုပ်ပိုင်းဆိုင်ရာ အမှန်တရားကို အားကိုးသည်**
- 🃏 ကာစီနိုသည် လိမ်လည်မှုအတွက် ဖွင့်ထားသည်။ ကျွန်ုပ်တို့သည် **ပွင့်လင်းသော သက်သေအတွက် ဖွင့်ထားသည်**
- ⏳ ကာစီနိုသည် ယာယီဖြစ်သည်။ ကျွန်ုပ်တို့သည် **အနုပညာနှင့် သိပ္ပံ၏ ထာဝရဖြစ်မှုကို အာရုံစိုက်သည်**

**ဤပရိုတိုကောကို အသုံးပြုသော token သည် "coin" သာမဟုတ်ပါ။ ၎င်းသည် နောက်ကွယ်တွင် ချွေး၊ ဆေးရောင်၊ code နှင့် ဒဿန ရှိသော ဒစ်ဂျစ်တယ် share ဖြစ်သည်။**

---

## 🗳️ 6) စီမံခန့်ခွဲမှုနှင့် အများပြည်သူ မှတ်ပုံတင် (Governance & Public Registry)

**ဤအပိုင်း၏ ရည်ရွယ်ချက်မှာ: [PoArt] စံနှုန်းကို "တစ်ဦးချင်း ယုံကြည်မှု" အဆင့်မှ မှတ်တမ်းတင်ခြင်း + အတည်ပြုခြင်း + အသိုက်အဝန်းစီမံခန့်ခွဲမှုဖြင့် ရေရှည်တည်တံ့သော အများပြည်သူ အခြေခံအဆောက်အအုံသို့ ပြောင်းလဲခြင်းဖြစ်သည်။**

### 6.1 Public Registry (အများပြည်သူ မှတ်ပုံတင်)

- **Public Registry:** အတည်ပြုပြီး ဒေတာအားလုံးကို `ilhanart.org/registry` (သို့မဟုတ် GitHub Registry) တွင် မှတ်တမ်းတင်သည်

**မှတ်တမ်းယုတ္တိဗေဒ (အကြံပြုထားသော စံနှုန်း - JSON path format):**

registry သို့ ဝင်ရောက်သော record တိုင်းတွင် ဤအနည်းဆုံး အတည်ပြုနိုင်သော အဓိက field များ ရှိသည်:

- **အထောက်အထားနှင့် အခြေအနေ:**
  - `certificate_id` (ဖတ်နိုင်သော ကိုးကား)
  - `status` (active / void)
  - `void_reason` (ရှိပါက)
  - `visibility` (private / masked / public)
  - `created_at` (timestamp)

- **ထုတ်ပေးသည့် အဖွဲ့အစည်း:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **လက်ရာ ဒေတာ:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (ဖြစ်နိုင်ပါက၊ token-gated identity အတွက်)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Forensic ဒေတာ:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Cryptographic သက်သေ:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **စီမံခန့်ခွဲမှု:**
  - `governance.decision`
  - `governance.veto_threshold`

Registry တွင် အလွှာ ၂ ခု ရှိနိုင်သည်:
- **1)** Human-readable index (web listing / ရှာဖွေမှု / filter)
- **2)** Machine-readable manifest (JSON record၊ PFE verification အတွက်)

**ဤနေရာရှိ "record" ကို PFE ၏ Evidence Pack → EvidenceRoot → NotarySeal chain ဖြင့် အတည်ပြုနိုင်သည်။ Registry သည် verification target ပေးသည်၊ "claim" မဟုတ်ပါ။**

---

### 6.2 40% အသိုက်အဝန်း ဗီတို (Token-Gated Governance)

- **40% အသိုက်အဝန်း ဗီတို:** အဆင့်ရရှိခြင်းမတိုင်မီ တစ်လအလိုတွင် မဲပေးခြင်းစတင်သည်။ **Token-Gated (Solana-Verified)** အသိုက်အဝန်း၏ 40% ကန့်ကွက်မှုသည် လျှောက်လွှာကို ပျက်ပြယ်စေမည်။

**မဲပေးအဆင့်များ (အကြံပြုထားသော ရှင်းလင်းသော လုပ်ငန်းစဉ်):**
- **လျှောက်လွှာ Window:** ကိုယ်စားလှယ်လောင်း ပရောဂျက်သည် "PoArt Candidate Registration" ဖွင့်သည် (candidate record သည် "pending" status တွင် ပေါ်လာသည်)
- **ပြန်လည်သုံးသပ်ကာလ:** အသိုက်အဝန်းအတွက် သက်သေကို ပြန်လည်သုံးသပ်ရန် ရက် ၃၀ (Evidence Pack + live broadcast record + metadata)
- **Token-gated Verification:** မဲပေးခြင်းကို Solana တွင် verified wallet မှတစ်ဆင့် ပြုလုပ်သည် (ဥပမာ သီးခြား token/NFT ကိုင်ဆောင်မှု + wallet signature)
- **ဗီတို စည်းမျဉ်း:** မဲ၏ 40% သည် **ကန့်ကွက် (NO / VETO)** ဖြစ်ပါက လျှောက်လွှာကို ငြင်းပယ်သည်
- **ပွင့်လင်းမြင်သာမှု:** မဲပေးရလဒ်များကို registry တွင် "decision record" အဖြစ် သိမ်းဆည်းသည် (ရက်စွဲ၊ အချိုး၊ snapshot ID)

---

### 6.3 Metadata Sync (ရုပ်ပိုင်းဆိုင်ရာလောကနှင့် ကိုက်ညီမှု)

- **Metadata Sync:** Registry ရှိ နည်းပညာဆိုင်ရာ ဒေတာသည် ရုပ်ပိုင်းဆိုင်ရာ ပိုင်ဆိုင်မှုနှင့် 100% ကိုက်ညီရမည်။

**"100% ကိုက်ညီမှု" ၏ နည်းပညာဆိုင်ရာ အဓိပ္ပာယ်ဖွင့်ဆိုချက် (အကြံပြုထားသော ရှင်းလင်းမှု):**
- **အနည်းဆုံး ကိုက်ညီမှု (မဖြစ်မနေ):**
  - Registry ရှိ `asset.fingerprints.sha256/sha512` သည် ရှိပြီးသားဖိုင်၏ hash နှင့် **အတိအကျ တူညီ** ရမည်
  - Registry ရှိ `proof.notary_seal` သည် ပြန်လည်ဖန်တီးသောအခါ **အတိအကျ တူညီ** ရမည် (Evidence Pack ရှိပါက)
- **ရုပ်ပိုင်းဆိုင်ရာ ကိုးကား ကိုက်ညီမှု (သက်သေ အမျိုးအစား):**
  - ရုပ်ပိုင်းဆိုင်ရာ လက်ရာ + live broadcast တွင် ပြသထားသော ရက်စွဲ/block ကိုးကား ကဲ့သို့သော သက်သေသည် Evidence Pack နှင့် ကိုက်ညီရမည်
- **Privacy လိုက်နာမှု:**
  - `masked` visibility ရှိ IP/location ကဲ့သို့သော field များကို **masking standard အတိုင်း** ထုတ်ဝေသည်

---

### 6.4 အငြင်းပွားမှု၊ ပြန်လည်သုံးသပ်မှုနှင့် ပယ်ဖျက်မှု (Dispute & Revocation)

Registry သည် "အတည်ပြုခြင်း" ယန္တရားသာမဟုတ်ပါ။ ၎င်းသည် **အတုဆန့်ကျင် အသက်ရှင်သော verification ယန္တရား** ဖြစ်သည်။

- အငြင်းပွားမှု စတင်သောအခါ record ကို **"review"** mode တွင် ထားနိုင်သည်
- အတုပြုလုပ်မှု စစ်ဆေးတွေ့ရှိပါက `status: void` အဖြစ် အမှတ်အသားပြုပြီး အကြောင်းပြချက် ထည့်သည်:
  - `void_reason` (AI အသုံးပြုခြင်း / ခိုးယူခြင်း / ပြုပြင်ခြင်း စသည်)
  - `revoked_at` (ပယ်ဖျက်အချိန်)
- ပယ်ဖျက်ဆုံးဖြတ်ချက်၏ အရင်းအမြစ် registry တွင် ရှင်းရှင်းလင်းလင်း ပေါ်သည်:
  - အသိုက်အဝန်း မဲပေးခြင်း / authorized panel / forensic examination record (အသုံးပြုသည့်အတိုင်း)

> **ဤအပိုင်းသည် registry ပေါ်ရှိ "Red Flag Protocol" အပိုင်းရှိ VOID အယူအဆ၏ အတွဲဖြစ်သည်။**

---

### 6.5 Registry Record နမူနာ (Machine-Readable)

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

> *မှတ်ချက်: `asset.fingerprints.sha512` နှင့် အခြား hash တန်ဖိုးများကို ပြသရန် အတွက် အတိုချုံးထားသည်။ အမှန်တကယ် အသုံးပြုမှုတွင် hexadecimal character string အပြည့်အဝကို အသုံးပြုသည်*

---

## 7) 🔐 နည်းပညာဆိုင်ရာ တံဆိပ် (NOTARY SEAL)

**PoArt Forensic Engine (PFE) v1.0** မှ ထုတ်လုပ်သော မယိမ်းယိုင်နိုင်သော တံဆိပ် algorithm:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] ဒစ်ဂျစ်တယ် Notary နှင့် Forensic သက်သေ ပရိုတိုကော (Beta v1.0)

> **"ယဉ်ကျေးမှုသည် အရင်းအနှီးထက် ကြီးမြတ်သည်။ သင်၏လက်ရာကို ယနေ့မှစ၍ ကာကွယ်ပါ၊ မနက်ဖြန်သို့ ယူဆောင်သွားပါ"**

---

## အဘယ်ကြောင့် အများပြည်သူသို့ ထုတ်ဖော်သနည်း။

တကယ့်လုံခြုံရေးသည် ပွင့်လင်းမြင်သာမှုမှ လာသည်။ ကျွန်ုပ်တို့၏ **Public Registry (အများပြည်သူ မှတ်ပုံတင်)** စနစ်ဖြင့် ကမ္ဘာပေါ်ရှိ မည်သူမဆို မည်သည့်နေရာမှမဆို မည်သည့် authority ကိုမှ မအားကိုးဘဲ ၎င်းတို့တွင်ရှိသော ဖိုင်သည် မူရင်းဟုတ်မဟုတ် စက္ကန့်ပိုင်းအတွင်း အတည်ပြုနိုင်သည်။

---

## 🧩 အဘယ်ကြောင့် "Visibility Module" များစွာ ရှိသနည်း။

ဤသည်မှာ code ၏ အရေးကြီးဆုံး အစိတ်အပိုင်းဖြစ်သည် (visibility select menu)။ ဤရွေးချယ်မှုများသည် အသုံးပြုသူများကို **"privacy vs. transparency"** ကို ချိန်ခွင်ညှိနိုင်စေသည်:

### 🔒 သီးသန့် (Private)

- **အခြေအနေ:** အနုပညာရှင်သည် လက်ရာကို ထုတ်ဝေလိုခြင်းမရှိသေးသော်လည်း timestamp ထုတ်ပြီး "ဤနေ့တွင် ဤအရာကို ကျွန်ုပ်လုပ်ခဲ့သည်" ဟု သက်သေပြလိုသည်
- **Code က ဘာလုပ်သနည်း:** ဒေတာကို database သို့ ရေးပြီး `visibility: "private"` label ကပ်သည်။ နောက်မှ "Public Read" policy ရေးသောအခါ `WHERE visibility = 'public'` ဖြင့် ဤ record များကို အများပြည်သူမှ ဝှက်ထားနိုင်သည်

### 🕶️ ဖုံးကွယ်ထား (Masked)

- **အခြေအနေ:** အနုပညာရှင်သည် ပွင့်လင်းမြင်သာမှုလိုချင်သော်လည်း အိမ်လိပ်စာ (IP location) တွေ့ရှိခံရမည်ကို စိုးရိမ်သည်
- **Code က ဘာလုပ်သနည်း:** `maskIP` နှင့် `maskLoc` function များသည် JavaScript ဘက်တွင် အလုပ်လုပ်ပြီး IP address ကို `88.241.***.***` format သို့ပြောင်းသည်၊ location ကို `***/TR` format သို့ပြောင်းပြီး censored version ကို database သို့ ပို့သည်
- **Privacy မှတ်ချက်:** Masking ကို browser တွင် လုပ်ဆောင်သည်။ Supabase သည် အမှန်တကယ် location ကို မမြင်ပါ။ **သို့သော်:** location data အတွက် ipapi.co ကဲ့သို့သော third-party API အသုံးပြုပါက ဤ provider များသည် request ပြုလုပ်စဉ် IP address ကို မြင်မည်
- **Masked mode တွင် တံဆိပ်ခတ်ခြင်း:** EvidenceRoot နှင့် NotarySeal တွက်ချက်မှုကို masked forensics data ဖြင့် လုပ်ဆောင်သည်။ ထို့ကြောင့် verification သည် deterministic အတိုင်း ရှိနေသည်

### 🌍 အပြည့်အဝ ထုတ်ဖော် (Public)

- **အခြေအနေ:** အပြည့်အဝ ပွင့်လင်းမြင်သာမှု။ [PoArt] စံနှုန်းအတိုင်း လက်ရာကို မည်သည့်နေရာ၊ မည်သည့်အချိန်နှင့် မည်သည့် network မှ ထုတ်လုပ်ကြောင်း ရှင်းလင်းစွာ ကြေညာသည်။

---

## 💡 နည်းပညာဆိုင်ရာ ဆန်းသစ်မှု

PoArt သည် ဖိုင် upload စနစ်သာမဟုတ်ပါ။ ၎င်းသည် နည်းပညာ အလွှာ ၃ ခုကို တစ်အိုးတည်းတွင် ပေါင်းစပ်ပြီး စံနှုန်းအသစ်များ ယူဆောင်လာသော **"Forensic Chain of Custody" (Forensic သက်သေ ထိန်းသိမ်းမှု chain)** engine ဖြစ်သည်။

**ဤအပိုင်းတွင် "engine" အဖြစ် ဖော်ပြထားသော အလွှာသည် ယခင် terminology ရှိ PoArt Forensic Engine (PFE) core နှင့် သက်ဆိုင်သည်။**

### 1) Client-Side Hashing (အမြင့်ဆုံး Privacy)

သင်၏ လက်ရာဖိုင်ကို server သို့ မည်သည့်အခါမှ upload မလုပ်ပါ။ Browser (Client-side) တွင် run သော ကျွန်ုပ်တို့၏ engine သည် သင်၏ ကိုယ်ပိုင်ကွန်ပျူတာတွင် ဖိုင်၏ hash (digital summary) ကို တွက်ချက်သည်။ Fingerprint နှင့် metadata သာ server သို့ ပို့သည်။

> **Privacy မှတ်ချက်:** လက်ရာဖိုင်ကို server သို့ upload မလုပ်ဘဲ ဤနည်းဖြင့် ကာကွယ်ထားသည်။ သို့သော် forensics data (IP/location) ကို ရွေးချယ်ထားသော visibility mode (private/masked/public) အတိုင်း share ပြုလုပ်သည်။

### 2) Forensic Data Fusion (Forensic စွမ်းအား)

၎င်းသည် သာမန် timestamp ထက် များစွာ ကျော်လွန်သည်။ စနစ်သည် အောက်ပါ data များကို တစ်ခုတည်းသော "Genesis Seal" တွင် ပေါင်းစပ်သည်:

- **Digital Summary (SHA-512):** လက်ရာ၏ pixel တစ်ခုပင် ပြောင်းလဲပါက ပျက်စီးမည့် digital fingerprint၊ cryptographic summary standard (SHA-512) အသုံးပြုသည်
- **တည်နေရာနှင့် အချိန်:** millisecond တိကျမှုရှိသော ရက်စွဲ၊ လုပ်ဆောင်မှုပြုလုပ်သော နိုင်ငံ၊ မြို့နှင့် ခရိုင်
- **Device Identity:** Operating system၊ browser နှင့် device အမျိုးအစား (User-Agent analysis)

---

## 🛡️ အသုံးပြုမှု Cases နှင့် အကျိုးကျေးဇူးများ

သင်သည် အနုပညာရှင်၊ စာရေးဆရာ သို့မဟုတ် designer ဖြစ်ပါက "ဤအရာကို ကျွန်ုပ်အရင်လုပ်ခဲ့သည်" ဟုပြောခြင်းသည် မလုံလောက်ပါ။ သက်သေပြရမည်။

**PoArt ဖြင့် တံဆိပ်ခတ်ထားသော သင်၏လက်ရာ:**

- **သင်္ချာဆိုင်ရာ သက်သေ:** သင်၏ဖိုင်၏ pixel တစ်ခုပင် ပြောင်းလဲပါက စနစ်က စစ်ဆေးတွေ့ရှိမည်။ ပြုပြင်ပြောင်းလဲခြင်း မဖြစ်နိုင်ပါ။
- **ဥပဒေဆိုင်ရာ အခြေခံ:** လက်ရာကို တံဆိပ်ခတ်သော ရက်စွဲ၊ မြို့နှင့် device ကို မှတ်တမ်းတင်ထားသည်။
- **ချက်ချင်း လက်မှတ်:** QR code နှင့် သင့်အတွက် ထူးခြားသော တံဆိပ်ပါဝင်သော **"Asset Identity Certificate"** ကို စက္ကန့်ပိုင်းအတွင်း ထုတ်လုပ်သည်။

---

## ⚙️ System Architecture နှင့် Technical Specifications

System ကို high performance နှင့် scalability အပေါ် အာရုံစိုက်၍ "Serverless" (server မဲ့) architecture ပေါ်တွင် ဒီဇိုင်းထုတ်ထားသည်။

| Layer | Technology | ဖော်ပြချက် |
|-------|------------|------------|
| **Cryptography** | SHA-256 & SHA-512 | အလွှာနှစ်ထပ် cryptographic summary |
| **Database** | Supabase (PostgreSQL) | JSONB data structure၊ RLS policies |
| **Forensic Data** | ipapi.co API | IP/location/time သုံးဆ |
| **Rendering** | html2canvas + jsPDF | Client-side PNG/PDF ထုတ်လုပ်မှု |
| **Frontend** | Vanilla JavaScript | Framework dependency မရှိ |
| **Security** | Client-side hashing | ဖိုင်ကို server သို့ မည်သည့်အခါမှ upload မလုပ် |

### ထင်ရှားသော Features

| Feature | အသေးစိတ် | ပြိုင်ဘက်များတွင် ရှိသလား? |
|---------|----------|--------------------------|
| **Drag & Drop UI** | ဖိုင်ဆွဲချ၊ ချက်ချင်း preview | ❌ အများစုမရှိ |
| **Multi-Format Export** | PNG၊ JSON၊ PDF - click တစ်ချက် | ⚠️ ကန့်သတ် |
| **Real-Time Preview** | လက်မှတ် live preview | ❌ မရှိ |
| **Privacy Controls** | Private/Masked/Public ရွေးချယ်မှု | ❌ မရှိ |
| **Client-Side Hashing** | ဖိုင် server သို့ မသွား | ✅ အနည်းငယ်သာ |
| **Forensic Metadata** | IP၊ location၊ device၊ time - အားလုံးတစ်နေရာတည်း | ❌ ခွဲထားသည် |
| **QR Verification** | ချက်ချင်း verification QR code | ⚠️ ကန့်သတ် |
| **Rate Limiting** | Spam protection (RLS + Client) | ❌ အများစုမရှိ |

---

## 🗺️ Roadmap: "Trustless" အနာဂတ်

လက်ရှိ version **(Beta v1.0)** ကို end users အတွက် အမြင့်ဆုံးအမြန်နှုန်း၊ ရိုးရှင်းသော interface နှင့် အခမဲ့ access ပေးရန် optimize လုပ်ထားသည်။ သို့သော် ကျွန်ုပ်တို့၏ နောက်ဆုံးအမြင်မှာ database admin (ကျွန်ုပ်တို့) ပင် ဝင်ရောက်စွက်ဖက်၍မရသော structure သို့ ပြောင်းရွှေ့ခြင်းဖြစ်သည်။

### Phase 1: Beta (ယခု Active)

- **Infrastructure:** Cloud Database (Supabase)
- **ရည်ရွယ်ချက်:** အမြန်နှုန်း၊ UX (user experience) အတားအဆီးများ ဖယ်ရှားခြင်းနှင့် adaptation။ "frictionless" security ပေးခြင်း

### 🚀 Phase 2: (Backend / Edge Function လိုအပ်)

ဤ phase သည် system ၏ အပြည့်အဝ "Client-Side" structure မှ ပိုမိုလုံခြုံပြီး စီမံခန့်ခွဲရလွယ်ကူသော "Server-Side Authority" structure သို့ အကူးအပြောင်းကို လွှမ်းခြုံသည်။

| Item | ဘာပေးသနည်း? | Tech Stack | အရေးပါမှု |
|------|-------------|------------|-----------|
| **`INSERT` → Edge Function** | Spam block + API Key security | Supabase Edge (Deno) | 🔴 မြင့် |
| **Wallet Signature** | Cryptographic identity verification | Solana Wallet Adapter | 🟡 အလယ်အလတ် |
| **IPFS/Arweave Backup** | Decentralized immutability | IPFS SDK + Pinata | 🟢 နိမ့် |
| **Revocation Mechanism** | အတုလက်မှတ် ပယ်ဖျက်ခြင်း | DB Schema Update | 🔴 မြင့် |
| **Audit Log** | Forensic investigation record | Custom logs table | 🟡 အလယ်အလတ် |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | 🟢 နိမ့် |
| **DID Integration** | Decentralized Identity | ION/Ceramic | 🟢 နိမ့် |

### Phase 3: အပြည့်အဝ Decentralization (ရေရှည်)

| Feature | ပန်းတိုင် | ETA |
|---------|---------|-----|
| **Blockchain Registry** | On-chain Ethereum/Solana record | 2026 Q4 |
| **DAO Governance** | အသိုက်အဝန်း စီမံခန့်ခွဲမှု | 2027 Q1 |
| **Multi-Chain Support** | Polygon၊ Arbitrum၊ Base | 2027 Q2 |
| **Legal Recognition** | Turkey တရားရုံးတွင် တရားဝင်မှု | 2027-2028 |
| **API for Developers** | Public API endpoint | 2026 Q3 |

---

## 📊 ပြိုင်ဘက် ခွဲခြမ်းစိတ်ဖြာမှု (အပ်ဒိတ်ပြီး)

PoArt ကို ရှိပြီးသား solutions များ၏ အားနည်းချက်များကို ဖြည့်ဆည်းသော "Sweet Spot" (အကောင်းဆုံးအမှတ်) တွင် နေရာချထားသည်။

| Feature | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **ကုန်ကျစရိတ်** | 🆓 အခမဲ့ | 🆓 | 💰 ငွေပေး | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ အလွန်လွယ် | ❌ CLI | ⚠️ အလယ်အလတ် | ⚠️ အလယ်အလတ် | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Live | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ mode ၃ ခု | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privacy | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ ပြည့်စုံ | ❌ | ❌ | ⚠️ ကန့်သတ် | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ ချက်ချင်း | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Turkish Support** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**ရှင်းလင်းချက်:**
- ✅ : အပြည့်အဝ support / ရှိသည်
- ⚠️ : ကန့်သတ် / ငွေပေး plan တွင်
- ❌ : မရှိ / မ support
- 🔄 : Roadmap တွင် (develop လုပ်နေ)
- 🆓 : လုံးဝအခမဲ့
- 💰 : ငွေပေး / subscription လိုအပ်

### ပြိုင်ဘက်များ၏ အားနည်းချက်များ၊ PoArt ၏ အားသာချက်များ

| အားနည်းချက် | ပြိုင်ဘက်များ | PoArt |
|------------|--------------|-------|
| **အသုံးပြုရ ခက်ခဲမှု** | CLI၊ API သိရန်လိုအပ်၊ wallet လိုအပ် | ဆွဲချ၊ click ၃ ချက်နဲ့ ပြီး |
| **ကုန်ကျစရိတ် အတားအဆီး** | $50-500/လ subscription | 100% အခမဲ့ |
| **Privacy** | ဖိုင်ကို server သို့ upload | Client-side၊ ဖိုင် မသွား |
| **Forensic Data** | timestamp သာ | IP၊ location၊ device၊ time - အားလုံး |
| **Turkish Support** | မရှိ သို့မဟုတ် အလွန်ကန့်သတ် | ဒေသခံဘာသာစကား support |
| **Open Source** | ပိတ်ထားသော သေတ္တာ | code အားလုံး GitHub တွင် ဖွင့်ထား |

---

## 🧬 Protocol Data Structure (JSON Schema)

**[PoArt] လက်မှတ်တိုင်းတွင် အောက်ပါ standard အတိုင်း ထုတ်လုပ်ထားသော သယ်ဆောင်နိုင်ပြီး အတည်ပြုနိုင်သော JSON identity card ရှိသည်:**

> **မှတ်ချက်:** ဤ Identity JSON format သည် user သို့ တင်ပြသော certificate format ဖြစ်သည်။ Registry record တွင် `identity.asset_data` အစား `registry.asset` ကို အသုံးပြုသည် (mapping: `identity.asset_data` == `registry.asset`)

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

## 🔬 Technical Depth: Sealing Algorithm

### Deterministic Hash Functions

```javascript
// Helper Functions: Digest ကို hex string အဖြစ် ပြောင်း
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// String ကို byte array အဖြစ် ပြောင်း
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Canonical forensics string generation (v1.0: fixed field order + UTF-8 + \n delimiter)
// Phase 2 မှတ်ချက်: RFC 8785 (JCS) ဖြင့် canonical JSON သို့ ပြောင်းမည်
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal Production Process (အပြည့်အဝ Deterministic)

```javascript
// 1. FileHash တွက်ချက် (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Forensic data စုဆောင်း (timestamp တစ်ခုတည်း အသုံးပြု)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // timestamp တစ်ခုတည်း generate
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // တူညီသော timestamp
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot generate (canonical encoding ဖြင့်)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal produce (တူညီသော timestamp အသုံးပြု)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Masking helper functions (IPv4 နှင့် IPv6 support)
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4 စစ်ဆေး
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 သို့မဟုတ် မသိသော format
  return "***";
}
```

### Verification Steps (အဆင့် ၂ ခု)

#### Quick Verify (မြန်ဆန်သော အတည်ပြု)

```javascript
// file hash သာ verify (မြန်ဆန်သော red flag)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Registry မှ fetch
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Hash နှိုင်းယှဉ်
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ မူရင်း - File hash ကိုက်ညီ"
    };
  } else {
    return {
      valid: false,
      message: "❌ အတု - ဖိုင် ပြုပြင်ပြောင်းလဲထားသည်"
    };
  }
}
```

#### Full Verify (အပြည့်အဝ အတည်ပြု)

```javascript
// EvidenceRoot နှင့် NotarySeal ပြန်လည်ထုတ်လုပ်ပြီး verify
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Registry မှ fetch
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash verify (မြန်ဆန်သော red flag)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ အတု - File hash မကိုက်ညီ" };
  }

  // 2) EvidenceRoot ပြန်လည်ထုတ်လုပ် (registry တွင် သိမ်းထားသော forensics ဖြင့်)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ မကိုက်ညီ - EvidenceRoot မမှန်" };
  }

  // 3) NotarySeal ပြန်လည်ထုတ်လုပ် (တူညီသော timestamp + signer_sig ဖြင့်)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ မကိုက်ညီ - NotarySeal မမှန်" };
  }

  // ရွေးချယ်နိုင်: Phase 2 တွင် signer_sig ကိုလည်း attestation_pubkey ဖြင့် verify
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ လက်မှတ် မမှန်" };

  return { valid: true, message: "✅ မူရင်း - Full Verify အောင်မြင်" };
}
```

> **အရေးကြီး မှတ်ချက်များ:**
> - **Quick Verify:** မြန်ဆန်စွာ အသုံးပြုရန် file hash သာ verify
> - **Full Verify:** protocol ၏ အလွှာအားလုံး verify (EvidenceRoot + NotarySeal)
> - hash operations အားလုံးကို fixed encoding နှင့် delimiters ဖြင့် deterministic ပုံစံ လုပ်ဆောင်သည်
> - **v1.0 canonicalization standard:** Fixed field order + UTF-8 encoding + `\n` delimiter
> - **Phase 2 plan:** RFC 8785 (JCS - JSON Canonicalization Scheme) ဖြင့် canonical JSON သို့ ပြောင်းမည်
> - Masked mode တွင် EvidenceRoot နှင့် NotarySeal တွက်ချက်မှုကို masked forensics ဖြင့် လုပ်ဆောင်သည်
> - process တစ်ခုလုံး (forensics + NotarySeal) တွင် timestamp တစ်ခုတည်း အသုံးပြုသည်။ determinism အာမခံသည်
> - **Forensics field names:** `ip_masked`၊ `location`၊ `device`၊ `timestamp` (code နှင့် registry အပြည့်အဝ ကိုက်ညီ)
> - **Registry path:** `certificate.asset.fingerprints` (verify code နှင့် အပြည့်အဝ ကိုက်ညီ)
> - **Registry ရှိ signer_sig:** `proof.signer_sig` field သည် Full Verify အတွက် လိုအပ်သည်
> - SignerSignature mechanism ကို Phase 2 တွင် Solana Wallet Adapter ဖြင့် activate လုပ်မည်။ v1.0 တွင် `attestation_pubkey` ဖြင့် verify နိုင်သည်

---

## 📈 Usage Statistics (2026 Q1 ပန်းတိုင်)

| Metric | ပန်းတိုင် | Status |
|--------|---------|--------|
| **စုစုပေါင်း လက်မှတ်** | 1,000 | 🔄 ဆက်လက်လုပ်ဆောင်နေ |
| **Active Users** | 500 | 🔄 ဆက်လက်လုပ်ဆောင်နေ |
| **Verification အရေအတွက်** | 5,000 | 🔄 ဆက်လက်လုပ်ဆောင်နေ |
| **Uptime** | 99.9% | ✅ Active |
| **Avg Response Time** | <200ms | ✅ အကောင်းဆုံး |

---

## 🌍 အသိုက်အဝန်းနှင့် Support

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 ပံ့ပိုးကူညီသူများ

PoArt protocol သည် open source community ၏ ပံ့ပိုးမှုဖြင့် ဆက်လက်ဖွံ့ဖြိုးနေသည်။

**ပံ့ပိုးကူညီရန်:**
1. Project ကို Fork လုပ်ပါ
2. feature branch ဖန်တီးပါ (`git checkout -b feature/amazing-feature`)
3. Commit ပြုလုပ်ပါ (`git commit -m 'Add amazing feature'`)
4. Push ပြုလုပ်ပါ (`git push origin feature/amazing-feature`)
5. Pull Request ဖွင့်ပါ

### 🛠️ ယခု ဘာလိုအပ်သနည်း? (အကူအညီတောင်းခံခြင်း)

PoArt protocol ၏ **Phase 2** development အတွက် အောက်ပါ topics များတွင် အတွေ့အကြုံရှိသော developers များထံမှ ပံ့ပိုးမှုကို စောင့်ဆိုင်းနေသည်:

* **Supabase Edge Functions:** Spam protection ကို server side သို့ ရွှေ့ခြင်း
* **Solana Web3.js:** Wallet Signing integration
* **IPFS / Arweave:** Archiving နှင့် pinning service integration

> Feature ထည့်ခြင်းမပြုမီ "Issues" tab တွင် ဆွေးနွေးမှု စတင်ပါ

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // ယဉ်ကျေးမှုသည် အရင်းအနှီးထက် ကြီးမြတ်သည်*

## 🧾 လိုင်စင်

MIT License © 2026 İlhan Art Gallery Initiative

အပြည့်အဝ စည်းမျဉ်းများအတွက် [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) ကို ကြည့်ပါ

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**ဤ project ကို [İlhan Art Gallery] initiative မှ develop လုပ်ခဲ့ပြီး ပွင့်လင်းမြင်သာမှုအတွက် source code ကို အများပြည်သူထံ ထုတ်ဖော်ထားသည်။**

**PROTOCOL V1.0 // SHA-512 ဖြင့် SEALED**

*© 2026 İLHAN ART | လက်ရာများ၊ ပုံများနှင့် အယူအဆများအတွက် အခွင့်အရေးအားလုံး Reserved*

---
