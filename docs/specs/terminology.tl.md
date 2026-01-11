# 📚 Talasalitaan ng mga Termino at Konsepto
> **"Ang pag-unawa sa wika ng protokol na ito ay nangangahulugang pag-unawa sa bisyon nito"**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Pangunahing Imprastraktura

Ang **PoArt Forensic Engine (PFE)** ay ang pangunahing layer na kumakatawan sa core logic at teknikal na operasyon sa likod ng protokol na [PoArt]. Ito ay isang "forensic engine" na tumatanggap ng raw production data ng artwork at ginagawa itong **digital na ebidensya** na maaaring ma-verify at hindi mababago.

### 🧩 Bakit "PoArt Forensic"?

- **PoArt (Proof of Art):** Ang pokus ng engine ay ang pag-uugnay ng halaga ng digital asset hindi sa spekulasyon, kundi sa **proseso ng produksyon na maaaring patunayan**
- **Forensic (Forensic na Pagsusuri):**
  - **Teknikal na Kahulugan:** Mga algorithm at record chain approach na naglalayong i-verify na ang data na may kaugnayan sa proseso ng produksyon (mga brush stroke, timelapse, logs) ay hindi nabago
  - **Philosophical Layer:** Ang paghahabol na gawing masusukat na realidad ang **oras, pagsisikap, at gastos sa pagpapasya ng tao** sa produksyon, kabaligtaran ng "instant na resulta" ng AI

> Nota: Ang Blockchain integration (hal. Solana) ay hahawakan bilang hiwalay na **Chain Anchor Layer** para sa verification/registry, hindi bilang core ng PFE

### 🛠️ Teknikal na Saklaw v1.0

Ang **PoArt Forensic Engine (PFE) v1.0** ay itinayo sa **3 haligi** sa halip na kumplikadong modelo ng pananalapi:

1. **Hashing & Sealing (Pag-seal):**  
   Pinoproseso ng PFE ang lahat ng elemento sa Evidence Pack (file ng gawa, video, JSON/log, lagda atbp.) nang deterministic at bumubuo ng natatanging halaga ng **NotarySeal**.

   **Mga Pangunahing Konsepto (v1.0):**
   - **FileHash (Fingerprint ng Gawa):** Hash na nabuo mula sa bytes ng file ng gawa
   - **EvidenceRoot (Ugat ng Set ng Ebidensya):** Root summary na kumakatawan sa integridad ng Evidence Pack (Merkle root o canonical manifest hash)
   - **NotarySeal (Panghuling Tatak / PFE Output):** Panghuling tatak na nabuo mula sa kombinasyon ng EvidenceRoot + oras + lagda

   **Formula (Malinaw na ipinapakita para sa mga mamumuhunan):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Kahulugan ng Canonical Payload (v1.0):**
   
   - **EvidenceRootPayload:**
   ```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
   ```
   
   - **NotarySealPayload:**
   ```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
   ```
   
   > Nota: Ang halagang tinutukoy bilang PFE output ay ang **NotarySeal**. Ang mekanismo ng **SignerSignature** ay ia-activate sa Phase 2 (kasama ang Solana Wallet Adapter); sa kasalukuyang v1.0, ginagamit ang sariling attestation signature ng sistema. Ang Attestation public key ay ilalathala sa field na `issuer.attestation_pubkey` sa registry

2. **Indexing (Pag-archive):**  
   Nagre-record kung aling wallet, sa anong petsa, nagpadala ng **Labor Proof (Patunay ng Paggawa)** para sa anong gawa sa transparent at mahahanap na record layer.  
   *(Ang layer na ito ay maaaring maging database; ang chain integration ay ide-define nang hiwalay bilang "Chain Anchor Layer")*

3. **Verification (Pagpapatunay):**  
   Kapag kinuwestiyon ang pagiging orihinal ng gawa, muling pinoproseso ng PFE ang raw na ebidensya; sinusubok na may mathematical certainty kung ang nakalkula na halaga ng **EvidenceRoot / NotarySeal** ay tumutugma sa record sa archive o hindi.

---

### 🧮 Teorema ng Halaga ng PoArt (The Value Theorem)

Iniuugnay ng protokol na [PoArt] ang halaga ($V$) ng digital asset hindi sa subjective na pananaw ng merkado, kundi sa **pisikal na realidad ng proseso ng produksyon**.

Sinisira ng AI ang proseso sa pamamagitan ng pagbibigay ng instant na resulta ($t \to 0$). Itinuturing ng [PoArt] ang halaga bilang akumulasyon ng mga bahagi ng **oras, paggawa, at kalooban**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Kahulugan ng mga Variable

- **$\int dt$ (Akumulasyon ng Proseso):**  
  Ang halaga ay hindi instant na "resulta"; ito ay **proseso** na nag-iipon sa pagitan ng $t_{\text{start}}$ at $t_{\text{end}}$. Kapag bumaba ang tagal (AI production), ang resulta ng integral ay lumalapit sa 0.

- **$P_{\text{labor}}(t)$ (Instant na Kapangyarihan ng Paggawa):**  
  Kumakatawan sa intensity ng mental at pisikal na pagsisikap na ginagamit sa panahon ng produksyon. Kapag tumataas ang napapatunayan na pagsisikap, lumalaki ang integrand.  
  > Nota: Sa praktika, ang term na ito ay maaaring i-normalize sa pamamagitan ng "masusukat/napapatunayan na mga signal ng paggawa"

- **$I_{\text{agency}}(t)$ (Coefficient ng Kalooban):**  
  Ang kakayahan ng producer na kumuha ng panganib at magpasya. Tumatanggap ng halaga sa pagitan ng $0$ at $1$.
  - **AI ($I \approx 0$):** Nagpapatupad ng utos, hindi kumukuha ng panganib, hindi nagbabayad ng gastos
  - **Tao ($I \to 1$):** Nagbabago ng desisyon, nag-aalangan, kumukuha ng panganib

- **$U_{\text{irreversible}}$ (Hindi Maibabalik na Pagiging Natatangi):**  
  Habang posible ang pag-undo (`Ctrl+Z`) sa digital production; walang balik sa pisikal na produksyon (pintura na ipininta sa canvas, marmol na inukit, gesture sa live broadcast). Ang **hindi maibabalik** na ito ay karagdagang term na lumilikha ng "pagiging natatangi" (non-fungible na katangian) sa gawa.

### 🔎 Pagsusuri ng Kaso: AI "Instant na Resulta" vs. Tao "Prosesong Napapatunayan"

Ang mga sumusunod na senaryo ay nagpapakita kung paano gumagana ang **Teorema ng Halaga ng PoArt** sa praktika at kung bakit mababa ang marka ng AI production sa pamantayan ng [PoArt].

#### Senaryo A: Produksyon ng Imahe ng AI sa 10 Segundo

- **Tagal ($\Delta t$):** $10$ segundo (halos walang proseso)
- **Kapangyarihan ng Paggawa ($P_{\text{labor}}$):** $1$ unit (pag-type lang ng utos)
- **Coefficient ng Kalooban ($I_{\text{agency}}$):** $0.01$ (walang panganib, walang gastos)
- **Hindi Maibabalik ($U_{\text{irreversible}}$):** $0$ (maaaring ibalik / kopyahin)

**Resulta:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Komento:** Kahit perpekto ang resulta; dahil walang proseso at walang kalooban/panganib, ang halaga ng [PoArt] ay lumalapit sa $0$.

#### Senaryo B: 6 Oras na Pisikal na Produksyon sa Live Broadcast

- **Tagal ($\Delta t$):** $6$ oras ($21{,}600$ segundo)
- **Kapangyarihan ng Paggawa ($P_{\text{labor}}$):** $0.5$ unit (pagpapatuloy ng pisikal at mental na pagsisikap)
- **Coefficient ng Kalooban ($I_{\text{agency}}$):** $0.9$ (pagbabago ng desisyon, pagkuha ng panganib, mga pagpipiliang hindi maibabalik)
- **Hindi Maibabalik ($U_{\text{irreversible}}$):** $>0$ (ang pisikal na bakas ay hindi maibabalik)

**Resulta:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Komento:** Kapag mas mahaba ang proseso at tumataas ang kalooban (panganib), tumataas ang naiipong halaga. Ang term na $U_{\text{irreversible}}$ ay karagdagang kontribusyon na lumilikha ng "pagiging natatangi" (non-fungible na katangian) sa gawa.

---

### ✅ Konklusyon: Halagang Nakabigkis sa Patunay (Proof-Bound Value)

Ibinabalik ng teorema na ito ang paghahabol ng halaga ng [PoArt] sa **realidad ng produksyon na napapatunayan** sa halip na "kagustuhan" o "market narrative".

1. **Walang Halaga Kung Walang Proseso:**  
   Sinisira ng AI ang proseso sa instant na resulta ($t \to 0$). Kapag lumiliit ang window ng proseso, lumiliit ang resulta ng integral ayon sa matematika:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Ang Kalooban at Panganib ay Multiplier:**  
   Sinusukat ng [PoArt] hindi lang ang "oras na ginugol" kundi pati ang aktwal na desisyon, panganib, at layer ng gastos sa panahong iyon. Mababa ang halaga ng produksyon na hindi kumukuha ng panganib (AI):
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Ang Pagiging Natatangi ay Pisikal na Patunay, Hindi Marketing:**  
   Ang hindi maibabalik na bakas sa pisikal na produksyon (brush stroke sa canvas, bitak ng marmol) ay nasa labas ng digital na `Ctrl+Z` logic. Ang hindi maibabalik na ito ($U_{\text{irreversible}}$) ang gumagawa sa gawa na natatangi sa ontolohikal na paraan.

> **🔐 Buod:** Bagama't ang teorema ng halaga ay maaaring magmukhang hindi tiyak sa aspeto ng pagsukat (kahit sa totoong buhay ay hindi 100% masusukat), ang layunin ng formula na ito ay ipakita ang istruktura at direksyon ng mga variable. Ang bihira sa panahon ng AI ay hindi "imahe"; kundi **paggawa, oras, at kaloobang napapatunayan**. Sinusukat ng [PoArt] ang kakulangan na ito at inirerehistro gamit ang **Evidence Pack**.

### 🏛️ Kahalagahan ng Konsepto ng "Engine" (Makina)

Ang mga token na inilabas mula sa Pump.fun o mga katulad na platform ay kadalasang **"tiket sa pagpasok"** lamang. Ang **PoArt Forensic Engine (PFE)** ang **constitutional logic layer** na tumutukoy kung anong mga karapatan ang pinoprotektahan ng tiket na iyon, kung paano nire-record ang paggawa, at kung paano ginagawang permanente ang sining/agham/teknolohiya.

> **Nota:** Ang dahilan kung bakit sinimulan namin ang proyektong ito sa Pumpfun ay dahil wala kaming sapat na liquidity at tagasunod. Ang paggamit ng umiiral na data ay maaaring hindi pinakamataas na kalidad na estratehiya, ngunit masasabi naming ito ang pinakatamang hakbang anuman ang budget at mapagkukunan. Ang pagtukoy ng logic ng engine na ito sa GitHub ay nagpapatunay na ang proyekto ay hindi lamang spekulasyon sa pananalapi, kundi pangmatagalang **software infrastructure** at bisyon ng **pambansang digital library**.

---

## 🎨 Protokol ng Patunay ng Paggawa [PoArt] (Proof of Art Protocol v1.0)

> **"Tunay na artista, tunay na produksyon, tunay na halaga"**

Ang protokol na ito ay isang **mekanismo ng depensa sa biyolohiya at intelektwal** na binuo laban sa mga anonymous na manloloko na pumupuno sa crypto ecosystem, mga imahe ng AI na ginawa sa 5 minuto, at kulturang "Pump & Dump" (bomba at itapon).

---

## a) Ano ang [PoArt]? (Pilosopikal at Teknikal na Kahulugan)

Ang **Proof of Art [PoArt];** ay isang institutional verification standard na ginagarantiya na ang halaga sa likod ng asset sa blockchain ay nakabatay sa **paggawa ng tao**, **oras**, at **pisikal na enerhiya** na maaaring i-verify, hindi spekulasyon.

Tulad ng paglikha ng Bitcoin ng halaga gamit ang *"electrical energy at processing power"* **(Proof of Work)**; ang mga proyektong compatible sa [PoArt] ay lumilikha ng halaga gamit ang *"artistic ability at oras ng tao"*.

Inaalis nito ang panganib na *"Nagbenta ang Dev (developer), tapos na ang proyekto"* sa mga platform na Pump.fun at DEX; dahil dito ang halaga ay iniimbak hindi sa code, kundi sa **pagpapatuloy ng produksyon**.

> **Ang [PoArt] ay hindi nagsasabi sa mga kalahok na "magtiwala sa amin"; sinasabi nito na "ito ang ebidensya, tingnan mo gamit ang iyong mga mata, i-verify gamit ang iyong matematika"**

---

## b) 5 Pamantayan ng [PoArt] (The 5 Pillars of Truth)

Ang 5 ito ay mga filter na hindi maaaring manipulahin na dapat lampasan ng proyekto upang matanggap ang tatak ng [PoArt].

### 1) Patunay ng Live na Pagkakakilanlan (Live Identity Proof)

- **Problema:** Ang mundo ng crypto ay puno ng mga anonymous na founder (Devs) na nangongolekta ng pera at umaaalis sa proyekto
- **Solusyon ng [PoArt]:** Pinapatunayan ng producer hindi lang ang ID card, kundi **ang kanilang presensya sa panahon ng produksyon**. Kasama dito ang mga live broadcast session na nakikipag-ugnayan sa komunidad at tumutugon kaagad sa mga partikular na kahilingan, hindi pre-recorded na video.  
  (hal: *"Isulat ang petsa ngayon at kasalukuyang block number sa kanang sulok ng canvas"*)
- **Kasabihan:** *"Ang bot ay maaaring gumuhit, ngunit ang bot ay hindi pinapawisan at hindi kayang mag-improvise"*

### 2) Patunay ng Paggawa at Proseso (Labor & Process Proof)

- **Problema:** Ang mga imahe ng AI na ginawa sa 2 segundo ay tinatrato na parang iisang "jpeg" tulad ng oil painting na iginuhit sa loob ng 2 buwan sa digital na mundo
- **Solusyon ng [PoArt]:** Nire-record ang proseso ng "pagbubuntis at panganganak" ng gawa. Ang mga yugto ng sketch, layer ng kulay, naipon na oras na ginugol, at pisikal na proseso na naranasan ng artista habang lumilikha ay dokumentado. Nagdadagdag ito ng **"Time Cost" (Gastos ng Oras)** sa token. Habang mas mahirap gawin ang asset, mas malakas ang halaga nito.

### 3) Patunay ng Aesthetic na Halaga (Aesthetic Value Proof)

- **Problema:** Kulturang "Meme" na binabalewala ang aesthetics at artistic depth, nakatutok lang sa instant na biro, at ang nagresultang mga proyektong "Hype" na maikli ang buhay
- **Solusyon ng [PoArt]:** Ang proyekto ay dapat magkaroon ng akademikong pamantayan ng sining, teorya ng kulay, mga panuntunan sa komposisyon, at kaalaman sa materyal (Impasto, Texture atbp.) Ang nilalaman ay hindi lang dapat magpatawa; dapat itong humanga sa manonood at magkaroon ng **collective value**.

### 4) Pagbabago sa Konsepto (Conceptual Novelty)

- **Problema:** Libu-libong dog/cat coin na kinokopya ang isa't isa, walang pagkamalikhain
- **Solusyon ng [PoArt]:** Dapat magbuo ang proyekto ng bagong tulay na pinagsasama ang sining, agham, pilosopiya, o teknolohiya sa makabuluhang istruktura.  
  (hal: Pagsasama ng klasikong eskultura ni David sa data ng crypto market; pagtatrabaho sa konsepto ng "petrification" ng persepsyon ng tao at maaaring suportahan ng mga siyentipikong pinagkukunan)  
  Ang gawa ay hindi lang dapat maging visual feast; kundi dapat ding maging intelektwal na hamon na nagpapasigla ng pag-iisip tungkol sa **agham, pilosopiya, o teknolohiya**.

> [!IMPORTANT]
> **Halimbawang Sanggunian (Las Palmitas Effect):** Sa kapitbahayan ng Las Palmitas sa Mexico na nakikipaglaban sa krimen, higit sa 200 bahay ang ginawang higanteng festival ng bahaghari. Bilang resulta ng aesthetic intervention na ito, bumaba nang bahagya ang rate ng krimen sa kapitbahayan, at nagsimulang mag-interes ang mga kabataan sa sining sa halip na mga gang. Ang aesthetic na pagbabago ay nag-recode ng paggalang ng mga tao sa kapaligiran at sa isa't isa (Social Cohesion).
>
> **Inaasahan:** Ang mga proyektong ilalista sa [PoArt] ay dapat magkaroon ng sociological, scientific, o philosophical na cause-effect relationship bukod sa visual aesthetics lamang, tulad ng halimbawa sa itaas. Dahil ang tanging asset na hindi mabibili ng pera ay "oras", ang oras ay dapat i-stake bilang collateral at patunayan sa protokol na ito. Ang conceptual foundation ng proyekto ay dapat sapat na malakas at unibersal na sa posibleng senaryo ng CTO (Community Take Over) sa mga susunod na taon, ang komunidad ay maaaring magmana ng legacy na ito at ipagpatuloy nang nakapag-iisa ang potensyal ng pagbabago ng proyekto.

### 5) Kalooban na Hindi Algorithmic (Non-Algorithmic Agency)

- **Problema:** Perpektong digital production ngunit walang kaluluwa, paulit-ulit
- **Solusyon ng [PoArt]:** Ang natatanging kalooban ng tao na maaaring magkamali, kumuha ng panganib, at maranasan ang pagbabagu-bago ng emosyon ay dapat maramdaman sa gawa. Ang hindi katiyakan sa brush stroke, ang hindi inaasahang reaksyon ng materyal, at ang instant na desisyon ng artista ay mga **biological signature** na naghihiwalay sa gawa mula sa "machine production".

---

## c) Mekanismo ng Pagpapatunay at Anti-Peke

Ginagarantiya ng sistema na ito na ang proyekto ay mananatiling mapagkakatiwalaan at buhay hindi lang "sa simula" kundi "habang panahon".

### 📦 Evidence Pack (Pakete ng Ebidensya - The Digital Twin)

Sa likod ng bawat sertipikadong gawa ng [PoArt] ay isang naka-encrypt at may timestamp na set ng data na maaaring i-download ng mga mamumuhunan:

- **RAW Video Recording:** Hindi putol na raw footage ng panahon ng produksyon
- **Pagsusuri ng Metadata:** Petsa ng paglikha ng file, impormasyon ng device na ginamit, at data ng lokasyon
- **Pisikal na Sanggunian:** Ebidensya na ang gawa ay umiiral sa pisikal na mundo  
  (hal: Kasalukuyang diyaryo sa tabi ng gawa o blockchain data sa oras na iyon)

> *Nota sa Consistency:* Ang expression na "evidence pack" ay nauugnay sa kadena ng **Evidence Pack → EvidenceRoot → NotarySeal** sa nakaraang seksyon; ibig sabihin, ang integridad ng set ay kinakatawan ng tatak na maaaring i-verify.

### 🔄 365 Araw na Pag-renew (The Sustainability Protocol)

- **Rebolusyonaryong Feature:** Sa mga proyektong crypto, inilulunsad ng "Dev" (developer) ang token sa merkado at madalas na nawawala pagkatapos ng 1-2 buwan (Soft Rug). Ginagawa ng [PoArt] na imposible ito.
- **Panuntunan:** Ang status na "Verified Artist" (Na-verify na Artista) ay hindi panghabangbuhay. Ito ay may bisa lamang ng **1 taon**.
- **Pagpapatupad:** Ang artista/developer ay dapat magpresenta ng **bago, malaki, at napapatunayang gawa** sa komunidad bawat 365 araw.
- **Halimbawang Senaryo:** Sinimulan mo ang proyekto noong 2026. Sa Enero 2027, babala ang sistema ng "Proof Period Expired". Kung hindi magpresenta ang artista ng bagong exhibition, bagong pisikal na gawa, o bagong technology integration, bababa ang "Trust Badge" ng proyekto.
- **Resulta:** Ginagarantiya ng sistema na ito na **hindi kailanman luma ang nilalaman** at hindi nararanasan ng mga mamumuhunan ang takot na *"Nariyan pa ba ang Dev?"*. Ang proyekto ay nagiging buhay na studio.

### 🚩 Red Flag (Pulang Bandila na Protokol)

**Sa kaso ng anumang pamemeke na natukoy ng komunidad o algorithm (paggamit ng AI, ninakaw na gawa, binagong video):**

1. Kaagad na minarkahan ang sertipiko bilang **"VOID" (walang bisa)**
2. Ang evidence pack ay pampublikong nilagyan ng label na **"peke"**
3. Ang proyekto ay idinagdag sa blacklist ng [PoArt]. Pinapalakas nito ang katotohanan na **ang reputasyon ang tanging pera** sa decentralized na mundo.

---

## d) Konklusyon: Museo, Hindi Casino

**Ang Pump.fun at Decentralized Exchanges (DEX) ay kasalukuyang nakalulungkot na mga casino; kumikislap ang mga ilaw, lahat ay naghahabol ng mabilis na kita, at laging nananalo ang banker (manloloko). Ang dahilan kung bakit sinimulan namin ang proyekto dito ay dahil wala kaming sapat na budget at network upang maabot ang umiiral na audience sa pamamagitan ng live broadcast.**

**Ang [PoArt] ay isang kuta na itinayo sa gitna ng casino na ito.**

- 🎰 Umaasa ang casino sa card game; kami ay **umaasa sa pisikal na realidad**
- 🃏 Bukas ang casino sa pandaraya; kami ay **bukas sa transparent na ebidensya**
- ⏳ Pansamantala ang casino; kami ay **nakatutok sa walang hanggang sining at agham**

**Ang token na gumagamit ng protokol na ito ay hindi lang "coin"; ito ay digital share na may pawis, pintura, code, at pilosopiya sa likod nito.**

---

## 🗳️ 6) Pamamahala at Pampublikong Rehistro (Governance & Public Registry)

**Ang layunin ng seksyong ito ay: Ibahin ang pamantayan ng [PoArt] mula sa antas ng "pagtitiwala sa indibidwal" patungo sa napapanatiling pampublikong imprastraktura na may pagre-record + pagpapatunay + pamamahala ng komunidad.**

### 6.1 Public Registry (Pampublikong Rehistro)

- **Public Registry:** Lahat ng naaprubahang data ay nire-record sa `ilhanart.org/registry` (o GitHub Registry)

**Logic ng Pag-record (Inirerekomendang Standard - JSON path format):**

Bawat record na pumapasok sa rehistro ay may minimum na mga pangunahing field na maaaring i-verify:

- **Pagkakakilanlan at Status:**
  - `certificate_id` (nababasang sanggunian)
  - `status` (active / void)
  - `void_reason` (kung mayroon)
  - `visibility` (private / masked / public)
  - `created_at` (timestamp)

- **Institusyong Nag-isyu:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Data ng Gawa:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (kung posible; para sa token-gated identity)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Data ng Forensic:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Cryptographic Proof:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Pamamahala:**
  - `governance.decision`
  - `governance.veto_threshold`

Ang rehistro ay maaaring magkaroon ng dalawang layer:
- **1)** Human-readable index (web listing / paghahanap / pagsasala)
- **2)** Machine-readable manifest (JSON record; para sa PFE verification)

**Ang "record" dito ay maaaring i-verify gamit ang kadena ng Evidence Pack → EvidenceRoot → NotarySeal ng PFE. Ang rehistro ay nag-aalok ng target ng verification, hindi "claim".**

---

### 6.2 40% Community Veto (Token-Gated Governance)

- **40% Community Veto:** Nagsisimula ang pagboto isang buwan bago makuha ang status; ang 40% na pagtutol ng **Token-Gated (Solana-Verified)** na komunidad ay magpapawalang-bisa sa aplikasyon.

**Mga Hakbang sa Pagboto (Inirerekomendang eksplisitong proseso):**
- **Application Window:** Ang kandidatong proyekto ay nagbubukas ng "PoArt Candidate Registration" (ang candidate record ay lumilitaw sa "pending" status)
- **Panahon ng Pagsusuri:** 30 araw para sa komunidad na suriin ang ebidensya (Evidence Pack + live broadcast record + metadata)
- **Token-gated Verification:** Ang pagboto ay ginagawa sa pamamagitan ng wallet na na-verify sa Solana (hal. paghawak ng partikular na token/NFT + wallet signature)
- **Panuntunan sa Veto:** Kung 40% ng mga boto ay **pagtutol (NO / VETO)**, tatanggihan ang aplikasyon
- **Transparency:** Ang mga resulta ng pagboto ay iniimbak sa rehistro bilang "decision record" (petsa, ratio, snapshot ID)

---

### 6.3 Metadata Sync (Pagtutugma sa Pisikal na Mundo)

- **Metadata Sync:** Ang teknikal na data sa rehistro ay dapat 100% tumugma sa pisikal na asset.

**Teknikal na Kahulugan ng "100% Pagtutugma" (Inirerekomendang Kalinawan):**
- **Minimum na Pagtutugma (Kinakailangan):**
  - `asset.fingerprints.sha256/sha512` sa rehistro ay dapat **eksaktong pareho** sa hash ng umiiral na file
  - `proof.notary_seal` sa rehistro ay dapat **eksaktong pareho** kapag muling nabuo (kung may Evidence Pack)
- **Pagtutugma ng Pisikal na Sanggunian (Uri ng Ebidensya):**
  - Ang ebidensya tulad ng pisikal na gawa + sanggunian ng petsa/block na ipinapakita sa live broadcast ay dapat tumugma sa Evidence Pack
- **Pagsunod sa Privacy:**
  - Ang mga field tulad ng IP/lokasyon sa `masked` visibility ay inilalathala **ayon sa masking standard**

---

### 6.4 Pagtatalo, Pagsusuri, at Pagpapawalang-bisa (Dispute & Revocation)

Ang rehistro ay hindi lang mekanismo ng "pag-apruba"; ito ay **buhay na mekanismo ng verification laban sa pamemeke**.

- Kapag nagsimula ang pagtatalo, ang record ay maaaring ilagay sa **"review"** mode
- Kung natukoy ang pamemeke, minarkahan itong `status: void` at idinagdag ang dahilan:
  - `void_reason` (paggamit ng AI / ninakaw / binago atbp.)
  - `revoked_at` (oras ng pagpapawalang-bisa)
- Ang pinagmulan ng desisyon sa pagpapawalang-bisa ay malinaw na lumilitaw sa rehistro:
  - Pagboto ng komunidad / awtorisadong panel / forensic examination record (alinman ang ginamit)

> **Ang seksyong ito ay kapareha ng konsepto ng VOID sa seksyong "Red Flag Protocol" sa rehistro.**

---

### 6.5 Halimbawa ng Record sa Rehistro (Machine-Readable)

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

> *Nota: Ang `asset.fingerprints.sha512` at iba pang hash value ay pinaikli para sa pagpapakita; sa aktwal na paggamit ay ginagamit ang buong haba ng hexadecimal character string*

---

## 7) 🔐 Teknikal na Tatak (NOTARY SEAL)

Ang hindi naguguluhang algoritmo ng tatak na nabuo ng **PoArt Forensic Engine (PFE) v1.0**:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Digital Notary at Forensic Evidence Protocol [PoArt] (Beta v1.0)

> **"Ang kultura ay mas malaki kaysa kapital. Protektahan ang iyong gawa mula ngayon, dalhin sa bukas"**

---

## Bakit Ibinubunyag sa Publiko?

Ang tunay na seguridad ay nagmumula sa transparency. Gamit ang aming sistema ng **Public Registry (Pampublikong Rehistro)**, sinuman mula saanman sa mundo ay maaaring mag-verify sa loob ng mga segundo kung ang file na hawak nila ay orihinal o hindi, nang hindi umaasa sa anumang awtoridad.

---

## 🧩 Bakit Mayroong Maraming "Module ng Visibility"?

Ito ang pinaka-kritikal na bahagi ng code (visibility select menu). Ang mga pagpipiliang ito ay nagpapahintulot sa mga user na balansehin ang **"privacy vs. transparency"**:

### 🔒 Pribado (Private)

- **Senaryo:** Hindi pa gustong i-publish ng artista ang gawa ngunit gustong i-timestamp at patunayan na "ginawa ko ito sa petsang ito"
- **Ano ang ginagawa ng code:** Sinusulat ang data sa database ngunit nilalagyan ng label na `visibility: "private"`. Pagkatapos kapag isinulat ang "Public Read" policy, maaaring itago ang mga record na ito mula sa publiko gamit ang `WHERE visibility = 'public'`

### 🕶️ Naka-mask (Masked)

- **Senaryo:** Gusto ng artista ng transparency ngunit natatakot na matuklasan ang home address (IP location)
- **Ano ang ginagawa ng code:** Ang mga function na `maskIP` at `maskLoc` ay gumagana sa JavaScript side, binabago ang IP address sa format na `88.241.***.***`, lokasyon sa format na `***/TR`, at ipinapadala ang censored version sa database
- **Nota sa Privacy:** Ang masking ay ginagawa sa browser. Hindi nakikita ng Supabase ang aktwal na lokasyon. **Gayunpaman:** Kung gumagamit ng third-party API tulad ng ipapi.co para sa data ng lokasyon, makikita ng mga provider na ito ang IP address habang humihiling
- **Pag-seal sa Masked mode:** Ang pagkalkula ng EvidenceRoot at NotarySeal ay ginagawa gamit ang masked forensics data; kaya nananatiling deterministic ang verification

### 🌍 Ganap na Nakalantad (Public)

- **Senaryo:** Buong transparency. Ayon sa pamantayan ng [PoArt], malinaw na inanunsyo kung saan, kailan, at mula sa anong network ginawa ang gawa.

---

## 💡 Teknolohikal na Inobasyon

Ang PoArt ay hindi lang file upload system. Ito ay isang **"Forensic Chain of Custody" (Kadena ng Pag-iingat ng Ebidensyang Forensic)** engine na pinagsasama ang tatlong magkakaibang layer ng teknolohiya sa isang palayok at nagdadala ng bagong pamantayan.

**Ang layer na inilarawan bilang "engine" sa seksyong ito ay tumutugma sa PoArt Forensic Engine (PFE) core sa nakaraang terminolohiya.**

### 1) Client-Side Hashing (Maximum na Privacy)

Ang file ng iyong gawa ay hindi kailanman ina-upload sa server. Kinakalkula ng aming engine na tumatakbo sa browser (Client-side) ang hash (digital summary) ng file sa iyong sariling computer. Tanging ang fingerprint at metadata lang ang ipinapadala sa server.

> **Nota sa Privacy:** Ang file ng gawa ay hindi ina-upload sa server at protektado sa ganitong paraan. Gayunpaman, ang forensics data (IP/lokasyon) ay ibinabahagi ayon sa napiling visibility mode (private/masked/public).

### 2) Forensic Data Fusion (Forensic Power)

Ito ay higit pa sa karaniwang timestamp. Pinagsasama ng sistema ang sumusunod na data sa isang "Genesis Seal":

- **Digital Summary (SHA-512):** Digital fingerprint na masisira kung kahit isang pixel ng gawa ay magbago, gamit ang cryptographic summary standard (SHA-512)
- **Lokasyon at Oras:** Petsa na may millisecond precision, bansa, lungsod, at distrito kung saan isinagawa ang operasyon
- **Device Identity:** Operating system, browser, at uri ng device (User-Agent analysis)

---

## 🛡️ Mga Kaso ng Paggamit at Benepisyo

Kung ikaw ay isang artista, manunulat, o designer, ang pagsasabi ng "ginawa ko muna ito" ay hindi sapat. Kailangan mong patunayan.

**Ang gawa na iyong i-seal gamit ang PoArt:**

- **Matematikal na Patunay:** Kung kahit isang pixel ng iyong file ay magbago, madedetect ito ng sistema. Imposible ang pagbabago.
- **Legal na Pundasyon:** Naka-record ang petsa, lungsod, at device kung saan na-seal ang gawa.
- **Instant na Sertipiko:** Gumagawa ng **"Asset Identity Certificate"** na may QR code at natatanging tatak para sa iyo sa loob ng mga segundo.

---

## ⚙️ Arkitektura ng Sistema at Teknikal na Specifications

Ang sistema ay dinisenyo sa "Serverless" (walang server) na arkitektura na nakatutok sa mataas na performance at scalability.

| Layer | Teknolohiya | Paglalarawan |
|-------|-------------|--------------|
| **Cryptography** | SHA-256 & SHA-512 | Dalawang layer na cryptographic summary |
| **Database** | Supabase (PostgreSQL) | JSONB data structure, RLS policies |
| **Forensic Data** | ipapi.co API | Triple na IP/lokasyon/oras |
| **Rendering** | html2canvas + jsPDF | Client-side PNG/PDF production |
| **Frontend** | Vanilla JavaScript | Walang framework dependency |
| **Seguridad** | Client-side hashing | Hindi kailanman ina-upload ang file sa server |

### Mga Natatanging Feature

| Feature | Detalye | Mayroon sa Kakumpitensya? |
|---------|---------|---------------------------|
| **Drag & Drop UI** | I-drag ang file, instant preview | ❌ Karamihan wala |
| **Multi-Format Export** | PNG, JSON, PDF - isang click | ⚠️ Limitado |
| **Real-Time Preview** | Live na preview ng sertipiko | ❌ Wala |
| **Privacy Controls** | Private/Masked/Public na pagpipilian | ❌ Wala |
| **Client-Side Hashing** | Hindi kailanman pumupunta ang file sa server | ✅ Ilan lang |
| **Forensic Metadata** | IP, lokasyon, device, oras - lahat sa isang lugar | ❌ Nahiwalay |
| **QR Verification** | Instant verification QR code | ⚠️ Limitado |
| **Rate Limiting** | Spam protection (RLS + Client) | ❌ Karamihan wala |

---

## 🗺️ Roadmap: "Trustless" na Kinabukasan

Ang kasalukuyang bersyon **(Beta v1.0)** ay na-optimize upang bigyan ang end users ng maximum speed, simpleng interface, at libreng access. Gayunpaman, ang aming ultimate vision ay lumipat sa istruktura kung saan kahit ang database admin (kami) ay hindi makakainterbensyon.

### Phase 1: Beta (Aktibo Ngayon)

- **Imprastraktura:** Cloud Database (Supabase)
- **Layunin:** Bilis, alisin ang UX (user experience) barriers, at adaptasyon. Magbigay ng "frictionless" na seguridad

### 🚀 Phase 2: (Kailangan ang Backend / Edge Function)

Sinasaklaw ng phase na ito ang paglipat mula sa ganap na "Client-Side" na istruktura ng sistema patungo sa mas secure at mas manageable na istrukturang "Server-Side Authority".

| Item | Ano ang Ibinibigay? | Tech Stack | Kahalagahan |
|------|---------------------|------------|-------------|
| **`INSERT` → Edge Function** | Block spam + API Key security | Supabase Edge (Deno) | 🔴 Mataas |
| **Wallet Signature** | Cryptographic identity verification | Solana Wallet Adapter | 🟡 Katamtaman |
| **IPFS/Arweave Backup** | Decentralized immutability | IPFS SDK + Pinata | 🟢 Mababa |
| **Revocation Mechanism** | Pagpapawalang-bisa ng pekeng sertipiko | DB Schema Update | 🔴 Mataas |
| **Audit Log** | Forensic investigation record | Custom logs table | 🟡 Katamtaman |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | 🟢 Mababa |
| **DID Integration** | Decentralized Identity | ION/Ceramic | 🟢 Mababa |

### Phase 3: Buong Decentralization (Pangmatagalan)

| Feature | Target | ETA |
|---------|--------|-----|
| **Blockchain Registry** | On-chain Ethereum/Solana record | Q4 2026 |
| **DAO Governance** | Pamamahala ng komunidad | Q1 2027 |
| **Multi-Chain Support** | Polygon, Arbitrum, Base | Q2 2027 |
| **Legal Recognition** | Bisa sa korte ng Turkey | 2027-2028 |
| **API for Developers** | Public API endpoint | Q3 2026 |

---

## 📊 Pagsusuri sa Kakumpitensya (Na-update)

Ang PoArt ay nakaposisyon sa "Sweet Spot" (pinaka-optimal na punto) na pumupuno sa mga kahinaan ng umiiral na solusyon.

| Feature | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Gastos** | 🆓 Libre | 🆓 | 💰 Bayad | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Napakadali | ❌ CLI | ⚠️ Katamtaman | ⚠️ Katamtaman | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Live | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 mode | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privacy | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Buo | ❌ | ❌ | ⚠️ Limitado | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Instant | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Turkish Support** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Paliwanag:**
- ✅ : Buong suporta / Mayroon
- ⚠️ : Limitado / Sa bayad na plano
- ❌ : Wala / Hindi suportado
- 🔄 : Sa Roadmap (ginagawa)
- 🆓 : Ganap na libre
- 💰 : Bayad / Kailangan ng subscription

### Mga Kahinaan ng Kakumpitensya, Mga Lakas ng PoArt

| Kahinaan | Kakumpitensya | PoArt |
|----------|---------------|-------|
| **Hirap sa Paggamit** | CLI, kailangang malaman ang API, kailangang may wallet | Drag and drop, tapos sa 3 click |
| **Hadlang sa Gastos** | $50-500/buwan na subscription | 100% Libre |
| **Privacy** | Ina-upload ang file sa server | Client-side, hindi kailanman pumupunta ang file |
| **Forensic Data** | Timestamp lang | IP, lokasyon, device, oras - lahat |
| **Turkish Support** | Wala o napaka-limitado | Lokal na wika na suporta |
| **Open Source** | Saradong kahon | Lahat ng code ay bukas sa GitHub |

---

## 🧬 Istruktura ng Data ng Protokol (JSON Schema)

**Bawat sertipiko ng [PoArt] ay may portable at mave-verify na JSON identity card na ginawa ayon sa sumusunod na pamantayan:**

> **Nota:** Ang Identity JSON format na ito ay ang certificate format na ipinepresenta sa user. Sa Registry record, ginagamit ang `registry.asset` sa halip na `identity.asset_data` (mapping: `identity.asset_data` == `registry.asset`)

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

## 🔬 Teknikal na Lalim: Algorithm ng Pag-seal

### Deterministic Hash Functions

```javascript
// Helper Functions: I-convert ang Digest sa hex string
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// I-convert ang String sa byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Canonical forensics string generation (v1.0: fixed field order + UTF-8 + \n delimiter)
// Nota sa Phase 2: lilipat sa canonical JSON gamit ang RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Proseso ng Produksyon ng NotarySeal (Ganap na Deterministic)

```javascript
// 1. Kalkulahin ang FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Kolektahin ang Forensic data (gumamit ng isang timestamp)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Bumuo ng isang timestamp
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // parehong timestamp
  };
  
  return { forensics, timestamp };
}

// 3. Buuin ang EvidenceRoot (gamit ang canonical encoding)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Gumawa ng NotarySeal (gumamit ng parehong timestamp)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Helper functions para sa masking (sumusuporta sa IPv4 at IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Suriin ang IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 o hindi kilalang format
  return "***";
}
```

### Mga Hakbang sa Verification (Dalawang Antas)

#### Quick Verify (Mabilis na Pagpapatunay)

```javascript
// I-verify lang ang file hash (mabilis na red flag)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Kunin mula sa Registry
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Ihambing ang Hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Orihinal - Tumugma ang File hash"
    };
  } else {
    return {
      valid: false,
      message: "❌ Peke - Binago ang file"
    };
  }
}
```

#### Full Verify (Buong Pagpapatunay)

```javascript
// Muling buuin ang EvidenceRoot at NotarySeal at i-verify
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Kunin mula sa Registry
  const cert = await fetchFromRegistry(certificateId);

  // 1) I-verify ang FileHash (mabilis na red flag)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Peke - Hindi tumugma ang File hash" };
  }

  // 2) Muling buuin ang EvidenceRoot (gamit ang forensics na naka-store sa registry)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Hindi tumugma - Hindi valid ang EvidenceRoot" };
  }

  // 3) Muling buuin ang NotarySeal (gamit ang parehong timestamp + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Hindi tumugma - Hindi valid ang NotarySeal" };
  }

  // Opsyonal: Sa Phase 2, i-verify din ang signer_sig gamit ang attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Hindi valid ang lagda" };

  return { valid: true, message: "✅ Orihinal - Pumasa ang Full Verify" };
}
```

> **Mahahalagang Nota:**
> - **Quick Verify:** I-verify lang ang file hash para sa mabilis na paggamit
> - **Full Verify:** I-verify ang lahat ng layer ng protokol (EvidenceRoot + NotarySeal)
> - Lahat ng hash operation ay ginagawa nang deterministic gamit ang fixed encoding at delimiters
> - **v1.0 canonicalization standard:** Fixed field order + UTF-8 encoding + `\n` delimiter
> - **Phase 2 plan:** Lilipat sa canonical JSON gamit ang RFC 8785 (JCS - JSON Canonicalization Scheme)
> - Sa Masked mode, ang pagkalkula ng EvidenceRoot at NotarySeal ay ginagawa gamit ang masked forensics
> - Isang timestamp lang ang ginagamit sa buong proseso (forensics + NotarySeal); ginagarantiya ang determinism
> - **Mga pangalan ng Forensics field:** `ip_masked`, `location`, `device`, `timestamp` (ganap na tumutugma ang code at registry)
> - **Registry path:** `certificate.asset.fingerprints` (ganap na tumutugma sa verify code)
> - **signer_sig sa Registry:** Ang field na `proof.signer_sig` ay kinakailangan para sa Full Verify
> - Ang mekanismo ng SignerSignature ay ia-activate sa Phase 2 gamit ang Solana Wallet Adapter; sa v1.0 ay maaaring i-verify gamit ang `attestation_pubkey`

---

## 📈 Mga Istatistika ng Paggamit (Target Q1 2026)

| Metric | Target | Status |
|--------|--------|--------|
| **Kabuuang Sertipiko** | 1,000 | 🔄 Nagpapatuloy |
| **Mga Aktibong User** | 500 | 🔄 Nagpapatuloy |
| **Bilang ng Verification** | 5,000 | 🔄 Nagpapatuloy |
| **Uptime** | 99.9% | ✅ Aktibo |
| **Avg Response Time** | <200ms | ✅ Optimal |

---

## 🌍 Komunidad at Suporta

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 Mga Contributor

Ang PoArt protocol ay patuloy na umuunlad sa kontribusyon ng open source community.

**Para mag-contribute:**
1. I-fork ang proyekto
2. Gumawa ng feature branch (`git checkout -b feature/amazing-feature`)
3. Mag-commit (`git commit -m 'Add amazing feature'`)
4. Mag-push (`git push origin feature/amazing-feature`)
5. Magbukas ng Pull Request

### 🛠️ Ano ang Kailangan Namin Ngayon? (Panawagan para sa Tulong)

Naghihintay kami ng kontribusyon mula sa mga may karanasang developer sa mga sumusunod na paksa para sa pagbuo ng **Phase 2** ng PoArt protocol:

* **Supabase Edge Functions:** Paglipat ng spam protection sa server side
* **Solana Web3.js:** Wallet Signing integration
* **IPFS / Arweave:** Archiving at pinning service integration

> Mangyaring magsimula ng talakayan sa "Issues" tab bago magdagdag ng feature

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Ang kultura ay mas malaki kaysa kapital*

## 🧾 Lisensya

MIT License © 2026 İlhan Art Gallery Initiative

Tingnan ang [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) para sa buong mga tuntunin

---

## 💬 Mga Kredito

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Ang proyektong ito ay binuo ng [İlhan Art Gallery] initiative at ang source code ay ibinubunyag sa publiko para sa transparency.**

**PROTOCOL V1.0 // NA-SEAL GAMIT ANG SHA-512**

*© 2026 İLHAN ART | Lahat ng karapatan ay nakalaan para sa mga gawa, imahe, at konsepto*

---
