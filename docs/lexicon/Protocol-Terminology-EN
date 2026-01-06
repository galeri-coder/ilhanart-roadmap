# 📜 Protocol Terminology & Technical Lexicon
> **Protocol Version:** 1.0 (Stable)  
> **Network Vision:** 2025 → 3000 Archive  
> **Ecosystem:** [PoArt] + [FPP]  
> **Status:** **HARD_LOCKED** (Active Documentation)  
> **Integrity:** SHA-512 Sealed (Digital Notary Compatible)

---

## Table of Contents
1. Pillars of the Protocol  
2. Roles & Entities  
3. Economic & Governance Metrics  
4. Security & Validation  
5. Validation & Persistence  
6. Decentralized Supervision  
7. The Michelangelo Framework (Meritocracy Engine)  
8. Cultural Multipliers & Ranking Levels  
9. Cut-off Thresholds & Network Metrics  
10. Intellectual Framework  
11. Advanced Sybil Resistance  
12. Generational Legacy & Governance  
13. Cultural Privilege Layers & Real-World Integration  
14. State Machine (Record Lifecycle)  
15. Minimal On-chain / Maximal Off-chain  
16. Appeals / Authority & Objection Mechanism (Institutional Trust Layer)  
17. Threat Model (Attack Catalog and Counter-Layers)  
18. Final Word: A Blueprint for Global Governance (Manifesto)  
19. Roadmap & Future Notes

---

## 🏛️ 1) Pillars of the Protocol

### **[PoArt] Proof of Art (v1.0)**
* **Definition:** The core protocol that verifies not only the final outcome of an artwork, but the entire **creation process** with technical data.  
* **Problem It Solves:** With the rise of Generative AI tools, real human labor becomes hard to prove in digital space and art’s “meta” value erodes.  
* **How It Works:** While creating the piece, the artist submits an **Evidence Pack** that covers every stage. The protocol seals this data with timestamps on-chain.  
* **Example Scenario:** If an artist creates a 40-hour impasto painting, the broadcast logs of those 40 hours, timelapse recordings of brush strokes, and digital fingerprints pass through the [PoArt] filter. Not only the “finished painting”, but the “40 hours of human effort” behind it is registered.

---

### **[FPP] Foundational Pillar Protocol (v1.0)**
* **Definition:** The main system that builds the ecosystem’s economic, governance, and social “load-bearing columns” (pillars) and rewards loyalty, continuity, and long-term participation.  
* **Problem It Solves:** The unfair “whoever prints money controls the whistle” logic in crypto and the damage caused by speculators who abandon projects.  
* **How It Works:** A user’s decision-making and governance weight is determined not by how much they hold, but by how solidly (pillar-like) and how long they hold it.  
* **Example Scenario:** A “whale” who enters today with 1,000,000 tokens may have lower voting power than a loyal “patron” who has held 100 tokens for a year.

---

## 👥 2) Roles & Entities

This protocol clarifies “who does what, and who cannot do what” to reduce misunderstandings and abuse.

- **Artist:**  
  Produces Evidence Packs for [PoArt], initiates records, and signs the annual validation (heartbeat).

- **Patron (Supporter):**  
  Gains status through continuity and contribution within [FPP]; carries weight in veto, supervision, and curation processes.

- **Validator (Community Verifier):**  
  Reviews Evidence Packs, flags inconsistencies, and participates in veto/objection processes.

- **Digital Notary (Self-Executing Contract):**  
  Deterministically verifies evidence + consensus + timestamp and seals it into the Public Registry.

- **Public Registry:**  
  The permanent identity layer for “approved records”. Record statuses are visible here (Verified/Legacy/Revoked, etc.).

- **Evidence Storage (IPFS/Arweave/Archive):**  
  The off-chain layer that stores raw data; only cryptographic roots are written on-chain.

---

## 📊 3) Economic & Governance Metrics

### 3.1) Epoch (Definition of the Time Window)
* **Definition:** The window that determines “which time interval” governance and validation calculations measure.  
* **Recommended Standard (v1.0):**
  - **Default Epoch:** 7 days  
  - **Critical Vote Guard Window:** 30 days (neutralizes short-term capital spikes before critical votes)

> Note: Epoch length can be parameterized. But since this document is “stable”, v1.0 must define clear defaults.

---

### 3.2) TWAB (Time-Weighted Average Balance)
* **Definition:** Time-Weighted Average Balance. The core metric that computes a wallet’s “loyalty” and “stability” coefficient in the ecosystem. It measures not only “how much” you have, but “how long” you have upheld it.

#### Mathematical Model (Normalized Average)
\[
\text{TWAB}=\frac{\sum_{i=1}^{n}(\text{Balance}_i \times \Delta t_i)}{\sum_{i=1}^{n}\Delta t_i}
\]

#### Raw Area Metric (Optional, for Scoring)
In some implementations, you need “area” instead of “average”. Then the naming must be explicit:
\[
\text{TWA}=\sum_{i=1}^{n}(\text{Balance}_i \times \Delta t_i)
\]

* **Problem It Solves:** **Whale Manipulation.** The pattern of buying a huge amount right before a vote and selling right after (pump-dump) is broken by “time friction”.  
* **TWAB Guard Logic:** Time cannot be bought. In critical votes, capital entering at the last minute becomes negligible under the guard window.

#### Voting Power Definition
Voting power is a TWAB-based function:
\[
\text{VotingPower} = f(\text{TWAB}, \text{EpochRules}, \text{StatusTier})
\]

* **Example (Logical):**
  - **Person A:** Bought 1,000,000 tokens 1 hour before a critical vote. Guard Window = 30 days. Impact is **very low**.  
  - **Person B:** Holds only 100 tokens but has kept them in cold storage for 365 days. Impact is **high**.  
* **Result:** The system prefers B’s 1-year loyalty over A’s last-minute money.  

---

### 3.3) Logarithmic Power Scoring
* **Definition:** A fairness mechanism that calculates power growth not linearly, but **logarithmically**, placing a ceiling on governance domination by capital.

#### Mathematical Model
\[
\text{Score} = \log_{10}(\text{TWAB} + 1)
\]

* **Problem It Solves:** **Capital Concentration (Plutocracy).** Prevents giant holders from suffocating the community’s voice.  
* **Example:**
  - TWAB = 10 → Score = log10(11) ≈ 1.04  
  - TWAB = 1,000,000 → Score = log10(1,000,001) ≈ 6.00  
* **Fairness Note:** Even if one party appears 100,000x “richer”, they cannot become “infinitely” stronger in governance. Mathematics allows small voices to combine into a counter-balance.

---

## 🛡️ 4) Security & Validation

### 4.1) Millennium Vault (10-Year Epochs)
* **Definition:** The highest-level “reputation vault” where assets are locked in 10-year periods (epochs).  
* **Problem It Solves:** Speculators optimized for short-term profit harming the 2025–3000 vision.  
* **Answer:** Only those who lock assets for 10 years and earn [FPP] “Foundational Pillar” status can shape the most critical decisions.

---

### 4.2) Evidence Pack
* **Definition:** The mandatory technical dataset required for a work to be approved by [PoArt].

#### Mandatory Content (Trinity of Proof)
1) **Live Logs:** 24/7 live streams and server/platform logs during production  
2) **Process Timelapse:** Accelerated process video from first stroke to final form  
3) **Digital Fingerprint:** Hash signed by the artist’s wallet (proof of non-tampering)

#### v1.0 Reinforcement (Chain Integrity Layer)
Trinity alone is not enough; the binding between components must also be sealed:
4) **Capture Manifest:**  
   Device/camera info, resolution, frame counts, durations, file list, checksums.  
5) **Merkle Root / Hash Chain:**  
\[
\text{EvidenceRoot} = \text{MerkleRoot}(\text{AllFiles})
\]
   One cryptographic root for all evidence files, the “single truth” written to chain.  
6) **Random Challenge Frames (Optional but Powerful):**  
   Low-friction “human proof” prompts triggered at random moments during the stream  
   (e.g., show a specific card, write a specific word, place a specific object in frame).  
   This dramatically increases the cost of AI reenact/deepfake forgery.

* **Problem It Solves:** A technically undeniable answer to “Was this truly made by a human hand with real effort?”

---

### 4.3) Sybil & Flash-loan Protection
* **Definition:** A mathematical barrier against bot-account (Sybil) and instant-loan (Flash-loan) attacks.  
* **Answer:** TWAB + Guard Window makes instant capital movement negligible in governance impact.

---

## 💾 4.4) Digital Notary (The Unshakeable Seal of the Protocol)
* **Definition:** A self-executing mechanism that filters [PoArt] and [FPP] data through technical checks, mathematically validates it, and irreversibly seals the final record into the **Public Registry**.

### Problems It Solves
1) **Central Authority and Bias:** Reduces subjective “elite approval” risk.  
2) **Data Manipulation:** Makes retroactive alteration of approved records technically impossible.  
3) **Gatekeeping:** Entry into a global archive is earned through proof, not taste.

### Verification Cycle (Triple Filter)
- **Evidence Pack Completeness:** Trinity + Manifest + EvidenceRoot  
- **Democratic Oversight:** Must not cross veto/quorum rules  
- **Cryptographic Signature:** SHA-512 signature verification

### Mathematical Approval Seal
\[
\text{NotarySeal} = \text{Hash}(\text{EvidenceRoot} + \text{VoterConsensus} + \text{TimeStamp})
\]

### Outcome (2026–3000)
Once a work receives the Digital Notary seal, it stops being merely the property of a single institution and becomes part of humanity’s long-horizon cultural heritage. The seal preserves the “who, when, and what labor” proof for centuries.

---

## 🏛️ 5) Validation & Persistence

### 5.1) 365-Day Continuous Cold Wallet Validation
* **Definition:** Holding an asset in cold storage (Ledger/Trezor, etc.) for 365 days with **stability**.

* **Problems It Solves:**
  1) Wash Trading  
  2) Speculative pressure  
  3) Hot wallet security vulnerabilities

#### v1.0 Update: “Penalty Ladder” instead of a single “Hard Reset”
A single transfer instantly zeroing everything is powerful but can punish genuine human error. v1.0 should be both strict and livable:

- **1st Violation (transfer before 365 days):**  
  TWAB is not fully deleted, but governance impact drops with a penalty multiplier:  
\[
\text{EffectiveTWAB} = \text{TWAB} \times 0.20
\]

- **2nd Violation:**  
\[
\text{EffectiveTWAB} = \text{TWAB} \times 0.05
\]

- **3rd Violation:**  
  Status becomes **Revoked**.

> This ladder keeps the system economically hostile to “fast-in fast-out” manipulation without fully burning genuine users on first mistakes.

#### Safe Migration Exception (Move Permit, Time-Lock)
For wallet migration or security upgrades:
- Open a **Move Permit** request  
- Apply a short **time-lock**  
- Community oversight (veto/quorum) remains active  
- Only the permit record and new address binding are written on-chain

---

### 5.2) Evidence Pack: Trinity of Proof
* **Components and Technical Detail:**
  1) **Live Stream Logs:** raw recordings + platform server log alignment  
  2) **Process Timelapse:** technical summary of layered construction  
  3) **Technical Logs:** metadata, coordinates, tool timeline  
  4) **EvidenceRoot:** single cryptographic root for all files (Merkle Root)

* **Problem It Solves:** Against AI producing “results” in seconds, it protects the “process proof” of human labor.

---

### 5.3) Annual Renewal Requirement (365-Day Heartbeat)
* **Definition:** A yearly signature that proves each Public Registry entry remains active and owned.  
* **Problems It Solves:** Dead data, abandoned wallets, passive collecting.

* **How It Works:**
  - Each record has a **Valid Until** date.  
  - System warns **30 days before** expiration.  
  - Owner signs again: “Still mine and still compliant.”  
  - If not renewed, status becomes **Legacy Archive**.

> Optional acceleration: If the project has annual archives plus frequent auditing, heartbeat can be reduced (e.g., 30 days). v1.0 default is 365 days.

---

## 🗳️ 6) Decentralized Supervision

### 6.1) Community Veto Mechanism (40% Threshold)
* **Definition:** A democratic safety barrier allowing a qualified minority to halt new entries or protocol changes.

#### v1.0 Update: Dual Lock with “Quorum + Veto”
A pure 40% veto can be distorted under low participation. Therefore:

- **Quorum (Minimum Participation):**  
  At least **25%** of total active voting weight must participate.  
- **Veto Threshold:**  
  Veto should ideally trigger not at 40% of participants, but at **40% of total active weight**.  
  (This fits the protocol’s “armor” intention.)

* **Problems It Solves:**
  1) Sybil Attacks  
  2) Collusion (coordinated approvals)  
  3) Bribery (buying votes)

* **Example Scenario:** An AI-generated image applies as “my labor”. Evidence Pack shows inconsistencies. If the community crosses the veto threshold under log scoring and TWAB, the record can never be sealed.

---

## ⚙️ 7) The Michelangelo Framework (Meritocracy Engine)

### 7.1) Michelangelo: The Meritocracy Philosophy
* **Definition:** The ranking and reputation engine. Prevents the system from becoming a “rich list” by enforcing merit-based hierarchy.  
* **Slogan:** *“You cannot buy your way to the top.”*  
* **Example:** A whale cannot be #1 just by depositing capital. The top belongs to those who contribute cultural value over years.

### 7.2) Status Formula: Time × Contribution
\[
\text{Status} = \text{HoldingTime} \times \text{CulturalContribution}
\]

* **HoldingTime:** days held intact in cold storage (e.g., 1420 days)  
* **CulturalContribution:** translations, curation, infrastructure, exhibition support, etc.

* **Problem It Solves:** Holding alone is passive. The system rewards those who both hold and build.

---

## 📊 8) Cultural Multipliers & Ranking Levels

### 8.1) Cultural Multiplier
* **Definition:** Bonus system added to final score.  
* **Application Areas:**
  - **Translation (JP/TR/EN):** science/philosophy/art texts (e.g., +4,500 Pts)  
  - **Curation:** registry quality control + veto participation  
  - **Infrastructure:** code, documentation, indexer contributions

* **Example:** 1000 days holding + 1 major translation can surpass thousands of passive holders.

### 8.2) Tier Classifications
1) **Legendary (Top 10):** highest veto and strategic authority  
2) **Senior (Top 50):** primary pillars, critical voice  
3) **Veteran (Top 100):** long-term verifiers

* **Rule:** Not static. If contribution stops or stability breaks, tier drops.

---

## 📈 9) Cut-off Thresholds & Network Metrics

### 9.1) Entry Thresholds
Thresholds must be single-source-of-truth in a stable spec:

- **Legendary Threshold:** **≥ 100,000 Pts**  
- **Top 100 Entry:** **≥ 45,000 Pts**

* **Problem It Solves:** Prevents overcrowding and quality collapse. The path to the top is protected by a mathematical barrier.

### 9.2) Network TWAB
* **Definition:** The ecosystem’s total TWAB capacity (e.g., 4.2M Network TWAB).  
* **Function:** As it increases, the system becomes harder to manipulate.  
* **24h New Entries:** Live feed of new [PoArt] entries in the last 24 hours.

---

## 🎨 10) Intellectual Framework

### 10.1) IPOW: Intellectual Proof of Work
* **Definition:** A reputation engine that requires high-quality human labor (translation, art, education, technical work) beyond holding capital.  
* **Problem It Solves:** “Passive stake” culture.  
* **Example:** A wallet holding 1M tokens with zero contribution can fall behind a wallet holding 100 tokens that actively translates documentation.

### 10.2) Intellectual Honesty Filter
* **Definition:** A stage that measures whether a user truly understands the subject during claims or critical votes.  
* **Problems It Solves:** copy-paste voting, AI spam, voting without understanding.

#### v1.0 Update: “Understanding Proof” instead of classic quizzes (Accessible)
Classic quizzes can punish users via language/accessibility barriers. Therefore:

**Option A (Short Summary):** summarize the proposal in 100 words  
**Option B (Risk Selection):** select 2 risks + write 1 justification  
**Option C (Objection Input):** submit 1 objection rationale if applicable

These modules measure understanding rather than memorization and raise automation costs.

---

## 🛡️ 11) Advanced Sybil Resistance

### 11.1) The Turnstile Mechanism
* **Definition:** A minimum participation threshold to enter the ecosystem (e.g., 250 ILHAN Token).  
* **Philosophy:** “Not a wall, a turnstile.”  
* **Problem It Solves:** Filling governance with zero-cost zombie wallets.  
* **Example:** A bot operator attempting 10,000 fake accounts must hold 250 tokens in each, making the attack economically irrational.

### 11.2) Zombie Wallet Filter (Active Claim Requirement)
* **Definition:** A filter requiring periodic proof that a wallet is “alive and active.”  
* **Rule:** Wallets that do not submit active claims are automatically removed from the Global Registry even if their score is high.  
* **Goal:** Keep the system composed of “living and producing” participants.

---

## 🧬 12) Generational Legacy & Governance

### 12.1) Generational Inheritance (Heir Designation)
* **Definition:** Members who maintain continuous Legendary status for 4 years (1460 days) can transfer reputation and rights to an heir.  
* **Problem It Solves:** Cultural value disappearing when a person dies or becomes inactive.  
* **Implementation:** Heir designation is accessible only after proving 4-year loyalty and is sealed on-chain.

### 12.2) Parliamentary Governance Rights
1) **Legendary (≥ 100k):** constitution, fee structures, strategy  
2) **Patron (50k–99k):** curation, supervision, votes  
3) **Member (< 50k):** proposals and small-scale decisions

* **Problem It Solves:** Replaces chaotic voting with “meritocratic democracy”.

---

## 🌍 13) Cultural Privilege Layers & Real-World Integration

> Note: Privileges in this section are “Future Roadmap” components, implemented gradually during 2026–2030.

### 13.1) The Annual Exhibition Right
* **Definition:** High-scoring verified artists/patrons can exhibit in a physical İlhan Art Gallery once per year for one week.  
* **Problem It Solves:** Independent artists’ difficulty accessing physical gallery space and high exhibition costs.  
* **How It Works:** Eligible users reserve time via calendar and use “reputation points” rather than money. This is the democratization of art.

### 13.2) Dynamic Art Pricing (JSON-Linked Discounts)
* **Definition:** Status functions as a discount key during physical/digital purchases.  
* **Implementation:**
  - Legendary: 50%+  
  - Patron: 30%  
  - Member: 10%  
* **Philosophy:** Not bargaining, but proven labor.

### 13.3) Physical Ecosystem Integration (Partner Integration)
- bookstores, cafes, cultural centers  
- QR-based status reading and claimable codes

### 13.4) Labor Over Capital: Meritocratic Access
\[
\text{ClaimRight} \propto \text{CulturalScore} + \log_{10}(\text{Balance})
\]
A student holding 250 tokens (turnstile limit) and contributing translations/art can gain more discounts, exhibition rights, and benefits than someone holding 100,000 tokens with zero contribution.

---

## 🧩 14) State Machine (Record Lifecycle)

A [PoArt] record and [FPP] status follow this deterministic flow:

1) **Draft**  
2) **Submitted**  
3) **Under Review**  
4) **Challenged** (objection opened)  
5) **Verified** (NotarySeal applied)  
6) **Renew Due** (heartbeat window approaching)  
7) **Legacy Archive** (not renewed, passive archive)  
8) **Revoked** (violation, evidence collapse, veto, multiple violations)

> This flow answers “what state am I in, and what happens next?” at a glance.

---

## 🔗 15) Minimal On-chain / Maximal Off-chain

### Written On-chain
- `EvidenceRoot` (Merkle Root)  
- `NotarySeal`  
- `TimeStamp`  
- `Signer` (artist/owner)  
- `Status` (Verified/Legacy/Revoked)  
- `Permit Records` (exceptions such as Move Permit)

### Stored Off-chain
- raw video files  
- timelapse  
- technical log files  
- manifest details  
- large archive sets (IPFS/Arweave)

**Goal:** Maximize verifiability without bloating the chain.

---

## 🏛️ 16) Appeals / Authority & Objection Mechanism (Institutional Trust Layer)

The objection mechanism is the institutional guarantee of trust.

- **Strategic Filter:** Objections must be evidence-based (not pure emotion/defamation).  
- **Community Veto:** 40% veto + quorum dual lock.  
- **Anti-Bot / Anti-Sybil:** (application layer) Solana-gated / stake-gated verification to choke bot flows.  
- **Evidence Pack Freezing:** When an objection opens, the relevant evidence pack is frozen (time-lock).  
- **Transparency / Time-Lock:** Every objection event is visible on a public timeline; sudden censorship or manipulation is blocked.

---

## 🧨 17) Threat Model (Attack Catalog and Counter-Layers)

- **Sybil Attack:** Turnstile + Zombie Filter + Quorum  
- **Flash-loan:** TWAB + Guard Window + Log Scoring  
- **Whale Domination:** Logarithmic Power Scoring + TWAB  
- **Wash Trading:** Cold Wallet Validation + Penalty Ladder  
- **Collusion:** Veto + Evidence Pack scrutiny + transparency  
- **Data Tampering:** EvidenceRoot + SHA-512 signatures + NotarySeal  
- **Bribery / Vote Buying:** Time-lock + quorum + contribution-weighted legitimacy  
- **Deepfake Process Forgery:** Random Challenge Frames + manifest + hash chain

---

## ⚖️ 18) Final Word: A Blueprint for Global Governance (Manifesto)

> Vision Note: The mathematical armor built by [FPP] and [PoArt] proposes a governance model that can improve not only an art gallery ecosystem, but also corrupted parliamentary systems and manipulated elections.

### 18.1) The End of Plutocracy
* **Definition:** Plutocracy is governance where decision power belongs solely to the richest minority.  
* **Protocol Response:** Logarithmic scoring places a ceiling on capital power, while “time” and “labor” become the true authority.  
* **Rationale:** The future of a society should belong not to the fattest wallet, but to those who contribute the most intellectual value.

### 18.2) The Meritocratic Parliament
Instead of populism and capital-centric politics, the model aims for a structure where those who internalize documentation and submit IPOW gain meaningful decision rights.

### 18.3) Security Against Vote Rigging (SHA-512 Election Security)
- Turnstile: makes bot manipulation economically irrational  
- TWAB: neutralizes last-minute “citizenship/vote purchase” via cheap transfers  
- 40% Veto + Quorum: ensures minority oversight without being crushed

### 18.4) The Conclusion: Saving the Future
This system is a design for a “new order” where proven labor defeats fraud, and a millennial vision defeats short-term impulses. The path to saving a society destined for misgovernance is to implement a protocol architecture proven mathematically fair and engineered to reduce human error.

---

## 📅 19) Roadmap & Future Notes
All items in this documentation are building blocks of the İlhan Art ecosystem’s long-horizon vision from 2026 to 3000. Each version update (v1.1, v1.2, etc.) will include technical integration processes for these privileges (API links, physical POS integrations, etc.).

---
