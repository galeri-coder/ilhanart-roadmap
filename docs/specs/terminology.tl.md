# 📚 DIKSYUNARYO NG TERMINOLOHIYA AT MGA KONSEPTO - Bahagi 1
> **"Ang pag-unawa sa wika ng protocol na ito ay pag-unawa sa bisyon nito."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Pangunahing Imprastraktura

**Ang PoArt Forensic Engine (PFE)** ay ang pangunahing layer na kumakatawan sa core logic at teknikal na operasyon sa likod ng [PoArt] protocol. Ito ang "forensic engine" na kumukuha ng raw production data ng sining at nagiging **digital na ebidensya** na verified at immutable.

### 🧩 Bakit "PoArt Forensic"?

- **PoArt (Proof of Art):** Ang focus ng engine ay ang pag-ugnay ng halaga ng digital asset hindi sa speculation; kundi sa **napatunayang proseso ng produksyon**.
- **Forensic (Forensic Verification):**
  - **Teknikal na Kahulugan:** Algorithm at record chain approach upang patunayan na ang data na nauugnay sa proseso ng produksyon (brush strokes, timelapse, logs) ay hindi na-manipulate.
  - **Philosophical Layer:** Laban sa "instant output" production ng Artificial Intelligence; ang claim na ang produksyon ng tao na may **oras, pagsisikap, at presyo ng desisyon** ay maaaring maging sukatan ng katotohanan.

> Tandaan: Ang blockchain (hal. Solana) integration ay hindi core ng PFE; ito ay hiwalay na tinutukoy bilang **Chain Anchor Layer** para sa verification/registry.

### 🛠️ v1.0 Teknikal na Saklaw

**Ang PoArt Forensic Engine (PFE) v1.0** ay itinayo sa **3 pangunahing haligi** sa halip na kumplikadong financial models:

1. **Hashing & Sealing (Pagtatak):**  
   Ang PFE ay deterministically nagpoproseso ng lahat ng elemento sa Evidence Pack (artwork file, video, JSON/log, signature atbp.) upang makagawa ng natatanging **NotarySeal** value.

   **Pangunahing konsepto (v1.0):**
   - **FileHash (fingerprint ng artwork):** Hash na ginawa mula sa bytes ng artwork file.
   - **EvidenceRoot (root ng evidence pack):** Root summary na kumakatawan sa integridad ng Evidence Pack (Merkle root o canonical manifest hash).
   - **NotarySeal (final seal / PFE Output):** Huling seal na ginawa mula sa kombinasyon ng EvidenceRoot + oras + signature.

   **Mga Formula (malinaw na makikita ng mga investor):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload Definitions (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Tandaan: Ang value na tinutukoy bilang PFE output ay **NotarySeal**. Ang **SignerSignature** mechanism ay ie-enable sa Phase 2 (kasama ang Solana Wallet Adapter); sa kasalukuyang v1.0, ginagamit ang system's own attestation signature. Ang Attestation public key ay nai-publish sa `issuer.attestation_pubkey` field ng registry.

2. **Indexing (Pag-archive):**  
   Nagre-record kung aling wallet, anong petsa, para sa aling artwork ang nag-submit ng **Labor Proof (Proof of Labor)**; sa transparent at searchable na record layer.  
   *(Ang layer na ito ay maaaring database; ang chain integration ay hiwalay na tinutukoy bilang "Chain Anchor Layer".)*

3. **Verification (Pag-verify):**  
   Kapag may tanong tungkol sa orihinal ng artwork, ang PFE ay muling nagpoproseso ng raw evidence; sinusubukan nang may mathematical certainty kung ang kinakalkula na **EvidenceRoot / NotarySeal** values ay tumutugma sa record sa archive.

---

### 🧮 PoArt Value Theorem (Teorama ng Halaga)

Ang [PoArt] protocol ay nag-uugnay ng halaga ($V$) ng digital asset hindi sa subjective market perception; kundi sa **pisikal na katotohanan ng proseso ng produksyon**.

Ang Artificial Intelligence (AI) ay pumupuksa sa proseso sa pamamagitan ng instant result ($t \to 0$). Ang [PoArt] ay tumatanggap ng halaga bilang; akumulasyon ng **oras, pagsisikap, at kalooban**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Kahulugan ng mga Variable

- **$\int dt$ (Process Accumulation):**  
  Ang halaga ay hindi instant na "output"; ito ay **proseso** na nag-aakumula sa pagitan ng $t_{\text{start}}$ at $t_{\text{end}}$. Habang bumababa ang tagal (AI production), ang resulta ng integral ay lumalapit sa 0.

- **$P_{\text{labor}}(t)$ (Instantaneous Labor Power):**  
  Kumakatawan sa intensity ng mental at physical effort na ginastos sa oras ng produksyon. Habang tumataas ang napatunayan na pagsisikap, lumalaki ang integrand.  
  > Tandaan: Ang term na ito ay maaaring i-normalize sa praktikal na paraan gamit ang "measurable/provable labor signals".

- **$I_{\text{agency}}(t)$ (Agency Coefficient):**  
  Ang kakayahan ng producer na kumuha ng risk at gumawa ng desisyon. Tumatagal ng value sa pagitan ng $0$ at $1$.
  - **AI ($I \approx 0$):** Sumusunod sa mga command, hindi kumukuha ng risk, walang binabayaran.
  - **Tao ($I \to 1$):** Nagbabago ng desisyon, nag-aalangan, kumukuha ng risk.

- **$U_{\text{irreversible}}$ (Irreversible Uniqueness):**  
  Habang ang undo (`Ctrl+Z`) ay posible sa digital production; sa physical production (pintura sa canvas, ukit sa marble, gesture sa live broadcast) walang pag-balik. Ang **hindi maibabalik na ito** ay karagdagang term na lumilikha ng "uniqueness" (non-fungible character) sa artwork.

### 🔎 Case Analysis: AI "Instant Output" vs. Human "Proven Process"

Ang sumusunod na sitwasyon ay nagpapakita kung paano gumagana ang **PoArt Value Theorem** sa praktikal at bakit ang AI productions ay nakakakuha ng mababang score sa [PoArt] standard.

#### Scenario A: Visual Production sa 10 Segundo gamit ang AI

- **Tagal ($\Delta t$):** $10$ segundo (halos walang proseso)
- **Labor Power ($P_{\text{labor}}$):** $1$ unit (pagsulat lang ng command)
- **Agency Coefficient ($I_{\text{agency}}$):** $0.01$ (walang risk, walang presyo)
- **Irreversibility ($U_{\text{irreversible}}$):** $0$ (reversible / copyable)

**Resulta:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Komento:** Kahit perpekto ang output; dahil walang prosesong naranasan at walang agency/risk, ang [PoArt] value ay lumalapit sa $0$.

#### Scenario B: 6 Oras na Physical Production sa Live Broadcast

- **Tagal ($\Delta t$):** $6$ oras ($21{,}600$ segundo)
- **Labor Power ($P_{\text{labor}}$):** $0.5$ unit (patuloy na physical at mental effort)
- **Agency Coefficient ($I_{\text{agency}}$):** $0.9$ (pagbabago ng desisyon, pagtanggap ng risk, hindi maibabalik na pagpili)
- **Irreversibility ($U_{\text{irreversible}}$):** $>0$ (hindi maibabalik ang physical traces)

**Resulta:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Komento:** Habang tumatagal ang proseso at tumataas ang agency (risk), ang halaga ay kumulative na tumataas. Ang term na $U_{\text{irreversible}}$ ay karagdagang kontribusyon na lumilikha ng "uniqueness" (non-fungible character) sa artwork.

---

### ✅ Konklusyon: Proof-Bound Value (Halaga na Nakakandado sa Patunay)

Ang theorem na ito ay nag-aalis ng value claim ng [PoArt] mula sa pagiging "preference" o "market narrative" at nag-uugnay nito sa **napatunayang katotohanan ng produksyon**.

1. **Walang Halaga Kung Walang Proseso:**  
   Ang AI ay pumupuksa sa proseso sa instant output ($t \to 0$). Habang sumasara ang process window, ang resulta ng integral ay mathematical necessity na bumababa:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Ang Agency at Risk ay Multiplier:**  
   Ang [PoArt] ay sumusukat hindi lamang ng "oras na ginugol"; kundi pati na rin ng tunay na desisyon, risk, at presyo sa oras na iyon. Ang produksyon na hindi kumukuha ng risk (AI) ay may mababang halaga:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Ang Uniqueness ay Physical Proof, Hindi Marketing:**  
   Ang mga bakas na hindi maibabalik sa physical production (canvas stroke, marble crack) ay lampas sa `Ctrl+Z` logic ng digital. Ang irreversibility na ito ($U_{\text{irreversible}}$) ay ontologically nagpapaka-unique sa artwork.

> **🔐 SUMMARY:** Kahit ang value theorem ay mukhang uncertain bilang measurement (kahit sa tunay na buhay ay hindi 100% masusukatan), ang layunin ng formula na ito ay; ipakita ang istruktura at direksyon ng mga variable. Sa AI age, ang bihira ay hindi "larawan"; kundi **napatunayang pagsisikap, oras, at kalooban.** Ang [PoArt] ay sumusukat ng kakulangan na ito at nagre-register gamit ang **Evidence Pack**.

### 🏛️ Kahalagahan ng Konsepto ng "Engine"

Ang mga token na lumalabas mula sa mga platform tulad ng Pump.fun o katulad nito ay kadalasang pawang **"access ticket"** lamang. Ang **PoArt Forensic Engine (PFE)** ay ang **constitutional logic layer** na tumutukoy kung aling karapatan ang pinoprotektahan ng ticket na iyon, kung paano irerehistro ang pagsisikap, at kung paano magiging permanente ang sining/agham/teknolohiya.

> **Tandaan:** Ang dahilan kung bakit namin sinimulan ang proyektong ito sa Pump.fun ay dahil wala kaming sapat na liquidity at bilang ng followers. Ang paggamit ng available data ay strategically ang pinaka-wastong hakbang kahit hindi ito ang pinakamataas na kalidad. Ang pagtukoy sa logic ng engine na ito sa GitHub nang independiyente sa budget at kakayahan ay nagpapatunay na ang proyekto ay hindi lamang financial speculation, kundi isang long-term **software infrastructure** at **digital national library** vision.

---

## 🎨 [PoArt] LABOR PROOF PROTOCOL (Proof of Art Protocol v1.0)

> **"Tunay na Artista, Tunay na Produksyon, Tunay na Halaga."**

Ang protocol na ito; ay **biological at intellectual defense mechanism** na binuo laban sa anonymous scammers na sumasaklaw sa crypto ecosystem, AI visuals na ginawa sa 5 minuto, at "Pump & Dump" culture.

---

## a) Ano ang [PoArt]? (Philosophical at Technical Definition)

**Proof of Art [PoArt];** ay isang institutional verification standard na ginagarantiya na ang halaga sa likod ng asset sa blockchain ay hindi nakabatay sa speculation; kundi sa verified **human labor**, **time**, at **physical energy**.

Tulad ng kung paano ang Bitcoin ay gumagawa ng halaga gamit ang *"Electricity at Processor Power"* **(Proof of Work)**; ang [PoArt] compliant projects ay gumagawa rin ng halaga gamit ang *"Spent Talent at Human Time"*. Nag-stake ng oras.

Nag-aalis ng risk na *"Developer (Dev) bumenta, tapos na ang project"* sa Pump.fun at DEX platforms; dahil dito ang halaga ay hindi nakaimbak sa code, kundi sa **sustainability ng produksyon**.

> **Ang [PoArt] ay hindi nagsasabi sa participant na "Magtiwala sa amin"; kundi "Heto ang mga patunay, tingnan mo sa iyong mga mata, i-verify mo sa iyong matematika."**

---

## b) [PoArt] 5-Pillar Standard (The 5 Pillars of Truth)

Ang 5 item na ito ay mga filter na hindi maaaring manipulahin na dapat lampasan ng project upang makatanggap ng [PoArt] seal.

### 1) Live Identity Proof (Patunay ng Live na Pagkakakilanlan)

- **Problema:** Ang crypto world ay puno ng anonymous founders (Dev) na walang malinaw na pagkakakilanlan na nag-iipon ng pera at nag-aabandona sa project.
- **[PoArt] Solusyon:** Ang producer ay nagpapatunay hindi lamang ng ID card, kundi ng **presensya niya sa oras ng produksyon**. Ito ay hindi pre-recorded videos, kundi live broadcast sessions na nakikipag-ugnayan sa komunidad at nagsasagawa ng mga instant specific requests.  
  (Hal: *"Isulat ang petsa ngayon at kasalukuyang block number sa kanang sulok ng canvas"*)
- **Motto:** *"Ang mga bot ay maaaring gumawa ng larawan pero ang mga bot ay hindi pumapawis at hindi makakapaglaro ng impromptu."*

### 2) Labor & Process Proof (Patunay ng Pagsisikap at Proseso)

- **Problema:** Ang AI visuals na ginawa sa 2 segundo at oil painting na ginawa sa 2 buwan ay pareho lamang na "jpeg" sa digital world.
- **[PoArt] Solusyon:** Ang "pregnancy at birth" process ng artwork ay naka-record. Ang sketch stages, paint layers, accumulated hours spent, at physical process na naranasan ng artist habang lumilikha ng artwork na iyon ay documented. Ito ay nagdadagdag ng **"Time Cost"** sa token. Habang mas mahirap ang produksyon ng asset, mas malakas ang halaga nito.

### 3) Aesthetic Value Proof (Patunay ng Aesthetic na Halaga)

- **Problema:** Ang "Meme" culture na nag-iignora sa aesthetics at artistic depth, nakatuon lamang sa instant comedy, at nagreresulta sa short-lived "Hype" projects.
- **[PoArt] Solusyon:** Ang project ay dapat may academic art standards, color theory, composition rules, at material knowledge (Impasto, Texture atbp.). Ang content ay hindi dapat tumawa lamang; dapat magdulot ng hanghang sa audience at may **collection value**.

### 4) Conceptual Novelty (Konsepto ng Pagkakabago)

- **Problema:** Libu-libong dog/cat coins na kopya ng isa't isa, malayo sa creativity.
- **[PoArt] Solusyon:** Ang project ay dapat gumawa ng bagong tulay na pinagsasama ang sining, agham, pilosopiya, o teknolohiya sa meaningful na istruktura.  
  (Hal: Pagsasama ng classic David sculpture sa crypto market data; sa pamamagitan nito ay proseso ng ideya ng "pagiging bato" ng human perception at maaaring ilatag gamit ang scientific sources.)  
  Ang artwork ay hindi dapat visual feast lamang; kundi intellectual challenge na nagpapaisip tungkol sa **Agham, Pilosopiya, o Teknolohiya**.

> [!IMPORTANT]
> **Reference Example (Las Palmitas Effect):**  
> Sa nakakalabang sa krimen na baryo ng Las Palmitas sa Mexico, higit sa 200 bahay ay naging malaking rainbow feast. Bilang resulta ng aesthetic intervention na ito, ang crime rates sa baryo ay bumaba sa tiyak na antas, ang mga kabataan ay nagsimulang mag-focus sa sining sa halip na gang. Ang aesthetic change ay nag-recode ng respeto ng mga tao sa kanilang kapaligiran at sa isa't isa (Social Cohesion).
>
> **Inaasahan:** Ang project na papasok sa [PoArt] list; tulad ng halimbawa sa itaas, ay dapat magkaroon ng sociological, scientific, o philosophical cause-effect relationship lampas sa pure visual aesthetics. Dahil ang tanging bagay na hindi mabibili ng pera ay "Oras", sa protocol na ito ang oras ay dapat i-stake bilang collateral at patunayan. Ang intellectual foundation ng project ay dapat napakalakas at universal na; kahit sa possible CTO (Community Take Over) scenario makalipas ang ilang taon, ang komunidad ay maaaring mag-inherit ng legacy na ito at autonomously magpatuloy ng innovative potential ng project.

### 5) Non-Algorithmic Agency (Kalooban na Hindi Algorithmic)

- **Problema:** Perpektong pero walang kaluluwa, paulit-ulit na digital productions.
- **[PoArt] Solusyon:** Ang orihinal na kalooban ng tao na maaaring magkamali, kumuha ng risk, at mag-experience ng emotional fluctuations ay dapat maramdaman sa artwork. Ang uncertainty sa brush strokes, ang unexpected reactions ng material, at ang instant decisions ng artist ay ang **Biological Signature** na naghihiwalay sa artwork mula sa "Machine Production".

---

**(Katapusan ng Bahagi 1 - Bahagi 2 ay magpapatuloy...)**

# PoArt Protocol - Bahagi 2

## c) Verification & Anti-Fraud Mechanism (Mekanismo ng Pag-verify at Laban sa Pandaraya)

Ang system na ito ay ginagarantiya na ang project ay hindi lamang "sa simula" kundi "magpakailanman" reliable at buhay.

### 📦 Evidence Pack (Pakete ng Ebidensya - The Digital Twin)

Sa likod ng bawat [PoArt] certified artwork, mayroon isang encrypted at time-stamped data package na maaaring i-download ng mga investor:

- **RAW Video Recordings:** Tuluy-tuloy na raw footage ng sandali ng produksyon.
- **Metadata Analysis:** Petsa ng creation ng file, impormasyon ng device na ginamit, at location data (Lungsod-Bansa).
- **Physical References:** Patunay na ang artwork ay umiiral sa physical world  
  (Hal: Kasalukuyang pahayagan na nakatayo sa tabi ng artwork o blockchain data sa oras na iyon).

> *Consistency note:* Ang expression na "evidence package" ay konektado sa **Evidence Pack → EvidenceRoot → NotarySeal** line sa nakaraang sections; ibig sabihin, ang integridad ng package ay kinakatawan ng verifiable seal.

### 🔄 365-Day Renewal (The Sustainability Protocol)

- **Revolutionary Feature:** Sa crypto projects, ang "Dev" (Developer) ay naglalabas ng token sa market at karaniwang nawawala pagkatapos ng 1-2 buwan (Soft Rug). Ang [PoArt] ay ginagawang imposible ito.
- **Patakaran:** Ang "Verified Artist" status ay hindi habambuhay. Tumatagal lamang ng **1 taon**.
- **Operasyon:** Ang artist/developer ay dapat mag-present sa komunidad ng **bagong, malaking, at napatunayang artwork** bawat 365 araw.
- **Sample Scenario:** Nagsimula ka ng project noong 2026. Sa January 2027, magbibigay ng babala ang system na "Proof Period Expired". Kung ang artist ay hindi magbibigay ng bagong exhibit, bagong physical artwork, o bagong technological integration, bababa ang "Trust Badge" ng project.
- **Resulta:** Ang system na ito ay ginagarantiya na ang **content ay hindi kailanman magiging luma** at ang investor ay hindi mag-aalala sa *"Nandito pa ba ang developer?"* Ang project ay nagiging living studio.

### 🚩 Red Flag Protocol (Protokol ng Pulang Bandila)

**Sa kaso ng anumang fraud (AI usage, stolen artwork, manipulated video) na natukoy ng komunidad o algorithms:**

1. Ang certificate ay agad na marka-markahan bilang **"VOID" (CANCELLED)**.
2. Ang evidence packages ay publicly na matatag bilang **"Fake"**.
3. Ang project ay ilalagay sa [PoArt] blacklist. Ito ay nagpapalakas ng katotohanang ang **reputasyon ay ang tanging currency** sa decentralized world.
4. Hindi maaaring gumamit ng [PoArt] expressions sa anumang publication, ang tanging valid source ay https://www.ilhanart.org/public-registry

---

## d) Konklusyon: Hindi Casino, Kundi Museo

**Ang Pump.fun at Decentralized Exchanges (DEX) ay sa kasalukuyan ay casino; kumikislap ang mga ilaw, lahat ay humahabol ng mabilis na kita, at ang house (scammers) ay palaging nanalo. Ang dahilan kung bakit namin sinimulan ang project dito ay dahil sinusubukan din naming pahusayin ito at dahil sa available data at live broadcasts ay may kapaligiran kami na makakaabot sa kasalukuyang audience.**

**Ang [PoArt] ay isang fortress na itinayo sa gitna ng casino na ito.**

- 🎰 Ang casino ay nakasalalay sa card games; tayo ay nakasalalay sa **pisikal na katotohanan**
- 🃏 Ang casino ay bukas sa pandaraya; tayo ay bukas sa **transparent na patunay**
- ⏳ Ang casino ay pansamantala; tayo ay nakatuon sa **walang hanggan ng sining at agham**

**Ang token na gumagamit ng protocol na ito ay hindi lamang "coin"; ito ay digital stock na may pawis, pintura, code, at pilosopiya sa likod.**

---

## 🗳️ 6) GOVERNANCE AT PUBLIC REGISTRY (Pamamahala at Pampublikong Talaan)

**Ang layunin ng section na ito ay: ilabas ang [PoArt] standard mula sa level ng "trust sa mga tao" at gawing sustainable public infrastructure gamit ang record + verification + community oversight.**

### 6.1 Public Registry (Pampublikong Talaan)

- **Public Registry:** Lahat ng approved data ay naka-record sa `ilhanart.org/registry` (o GitHub Registry).

**Record logic (recommended standard - JSON path format):**

Ang bawat record na pumapasok sa registry ay may minimum na mga verifiable core field na ito:

- **Identity & Status:**
  - `certificate_id` (readable reference)
  - `status` (active / void)
  - `void_reason` (kung mayroon)
  - `visibility` (private / masked / public)
  - `created_at` (timestamp)

- **Issuing Institution:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Artwork Information:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet`
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Forensic Data:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Cryptographic Evidence:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Governance:**
  - `governance.decision`
  - `governance.review_notes`

---

### 6.2 PoArt Verified Application Process

**Ang PoArt Verified applications ay sinusuri ng İlhanArt Gallery ayon sa 5 PoArt standards. Ang community feedback ay isinasaalang-alang, ngunit ang final decision ay nakasalalay sa curatorial team. Ang mga desisyon ay transparently ipinaliwanag at naka-record sa ilhanart.org/registry.**

#### Application Process

**Application:**
- Ang artist/project ay nag-apply ng PoArt Verified
- Inihahanda ang Evidence Pack (video recordings, metadata, live broadcast links)
- Ipinapadala ang application sa İlhanArt Gallery

**Review (30 Days):**
- Ang gallery team ay detalyadong sinusuri ang Evidence Pack
- Sinusuri ang lahat ng 5 PoArt standards:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Interview sa artist (optional)

**Community Consultation:**
- Ang Evidence Pack ay publicly shared sa panahon ng application process
- Ang komunidad ay maaaring magbigay ng feedback sa pamamagitan ng ilhanart.org
- Ang token holders (minimum 10,000 $CULTURE) ay maaaring mag-suggest
- **Lahat ng feedback ay isinasaalang-alang sa review process**
- **Ngunit ang final decision ay nakasalalay sa curatorial assessment**

**Decision:**
- Ang gallery ay nag-approve o nagtanggihan ng application
- Ang rationale ng desisyon ay transparently ipinaliwanag
- Kung approved → PoArt Verified badge
- Kung rejected → maaaring mag-apply muli pagkatapos ng 6 buwan

**Transparency:**
- Lahat ng applications at decisions ay naka-record sa ilhanart.org/registry
- Ang Decision record ay publicly published:
  - Application date
  - Review process summary
  - Decision (Approved / Rejected)
  - Decision rationale (maikling paliwanag)
  - Community feedback summary (anonymous)

#### Bakit Curatorial Decision?

**Quality Control:**  
Ang PoArt Verified status ay high-standard badge. Ang curatorial assessment ay ginagarantiya ang pagpapanatili ng standards na ito.

**Speculative Manipulation Prevention:**  
Sa Pump.fun tokens, ang full on-chain governance (hal: Realms, DAO voting) ay technically hindi posible. Ang off-chain voting systems ay bukas sa whale manipulation at coordinated attacks. Ang curatorial decision ay nag-aalis ng risk na ito.

**Operational Efficiency:**  
Mabilis at malinaw na decision process sa halip na kumplikadong voting mechanisms. Ang mga artist ay makakakuha ng resulta sa loob ng 30 araw.

**Community Participation:**  
Ang community feedback ay ganap na isinasaalang-alang at nag-aambag sa decision process. Ngunit ang final decision ay nasa curatorial team na protected mula sa manipulation.

**Future:**  
Kapag mature na ang project (2027+), ang community consultation mechanism ay maaaring palakasin. Ngunit ang curatorial standard protection ay nananatiling permanent.

---

### 6.3 Token Utility (Mga Gamit ng Token)

**Mga benepisyo na ibinibigay sa $CULTURE token holders:**

**1. Priority Access sa Gallery Events:**
- Karapatang mag-exhibit ng 1 linggo bawat taon sa İlhanArt Gallery (transferable right)
- Drop painting discounts
- 10% hanggang 30% discount sa mga paintings sa gallery

**2. Full Access sa PoArt Registry:**
- Detalyadong records ng lahat ng authenticated artworks
- Full versions ng Evidence Packs
- Forensic verification tools

**3. Advisory Voting:**
- Consultation rights sa PoArt Verified applications
- Access sa community feedback channels
- Participation sa governance discussions

**4. Exclusive Content:**
- Studio behind-the-scenes content
- Artist interviews at process videos
- Technical documentation access

**Tandaan:**  
Ang token holders ay nagbibigay ng advisory vote. Ang final decision ay sa curatorial team. Ang structure na ito ay pinili upang maiwasan ang whale manipulation at speculative attacks. Walang staking reward dahil naghahanap kami ng long-term cultural participants, hindi short-term mercenary capital.

---

### 6.4 Metadata Sync (Pagkakasundo sa Physical World)

**Ang pagtukoy ng "100% match" technically:**

- **Minimum match (mandatory):**
  - Ang `asset.fingerprints.sha256/sha512` sa registry at ang hash ng file na hawak ay dapat **eksaktong pareho**.
  - Ang `proof.notary_seal` sa registry kapag muling ginawa (kung may Evidence Pack) ay dapat **eksaktong pareho**.

---

### 6.5 Dispute, Review, at Revocation

Ang registry ay hindi lamang "approval" mechanism; kundi **buhay na oversight mechanism laban sa fraud**.

- Kapag nagsimula ang dispute, ang record ay maaaring ipasok sa **"review"** mode.
- Kung natukoy ang fraud, marka-markahan bilang `status: void` at idadagdag ang rationale:
  - `void_reason` (AI usage / stolen / manipulation atbp.)
  - `revoked_at` (revocation time)
- Ang source ng revocation decision ay malinaw na makikita sa registry:
  - curatorial review / community dispute / forensic analysis note (alinman ang applicable)

---

### 6.6 Sample Registry Record (Machine-readable)

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
      "sha512": "41e5e0d007a2a77b6e0e3ebc548fbaa2788ea265193434f58d23e8c0f5bb20a0..."
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
    "review_notes": "Met all 5 PoArt standards."
  }
}
```

---

## 7) 🔐 TECHNICAL SEAL (NOTARY SEAL)

**Unshakeable seal algorithm na ginawa ng PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

## 🗺️ Roadmap: "Trustless" Future

### Phase 1: Beta v1.0 (Live Na Ngayon)

**Infrastructure:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + IPFS backup)
- Gallery self-attestation (centralized pero transparent)

**Token:**
- Platform: Pump.fun
- Liquidity: Raydium (automatic)
- Governance: Advisory only (community consultation)

**Layunin:**
- Speed, alisin ang UX barriers
- "Frictionless" security
- Community building

**Token Utility (v1.0):**
- Priority access sa gallery events
- PoArt Registry viewing
- Advisory voting rights

---

### 🚀 Phase 2: Decentralized Authority (2026 Q2-Q4)

| Feature | Ano ang Makukuha? | Tech Stack | ETA |
|---------|---------------|------------|-----|
| **Edge Function INSERT** | Spam prevention + API Key security | Supabase Edge (Deno) | Q2 2026 |
| **Wallet Signature** | Decentralized identity | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | Decentralized archive | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | Fake certificate cancellation | DB Schema Update | Q2 2026 |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain voting (x/web) + wallet signature
- Community representatives election
- Multi-sig operations control
- Weighted advisory voting (with whale cap)

---

### Phase 3: Full Decentralization (2027+)

| Feature | Target | ETA |
|---------|-------|-----|
| **On-Chain Registry** | Solana on-chain record | Q1 2027 |
| **Enhanced Token Utility** | NFT mint, advanced features | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **Legal Recognition** | Validity sa Turkish courts | 2027-2028 |

---

## 🔬 Technical Depth: Seal Algorithm

### Deterministic Hash Functions

```javascript
// FileHash calculation (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// EvidenceRoot creation
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// NotarySeal production
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}
```

### Verification Flow (Two Levels)

#### Quick Verify (Mabilis na Pag-verify)

```javascript
// Check file hash lang (mabilis na pulang bandila)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  if (userFileHash === originalHash) {
    return { valid: true, message: "✅ Original - File hash match" };
  } else {
    return { valid: false, message: "❌ Fake - File manipulated" };
  }
}
```

#### Full Verify (Kumpletong Pag-verify)

```javascript
// Muling gumawa ng EvidenceRoot at NotarySeal at i-verify
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash check
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Fake - File hash mismatch" };
  }

  // 2) Muling gumawa ng EvidenceRoot
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Mismatch - EvidenceRoot" };
  }

  // 3) Muling gumawa ng NotarySeal
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Mismatch - NotarySeal" };
  }

  return { valid: true, message: "✅ Original - Full Verify passed" };
}
```

---

## 💬 Huling mga Tandaan

### Pump.fun at Katotohanan

Ang proyektong ito ay sinimulan sa Pump.fun dahil:
- ✅ Liquidity access (Raydium automatic migration)
- ✅ Existing community access
- ✅ Mababang initial cost

Ngunit linawin natin:
- **Ang token price** ay hindi sukatan ng artistic success
- **Ang operational budget** token value ay mahalaga (gallery, exhibits, infrastructure)
- **Success metrics:** Authenticated artworks + community engagement + physical visitors

### Governance at Decentralization

**v1.0 Reality (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (centralized pero transparent)
- Governance: Advisory only (curatorial final decision)

**v2.0+ Vision (2027+):**
- Registry: On-chain (Solana)
- Signatures: Wallet-based (decentralized)
- Governance: Hybrid (community advisory + curatorial quality)

Ang structure na ito ay nagbibigay ng **operational efficiency** at **quality control** sa early stage, habang nagbubukas ng daan para sa **community participation** sa hinaharap.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Kultura, Mas Malaki kaysa Kapital*

## 🧾 License

MIT License © 2026 İlhan Art Gallery Initiative

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) 
![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) 
![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) 
![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Ang proyektong ito ay binuo gamit ang [İlhan Art Gallery] initiative, ang source codes ay bukas sa publiko para sa transparency.**

**PROTOCOL V1.0 // SEALED GAMIT ANG SHA-512**

*© 2026 İLHAN ART | Nakalaan ang Lahat ng Karapatan sa Artworks, Visuals, at Ideas.*

---

