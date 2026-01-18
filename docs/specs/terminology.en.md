# 📚 TERMINOLOGY & CONCEPTS GLOSSARY
> **"Understanding the language of this protocol means understanding its vision."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Core Infrastructure

**PoArt Forensic Engine (PFE)** is the core layer representing the fundamental logic and technical operation behind the [PoArt] protocol. This "forensic engine" takes raw production data from an artwork and transforms it into verifiable and immutable **digital evidence**.

### 🧩 Why "PoArt Forensic"?

- **PoArt (Proof of Art):** The engine's focus is to tie the value of a digital asset not to speculation, but to a **verifiable production process**.
- **Forensic (Forensic Verification):**
  - **Technical Definition:** An algorithmic and record-chain approach to verify that production process data (brush strokes, timelapse, logs) has not been manipulated.
  - **Philosophical Layer:** Against artificial intelligence's "instant output" production; the claim to transform human production containing **time, effort, and decision cost** into measurable reality.

> Note: Blockchain (e.g., Solana) integration is not the core of PFE; it will be handled separately as a **Chain Anchor Layer** for verification/registry purposes.

### 🛠️ v1.0 Technical Scope

**PoArt Forensic Engine (PFE) v1.0** is built on **3 main pillars** rather than complex financial models:

1. **Hashing & Sealing:**  
   PFE deterministically processes all elements within the Evidence Pack (artwork file, video, JSON/log, signature, etc.) to produce a unique **NotarySeal** value.

   **Core concepts (v1.0):**
   - **FileHash (artwork fingerprint):** Hash generated from the artwork file's bytes.
   - **EvidenceRoot (evidence package root):** Root digest representing the integrity of the Evidence Pack (Merkle root or canonical manifest hash).
   - **NotarySeal (final seal / PFE Output):** Final seal generated from EvidenceRoot + time + signature combination.

   **Formulas (clearly visible to investors):**
   
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
   
   > Note: The value referred to as PFE output is **NotarySeal**. The **SignerSignature** mechanism will be activated in Phase 2 (with Solana Wallet Adapter); in current v1.0, the system's own attestation signature is used. Attestation public key is published in the `issuer.attestation_pubkey` field in the registry.

2. **Indexing (Archiving):**  
   Records which wallet, on which date, submitted **Labor Proof** for which artwork; into a transparent and queryable record layer.  
   *(This layer can be a database; chain integration is separately defined as "Chain Anchor Layer".)*

3. **Verification:**  
   When an artwork's authenticity is questioned, PFE reprocesses the raw evidence; mathematically tests with certainty whether the calculated **EvidenceRoot / NotarySeal** values match the archive record.

---

### 🧮 PoArt Value Theorem (The Value Theorem)

The [PoArt] protocol relates the value ($V$) of a digital asset not to subjective market perception, but to the **physical reality of the production process**.

Artificial Intelligence (AI) delivers results instantly ($t \to 0$), destroying the process. [PoArt] treats value as the accumulation of **time, labor, and agency** components.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Variable Definitions

- **$\int dt$ (Process Accumulation):**  
  Value is not an instant "output"; it is a **process** accumulated between $t_{\text{start}}$ and $t_{\text{end}}$. As duration decreases (AI production), the integral result approaches 0.

- **$P_{\text{labor}}(t)$ (Instantaneous Labor Power):**  
  Represents the intensity of mental and physical effort expended at the moment of production. As provable effort increases, the integrand grows.  
  > Note: This term can practically be normalized through "measurable/provable labor signals."

- **$I_{\text{agency}}(t)$ (Agency Coefficient):**  
  The producer's capacity for risk-taking and decision-making. Takes a value between $0$ and $1$.
  - **AI ($I \approx 0$):** Executes commands, takes no risk, pays no cost.
  - **Human ($I \to 1$):** Changes decisions, hesitates, takes risks.

- **$U_{\text{irreversible}}$ (Irreversible Singularity):**  
  While undo (`Ctrl+Z`) is possible in digital production; in physical production (paint applied to canvas, chiseled marble, live broadcast gesture) there is no return. This **irreversibility** is an additional term that creates "singularity" (non-fungible character) in the artwork.

### 🔎 Case Analysis: AI "Instant Output" vs. Human "Proven Process"

The following scenario demonstrates how the **PoArt Value Theorem** works in practice and why AI productions score low in the [PoArt] standard.

#### Scenario A: Visual Production in 10 Seconds with AI

- **Duration ($\Delta t$):** $10$ seconds (virtually no process)
- **Labor Power ($P_{\text{labor}}$):** $1$ unit (only command writing)
- **Agency Coefficient ($I_{\text{agency}}$):** $0.01$ (no risk, no cost)
- **Irreversibility ($U_{\text{irreversible}}$):** $0$ (reversible / copyable)

**Result:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Commentary:** Even if the output is flawless; because the process was not experienced and contains no agency/risk, the [PoArt] value approaches $0$.

#### Scenario B: 6-Hour Physical Production in Live Broadcast

- **Duration ($\Delta t$):** $6$ hours ($21{,}600$ seconds)
- **Labor Power ($P_{\text{labor}}$):** $0.5$ units (continuity of physical and mental effort)
- **Agency Coefficient ($I_{\text{agency}}$):** $0.9$ (decision changes, risk-taking, irreversible choices)
- **Irreversibility ($U_{\text{irreversible}}$):** $>0$ (physical traces cannot be undone)

**Result:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Commentary:** As the process lengthens and agency (risk) increases, value accumulates cumulatively. The $U_{\text{irreversible}}$ term is an additional contribution that creates "singularity" (non-fungible character) in the artwork.

---

### ✅ Conclusion: Proof-Bound Value

This theorem removes [PoArt]'s value claim from being a "like" or "market narrative" and ties it to **provable production reality**.

1. **No Process, No Value:**  
   AI destroys the process in instant output ($t \to 0$). As the process window narrows, the integral result mathematically must shrink:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Agency and Risk Are Multipliers:**  
   [PoArt] measures not only "time spent" but also the real decision, risk, and cost layer during that time. A production with no risk (AI) has low value:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Singularity Is Physical Evidence, Not Marketing:**  
   Irreversible traces in physical production (canvas stroke, marble chip) are outside the `Ctrl+Z` logic of digital. This irreversibility ($U_{\text{irreversible}}$) ontologically singularizes the artwork.

> **🔐 SUMMARY:** Although the value theorem may seem uncertain as a measurement (even if 100% correspondence cannot be fully measured in real life), the purpose of this formula is to show the structure and direction of variables. In the AI age, what is rare is not "image" but **provable labor, time, and agency.** [PoArt] measures this scarcity and certifies it with **Evidence Pack**.

### 🏛️ Importance of the "Engine" Concept

Tokens emerging from Pump.fun or similar platforms are often merely **"access tickets"**. **PoArt Forensic Engine (PFE)** is the **constitutional logic layer** that determines what rights that ticket protects, how labor will be recorded, and how art/science/technology will be perpetuated.

> **Note:** The reason we launched this project on Pump.fun is that we did not have sufficient liquidity and follower count. Using existing data was strategically the most correct move, though not the highest quality. Regardless of budget and resources, defining this engine's logic on GitHub proves that the project is not just financial speculation, but a long-term **software infrastructure** and **digital national library** vision.

---

## 🎨 [PoArt] LABOR PROOF PROTOCOL (Proof of Art Protocol v1.0)

> **"Real Artist, Real Production, Real Value."**

This protocol is a **biological and intellectual defense mechanism** developed against anonymous scammers surrounding the crypto ecosystem, artificial intelligence visuals produced in 5 minutes, and "Pump & Dump" culture.

---

## a) What is [PoArt]? (Philosophical and Technical Definition)

**Proof of Art [PoArt];** is an institutional verification standard that guarantees that the value behind an asset on the blockchain is based not on speculation, but on verifiable **human labor**, **time**, and **physical energy**.

Just as Bitcoin generates value with *"Electricity and Processor Power"* **(Proof of Work)**; [PoArt] compliant projects generate value with *"Artistic Skill and Human Time"*.

It eliminates the *"Developer sold, project finished"* risk in Pump.fun and DEX platforms; because here value is not in the code but in **continuity of production**.

> **[PoArt] does not tell its participant "Trust us"; it says "Here is the evidence, see with your eyes, verify with your mathematics."**

---

## b) [PoArt] 5 Pillars Standard (The 5 Pillars of Truth)

These 5 items are non-manipulable filters that a project must pass to receive the [PoArt] seal.

### 1) Live Identity Proof

- **Problem:** The crypto world is full of anonymous founders (Devs) with unclear identities who collect money and abandon the project.
- **[PoArt] Solution:** The producer proves not just an ID card, but **presence at the moment of production**. This includes not pre-recorded videos, but live broadcast sessions where interaction with the community occurs and specific instant requests are fulfilled.  
  (Example: *"Write today's date and current block number on the right corner of the canvas"*)
- **Motto:** *"Bots can make pictures but bots don't sweat and can't improvise."*

### 2) Labor & Process Proof

- **Problem:** AI (Artificial Intelligence) visuals produced in 2 seconds and oil paintings made in 2 months receiving the same "jpeg" treatment in the digital world.
- **[PoArt] Solution:** The artwork's "pregnancy and birth" process is recorded. Sketch stages, paint layers, cumulative hours spent, and the physical process the artist experienced while creating that artwork are documented. This adds **"Time Cost"** to the token. The harder an asset's production, the more solid its value.

### 3) Aesthetic Value Proof

- **Problem:** "Meme" culture ignoring aesthetics and artistic depth, focusing only on instant comedy, resulting in short-lived "Hype" projects.
- **[PoArt] Solution:** The project must possess academic art standards, color theory, composition rules, and material knowledge (Impasto, Texture, etc.). Content should not just amuse; it should inspire admiration in the viewer and carry **collection value**.

### 4) Conceptual Novelty

- **Problem:** Thousands of dog/cat coins that are copies of each other, far from creativity.
- **[PoArt] Solution:** The project must build a new bridge that meaningfully combines art, science, philosophy, or technology.  
  (Example: Combining classical David sculpture with crypto market data; processing the idea of human perception "turning to stone" through this and grounding it with scientific sources.)  
  The artwork is not just a visual feast; it must also be an intellectual challenge that makes you think about **Science, Philosophy, or Technology**.

> [!IMPORTANT]
> **Reference Example (Las Palmitas Effect):**  
> In Mexico's crime-ridden Las Palmitas neighborhood, over 200 houses were transformed into a massive rainbow spectacle. As a result of this aesthetic intervention, crime rates in the neighborhood decreased to some extent, and young people began engaging with art instead of gangs. Aesthetic change recoded people's respect for their environment and each other (Social Cohesion).
>
> **Expectation:** A project entering the [PoArt] list must, like the example above, contain a sociological, scientific, or philosophical cause-effect relationship beyond pure visual aesthetics. Since "Time" is the only asset that cannot be purchased with money, in this protocol time must be staked and proven as collateral. The project's conceptual foundation must be so strong and universal that; years later, even in a possible CTO (Community Take Over) scenario, the community can take over this legacy and autonomously continue the project's innovative potential.

### 5) Non-Algorithmic Agency

- **Problem:** Perfect but soulless, repetitive digital productions.
- **[PoArt] Solution:** The human's unique agency that can err, take risks, and experience emotional fluctuations must be felt in the artwork. The uncertainty in brush strokes, unexpected material reactions, and the artist's instant decisions are the **Biological Signature** that distinguishes the artwork from "Machine Production".

---

## c) Verification & Anti-Fraud Mechanism

This system ensures the project remains reliable and alive not just "at the start" but "forever".

### 📦 Evidence Pack (The Digital Twin)

Behind each [PoArt] certified artwork is an encrypted and timestamped data package that investors can download:

- **RAW Video Recordings:** Uninterrupted raw footage of the production moment.
- **Metadata Analysis:** File creation date, device information used, and location data.
- **Physical References:** Evidence that the artwork exists in the physical world  
  (Example: Current newspaper standing next to the artwork or blockchain data at that moment).

> *Consistency note:* The "evidence pack" phrase connects to the **Evidence Pack → EvidenceRoot → NotarySeal** line in previous sections; meaning the package's integrity is represented by a verifiable seal.

### 🔄 365-Day Renewal (The Sustainability Protocol)

- **Revolutionary Feature:** In crypto projects, the "Dev" (Developer) releases the token to market and usually disappears after 1-2 months (Soft Rug). [PoArt] makes this impossible.
- **Rule:** "Verified Artist" status is not lifetime. It is only valid for **1 year**.
- **Operation:** Artist/Developer must present a **new, major, and provable artwork** to the community every 365 days.
- **Example Scenario:** You launched the project in 2026. In January 2027, the system gives "Proof Period Expired" warning. If the artist does not present a new exhibition, new physical artwork, or new technological integration, the project's "Trust Badge" drops.
- **Result:** This system ensures **content never loses its relevance** and the investor never experiences *"Is the developer still here?"* fear. The project becomes a living studio.

### 🚩 Red Flag Protocol

**In case of any fraud (AI use, stolen artwork, manipulated video) detected by the community or algorithms:**

1. Certificate is immediately marked as **"VOID"**.
2. Evidence packages are publicly labeled as **"Fake"**.
3. Project is added to [PoArt] blacklist. This reinforces the reality that in a decentralized world, **reputation is the only currency**.

---

## d) Conclusion: Not a Casino, a Museum

**Pump.fun and Decentralized Exchanges (DEX) are unfortunately casinos right now; lights flash, everyone chases quick gains, and the house (scammers) always wins. The reason we started the project here is lack of sufficient budget and having existing audience through live broadcasts.**

**[PoArt] is a fortress built in the middle of this casino.**

- 🎰 Casino is based on card games; we are based on **physical reality**.
- 🃏 Casino is open to cheating; we are open to **transparent evidence**.
- ⏳ Casino is temporary; we focus on **infinity of art and science**.

**A token using this protocol is not just a "coin"; it is a digital stock certificate containing sweat, paint, code, and philosophy behind it.**

---

## 🗳️ 6) GOVERNANCE & PUBLIC REGISTRY

**The purpose of this section is: To transform the [PoArt] standard from a "trust in people" plane into a sustainable public infrastructure with registration + verification + community oversight.**

### 6.1 Public Registry

- **Public Registry:** All approved data is recorded at `ilhanart.org/registry` (or GitHub Registry).

**Registry logic (recommended standard - JSON path format):**

Every record entering the registry carries these minimum verifiable core fields:

- **Identity & Status:**
  - `certificate_id` (readable reference)
  - `status` (active / void)
  - `void_reason` (if any)
  - `visibility` (private / masked / public)
  - `created_at` (timestamp)

- **Issuing Institution:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Artwork Information:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (if possible; for token holder identity)
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

The registry can have two layers:
- **1)** Human-readable index (web listing / search / filter)
- **2)** Machine-readable manifest (JSON records; for PFE verification)

**The "record" here becomes verifiable through PFE's Evidence Pack → EvidenceRoot → NotarySeal chain. The registry offers a verification target, not a "claim".**

---

### 6.2 PoArt Verified Application Process

**PoArt Verified applications are evaluated by İlhanArt Gallery according to 5 PoArt standards. Community feedback is considered, but the final decision belongs to the curatorial team. Decisions are explained transparently and recorded at ilhanart.org/registry.**

#### Application Process

**Application:**
- Artist/project submits PoArt Verified application
- Evidence Pack is prepared (video recordings, metadata, live broadcast links)
- Application is sent to İlhanArt Gallery

**Review (30 Days):**
- Gallery team examines Evidence Pack in detail
- All 5 PoArt standards are checked:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Artist interview (optional)

**Community Advisory:**
- Evidence Pack is publicly shared during the application process
- Token holders (minimum 10,000 $CULTURE) can especially make recommendations
- **All feedback is considered during the review process**
- **However, the final decision depends on curatorial evaluation**

**Decision:**
- Gallery approves or rejects the application
- Decision rationale is explained transparently
- If approved → PoArt Verified badge
- If rejected → Can reapply after 6 months

**Transparency:**
- All applications and decisions are recorded at ilhanart.org/registry
- Decision record is published publicly:
  - Application date
  - Review process summary
  - Decision (Approved / Rejected)
  - Decision rationale (brief explanation)
  - Community feedback summary (anonymous)

#### Why Curatorial Decision?

**Quality Control:**  
PoArt Verified status is a badge with high standards. Curatorial evaluation guarantees the preservation of these standards.

**Preventing Speculative Manipulation:**  
Full on-chain governance (e.g., Realms, DAO voting) with Pump.fun tokens is technically not possible. Off-chain voting systems are vulnerable to whale manipulation and coordinated attacks. Curatorial decision eliminates this risk.

**Operational Efficiency:**  
Fast and clear decision process instead of complex voting mechanisms. Artists receive results within 30 days.

**Community Participation:**  
Community feedback is fully considered and affects the decision process. However, the final decision belongs to the curatorial team protected from manipulation.

**Future:**  
Once the project matures (2027+), the community advisory mechanism can be strengthened. However, curatorial standard protection remains permanent.

---

### 6.3 Token Utility

**Benefits provided to $CULTURE token holders:**

**1. Gallery Events Priority Access:**
- İlhanArt Gallery physical exhibition openings
- Artist meetings and studio visits
- Private collection viewings

**2. PoArt Registry Full Access:**
- Detailed records of all authenticated artworks
- Full versions of Evidence Packs
- Forensic verification tools

**3. Advisory Voting:**
- Advisory rights in PoArt Verified applications
- Access to community feedback channels
- Participation in governance discussions

**4. Exclusive Content:**
- Studio behind-the-scenes content
- Artist interviews and process videos
- Technical documentation access

**Note:**  
Token holders provide advisory votes. Final decision belongs to the curatorial team. This structure is preferred to prevent whale manipulation and speculative attacks. There are no staking rewards because we seek long-term cultural participants, not short-term mercenary capital.

---

### 6.4 Metadata Sync (Physical World Alignment)

- **Metadata Sync:** Technical data in the registry must match 100% with the physical asset.

**Technically defining "100% match" (recommended clarity):**

- **Minimum match (mandatory):**
  - Registry's `asset.fingerprints.sha256/sha512` and the file's hash on hand must be **exactly the same**.
  - Registry's `proof.notary_seal` when reproduced (if Evidence Pack exists) must be **exactly the same**.

- **Physical reference match (evidence type):**
  - Physical artwork shown in live broadcast + date/block reference evidence must be consistent with Evidence Pack.

- **Privacy compliance:**
  - In `masked` visibility, fields like IP/location are published **in compliance with masking standard**.

---

### 6.5 Dispute & Revocation

The registry is not just an "approval" mechanism; it is a **living oversight mechanism against fraud**.

- When a dispute is initiated, the record can be put into **"review"** mode.
- If fraud is detected, it is marked as `status: void` and rationale is added:
  - `void_reason` (AI use / theft / manipulation, etc.)
  - `revoked_at` (revocation time)
- The source of the revocation decision is clearly visible in the registry:
  - curatorial review / community dispute / forensic analysis note (whichever applies)

> **This section is the registry counterpart of the VOID concept in the "Red Flag Protocol" section.**

---

### 6.6 Example Registry Record (Machine-readable)
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

> *Note: `asset.fingerprints.sha512` and other hash values are shortened for display purposes; in actual implementation, full-length hexadecimal character strings are used.*

---

## 7) 🔐 TECHNICAL SEAL (NOTARY SEAL)

**The unshakeable seal algorithm produced by PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Digital Notary & Forensic Evidence Protocol (Beta v1.0)

> **"Culture is greater than capital. Protect your artworks today, carry them to tomorrow."**

---

## Why Public?

Real security comes from transparency. Thanks to our **Public Registry** system, anyone anywhere in the world can verify whether the file they have is original within seconds, without needing any authority.

---

## 🧩 Why Multiple "Visibility Modules"?

This is the most critical part of the code (visibility select menu). These options allow users to balance **"Privacy vs. Transparency"**:

### 🔒 Private

- **Scenario:** The artist doesn't want to publish the artwork yet but wants to timestamp it to prove "I made this on this date".
- **What the Code Does:** Writes data to the database but stamps `visibility: "private"` tag. Later when writing "Public Read" policy, you can hide these records from the public by saying `WHERE visibility = 'public'`.

### 🕶️ Masked

- **Scenario:** The artist wants transparency but fears their home address (IP location) being found.
- **What the Code Does:** `maskIP` and `maskLoc` functions work on the JavaScript side. Converts IP address to `88.241.***.***` form, location to `***/TR` form, and sends the censored version to the database.
- **Privacy Note:** Masking is done in the browser; Supabase doesn't see the real location. **However:** If third-party APIs like ipapi.co are used for location data, these providers see the IP address at the time of request.
- **Sealing in Masked Mode:** EvidenceRoot and NotarySeal calculation is done with masked forensics data; thus verification remains deterministic.

### 🌍 Public

- **Scenario:** Full transparency. Per [PoArt] standard, where, when, from which network the artwork was produced is clearly declared.

---

## 💡 Technological Innovation

PoArt is not just a file upload system. It is a **"Forensic Chain of Custody"** engine that fuses three different technology layers in one pot and brings a new standard.

**The layer described as "engine" in this section corresponds to the PoArt Forensic Engine (PFE) core in previous terminology.**

### 1) Client-Side Hashing (Maximum Privacy)

Your artwork files are never uploaded to the server. Our browser-based (Client-side) engine calculates the file's hash (digital digest) on your own computer. Only this fingerprint and metadata are sent to the server.

> **Privacy Note:** The artwork file is not uploaded to the server and is thus protected. However, forensics data (IP/location) is shared according to the selected visibility mode (private/masked/public).

### 2) Forensic Data Fusion (Forensic Power)

It is much more than an ordinary timestamp. The system combines these data into a single "Genesis Seal":

- **Digital Digest (SHA-512):** Digital fingerprint that will break if even a single pixel of the artwork changes, using cryptographic digest (SHA-512) standard.
- **Location & Time:** Date with millisecond precision, country, city, and district data of where the transaction was made.
- **Device Identity:** Operating system, browser, and device type (User-Agent analysis).

---

## 🛡️ Use Cases and Benefits

If you are an artist, writer, or designer, saying "I made this before" is not enough, you need to prove it.

**An artwork you seal with PoArt:**

- **Mathematical Proof:** If even a single pixel of your file changes, the system understands. Manipulation is impossible.
- **Legal Basis:** At what date, in which city, from which device the artwork was sealed is on record.
- **Instant Certificate:** Generates a **"Asset Identity Certificate"** with QR code and seal, special to you, within seconds.

---

## ⚙️ System Architecture and Technical Features

The system is designed on a "Serverless" architecture, focused on high performance and scalability.

| Layer | Technology | Description |
|-------|-----------|-------------|
| **Cryptography** | SHA-256 & SHA-512 | Dual-layer cryptographic digest |
| **Database** | Supabase (PostgreSQL) | JSONB data structure, RLS policies |
| **Forensic Data** | ipapi.co API | IP/Location/Time trinity |
| **Rendering** | html2canvas + jsPDF | Client-side PNG/PDF generation |
| **Frontend** | Vanilla JavaScript | Zero framework dependency |
| **Security** | Client-side hashing | File never goes to server |

### Featured Capabilities

| Feature | Detail | In Competitors? |
|---------|--------|-----------------|
| **Drag & Drop UI** | File drag-drop, instant preview | ❌ Most don't have |
| **Multi-Format Export** | PNG, JSON, PDF - one click | ⚠️ Limited |
| **Real-Time Preview** | Live certificate preview | ❌ None |
| **Privacy Controls** | Private/Masked/Public options | ❌ None |
| **Client-Side Hashing** | File never goes to server | ✅ Only a few |
| **Forensic Metadata** | IP, location, device, time - all together | ❌ Fragmented |
| **QR Verification** | Instant verification QR code | ⚠️ Limited |
| **Rate Limiting** | Spam protection (RLS + Client) | ❌ Most don't have |

---

## 🗺️ Roadmap: "Trustless" Future

The current version **(Beta v1.0)** is optimized to provide end users maximum speed, easy interface, and free access. However, our ultimate vision is to transition to a structure where even the database administrator (us) cannot intervene.

### Phase 1: Beta v1.0 (Currently Live)

**Infrastructure:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + IPFS backup)
- Gallery self-attestation (centralized but transparent)

**Token:**
- Platform: Pump.fun
- Liquidity: Raydium (automatic)
- Governance: Advisory only (community advisory)

**Purpose:**
- Speed, remove UX barriers
- Provide "frictionless" security
- Community building

**Token Utility (v1.0):**
- Gallery events priority access
- PoArt Registry viewing
- Advisory voting rights

---

### 🚀 Phase 2: Decentralized Authority (2026 Q2-Q4)

This phase covers the transition from a fully "Client-Side" operating structure to a more secure and decentralized structure.

| Feature | What Does It Provide? | Tech Stack | ETA |
|---------|----------------------|------------|-----|
| **Edge Function INSERT** | Spam prevention + API Key security | Supabase Edge (Deno) | Q2 2026 |
| **Wallet Signature** | Decentralized identity | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | Decentralized archive | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | Fake certificate revocation | DB Schema Update | Q2 2026 |
| **Audit Log** | Forensic query record | Custom logs table | Q3 2026 |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain voting (x/web) + wallet signature
- Community representatives election (first 90 days)
- Multi-sig operations wallet control
- Weighted advisory voting (with whale cap)

**Immutability:**
- Registry backup with IPFS hashes
- Bitcoin timestamp anchoring
- Cross-chain verification preparation

---

### Phase 3: Full Decentralization (2027+)

| Feature | Goal | ETA |
|---------|------|-----|
| **On-Chain Registry** | Solana on-chain recording | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **DID Integration** | Decentralized Identity | Q3 2027 |
| **Community Governance** | Strengthened advisory system | Q4 2027 |
| **Legal Recognition** | Validity in Turkish courts | 2027-2028 |
| **API for Developers** | Public API endpoint | Q3 2027 |

**Governance Evolution:**
- v3.0: Hybrid model (curatorial + community weighted)
- 2028+: Full community governance (optional)
- Curatorial quality control always preserved

---

## 🧬 Protocol Data Structure (JSON Schema)

**Each [PoArt] certificate has a portable and verifiable JSON identity card produced in the following standard.**

> **Note:** This Identity JSON format is the certificate format presented to the user. In registry records, `registry.asset` is used instead of `identity.asset_data` (mapping: `identity.asset_data` == `registry.asset`).
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

## 🔬 Technical Depth: Seal Algorithm

### Deterministic Hash Functions
```javascript
// Helper Functions: Convert digest to hex string
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Convert string to byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Canonical forensics string generation (v1.0: fixed field order + UTF-8 + \n delimiter)
// Phase 2 note: Will transition to canonical JSON with RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal Production Process (Fully Deterministic)
```javascript
// 1. FileHash calculation (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Forensic data collection (single timestamp usage)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Single timestamp generation
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Same timestamp
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot creation (with canonical encoding)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal generation (using same timestamp)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Masking helper functions (IPv4 and IPv6 support)
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4 check
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 or unknown format
  return "***";
}
```

### Verification Flow (Two Levels)

#### Quick Verify (Fast Verification)
```javascript
// Only checks file hash (quick red flag)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Fetch from registry
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Hash comparison
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Original - File hash matches"
    };
  } else {
    return {
      valid: false,
      message: "❌ Fake - File has been manipulated"
    };
  }
}
```

#### Full Verify (Complete Verification)
```javascript
// Reproduces and verifies EvidenceRoot and NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Fetch from registry
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash check (quick red flag)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Fake - File hash doesn't match" };
  }

  // 2) Reproduce EvidenceRoot (with forensics stored in registry)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Mismatch - EvidenceRoot doesn't hold" };
  }

  // 3) Reproduce NotarySeal (with same timestamp + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Mismatch - NotarySeal doesn't hold" };
  }

  // Optional: In Phase 2, also verify signer_sig with attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Invalid signature" };

  return { valid: true, message: "✅ Original - Full Verify passed" };
}
```

> **Important Notes:**
> - **Quick Verify:** Only checks file hash for quick usage.
> - **Full Verify:** Verifies all protocol layers (EvidenceRoot + NotarySeal).
> - All hash operations are done deterministically, with fixed encoding and delimiters.
> - **v1.0 canonicalization standard:** Fixed field order + UTF-8 encoding + `\n` delimiter.
> - **Phase 2 plan:** Transition to canonical JSON with RFC 8785 (JCS - JSON Canonicalization Scheme).
> - In masked mode, EvidenceRoot and NotarySeal calculation is done with masked forensics.
> - Single timestamp is used throughout the process (forensics + NotarySeal); determinism is guaranteed.
> - **Forensics field names:** `ip_masked`, `location`, `device`, `timestamp` (code and registry fully compatible).
> - **Registry path:** `certificate.asset.fingerprints` (fully compatible with verify code).
> - **Registry signer_sig:** `proof.signer_sig` field is required for Full Verify.
> - SignerSignature mechanism will be activated in Phase 2 with Solana Wallet Adapter; in v1.0, verification can be done with `attestation_pubkey`.

---

## 📊 Competitor Analysis (Updated)

PoArt is positioned on the "Sweet Spot" that completes the deficiencies of existing solutions.

| Feature | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Cost** | 🆓 Free | 🆓 | 💰 Paid | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Very Easy | ❌ CLI | ⚠️ Medium | ⚠️ Medium | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Live | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Modes | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privacy | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Complete | ❌ | ❌ | ⚠️ Limited | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Instant | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Turkish Support** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Legend:**
- ✅ : Full support / available
- ⚠️ : Limited / in paid plans
- ❌ : None / not supported
- 🔄 : In roadmap (under development)
- 🆓 : Completely free
- 💰 : Paid / subscription required

### Competitors' Weaknesses, PoArt's Strengths

| Weakness | Competitors | PoArt |
|----------|-------------|-------|
| **Difficulty of Use** | CLI, API knowledge, wallet required | Drag-drop, done in 3 clicks |
| **Cost Barrier** | $50-500/month subscription | 100% free |
| **Privacy** | File uploaded to server | Client-side, file never goes |
| **Forensic Data** | Only timestamp | IP, location, device, time - all |
| **Turkish Support** | None or very limited | Native language support |
| **Open Source** | Black box | All code open on GitHub |

---

## 📈 Usage Statistics (2026 Q1 Targets)

| Metric | Target | Status |
|--------|--------|--------|
| **Total Certificates** | 1,000 | 🔄 In Progress |
| **Active Users** | 500 | 🔄 In Progress |
| **Verification Count** | 5,000 | 🔄 In Progress |
| **Uptime** | 99.9% | ✅ Active |
| **Avg Response Time** | <200ms | ✅ Optimal |

---

## 🌍 Community & Support

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Website:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Contributors

The PoArt protocol continues to evolve with contributions from the open-source community.

**To contribute:**
1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

### 🛠️ What Do We Need Right Now? (Call for Help)

For PoArt Protocol **Phase 2** developments, we are awaiting contributions from experienced developers in the following areas:

* **Supabase Edge Functions:** Moving spam protection to server-side.
* **Solana Web3.js:** Wallet Signing integration.
* **IPFS / Arweave:** Archive and pinning services integration.
* **Community Tools:** voting systems, analytics dashboard.

> Please start a discussion in the "Issues" tab before adding a feature.

---

## 💬 Final Notes

### Pump.fun and Reality

This project was launched on Pump.fun because:
- ✅ Liquidity access (Raydium automatic migration)
- ✅ Existing community access
- ✅ Low startup cost

However, let's clarify:
- **Token price** is not an indicator of artistic success
- Token value is important for **operational budget** (gallery, exhibitions, infrastructure)
- **Success metrics:** Authenticated artworks + community engagement + physical visitors

### Governance and Decentralization

**v1.0 Reality (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (centralized but transparent)
- Governance: Advisory only (curatorial final decision)

**v2.0+ Vision (2027+):**
- Registry: On-chain (Solana)
- Signatures: Wallet-based (decentralized)
- Governance: Hybrid (community advisory + curatorial quality)
- Token utility: Enhanced features + advanced access

This structure provides **operational efficiency** and **quality control** in early stages while keeping the path open to increase **community participation** in the future.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital"*

## 🧾 License

MIT License © 2026 İlhan Art Gallery Initiative

See [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) for full terms.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**This project has been developed by [İlhan Art Gallery] initiative, and the source codes are publicly available for transparency.**

**PROTOCOL V1.0 // SEALED WITH SHA-512.**

*© 2026 İLHAN ART | ALL RIGHTS RESERVED FOR ARTWORKS, VISUALS, AND IDEAS.*

---
