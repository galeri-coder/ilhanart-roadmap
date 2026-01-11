```markdown
# 📚 វាក្យសព្ទ និង គោលគំនិត
> **"ការយល់ដឹងអំពីភាសានៃពិធីការនេះ គឺជាការយល់ដឹងអំពីចក្ខុវិស័យរបស់វា"**

## ⚙️ PoArt Forensic Engine (PFE) v1.0 – Core Architecture  

**PoArt Forensic Engine (PFE)** គឺជាស្រទាប់ស្នូលដែលតំណាងឱ្យតក្កវិជ្ជា និងប្រតិបត្តិការបច្ចេកទេសនៅពីក្រោយពិធីការ
[PoArt]។ វាមិនមែនគ្រាន់តែជាប្រព័ន្ធរក្សាទុកឯកសារទេ ប៉ុន្តែជា **Forensic Engine** ដែលយកទិន្នន័យផលិតកម្មដើមនៃស្នាដៃសិល្បៈ 
ហើយប្រែក្លាយវាទៅជា **Digital Evidence** ដែលអាចផ្ទៀងផ្ទាត់បាន និងមិនអាចកែប្រែបាន។  

---

### 🧩 ហេតុអ្វីបានជា "PoArt Forensic"?

- **PoArt (Proof of Art):** ម៉ាស៊ីននេះផ្តោតលើការភ្ជាប់តម្លៃនៃទ្រព្យសម្បត្តិឌីជីថល
មិនមែនតាមការស្មានប៉ុណ្ណោះទេ ប៉ុន្តែតាម **ដំណើរការផលិតកម្មដែលអាចបញ្ជាក់បាន**។  

- **Forensic (កោសល្យវិច្ច័យ):**  
  - **Technical Definition:** Algorithms និងវិធីសាស្ត្រខ្សែសង្វាក់កំណត់ត្រា ដើម្បីបញ្ជាក់ថា
  ទិន្នន័យដែលទាក់ទងនឹងដំណើរការផលិត (drawing strokes, timelapse video, logs) មិនត្រូវបានកែច្នៃ។  
  - **Philosophical Layer:** បង្ហាញការបំប្លែង **ពេលវេលា កម្លាំងពលកម្ម និងឆន្ទៈមនុស្ស
  ** ទៅជា ទិន្នន័យដែលអាចវាស់វែងបាន។  

> 💬 Note: Blockchain integration (e.g. Solana) មិនមែនជាផ្នែកស្នូលនៃ PFE ទេ; វាធ្វើជាស្រទាប់ដាច់ដោយឡែក – **Chain Anchor Layer** – សម្រាប់ការផ្ទៀងផ្ទាត់ និងការចុះបញ្ជី។  

---

## 🛠️ វិសាលភាពបច្ចេកទេស v1.0  

**PoArt Forensic Engine (PFE) v1.0** មានសសរស្តម្ភបីស្រទាប់សំខាន់៖  

---

### 1️⃣ Hashing & Sealing (ការបិទត្រា)

PFE ដំណើរការធាតុទាំងអស់នៅក្នុង Evidence Pack (ឯកសារ, វីដេអូ, JSON/logs, signatures ...) តាមរបៀប deterministic ហើយបង្កើតតម្លៃ **NotarySeal** តែមួយគត់។  

#### 🔹 Core Concepts  

- **FileHash (ស្នាមម្រាមដៃឯកសារ):** Hash ដែលបានបង្កើតពី bytes នៃឯកសារស្នាដៃ។  
- **EvidenceRoot:** សេចក្តីសង្ខេបឫសគល់ (Merkle root ឬ manifest hash) តំណាងឱ្យភាពសុចរិតនៃ Evidence Pack។  
- **NotarySeal (ត្រាចុងក្រោយ):** បង្កើតពីការរួមបញ្ចូល EvidenceRoot + TimeStamp + Signature។  

#### 📘 Formulae  

```math
FileHash₅₁₂ = SHA-512(ArtworkFileBytes)
NotarySeal = SHA-512(EvidenceRoot | SignerSignature | TimeStamp)
```

#### Canonical Payload Structure  

**EvidenceRootPayload**

```text
file_sha512:{sha512}
forensics:{canonicalForensics(forensics)}
```

**NotarySealPayload**

```text
evidence_root:{evidence_root}
signer_sig:{signer_sig}
timestamp:{timestamp}
```

> 🔒 Output Value = **NotarySeal**  
> SignerSignature (Phase 2) នឹងប្រើ Solana Wallet Adapter; នៅក្នុង v1.0 ប្រើ attestation key របស់ប្រព័ន្ធ។  

---

### 2️⃣ Indexing Layer (ការរក្សាទុក)

តួនាទី៖ កត់ត្រាថា Wallet ណា នៅពេលណា បានផ្ញើ **Labor Proof** សម្រាប់ស្នាដៃណា ទៅកាន់ស្រទាប់កំណត់ត្រា (Transparent Index Layer)។  
អាចប្រើជា local database ឬ Chain Anchor Layer នៅដំណាក់កាលក្រោយ។  

---

### 3️⃣ Verification Layer (ការផ្ទៀងផ្ទាត់)

នៅពេលមានសំណួរអំពីភាពត្រឹមត្រូវនៃស្នាដៃ → PFE នឹងគណនាឡើងវិញ EvidenceRoot និង NotarySeal → ប្រៀបធៀបជាមួយតម្លៃដែលបានរក្សាទុកក្នុង Registry ដើម្បីបញ្ជាក់ភាពសុចរិត។  

---

## 🧮 PoArt Value Theorem (ទ្រឹស្តីបទតម្លៃ PoArt)

**PoArt** ភ្ជាប់តម្លៃ (V) នៃទ្រព្យសម្បត្តិឌីជីថលទៅនឹង **ការពិតនៃដំណើរការផលិត** មិនមែនតម្លៃទីផ្សារស្មាននោះទេ។  

> AI បំប្លែងពេលវេលា → លទ្ធផលភ្លាមៗ (t → 0)  
> PoArt → តម្លៃកើតចេញពីពេលវេលា + កម្លាំងពលកម្ម + ឆន្ទៈ (agency)  

```math
V_PoArt = ∫_{t_start}^{t_end} [ P_labor(t) × I_agency(t) ] dt + U_irreversible
```

#### Variable Definitions  

| Symbol | Meaning |
|:--|:--|
| ∫dt | ការប្រមូលផ្តុំដំណើរការ (the process integral) |
| P_labor(t) | កម្លាំងពលកម្មភ្លាមៗ (time-dependent labor power) |
| I_agency(t) | មេគុណឆន្ទៈ (agency coefficient) |
| U_irreversible | ភាពមិនអាចត្រឡប់វិញបាន (irreversibility constant) |

- **AI (I ≈ 0):** No risk, no cost, algorithmic repetition.  
- **Human (I → 1):** Risk, decision, imperfection → uniqueness.  

---

### 🔎 Example Comparison  

#### Scenario A – AI Generated Image (10 seconds)

```text
Δt = 10 sec
P_labor = 1
I_agency = 0.01
U_irreversible = 0
```

```math
V_AI ≈ ∫₀¹⁰ (1×0.01) dt + 0 = 0.1
```

➡️ Fast, effortless → Near-zero value under PoArt.  

#### Scenario B – Human Live Art (6 hours)

```text
Δt = 21 600 sec
P_labor = 0.5
I_agency = 0.9
U_irreversible > 0
```

```math
V_Human ≈ ∫₀²¹⁶⁰⁰ (0.5×0.9) dt + U_irreversible ≈ 9720 + U_irreversible
```

➡️ Time + agency + irreversible labor = high cumulative value.  

---

### ✅ Conclusion – Proof-Bound Value  

1. **No process → No value**
```math
Δt ↓ ⇒ ∫ (P×I) dt → 0
```

2. **Agency amplifies value**
```math
V_PoArt ∝ ∫ (P_labor × I_agency) dt
```

3. **Irreversibility = Ontological uniqueness**  
Physical traces (paint, marble cracks) create non-fungible reality.  

> **In short:** In the AI age, rarity ≠ image; rarity = **verifiable human labor, time, and agency**.  

---
```
```markdown
# ⚙️ PoArt Protocol v1.0 – Structural Overview  

**PoArt Protocol v1.0** គឺជាសំណង់ស្ដង់ដារសម្រាប់ការផ្ទៀងផ្ទាត់ស្នាដៃសិល្បៈដែលផ្អែកលើដំណើរការផលិតកម្ម។  
វាបង្កើតជាស្រទាប់នៃភាពជឿជាក់ ដែលភ្ជាប់ពី **ស្នាដៃសិល្បៈដើម (source artwork)** ដល់ **តម្លៃចុងក្រោយ (verifiable asset value)**។  

---

## 🌐 Architecture Layers  

| Layer | Name | Role |
|:--|:--|:--|
| L1 | **PoArt Forensic Engine (PFE)** | ការបង្កើតភស្តុតាងឌីជីថល (Digital Evidence Creation) |
| L2 | **Proof Registry Layer** | ការចុះបញ្ជី និងការផ្ទៀងផ្ទាត់តម្លៃតាមសហគមន៍ |
| L3 | **Chain Anchor Layer (Optional)** | Blockchain anchoring (Solana / custom chain) |
| L4 | **Presentation Layer** | ការបង្ហាញស្នាដៃ និងសេចក្ដីយោង (web / exhibition / PoArt ID) |

---

## 🧱 Data Flow  

```text
[Creation Data] 
   ↓
[PoArt Forensic Engine (PFE)] → EvidenceRoot + NotarySeal  
   ↓
[Registry Layer] (stores: wallet, seal, metadata)
   ↓
[Presentation Layer] (verifiable proof displayed)
```

- **One-way Integrity:** EvidenceRoot នឹងត្រូវបានបញ្ចូលនៅក្នុង Proof Registry → Hash anchoring → Optional blockchain seal  
- **Transparency:** ទិន្នន័យមិនត្រូវបានរក្សាទុកជាឯកសារទាំងមូលទេ ប៉ុន្តែជា fingerprints (hashes only)  
- **Privacy by Design:** គ្មានការបង្ហាញនូវខ្លឹមសារ ឬឯកសារស្នាដៃដើមឡើយ  

---

## 🧩 Structural Components  

### 1️⃣ Evidence Pack  

Evidence Pack គឺជាសំណុំទិន្នន័យដែលបង្ហាញពីដំណើរការផលិតស្នាដៃ។  
វាអាចរួមមាន៖  

```text
/PoArtEvidencePack/
│
├── metadata.json
├── timelapse.mp4
├── creation_log.json
├── forensics.json
└── final_artwork.png
```

> Hash របស់ folder នេះទាំងមូល ត្រូវបានប្រើសម្រាប់បង្កើត **EvidenceRoot**។  

---

### 2️⃣ Registry Record  

```json
{
  "wallet": "So1anaWalletAddress",
  "evidence_root": "sha512:ab43d...91fe",
  "notary_seal": "sha512:d221...b72f",
  "timestamp": "2026-01-10T14:52:31Z",
  "signature": "sig:c4f...de0a"
}
```

> Record នេះអាចបញ្ជាក់បានតាមរយៈ PoArt API ឬ Smart Contract នៅលើ Chain Anchor Layer។  

---

## 🔏 Proof Lifecycle  

| Step | Name | Description |
|:--|:--|:--|
| 1 | **Creation** | Artist produces original work with digital traces (video, logs, etc.) |
| 2 | **Forensic Processing** | PFE hashes and seals all evidence components |
| 3 | **Registration** | Registry stores the NotarySeal and links it to the creator wallet |
| 4 | **Anchoring (optional)** | NotarySeal anchored to blockchain for immutable timestamp |
| 5 | **Verification** | Anyone can validate the artwork by recomputing the EvidenceRoot |

---

## 📄 Five Pillars of Truth  

The PoArt ecosystem is built upon **Five Pillars of Truth**, each representing a philosophical and technical foundation of authenticity.

| Pillar | Name | Description |
|:--|:--|:--|
| I | **Proof of Creation** | ការបង្ហាញពីដំណើរការផលិតដែលអាចបញ្ជាក់បាន។ |
| II | **Proof of Labor** | ការវាស់វែងពេលវេលា និងកម្លាំងពលកម្មរបស់មនុស្ស។ |
| III | **Proof of Agency** | ការបញ្ជាក់ឆន្ទៈ និងការសម្រេចចិត្តរបស់អ្នកបង្កើត។ |
| IV | **Proof of Irreversibility** | ភាពមិនអាចត្រឡប់វិញបាននៃដំណើរការ (time, material). |
| V | **Proof of Integrity** | ភាពសុចរិតនៃទិន្នន័យតាមរយៈ cryptographic sealing។ |

---

### 🪞 1. Proof of Creation  

> “Existence before representation.”

Every artistic act leaves **digital and temporal fingerprints**.  
These fingerprints, when properly captured and hashed, prove **creation** —  
not only the output but also the *process of becoming*.  

```math
Proof_of_Creation = H( Σ ProcessData_i )
```

---

### 🔨 2. Proof of Labor  

Labor is **time + effort + intentionality**.  
PFE measures this through activity logs, duration tracking, and timelapse analysis.

```math
L = ∫_{t₀}^{t₁} P_labor(t) dt
```

> The longer and more complex the traceable labor, the higher its PoArt weight.  

---

### 🧭 3. Proof of Agency  

Agency is the measure of **human intervention** within a process.  
It distinguishes between algorithmic generation and intentional creation.

```math
A = Σ (decision_events × human_input_intensity)
```

> High agency → Non-automated, non-repeatable outcomes.  

---

### ⏳ 4. Proof of Irreversibility  

Irreversibility marks the **entropy** embedded in creation.  
A stroke, a chisel mark, or digital paint layer once committed — cannot be undone without loss.

```math
U_irreversible > 0  ⇔  process ≠ reversible
```

> This forms the ontological core of PoArt value.  

---

### 🛡️ 5. Proof of Integrity  

Cryptographic hashing, digital signatures, and timestamp sealing  
collectively ensure that once evidence is sealed, **it cannot be altered**.

```math
Integrity = SHA512(EvidenceRoot | Signature | Timestamp)
```

> Any change in input → instantly invalidates NotarySeal.  

---

## 🌍 Interoperability  

PoArt Protocol v1.0 ត្រូវបានរចនាឡើងដើម្បីធ្វើការ​ជាមួយស្ថាបត្យកម្មឌីជីថលផ្សេងៗ៖  

- **Solana Layer** → optional blockchain anchoring  
- **IPFS Storage** → decentralized file reference  
- **PoArt ID** → universal identifier for artworks  

---

## 🧠 Philosophical Context  

PoArt recognizes **human time** as a scarce and measurable resource —  
transforming creation into a **verifiable economic and ethical act**.

> “To create is to leave irreversible proof of time.”

This turns artistic production into a form of **forensic evidence**,  
bridging aesthetics with epistemology.  

---

## 🔚 Summary  

- PoArt bridges *artistic authenticity* and *cryptographic verifiability*.  
- PFE ensures that every act of creation becomes **forensically traceable**.  
- Value is redefined: not by market hype, but by **human time, effort, and agency**.  

> **PoArt is not about minting art; it’s about proving existence.**  

---
```
```markdown
# 🧬 PoArt Addendum – Ontology, Ethics & PoArt ID System  

## 🧠 Ontological Foundation  

> “Art, when verified, becomes an act of truth.”

PoArt គឺជាការបង្កើតប្រព័ន្ធសម្រាប់ការផ្ទៀងផ្ទាត់អត្ថន័យនៃស្នាដៃសិល្បៈតាមរយៈអត្រាពិត។  
វាបំបែកស្នាដៃសិល្បៈចេញពីការស្មានថាជាទ្រព្យសម្បត្តិជួញដូរ ហើយដាក់វាក្រោមក្របខ័ណ្ឌនៃ **Forensic Ontology**។  

### Core Principles  

1. **Existence over Representation**  
   > យើងមិនបង្ហាញស្នាដៃដើម្បីឲ្យគេជឿទេ ប៉ុន្តែបង្ហាញការបានកើតឡើង។  
   Creation = event + trace + time.

2. **Truth as a Temporal Function**  
   > ភាពពិតមិនមែនជាចំណុចទេ ប៉ុន្តែជាដំណើរការ (process).  

3. **Value through Irreversibility**  
   > ការបាត់បង់សមត្ថភាពក្នុងការត្រឡប់វិញ គឺជាអនុសញ្ញានៃភាពជាអង្គភាពពិត។  

---

## 🔍 Ethical Context  

PoArt មិនត្រឹមតែជាបច្ចេកវិទ្យា តែជាគោលការណ៍សីលធម៌សម្រាប់សិល្បករ និងប្រព័ន្ធឌីជីថលទាំងមូល។  

### ⚖️ Ethical Directives  

| Principle | Description |
|:--|:--|
| **Transparency** | All creative processes that claim value must be verifiable. |
| **Authenticity** | No forgery or simulation can replace verifiable origin. |
| **Respect for Time** | Human time → irreplaceable → core of value. |
| **Non-exploitation of AI labor** | AI may assist, but not own authorship. |
| **Right to Trace** | Artists retain the right to cryptographically trace their works. |

> PoArt = *Ethical infrastructure for creation.*

---

## 🪪 PoArt ID System  

**PoArt ID** គឺជាប្រព័ន្ធសម្គាល់ស្នាដៃតែមួយគត់ដែលភ្ជាប់ជាមួយ NotarySeal និង EvidenceRoot។  
វាធ្វើឲ្យអាចតាមដានស្នាដៃក្នុងជីវិតឌីជីថលរបស់វា។  

### Structure  

```json
{
  "poart_id": "PFE-2026-01-000394",
  "creator_wallet": "So1anaWalletAddress",
  "notary_seal": "sha512:d221...b72f",
  "registry_uri": "https://registry.poart.io/artwork/PFE-2026-01-000394",
  "version": "1.0"
}
```

> PoArt ID មិនមែនជាតម្លៃហិរញ្ញវត្ថុទេ ប៉ុន្តែជាការធានាផ្នែកអត្តសញ្ញាណនៃស្នាដៃ។  

---

## ⚙️ Verification Example  

### Verify using PoArt CLI  

```bash
poart verify --id PFE-2026-01-000394
```

**Output:**
```text
✔ EvidenceRoot match
✔ NotarySeal verified
✔ Signature valid
✔ Timestamp integrity confirmed
Result: ✅ Authentic (PoArt v1.0 Compliant)
```

> Verification engine បង្ហាញភាពត្រឹមត្រូវជាសាធារណៈ ដោយមិនបង្ហាញឯកសារដើមទេ។  

---

## 🧩 Integration Points  

| System | Purpose |
|:--|:--|
| **Solana Chain** | Anchoring of NotarySeal (immutability layer) |
| **IPFS** | Storage of hashed metadata and evidence |
| **PoArt Gateway API** | JSON-based verification endpoint |
| **Web Layer** | Artwork exhibition, QR validation via PoArt ID |

### Example API Request  

```bash
curl -X GET "https://api.poart.io/v1/verify?id=PFE-2026-01-000394"
```

**Response**
```json
{
  "verified": true,
  "status": "authentic",
  "timestamp": "2026-01-11T09:15:45Z"
}
```

---

## 🧱 Future Extensions  

| Area | Description |
|:--|:--|
| **PFE v2.0** | AI-assisted forensic data classification |
| **PoArt Chain** | Dedicated Layer-1 verification network |
| **Temporal NFTs** | Assets that evolve with creator’s labor logs |
| **PoArt DAO** | Governance by verified creators |

---

## 🪶 Philosophical Postscript  

> “Proof of Art is Proof of Being.”

PoArt ទទួលស្គាល់ថា ស្នាដៃមនុស្សគឺជាភស្តុតាងនៃការរស់នៅ។  
ការបង្កើតគឺជាដំណើរការផលិតភាពពិត ដែលបញ្ចេញពីចិត្តនិងពេលវេលា។  

```math
Existence = Creation + Time + Irreversibility
```

នៅក្នុងអាកាសធាតុ AI ដែលការបង្កើតអាចកើតឡើងភ្លាមៗ —  
PoArt ត្រឡប់មករកអត្ថន័យដើមនៃការបង្កើត:  
**សិល្បៈជាភស្តុតាងនៃមនុស្ស។**

---

## 🔚 Closing Statement  

- PoArt Forensic Engine (PFE) បង្កើតជាមុខងារផ្លូវចិត្តនៃការផ្ទៀងផ្ទាត់ស្នាដៃ។  
- Proof Registry Layer ផ្តល់នូវភាពជឿជាក់តាមសហគមន៍។  
- PoArt ID ផ្តល់អត្តសញ្ញាណជានិច្ចសម្រាប់ស្នាដៃ។  

> “Through proof, we return art to truth.”  
> — PoArt Protocol v1.0, 2026  

---
```
