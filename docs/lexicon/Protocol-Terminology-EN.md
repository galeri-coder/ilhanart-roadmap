---
title: "Ilhan Art Protocol"
version: "1.0 (Stable)"
status: "HARD_LOCKED"
integrity: "SHA-512"
ecosystem: "[PoArt] + [FPP]"
last_updated: "2026-01-07"
---


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
16. Appeals / Authority & Objection Mechanism  
17. Threat Model  
18. Final Word: A Blueprint for Global Governance  
19. Roadmap & Future Notes  

---

## 🏛️ 1) Pillars of the Protocol

### [PoArt] Proof of Art (v1.0)
* **Definition:** The core protocol that verifies not only the final outcome of an artwork but also the entire creative process through technical data.  
* **Problem Solved:** With Generative AI’s rise, authentic human labor becomes unverifiable, degrading art’s intrinsic value.  
* **How It Works:** Artists submit an **Evidence Pack** containing every stage of creation. The protocol seals it on-chain with timestamps.  
* **Example:** A 40-hour painting includes video logs, timelapse, and digital fingerprints—proofing both *the result* and *the 40 hours of human effort*.

---

### [FPP] Foundational Pillar Protocol (v1.0)
* **Definition:** The system that builds economic and social “pillars” of the ecosystem—rewarding loyalty, continuity, and contribution.  
* **Problem Solved:** Prevents speculative dominance where wealth dictates governance.  
* **How It Works:** Governance weight depends not on wealth, but on *stability* and *duration* of holding.  
* **Example:** A “whale” entering with 1,000,000 tokens today may have less voting power than a “patron” holding 100 tokens for a year.

---

## 👥 2) Roles & Entities

Defines “who does what” to eliminate ambiguity and abuse.

- **Artist:** Produces Evidence Packs for [PoArt]; initiates records and annual validations.  
- **Patron:** Earns influence in [FPP] through loyalty and contribution; participates in veto and curation.  
- **Validator:** Reviews Evidence Packs; flags inconsistencies; assists in objection processes.  
- **Digital Notary:** Self-executing contract verifying consensus, hash, and timestamp, sealing data to the Public Registry.  
- **Public Registry:** The permanent record layer showing Verified, Legacy, or Revoked statuses.  
- **Evidence Storage:** Off-chain IPFS/Arweave archive storing raw data; only cryptographic roots go on-chain.

---

## 📊 3) Economic & Governance Metrics

### 3.1) Epoch & Time Windows
Defines which time intervals determine validity and voting.

| Type | Duration | Purpose |
|:--|:--|:--|
| **Operational Epoch** | 7 Days | Routine updates, logs, scoring |
| **Critical Guard Window** | 30 Days | Neutralizes last-minute capital influx |
| **Integrity Cycle** | 365 Days | Annual validation through Evidence Pack |

---

### 3.2) TWAB (Time-Weighted Average Balance)

**Mathematical Model:**  
$TWAB = \dfrac{\sum_{i=1}^{n}(Balance_i \times \Delta t_i)}{\sum_{i=1}^{n}\Delta t_i}$

**Optional Raw Metric:**  
$TWA = \sum_{i=1}^{n}(Balance_i \times \Delta t_i)$

* **Purpose:** Measures not only *how much* but *how long* value remains in the system.  
* **Effect:** Deters “flash” influence — last-minute token purchases have minimal effect on voting outcomes.

---

### 3.3) Voting Power Function  
$VotingPower = f(TWAB, EpochRules, StatusTier)$

* **Guard Window Impact:** Votes look back 30 days for eligibility.  
* **Result:** Time dominates over sudden wealth.

---

### 3.4) Logarithmic Power Scoring  

$Score = \log_{10}(TWAB + 1)$  
$VotingPower = Score \times g(EpochRules, StatusTier)$

| TWAB | Log Score | Governance Power |
|:--|:--|:--|
| 10 | 1.04 | Entry level |
| 1,000 | 3.00 | Moderate influence |
| 1,000,000 | 6.00 | Upper limit plateau |

> **Simulation:**  
> View real-time calculations or test scenarios via [PoArt Simulation Console](https://galeri-coder.github.io/ilhanart-protocol/[PoArt]/).

## 🛡️ 4) Security & Validation

### 4.1) Millennium Vault (1-Year Epochs)
* **Definition:** Highest-tier reputation vault; assets locked for one year.  
* **Purpose:** Protects the long-horizon (2025 → 3000) vision through verified stability.  
* **Access:** Only holders locked ≥ 1 year with [FPP] “Foundational Pillar” status can shape critical votes.

---

### 4.2) Evidence Pack (Chain Integrity Layer)
A mandatory technical data set for [PoArt] validation.

#### Required Components — The Trinity of Proof
1. **Live Logs:** Real-time creation footage + server logs.  
2. **Process Timelapse:** From first to last brush stroke.  
3. **Digital Fingerprint:** Artist wallet–signed hash ensuring authenticity.  

#### Additional Proof Layers
4. **Capture Manifest:** Device, resolution, frame rate, checksums.  
5. **Merkle Root / Hash Chain:**  
   $EvidenceRoot = MerkleRoot(AllFiles)$  
   All files collapse into a single root — *the one truth* sealed on-chain.  
6. **Random Challenge Frames:** Random “human verification” prompts preventing deepfakes.  

* **Outcome:** Offers irrefutable technical proof that the artwork was human-made.

---

### 4.3) Sybil & Flash-loan Defense
* **Function:** Combines TWAB + Guard Window to make short-term capital irrelevant.  
* **Result:** Flash loans and bot swarms lose governance influence.

---

### 4.4) Digital Notary (Immutable Protocol Seal)  
$NotarySeal = Hash(EvidenceRoot + VoterConsensus + TimeStamp)$  

* Verifies [PoArt] & [FPP] integrity.  
* Seals verified data to **Public Registry**.  
* Removes reliance on centralized or subjective gatekeeping.  
* **Legacy Effect (2026 – 3000):** Each notarized piece becomes part of a verifiable cultural archive.

---

## 🏛️ 5) Validation & Persistence

### 5.1) 365-Day Continuous Cold-Wallet Verification
**Definition:** Assets must remain in verified cold storage (Ledger, Trezor, etc.) for 365 consecutive days.

**Problems Solved**
1. Wash Trading  
2. Speculative pressure  
3. Hot-wallet security vulnerabilities  

#### v1.0 Update — “Penalty Ladder” (instead of Hard Reset)  
Gradual penalty system ensures strict but humane enforcement.

**1st Violation (before 365 days):**  
$EffectiveTWAB = TWAB \times 0.20$

**2nd Violation:**  
$EffectiveTWAB = TWAB \times 0.05$

**3rd Violation:** Status = **Revoked**

> Prevents “quick in/out” manipulations while preserving honest users’ progress.

#### Safe-Transfer Exception (Move Permit / Time-Lock)
For legitimate transfers:  
- Submit **Move Permit** request  
- Apply short **time-lock**  
- Community oversight remains active  
- Only the permit and new address link are written on-chain  

---

### 5.2) Evidence Pack — Trinity of Proof
Components:  
1. **Live Stream Logs** (raw + server sync)  
2. **Process Timelapse**  
3. **Technical Logs** (metadata, tool usage)  
4. **EvidenceRoot** (single Merkle Root)  

> Protects *process authenticity* over product appearance.

---

### 5.3) Annual Renewal Requirement (365-Day Heartbeat)
* Each verified record must renew annually via signature.  
* **Reminders:** Issued 30 days before expiration.  
* **Failure to renew:** Downgrades to *Legacy Archive*.  
* **Goal:** Avoid dead data and ghost ownerships.

---

## 🗳️ 6) Decentralized Supervision

### 6.1) Community Veto Mechanism (40% Threshold)
* **Definition:** Democratic safeguard allowing a qualified minority to halt proposals.  
* **Dual-Lock Condition (v1.0):**
  - **Quorum:** ≥ 25% participation required  
  - **Veto Trigger:** ≥ 40% of total active weight  

**Protection Against**
1. Sybil Attacks  
2. Collusion  
3. Vote Bribery  

> Example: AI-generated art flagged by validators cannot pass if 40% of active TWAB weight vetoes it.

---

### 6.2) Emergency Governance / Fallback Council  
Prevents deadlocks when participation drops too low.

$Deadlock = (ParticipationRate < 25\%) \land (ProposalTimeout > 7\,days)$

If `Deadlock = TRUE`:  
1. Top 10% of Impasto members form **Fallback Council**.  
2. Decisions require ≥ ⅔ consensus.  
3. Must be ratified within 30 days by community referendum.  
4. All actions recorded in the **Emergency Ledger (SHA-512)**.

## ⚙️ 7) The Michelangelo Framework (Meritocracy Engine)

### 7.1) Michelangelo Philosophy
* **Definition:** Ranking and reputation system ensuring cultural contribution outweighs wealth.  
* **Slogan:** *“You cannot buy your way to the top.”*  
* **Purpose:** Replaces “rich lists” with effort-based legitimacy.

---

### 7.2) Status Formula
$Status = HoldingTime \times CulturalContribution$

- **HoldingTime:** Duration (days) of uninterrupted holding.  
- **CulturalContribution:** Translation, curation, infrastructure, education, etc.

**Problem Solved:** Encourages hybrid participation — economic + intellectual labor.

---

### 7.3) Cultural Contribution Domains

| Domain | Description | Example Points |
|:--|:--|:--|
| Translation | Art, philosophy, science texts | +4,500 |
| Curation | Archive QA, registry supervision | +2,000 |
| Infrastructure | Code, docs, maintenance | +3,000 |
| Education | Public lectures, media | +1,500 |

> Combined weight recalculates quarterly through [FPP] to sustain fairness.

---

### 7.4) Status Decay  
Inactive users lose a fraction of reputation over time.  

$StatusDecay = e^{-\lambda t}$  

Where `λ` is the decay rate (v1.0 = 0.0005 per day).  

> Keeps ranking dynamic and self-cleaning.

---

## 📊 8) Cultural Multipliers & Ranking Levels

### 8.1) Cultural Multiplier
* **Definition:** Final scoring bonus for contributors impacting ecosystem growth.  
* **Domains:**  
  - Translation  
  - Curation  
  - Infrastructure  
  - Education  
  - Governance participation  

$FinalScore = BaseScore \times (1 + CulturalMultiplier)$

---

### 8.2) Tier Classifications (Rütbe Sınıfları)

| Tier | Range / Puan | Role & Privileges |
|:--|:--|:--|
| **Impasto (≥100k)** | Constitutional Level | Defines core governance strategy, fee model, and long-term direction |
| **Texture (50k–99k)** | Curatorial Level | Oversees audits, curations, and voting coordination |
| **Primer (<50k)** | Member Level | Can submit proposals and participate in minor decisions |

> Ranks adjust dynamically with contribution flow and decay rate recalculations under [FPP].


---
## 📈 9) Cut-off Thresholds & Network Metrics

### 9.1) Entry Thresholds
 Tier | Required Points | Description |
|:--|:--|:--|
| **Impasto (≥100,000)** | Full constitutional authority | Defines governance, strategy, and system parameters |
| **Texture (50,000–99,999)** | Senior curator level | Participates in audits, curation, and high-level voting |
| **Primer (<50,000)** | General member level | May submit proposals and vote on minor issues |

**Goal:** Ensure proportional influence and governance balance as the network expands.

---

### 9.2) Network TWAB (Global Stability Index)
* **Definition:** Aggregate of all participant TWABs.  
* **Interpretation:** The higher the network TWAB, the harder to manipulate governance.  
* **Live Metric:** Displays new [PoArt] entries every 24 hours.

---

## 🎨 10) Intellectual Framework

### 10.1) IPOW — Intellectual Proof of Work
* **Definition:** Validation of high-value human labor beyond financial staking.  
* **Mechanics:** Rewards intellectual, creative, and infrastructural outputs.  
* **Example:**  
  - 1 M tokens + no contribution → Low rank  
  - 100 tokens + consistent translation work → High rank  

---

### 10.2) Intellectual Honesty Filter
* **Definition:** Measures whether a voter comprehends the subject before voting.  
* **v1.0 Accessible Modes:**  
  - **A)** Summarize proposal ≤ 100 words  
  - **B)** Select 2 risks + add 1 justification  
  - **C)** Submit 1 counterargument  

> Evaluates understanding instead of memorization; resists AI spam and blind voting.


## 🛡️ 11) Advanced Sybil Resistance

### 11.1) Turnstile Mechanism
* **Definition:** Minimum entry threshold to deter zero-cost bot creation.  
* **Standard (v1.0):** 250 ILHAN tokens.  
* **Philosophy:** “A turnstile, not a wall.”  
* **Purpose:** Creates economic friction against Sybil attacks.  
* **Example:** A botnet of 10,000 wallets now costs 2.5 M tokens — attack becomes irrational.

---

### 11.2) Zombie Wallet Filter (Active Claim Requirement)
* **Definition:** Requires wallets to periodically confirm activity through simple heartbeat signatures.  
* **Rule:** Inactive wallets are delisted from the Global Registry, regardless of score.  
* **Purpose:** Keeps the network composed of *living participants*.  
* **Frequency:** Default = 365 days, adjustable per epoch rules.

---

## 🧬 12) Generational Legacy & Governance

### 12.1) Generational Inheritance
* **Definition:** impasto-tier members (≥100k points) maintaining active status for 4 consecutive years (1460 days) can assign a verified heir.  
* **Purpose:** Prevents cultural and governance value from dying with inactive or deceased members.  
* **Implementation:**  
  - Heir activation possible only after 4-year proof of continuity.  
  - Heir verification sealed on-chain with multi-signature authentication.

---

### 12.2) Parliamentary Governance Rights

| Tier | Role | Powers |
|:--|:--|:--|
| **Impasto (≥100k)** | Founders / Constitutional Council | Defines protocol-level strategy |
| **Texture (50k–99k)** | Senior Curators | Manage curation + auditing |
| **Primer (<50k)** | General Members | Proposal input + minor votes |

> Replaces chaotic populism with structured, meritocratic democracy.

---

## 🌍 13) Cultural Privilege Layers & Real-World Integration

> **Note:** These privileges are part of the 2026–2030 roadmap for hybrid physical–digital implementation.

---

### 13.1) Annual Exhibition Right
* **Definition:** Verified high-score artists/patrons gain one annual 7-day slot at Ilhan Art Gallery.  
* **Purpose:** Democratizes exhibition access; eliminates cost barriers.  
* **Mechanism:**  
  - Booking via on-chain calendar.  
  - Slots allocated by reputation, not capital.  

---

### 13.2) Dynamic Art Pricing (JSON-Linked Discounts)

* **Definition:** Dynamic pricing API where cultural status determines the discount factor.  
* **Structure:**  
  - **Impasto (≥100k)** → 50%+ discount  
  - **Texture (50k–99k)** → 30% discount  
  - **Primer (<50k)** → 10% discount  
* **Philosophy:** “No bargaining — only verified merit determines value.”  
* **Goal:** Encourage cultural contribution while maintaining transparent, algorithmic fairness.


---

### 13.3) Physical Ecosystem Integration
* Partner network: bookstores, cafés, cultural centers.  
* QR-based scanning for verifying status and claiming real-world privileges.  
* Connected via lightweight JSON API for instant validation.

---

### 13.4) Labor Over Capital — Meritocratic Access
* **Principle:** Cultural effort outweighs raw capital in privilege allocation.  
* **Mathematical Model:**  
  $ClaimRight \propto CulturalScore + \log_{10}(Balance)$  
* **Example:**  
  - Contributor A → 250 tokens + consistent creation = high ClaimRight  
  - Holder B → 100,000 tokens + inactivity = lower ClaimRight  

> Shifts the system from plutocracy to *laborocracy.*

---

## 🧩 14) State Machine (Lifecycle of a Record)

### Process Flow  
A [PoArt] record + [FPP] status follows an irreversible sequence:

1. **Draft** → created locally  
2. **Submitted** → uploaded for validation  
3. **Under Review** → validators audit evidence  
4. **Challenged** → objection raised  
5. **Verified** → [Digital Notary] seal applied  
6. **Renew Due** → heartbeat reminder (annual)  
7. **Legacy Archive** → expired, archived  
8. **Revoked** → violation or multi-infraction  

---

### State Transition Rules  

| From | To | Condition |
|:--|:--|:--|
| Draft | Submitted | Artist upload complete |
| Submitted | Under Review | Validator acceptance |
| Under Review | Verified | Consensus ≥ 66% |
| Under Review | Challenged | Objection raised |
| Challenged | Revoked | Objection upheld |
| Challenged | Verified | Community overturns veto |
| Verified | Legacy | Heartbeat expired |
| Legacy | Revoked | Manual audit failure |

> Enables transparent “where am I now?” tracking for every on-chain record.

---

## 🔗 15) Minimal On-chain / Maximal Off-chain

### On-chain Data
- `EvidenceRoot` (Merkle Root)  
- `NotarySeal`  
- `TimeStamp`  
- `Signer` (Artist/Owner)  
- `Status` (Verified / Legacy / Revoked)  
- `Permit` records (Move Permits / Heir links)

### Off-chain Data
- Raw videos  
- Timelapse sequences  
- Technical logs  
- Manifests and metadata  
- Large archive bundles (IPFS / Arweave)

**Goal:** Ensure verifiability without blockchain bloat.  
**Integrity:** SHA-512 verification cross-checks on request.

---

## 🏛️ 16) Appeals / Authority & Objection Mechanism

**Purpose:** Institutional layer guaranteeing fairness, transparency, and procedural justice.

---

### 16.1) Core Principles
- **Evidence-Based:** Appeals must include verifiable data.  
- **No Emotional Bias:** Subjective or defamatory claims auto-dismissed.  
- **Transparency:** All appeal events are timestamped and publicly visible.  
- **Freeze Protocol:** Evidence Packs involved in disputes are time-locked during investigation.

---

### 16.2) Community Safeguards
- **Veto Threshold:** 40% active TWAB weight.  
- **Quorum Requirement:** 25% minimum participation.  
- **Anti-Sybil Gate:** Turnstile + Stake Verification.  
- **AI Prevention:** Natural-language justification filters eliminate spam appeals.

---

### 16.3) Appeal Lifecycle
1. **Appeal Initiated** → validator or member submits claim.  
2. **Evidence Freeze** → related files locked.  
3. **Community Review** → Veto / Quorum triggered.  
4. **Resolution Vote** → 7-day window.  
5. **Decision Execution** → SHA-512 sealed.  

> Protects the system from hidden censorship and arbitrary power.

---

## 🧨 17) Threat Model (Attack Catalog & Countermeasures)

| Threat | Countermeasure |
|:--|:--|
| **Sybil Attack** | Turnstile + Zombie Filter + Quorum |
| **Flash-loan** | TWAB + Guard Window + Log Scoring |
| **Whale Domination** | Logarithmic Power Scoring + TWAB |
| **Wash Trading** | Cold Wallet Verification + Penalty Ladder |
| **Collusion** | Veto + Transparency Ledger |
| **Data Tampering** | EvidenceRoot + SHA-512 + NotarySeal |
| **Vote Bribery** | Time-lock + Quorum-weighted legitimacy |
| **Deepfake Forgery** | Random Challenge Frames + Hash Chain |

> Each mitigation method is mathematically defined and version-controlled under [FPP].

---

## ⚖️ 18) Final Word — A Blueprint for Global Governance

> *“Art is the prototype. Governance is the canvas.”*

Built by [PoArt] and [FPP], this framework proves that the same  
mathematical architecture safeguarding cultural truth can also repair broken democracies.

---

### 18.1) End of Plutocracy
* **Definition:** A system ruled by wealth, not merit.  
* **Protocol Response:**  
  - Logarithmic scoring limits money’s dominance.  
  - Time and labor become the core legitimacy metrics.  
* **Principle:** Ownership ≠ authorship — contribution defines legitimacy.

---

### 18.2) Meritocratic Parliament
* Replaces populism and capital-driven politics.  
* Empowers those who internalize documentation and contribute IPOW.  
* Turns governance into a *craft*, not a popularity contest.

---

### 18.3) Electoral Integrity (SHA-512 Security)
* **Turnstile:** Prevents bot-based citizen inflation.  
* **TWAB:** Nullifies last-minute transfers and vote buying.  
* **Veto + Quorum:** Guarantees minority oversight.  

> A new digital constitution, immune to manipulation.

---

### 18.4) Manifesto — Saving the Future
This protocol is not only a design for art,  
but a **governance archetype** for the next millennium.

It aims to build societies where:
- Verified effort > empty wealth  
- Long-term vision > instant gratification  
- Mathematical fairness > political bias  

> **“In the age of automation, humanity’s proof of worth is its willingness to create.”**

---

## 📅 19) Roadmap & Future Notes

| Phase | Year | Focus |
|:--|:--|:--|
| **v1.0** | 2026 | Core Proof & Validation (current spec) |
| **v1.1** | 2027 | Public Registry API & Simulation Console |
| **v1.2** | 2028 | Partner Integrations (POS / QR Systems) |
| **v2.0** | 2030 | Governance Automation + Cross-protocol Indexing |

> Timeline from 2026 → 3000 forms the *Ilhan Art Millennium Vision*:  
> a cultural, economic, and ethical system engineered for centuries of continuity.

---

## 🔐 Hash Signature (v1.0 Hard-Locked)
