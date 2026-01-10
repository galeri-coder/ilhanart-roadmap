# 📚 TERMINOLOGY & CONCEPTS GLOSSARY
> **"To understand the language of this protocol is to understand its vision."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Core Infrastructure

**PoArt Forensic Engine (PFE)** is the main layer representing the core logic and technical operation behind the [PoArt] protocol. This is the "forensic engine" that takes the raw production data of an artwork and transforms it into verifiable and immutable **digital evidence**.

### 🧩 Why "PoArt Forensic"?

- **PoArt (Proof of Art):** The engine's focus is to tie the value of a digital asset not to speculation, but to a **provable production process**.
- **Forensic (Forensic Verification):**
  - **Technical Definition:** An algorithm and chain-of-custody approach aimed at verifying that production process data (brush strokes, timelapse, logs) has not been manipulated.
  - **Philosophical Layer:** Against AI's "instant output" production; the claim of transforming **human production containing time, effort, and decision cost** into measurable reality.

> Note: Blockchain integration (e.g., Solana) is not the core of PFE; it is treated as a separate **Chain Anchor Layer** to be defined for verification/registry purposes.

### 🛠️ v1.0 Technical Scope

**PoArt Forensic Engine (PFE) v1.0** is built on these **3 main pillars** instead of complex financial models:

1. **Hashing & Sealing:**  
   PFE deterministically processes all items in the Evidence Pack (artwork file, video, JSON/log, signature, etc.) to produce the unique **NotarySeal** value.

   **Core concepts (v1.0):**
   - **FileHash (artwork fingerprint):** Hash generated from the bytes of the artwork file.
   - **EvidenceRoot (evidence pack root):** Root digest representing the integrity of the Evidence Pack (Merkle root or canonical manifest hash).
   - **NotarySeal (final seal / PFE Output):** The final seal generated from the combination of EvidenceRoot + time + signature.

   **Formulas (clearly visible to investors):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   > Note: The value referred to as PFE output is **NotarySeal**. (The previous naming "Sol Ate Output" has been mapped to **NotarySeal** here.)

2. **Indexing (Archiving):**  
   Records which wallet, on which date, submitted **Labor Proof** for which artwork to a transparent and queryable registry layer.  
   *(This layer can be a database; chain integration is separately defined as "Chain Anchor Layer".)*

3. **Verification:**  
   When an artwork's authenticity is questioned, PFE reprocesses raw evidence; mathematically tests whether the calculated **EvidenceRoot / NotarySeal** values match the archive record.

---

### 🧮 PoArt Value Theorem (The Value Theorem)

The [PoArt] protocol relates the value of a digital asset ($V$) not to subjective market perception, but to the **physical reality of the production process**.

Artificial Intelligence (AI) destroys the process by delivering results instantly ($t \to 0$). [PoArt] treats value as the accumulation of **time, labor, and will** components.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Variable Definitions

- **$\int dt$ (Process Accumulation):**  
  Value is not an instant "output"; it is a **process** accumulated between $t_{\text{start}}$ and $t_{\text{end}}$. As duration decreases (AI production), the integral result approaches 0.

- **$P_{\text{labor}}(t)$ (Instantaneous Labor Power):**  
  Represents the intensity of mental and physical effort expended at the moment of production. As provable effort increases, the integrand grows.  
  > Note: This term can be normalized in practice through "measurable/provable labor signals".

- **$I_{\text{agency}}(t)$ (Will Coefficient):**  
  The producer's capacity for risk-taking and decision-making. Takes a value between $0$ and $1$.
  - **AI ($I \approx 0$):** Executes commands, takes no risk, pays no cost.
  - **Human ($I \to 1$):** Changes decisions, hesitates, takes risks.

- **$U_{\text{irreversible}}$ (Irreversible Singularity):**  
  While undo (`Ctrl+Z`) is possible in digital production; in physical production (paint applied to canvas, carved marble, gestures in live broadcast) there is no return. This **irreversibility** is an additional term that creates "singularity" (non-fungible character) in the work.


### 🔎 Case Analysis: AI "Instant Output" vs. Human "Proven Process"

The following scenario shows how the **PoArt Value Theorem** works in practice and why AI productions score low in the [PoArt] standard.

#### Scenario A: Visual Production with AI in 10 Seconds

- **Duration ($\Delta t$):** $10$ seconds (virtually no process)
- **Labor Power ($P_{\text{labor}}$):** $1$ unit (only command writing)
- **Will Coefficient ($I_{\text{agency}}$):** $0.01$ (no risk, no cost)
- **Irreversibility ($U_{\text{irreversible}}$):** $0$ (reversible / copyable)

**Result:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Interpretation:** Even if the output is flawless; because no process was experienced and it contains no will/risk, the [PoArt] value approaches $0$.

#### Scenario B: 6-Hour Physical Production on Live Broadcast

- **Duration ($\Delta t$):** $6$ hours ($21{,}600$ seconds)
- **Labor Power ($P_{\text{labor}}$):** $0.5$ unit (continuity of physical and mental effort)
- **Will Coefficient ($I_{\text{agency}}$):** $0.9$ (decision changes, risk-taking, irreversible choices)
- **Irreversibility ($U_{\text{irreversible}}$):** $>0$ (physical traces cannot be undone)

**Result:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Interpretation:** As the process lengthens and will (risk) increases, value accumulates cumulatively. The $U_{\text{irreversible}}$ term is an additional contribution that creates "singularity" (non-fungible character) in the work.

---

### ✅ Conclusion: Proof-Bound Value

This theorem removes [PoArt]'s value claim from being a "like" or "market narrative" and ties it to a **provable production reality**.

1. **No Value Without Process:**  
   AI destroys the process in instant output ($t \to 0$). As the process window narrows, the integral result shrinks as a mathematical necessity:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Will and Risk are Multipliers:**  
   [PoArt] measures not only "time spent" but also the real decision, risk, and cost layer during that time. The value of production without risk (AI) is low:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Singularity is Physical Evidence, Not Marketing:**  
   Irreversible traces in physical production (canvas stroke, marble crack) are outside the `Ctrl+Z` logic of digital. This irreversibility ($U_{\text{irreversible}}$) ontologically singularizes the work.

> **🔐 SUMMARY:** Although the value theorem may seem uncertain as a measurement (even if its 100% equivalent cannot be fully measured in real life), the purpose of this formula is to show the design and direction of variables. What is rare in the AI age is not "image"; it is **provable labor, time, and will.** [PoArt] measures this scarcity and registers it with **Evidence Pack**.

### 🏛️ The Importance of "Engine" Concept

Tokens from Pump.fun or similar platforms are often merely **"access tickets."** **PoArt Forensic Engine (PFE)** is the **constitutional logic layer** that determines what rights that ticket protects, how labor is recorded, and how art/science/technology is immortalized.

> **Note:** The reason we started this project on Pumpfun is that we don't have sufficient liquidity and follower count. Using existing data was strategically not the highest quality but we can say it was the right move. Regardless of budget and resources, defining this engine's logic on GitHub proves that the project is not just financial speculation, but a long-term **software infrastructure** and **digital national library** vision.

---

## 🎨 [PoArt] PROOF OF LABOR PROTOCOL (Proof of Art Protocol v1.0)

> **"Real Artist, Real Production, Real Value."**

This protocol is a **biological and intellectual defense mechanism** developed against anonymous scammers plaguing the crypto ecosystem, AI images produced in 5 minutes, and the "Pump & Dump" culture.

---

## a) What is [PoArt]? (Philosophical and Technical Definition)

**Proof of Art [PoArt];** is an institutional verification standard that guarantees that the value behind an asset on the blockchain is based not on speculation, but on verifiable **human labor**, **time**, and **physical energy**.

Just as Bitcoin produces value through *"Electricity and Processing Power"* **(Proof of Work)**; [PoArt] compliant projects produce value through *"Artistic Talent and Human Time."*

It eliminates the *"Developer (Dev) sold, project ended"* risk on Pump.fun and DEX platforms; because here the value lies not in code, but in the **continuity of production**.

> **[PoArt] doesn't say "Trust us" to its participants; it says "Here are the proofs, see with your eyes, verify with your mathematics."**

---

## b) [PoArt] 5 Standards (The 5 Pillars of Truth)

These 5 items are non-manipulable filters that a project must pass to receive the [PoArt] seal.

### 1) Live Identity Proof

- **Problem:** The crypto world is full of anonymous founders (Devs) whose identities are unknown, who collect money and abandon the project.
- **[PoArt] Solution:** The producer proves not only their ID, but their **presence at the moment of production**. This includes live broadcast sessions where specific instant requests are fulfilled while interacting with the community, not with pre-recorded videos.  
  (E.g., *"Write today's date and current block number on the right corner of the canvas"*)
- **Motto:** *"Bots can paint, but bots don't sweat and can't improvise."*

### 2) Labor & Process Proof

- **Problem:** AI images produced in 2 seconds and oil paintings made in 2 months receiving the same "jpeg" treatment in the digital world.
- **[PoArt] Solution:** The "pregnancy and birth" process of the artwork is recorded. Sketch stages, paint layers, cumulative hours spent, and the physical process the artist went through while creating that work are documented. This adds **"Time Cost"** to the token. The harder the production of an asset, the stronger its value.

### 3) Aesthetic Value Proof

- **Problem:** "Meme" culture ignoring aesthetics and artistic depth, focusing only on instant comedy, resulting in short-lived "Hype" projects.
- **[PoArt] Solution:** The project must have academic art standards, color theory, composition rules, and material knowledge (Impasto, Texture, etc.). Content should not only make people laugh; it should inspire admiration and carry **collection value**.

### 4) Conceptual Novelty

- **Problem:** Thousands of dog/cat coins that are copies of each other, far from creativity.
- **[PoArt] Solution:** The project must build a new bridge that combines art, science, philosophy, or technology in a meaningful structure.  
  (E.g., Combining the classical David statue with crypto market data; processing the idea of human perception "turning to stone" and being able to base this on scientific sources.)  
  The work should be not only a visual feast but also an intellectual challenge that makes one think about **Science, Philosophy, or Technology**.

> [!IMPORTANT]
> **Reference Example (Las Palmitas Effect):** In Las Palmitas neighborhood in Mexico, struggling with crime, more than 200 houses were transformed into a giant rainbow celebration. As a result of this aesthetic intervention, crime rates in the neighborhood dropped to a certain extent, and young people began to engage with art instead of gangs. Aesthetic change has recoded people's respect for their environment and each other (Social Cohesion).
>
> **Expectation:** A project entering the [PoArt] list; just like in the example above, should contain a sociological, scientific, or philosophical cause-and-effect relationship beyond mere visual aesthetics. Since the only asset that cannot be bought with money is "Time," in this protocol, time must be staked and proven as collateral. The intellectual foundation of the project must be so strong and universal that; even in a possible CTO (Community Take Over) scenario years later, the community can inherit this legacy and autonomously continue the project's innovative potential.

### 5) Non-Algorithmic Agency

- **Problem:** Perfect but soulless, repetitive digital productions.
- **[PoArt] Solution:** The unique will of humans who can make mistakes, take risks, and experience emotional fluctuations should be felt in the work. The uncertainty in brush strokes, unexpected reactions of materials, and the artist's instant decisions are the **Biological Signature** that separates the work from "Machine Production."

---

## c) Verification & Anti-Counterfeiting Mechanism

This system ensures that the project remains reliable and alive not only "at the beginning" but "forever."

### 📦 Evidence Pack - The Digital Twin

Behind every [PoArt] certified artwork, there is an encrypted and timestamped data package that investors can download:

- **RAW Video Recordings:** Uninterrupted raw footage of the production moment.
- **Metadata Analysis:** File creation date, device information used, and location data.
- **Physical References:** Evidence that the work exists in the physical world  
  (E.g., Current newspaper next to the work or blockchain data at that moment).

> *Consistency note:* The "evidence pack" expression connects to the **Evidence Pack → EvidenceRoot → NotarySeal** chain in previous sections; i.e., the integrity of the pack is represented by a verifiable seal.

### 🔄 365-Day Renewal (The Sustainability Protocol)

- **Revolutionary Feature:** In crypto projects, the "Dev" (Developer) launches the token and usually disappears 1-2 months later (Soft Rug). [PoArt] makes this impossible.
- **Rule:** "Verified Artist" status is not lifetime. It is only valid for **1 year**.
- **Operation:** The artist/developer must present a **new, large, and provable work** to the community every 365 days.
- **Example Scenario:** You launched the project in 2026. In January 2027, the system gives a "Proof Period Expired" warning. If the artist does not present a new exhibition, a new physical work, or a new technological integration, the project's "Trust Badge" drops.
- **Result:** This system ensures that **content never becomes outdated** and the investor never experiences the fear of *"Is the developer still here?"*. The project becomes a living studio.

### 🚩 Red Flag Protocol

**In case of any counterfeiting (AI use, stolen work, manipulated video) detected by the community or algorithms:**

1. The certificate is immediately marked as **"VOID"**.
2. Evidence packages are publicly labeled as **"Fake"**.
3. The project is blacklisted from [PoArt]. This reinforces the reality that **reputation is the only currency** in a decentralized world.

---

## d) Conclusion: Not a Casino, a Museum

**Pump.fun and Decentralized Exchanges (DEX) are unfortunately casinos right now; lights flash, everyone chases quick gains, and the house (scammers) always wins. The reason we started the project here is that we don't have enough budget and we have an environment that will reach the existing audience through live broadcasts.**

**[PoArt] is a castle built in the middle of this casino.**

- 🎰 Casinos rely on card games; we rely on **physical reality**.
- 🃏 Casinos are open to cheating; we are open to **transparent evidence**.
- ⏳ Casinos are temporary; we focus on **the eternity of art and science**.

**A token using this protocol is not just a "coin"; it is a digital stock that contains sweat, paint, code, and philosophy behind it.**

---

## 🗳️ 6) GOVERNANCE AND PUBLIC REGISTRY

**The purpose of this section is: To transform the [PoArt] standard from a "trust in people" plane into a sustainable public infrastructure with registry + verification + community oversight.**

### 6.1 Public Registry

- **Public Registry:** All approved data is recorded at `ilhanart.org/registry` (or GitHub Registry).

**Registry logic (proposed standard):**
- Each record entering the registry carries minimum these verifiable core fields:
  - `certificate_id` (readable reference)
  - `notary_seal` (final seal; PFE output)
  - `evidence_root` (evidence pack root)
  - `file_sha256` / `file_sha512` (artwork file fingerprint)
  - `creator` (text name) + if possible `creator_wallet` (for token-gated identity)
  - `created_at` (timestamp)
  - `status` (active / void) + `void_reason` (if applicable)
  - `visibility` (private / masked / public)
- The registry can have two layers:
  - **1)** Human-readable index (web listing / search / filter)
  - **2)** Machine-readable manifest (JSON records; for PFE verification)

**The "record" here becomes verifiable with PFE's Evidence Pack → EvidenceRoot → NotarySeal chain. The registry offers a verification target, not a "claim".**

---

### 6.2 40% Community Veto (Token-Gated Governance)

- **40% Community Veto:** Voting begins one month before status is gained; **Token-Gated (Solana-Verified)** community's 40% objection invalidates the application.

**Voting flow (proposed clear process):**
- **Application window:** Candidate project opens "PoArt candidate registration" (candidate records appear in "pending" status).
- **Review period:** Community reviews evidence for 30 days (Evidence Pack + live broadcast recordings + metadata).
- **Token-gated verification:** Voting is done with Solana-verified wallets (e.g., specific token/NFT ownership + wallet signature).
- **Veto rule:** If 40% of votes are **objection (NO / VETO)**, the application is rejected.
- **Transparency:** Voting result is stored in the registry as "decision record" (date, ratio, snapshot ID).

---

### 6.3 Metadata Sync (Physical World Matching)

- **Metadata Sync:** Technical data in the registry must match the physical asset 100%.

**Technically defining "100% match" (proposed clarity):**
- **Minimum match (mandatory):**
  - The `file_sha256/sha512` in the registry and the hash of the file at hand must be **exactly the same**.
  - When the `notary_seal` in the registry is regenerated (if Evidence Pack exists), it must be **exactly the same**.
- **Physical reference match (evidence type):**
  - Evidence such as physical work shown in live broadcast + date/block reference must be consistent with Evidence Pack.
- **Privacy compliance:**
  - In `masked` visibility, fields like IP/location are published **according to masking standard**.

---

### 6.4 Dispute, Review, and Revocation

The registry is not only an "approval" mechanism; it is a **living oversight mechanism against counterfeiting**.

- When a dispute is initiated, the record can be put in **"review"** mode.
- If counterfeiting is detected, it is marked as `status: void` and reason is added:
  - `void_reason` (AI use / stolen / manipulation, etc.)
  - `revoked_at` (revocation time)
- The source of the revocation decision is clearly visible in the registry:
  - community voting / authorized board / forensic review note (whichever applies)

> **This section is the registry counterpart of the VOID concept in the "Red Flag Protocol" section.**

---

### 6.5 Sample Registry Record (Machine-readable)

```json
{
  "certificate_id": "POART-AB12CD34",
  "status": "active",
  "visibility": "masked",
  "created_at": "2026-01-09T12:34:56.000Z",
  "asset": {
    "title": "Untitled",
    "creator": "Anonymous",
    "file_sha256": "e4123f83b44a409d7a43f0897837876dfabb3320db63dadbb34c54281f38a6ba",
    "file_sha512": "41e5e0d007a2a77b6e0e3ebc548fbaa2788ea265193434f58d23e8c0f5bb20a0..."
  },
  "proof": {
    "evidence_root": "7f8a9b2c...",
    "notary_seal": "9d3e5a1f..."
  },
  "governance": {
    "decision": "approved",
    "veto_threshold": 0.40
  }
}
```

---

## 7) 🔐 TECHNICAL SEAL (NOTARY SEAL)

Unshakeable seal algorithm produced by **PoArt Forensic Engine (PFE) v1.0**:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Digital Notary & Forensic Evidence Protocol (Beta v1.0)

> **"Culture is greater than capital. Protect your works today, carry them to tomorrow."**

---

## Why Public?

Real security comes from transparency. Thanks to our **Public Registry** system, anyone anywhere in the world can verify within seconds whether the file in their hand is original, without needing any authority.

---

## 🧩 Why Multiple "Visibility Modules"?

This is the most critical part of the code (visibility select menu). These options allow users to balance **"Privacy vs. Transparency"**:

### 🔒 Private

- **Scenario:** The artist doesn't want to publish the work yet but wants to timestamp it and prove "I made this on this date."
- **What the Code Does:** Writes data to the database but stamps `visibility: "private"`. Later, when writing "Public Read" policy, you can hide these records from the public by saying `WHERE visibility = 'public'`.

### 🕶️ Masked

- **Scenario:** The artist wants transparency but is afraid of their home address (IP location) being found.
- **What the Code Does:** `maskIP` and `maskLoc` functions run on the JavaScript side. Converts IP address to `88.241.***.***` format, location to `***/Turkey` format, and sends the censored version to the database.
- **Security:** This is very clever because censorship is done in the user's browser, not on the server. So even Supabase can't see the real location.

### 🌍 Public

- **Scenario:** Full transparency. According to the [PoArt] standard, where, when, and from which network the work was produced is clearly declared.

---

## 💡 Technological Innovation

PoArt is not just a file upload system. It is a **"Forensic Chain of Custody"** engine that brings a new standard by melting three different technology layers in one pot.

**The layer described as "engine" in this section corresponds to the PoArt Forensic Engine (PFE) core in previous terminology.**

### 1) Client-Side Hashing (Maximum Privacy)

Your files are never uploaded to the server. Our browser-based (Client-side) engine calculates the hash (digital summary) of the file on your own computer. Only this fingerprint and metadata are sent to the server. **Your privacy is 100% protected.**

> **The "never uploaded to server" statement is valid for the artwork file; fields needed for the system's verification/registry needs (hash + metadata) are evaluated separately.**

### 2) Forensic Data Fusion

It's much more than an ordinary timestamp. The system combines the following data in a single "Genesis Seal":

- **Digital DNA (SHA-512):** Military-standard cryptographic signature that will break even if a single pixel of the work changes.
- **Location & Time:** Millisecond-precise date, country, city, and district data when the transaction was made.
- **Device ID:** Operating system, browser, and device type (User-Agent analysis).

---

## 🛡️ Use Cases and Benefits

If you're an artist, writer, or designer, saying "I did this before" is not enough, you need to prove it.

**A work sealed with PoArt:**

- **Mathematical Proof:** The system detects even if a single pixel of your file changes. Manipulation is impossible.
- **Legal Basis:** It is on record which date, which city, which device the work was sealed from.
- **Instant Certificate:** Produces a custom **"Asset Identity Certificate"** with QR code and seal in seconds.

---

## ⚙️ System Architecture and Technical Features

The system is designed on a "Serverless" architecture, focused on high performance and scalability.

| Layer | Technology | Description |
|-------|------------|-------------|
| **Cryptography** | SHA-256 & SHA-512 | Dual-layer hashing - military standard |
| **Database** | Supabase (PostgreSQL) | JSONB data structure, RLS policies |
| **Forensic Data** | ipapi.co API | IP/Location/Time triad |
| **Rendering** | html2canvas + jsPDF | Client-side PNG/PDF production |
| **Frontend** | Vanilla JavaScript | Zero framework dependency |
| **Security** | Client-side hashing | File never uploaded to server |

### Highlighted Features

| Feature | Detail | In Competitors? |
|---------|--------|-----------------|
| **Drag & Drop UI** | File drag-drop, instant preview | ❌ Most don't have |
| **Multi-Format Export** | PNG, JSON, PDF - one click | ⚠️ Limited |
| **Real-Time Preview** | Live certificate preview | ❌ None |
| **Privacy Controls** | Private/Masked/Public options | ❌ None |
| **Client-Side Hashing** | File never goes to server | ✅ Only a few |
| **Forensic Metadata** | IP, location, device, time - all in one | ❌ Fragmented |
| **QR Verification** | Instant verification QR code | ⚠️ Limited |
| **Rate Limiting** | Spam protection (RLS + Client) | ❌ Most don't have |

---

## 🗺️ Roadmap: "Trustless" Future

The current version **(Beta v1.0)** is optimized to provide maximum speed, easy interface, and free access to end users. However, our ultimate vision is to transition to a structure where even the database administrator (us) cannot intervene.

### Phase 1: Beta (Currently Live)

- **Infrastructure:** Cloud Database (Supabase).
- **Purpose:** Speed, removing UX (User Experience) barriers and adaptation. Providing "frictionless" security.

### 🚀 Phase 2: (Requiring Backend / Edge Function)

This phase covers the transition from the system's completely "Client-Side" working structure to a more secure and manageable "Server-Side Authority" structure.

| Item | What Does It Gain? | Tech Stack | Priority |
|------|-------------------|------------|----------|
| **`INSERT` → Edge Function** | Spam prevention + API Key security | Supabase Edge (Deno) | 🔴 High |
| **Wallet Signature** | Cryptographic identity verification | Solana Wallet Adapter | 🟡 Medium |
| **IPFS/Arweave Backup** | Decentralized immutability | IPFS SDK + Pinata | 🟢 Low |
| **Revocation Mechanism** | Fake certificate cancellation | DB Schema Update | 🔴 High |
| **Audit Log** | Forensic query record | Custom logs table | 🟡 Medium |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | 🟢 Low |
| **DID Integration** | Decentralized Identity | ION/Ceramic | 🟢 Low |

### Phase 3: Full Decentralization (Long Term)

| Feature | Target | ETA |
|---------|--------|-----|
| **Blockchain Registry** | Ethereum/Solana on-chain record | Q4 2026 |
| **DAO Governance** | Community management | Q1 2027 |
| **Multi-Chain Support** | Polygon, Arbitrum, Base | Q2 2027 |
| **Legal Recognition** | Validity in Turkish courts | 2027-2028 |
| **API for Developers** | Public API endpoint | Q3 2026 |

---

## 📊 Competitor Analysis (Updated)

PoArt is positioned on the "Sweet Spot" that completes the gaps of existing solutions.

| Feature | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Cost** | 🆓 Free | 🆓 | 💰 Paid | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Very Easy | ❌ CLI | ⚠️ Medium | ⚠️ Medium | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Live | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Modes | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privacy | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Full | ❌ | ❌ | ⚠️ Limited | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Instant | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Turkish Support** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Legend:**
- ✅ : Full support / available
- ⚠️ : Limited / in paid plans
- ❌ : None / not supported
- 🔄 : On Roadmap (in development)
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
| **Open Source** | Closed box | All code open on GitHub |

---

## 🧬 Protocol Data Structure (JSON Schema)

**Each [PoArt] certificate has a portable and verifiable JSON identity card produced in the following standard.**

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
    "origin_ip_masked": "46.1.***.***",
    "device_signature": "Brave (Windows;Monster,Tulpar)...",
    "location": "Istanbul, TR"
  }
}
```

---

## 🔬 Technical Depth: Seal Algorithm

### NotarySeal Production Process

```javascript
// 1. FileHash calculation (client-side)
const fileBuffer = await file.arrayBuffer();
const sha256 = await crypto.subtle.digest('SHA-256', fileBuffer);
const sha512 = await crypto.subtle.digest('SHA-512', fileBuffer);

// 2. Forensic data collection
const forensics = {
  ip: await fetch('https://ipapi.co/json/').then(r => r.json()),
  device: navigator.userAgent,
  timestamp: new Date().toISOString()
};

// 3. EvidenceRoot creation
const evidenceRoot = sha512(
  fileHash + forensics.ip + forensics.timestamp
);

// 4. NotarySeal production
const notarySeal = sha512(
  evidenceRoot + signerSignature + timestamp
);
```

### Verification Flow

```javascript
// 1. User re-hashes the file
const userFileHash = sha512(file);

// 2. Original hash is fetched from system
const { sha512: originalHash } = await fetchFromRegistry(certId);

// 3. Mathematical comparison
if (userFileHash === originalHash) {
  return "✅ Original - Unmodified";
} else {
  return "❌ Fake - File has been manipulated";
}
```

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
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 Contributors

The PoArt protocol continues to develop with contributions from the open source community.

**To contribute:**
1. Fork
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit (`git commit -m 'Add amazing feature'`)
4. Push (`git push origin feature/amazing-feature`)
5. Open Pull Request

### 🛠️ What Do We Need Right Now? (Call for Help)

We are waiting for contributions from experienced developers on the following topics for PoArt Protocol **Phase 2** developments:

* **Supabase Edge Functions:** Moving spam protection to server side.
* **Solana Web3.js:** Wallet Signing integration.
* **IPFS / Arweave:** Archiving and pinning services integration.

> Please start a discussion in the "Issues" tab before adding a feature.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Culture is Greater Than Capital*

## 🧾 License

MIT License © 2026 İlhan Art Gallery Initiative

See [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) for full terms.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**This project has been developed with the [İlhan Art Gallery] initiative, and source codes are publicly available for transparency.**

**PROTOCOL V1.0 // SEALED WITH SHA-512.**

*© 2026 İLHAN ART | ALL RIGHTS RESERVED FOR WORKS, VISUALS, AND IDEAS.*

---
