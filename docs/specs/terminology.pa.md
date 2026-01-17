# 📚 ਸ਼ਬਦਾਵਲੀ ਅਤੇ ਧਾਰਨਾਵਾਂ ਦੀ ਸ਼ਬਦਕੋਸ਼ - ਭਾਗ 1
> **"ਇਸ ਪ੍ਰੋਟੋਕੋਲ ਦੀ ਭਾਸ਼ਾ ਨੂੰ ਸਮਝਣਾ, ਇਸਦੇ ਦ੍ਰਿਸ਼ਟੀਕੋਣ ਨੂੰ ਸਮਝਣਾ ਹੈ।"**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: ਕੋਰ ਬੁਨਿਆਦ

**PoArt Forensic Engine (PFE)**, [PoArt] ਪ੍ਰੋਟੋਕੋਲ ਦੇ ਪਿੱਛੇ ਮੁੱਖ ਤਰਕ ਅਤੇ ਤਕਨੀਕੀ ਕਾਰਜਸ਼ੀਲਤਾ ਨੂੰ ਦਰਸਾਉਂਦੀ ਮੁੱਖ ਪਰਤ ਹੈ। ਕਲਾਕ੍ਰਿਤੀ ਦੇ ਕੱਚੇ ਉਤਪਾਦਨ ਡੇਟਾ ਨੂੰ ਲੈ ਕੇ, ਇਸਨੂੰ ਪ੍ਰਮਾਣਿਤ ਅਤੇ ਅਟੱਲ **ਡਿਜੀਟਲ ਸਬੂਤ** ਵਿੱਚ ਬਦਲਣ ਵਾਲਾ "ਫੋਰੈਂਸਿਕ ਇੰਜਣ" ਇਹ ਹੈ।

### 🧩 ਕਿਉਂ "PoArt Forensic"?

- **PoArt (Proof of Art):** ਇੰਜਣ ਦਾ ਫੋਕਸ, ਇੱਕ ਡਿਜੀਟਲ ਸੰਪੱਤੀ ਦੀ ਕੀਮਤ ਨੂੰ ਕਿਆਸਅਰਾਈ 'ਤੇ ਨਹੀਂ, **ਪ੍ਰਮਾਣਿਤ ਉਤਪਾਦਨ ਪ੍ਰਕਿਰਿਆ** 'ਤੇ ਅਧਾਰਤ ਕਰਨਾ ਹੈ।
- **Forensic (ਫੋਰੈਂਸਿਕ ਪ੍ਰਮਾਣਿਕਤਾ):**
  - **ਤਕਨੀਕੀ ਪਰਿਭਾਸ਼ਾ:** ਉਤਪਾਦਨ ਪ੍ਰਕਿਰਿਆ ਨਾਲ ਸਬੰਧਤ ਡੇਟਾ (ਬ੍ਰਸ਼ ਸਟ੍ਰੋਕਸ, ਟਾਈਮਲੈਪਸ, ਲੌਗਸ) ਨੂੰ ਹੇਰਾਫੇਰੀ ਨਹੀਂ ਕੀਤਾ ਗਿਆ ਹੈ, ਇਹ ਪ੍ਰਮਾਣਿਤ ਕਰਨ ਲਈ ਐਲਗੋਰਿਦਮ ਅਤੇ ਰਿਕਾਰਡ ਚੇਨ ਪਹੁੰਚ।
  - **ਦਾਰਸ਼ਨਿਕ ਪਰਤ:** ਆਰਟੀਫਿਸ਼ੀਅਲ ਇੰਟੈਲੀਜੈਂਸ ਦੇ "ਤੁਰੰਤ ਆਉਟਪੁੱਟ" ਉਤਪਾਦਨ ਦੇ ਵਿਰੁੱਧ; **ਮਨੁੱਖੀ ਸਮੇਂ, ਮਿਹਨਤ ਅਤੇ ਫੈਸਲੇ ਦੀ ਕੀਮਤ** ਵਾਲੇ ਉਤਪਾਦਨ ਨੂੰ ਮਾਪਣਯੋਗ ਵਾਸਤਵਿਕਤਾ ਵਿੱਚ ਬਦਲਣ ਦਾ ਦਾਅਵਾ।

> ਨੋਟ: ਬਲਾਕਚੇਨ (ਜਿਵੇਂ ਕਿ Solana) ਏਕੀਕਰਣ, PFE ਦਾ ਮੁੱਖ ਹਿੱਸਾ ਨਹੀਂ ਹੈ; ਪ੍ਰਮਾਣਿਕਤਾ/ਰਜਿਸਟ੍ਰੀ ਲਈ ਇਹ ਵੱਖਰੇ ਤੌਰ 'ਤੇ ਪਰਿਭਾਸ਼ਿਤ ਕੀਤਾ ਜਾਣ ਵਾਲਾ **Chain Anchor Layer** ਹੈ।

### 🛠️ v1.0 ਤਕਨੀਕੀ ਦਾਇਰਾ

**PoArt Forensic Engine (PFE) v1.0**, ਗੁੰਝਲਦਾਰ ਵਿੱਤੀ ਮਾਡਲਾਂ ਦੀ ਬਜਾਏ ਇਹਨਾਂ **3 ਮੁੱਖ ਥੰਮ੍ਹਾਂ** 'ਤੇ ਬਣਾਇਆ ਗਿਆ ਹੈ:

1. **Hashing & Sealing (ਮੋਹਰਬੰਦੀ):**  
   PFE, Evidence Pack ਵਿੱਚ ਸਾਰੇ ਤੱਤਾਂ (ਕਲਾਕ੍ਰਿਤੀ ਫਾਈਲ, ਵੀਡੀਓ, JSON/ਲੌਗ, ਦਸਤਖ਼ਤ ਆਦਿ) ਨੂੰ ਨਿਰਧਾਰਿਤ ਤਰੀਕੇ ਨਾਲ ਪ੍ਰੋਸੈਸ ਕਰਕੇ ਵਿਲੱਖਣ **NotarySeal** ਮੁੱਲ ਪੈਦਾ ਕਰਦਾ ਹੈ।

   **ਮੁੱਖ ਧਾਰਨਾਵਾਂ (v1.0):**
   - **FileHash (ਕਲਾਕ੍ਰਿਤੀ ਫਿੰਗਰਪ੍ਰਿੰਟ):** ਕਲਾਕ੍ਰਿਤੀ ਫਾਈਲ ਦੇ ਬਾਈਟਸ ਤੋਂ ਤਿਆਰ ਕੀਤਾ ਗਿਆ hash।
   - **EvidenceRoot (ਸਬੂਤ ਪੈਕੇਜ ਰੂਟ):** Evidence Pack ਦੀ ਸੰਪੂਰਨਤਾ ਨੂੰ ਦਰਸਾਉਂਦਾ ਰੂਟ ਸਾਰ (Merkle root ਜਾਂ canonical manifest hash)।
   - **NotarySeal (ਅੰਤਮ ਮੋਹਰ / PFE Output):** EvidenceRoot + ਸਮਾਂ + ਦਸਤਖ਼ਤ ਦੇ ਸੁਮੇਲ ਤੋਂ ਪੈਦਾ ਕੀਤੀ ਅੰਤਮ ਮੋਹਰ।

   **ਫਾਰਮੂਲੇ (ਨਿਵੇਸ਼ਕਾਂ ਲਈ ਸਪਸ਼ਟ ਦਿਖਾਈ ਦੇਣ ਵਾਲੇ ਰੂਪ ਵਿੱਚ):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload ਪਰਿਭਾਸ਼ਾਵਾਂ (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > ਨੋਟ: PFE ਆਉਟਪੁੱਟ ਵਜੋਂ ਸੰਕੇਤ ਕੀਤਾ ਗਿਆ ਮੁੱਲ **NotarySeal** ਹੈ। **SignerSignature** ਵਿਧੀ ਫੇਜ਼ 2 ਵਿੱਚ (Solana Wallet Adapter ਨਾਲ) ਕਿਰਿਆਸ਼ੀਲ ਕੀਤੀ ਜਾਵੇਗੀ; ਮੌਜੂਦਾ v1.0 ਵਿੱਚ ਸਿਸਟਮ ਦਾ ਆਪਣਾ attestation ਦਸਤਖ਼ਤ ਵਰਤਿਆ ਜਾਂਦਾ ਹੈ। Attestation public key ਰਜਿਸਟ੍ਰੀ ਵਿੱਚ `issuer.attestation_pubkey` ਫੀਲਡ ਵਿੱਚ ਪ੍ਰਕਾਸ਼ਿਤ ਕੀਤੀ ਜਾਂਦੀ ਹੈ।

2. **Indexing (ਪੁਰਾਲੇਖ):**  
   ਕਿਹੜੇ ਵਾਲਿਟ ਨੇ, ਕਿਸ ਤਾਰੀਖ਼ 'ਤੇ, ਕਿਸ ਕਲਾਕ੍ਰਿਤੀ ਲਈ **Labor Proof (ਮਿਹਨਤ ਦਾ ਸਬੂਤ)** ਪੇਸ਼ ਕੀਤਾ, ਇਹ; ਪਾਰਦਰਸ਼ੀ ਅਤੇ ਖੋਜਯੋਗ ਰਿਕਾਰਡ ਪਰਤ ਵਿੱਚ ਦਰਜ ਕਰਦਾ ਹੈ।  
   *(ਇਹ ਪਰਤ ਡੇਟਾਬੇਸ ਹੋ ਸਕਦੀ ਹੈ; ਚੇਨ ਏਕੀਕਰਣ ਵੱਖਰੇ ਤੌਰ 'ਤੇ "Chain Anchor Layer" ਵਜੋਂ ਪਰਿਭਾਸ਼ਿਤ ਕੀਤਾ ਜਾਂਦਾ ਹੈ।)*

3. **Verification (ਪ੍ਰਮਾਣਿਕਤਾ):**  
   ਜਦੋਂ ਕਿਸੇ ਕਲਾਕ੍ਰਿਤੀ ਦੀ ਮੂਲਤਾ ਬਾਰੇ ਪੁੱਛਗਿੱਛ ਕੀਤੀ ਜਾਂਦੀ ਹੈ ਤਾਂ PFE, ਕੱਚੇ ਸਬੂਤਾਂ ਨੂੰ ਦੁਬਾਰਾ ਪ੍ਰੋਸੈਸ ਕਰਦਾ ਹੈ; ਗਣਿਤ ਕੀਤੇ **EvidenceRoot / NotarySeal** ਮੁੱਲਾਂ ਦਾ ਪੁਰਾਲੇਖ ਵਿੱਚ ਰਿਕਾਰਡ ਨਾਲ ਮੇਲ ਖਾਂਦਾ ਹੈ ਜਾਂ ਨਹੀਂ, ਇਹ ਗਣਿਤਿਕ ਨਿਸ਼ਚਿਤਤਾ ਨਾਲ ਟੈਸਟ ਕਰਦਾ ਹੈ।

---

### 🧮 PoArt ਮੁੱਲ ਸਿਧਾਂਤ (The Value Theorem)

[PoArt] ਪ੍ਰੋਟੋਕੋਲ, ਇੱਕ ਡਿਜੀਟਲ ਸੰਪੱਤੀ ਦੀ ਕੀਮਤ ($V$) ਨੂੰ ਵਿਅਕਤੀਗਤ ਬਜ਼ਾਰ ਧਾਰਨਾ ਨਾਲ ਨਹੀਂ, **ਉਤਪਾਦਨ ਪ੍ਰਕਿਰਿਆ ਦੀ ਭੌਤਿਕ ਵਾਸਤਵਿਕਤਾ** ਨਾਲ ਜੋੜਦਾ ਹੈ।

ਆਰਟੀਫਿਸ਼ੀਅਲ ਇੰਟੈਲੀਜੈਂਸ (AI), ਨਤੀਜਾ ਤੁਰੰਤ ਦੇ ਕੇ ($t \to 0$) ਪ੍ਰਕਿਰਿਆ ਨੂੰ ਖ਼ਤਮ ਕਰ ਦਿੰਦੀ ਹੈ। [PoArt] ਕੀਮਤ ਨੂੰ; **ਸਮਾਂ, ਮਿਹਨਤ ਅਤੇ ਇੱਛਾ** ਤੱਤਾਂ ਦੇ ਸੰਚਿਤ ਰੂਪ ਵਜੋਂ ਲੈਂਦਾ ਹੈ।

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### ਚਰਾਂ ਦੀ ਪਰਿਭਾਸ਼ਾ

- **$\int dt$ (ਪ੍ਰਕਿਰਿਆ ਸੰਚਿਤੀ):**  
  ਕੀਮਤ, ਤੁਰੰਤ "ਆਉਟਪੁੱਟ" ਨਹੀਂ ਹੈ; $t_{\text{start}}$ ਅਤੇ $t_{\text{end}}$ ਵਿਚਕਾਰ ਇਕੱਠੀ ਹੋਈ **ਪ੍ਰਕਿਰਿਆ** ਹੈ।

- **$P_{\text{labor}}(t)$ (ਤੁਰੰਤ ਮਿਹਨਤ ਸ਼ਕਤੀ):**  
  ਉਤਪਾਦਨ ਸਮੇਂ ਖਰਚ ਕੀਤੀ ਗਈ ਮਾਨਸਿਕ ਅਤੇ ਸਰੀਰਕ ਮਿਹਨਤ ਦੀ ਤੀਬਰਤਾ।

- **$I_{\text{agency}}(t)$ (ਇੱਛਾ ਗੁਣਾਂਕ):**  
  ਉਤਪਾਦਕ ਦੀ ਜੋਖਮ ਲੈਣ ਅਤੇ ਫੈਸਲਾ ਲੈਣ ਦੀ ਸਮਰੱਥਾ।

- **$U_{\text{irreversible}}$ (ਅਟੱਲ ਵਿਲੱਖਣਤਾ):**  
  ਭੌਤਿਕ ਉਤਪਾਦਨ ਵਿੱਚ ਗੇਰੀ ਡੋਂਦਰੂਲੈਂਮਜ਼ਲਕ ਤਰਲੀਕਨ।

---

## 🎨 [PoArt] ਮਿਹਨਤ ਸਬੂਤ ਪ੍ਰੋਟੋਕੋਲ (Proof of Art Protocol v1.0)

> **"ਅਸਲੀ ਕਲਾਕਾਰ, ਅਸਲੀ ਉਤਪਾਦਨ, ਅਸਲੀ ਮੁੱਲ।"**

ਇਹ ਪ੍ਰੋਟੋਕੋਲ; ਕ੍ਰਿਪਟੋ ਈਕੋਸਿਸਟਮ ਨੂੰ ਘੇਰਨ ਵਾਲੇ ਅਗਿਆਤ ਧੋਖੇਬਾਜ਼ਾਂ, 5 ਮਿੰਟ ਵਿੱਚ ਤਿਆਰ ਕੀਤੇ ਆਰਟੀਫਿਸ਼ੀਅਲ ਇੰਟੈਲੀਜੈਂਸ ਦ੍ਰਿਸ਼ਾਂ ਅਤੇ "Pump & Dump" ਸੱਭਿਆਚਾਰ ਦੇ ਵਿਰੁੱਧ ਵਿਕਸਤ ਕੀਤੀ ਗਈ **ਜੈਵਿਕ ਅਤੇ ਬੌਧਿਕ ਰੱਖਿਆ ਵਿਧੀ ਹੈ।**

## a) [PoArt] ਕੀ ਹੈ?

**Proof of Art [PoArt];** ਬਲਾਕਚੇਨ 'ਤੇ ਇੱਕ ਸੰਪੱਤੀ ਦੇ ਪਿੱਛੇ ਮੁੱਲ ਦਾ, ਕਿਆਸਅਰਾਈ 'ਤੇ ਨਹੀਂ; ਪ੍ਰਮਾਣਿਤ **ਮਨੁੱਖੀ ਮਿਹਨਤ**, **ਸਮੇਂ** ਅਤੇ **ਭੌਤਿਕ ਊਰਜਾ** 'ਤੇ ਅਧਾਰਤ ਹੋਣ ਦੀ ਗਾਰੰਟੀ ਦੇਣ ਵਾਲਾ ਸੰਸਥਾਗਤ ਪ੍ਰਮਾਣਿਕਤਾ ਮਿਆਰ ਹੈ।

> **[PoArt], ਭਾਗੀਦਾਰ ਨੂੰ "ਸਾਡੇ 'ਤੇ ਭਰੋਸਾ ਕਰੋ" ਨਹੀਂ ਕਹਿੰਦਾ; "ਇਹ ਸਬੂਤ ਹਨ, ਆਪਣੀਆਂ ਅੱਖਾਂ ਨਾਲ ਦੇਖੋ, ਆਪਣੇ ਗਣਿਤ ਨਾਲ ਪ੍ਰਮਾਣਿਤ ਕਰੋ" ਕਹਿੰਦਾ ਹੈ।**

## b) [PoArt] 5-ਥੰਮ੍ਹ ਮਿਆਰ

### 1) ਲਾਈਵ ਪਛਾਣ ਸਬੂਤ (Live Identity Proof)

- **ਸਮੱਸਿਆ:** ਕ੍ਰਿਪਟੋ ਦੁਨੀਆ, ਪਛਾਣ-ਰਹਿਤ ਅਗਿਆਤ ਸੰਸਥਾਪਕਾਂ ਦੁਆਰਾ ਪੈਸੇ ਇਕੱਠੇ ਕਰਕੇ ਪ੍ਰੋਜੈਕਟ ਛੱਡਣ ਨਾਲ ਭਰੀ ਪਈ ਹੈ।
- **[PoArt] ਹੱਲ:** ਉਤਪਾਦਕ, ਸਿਰਫ਼ ਪਛਾਣ ਪੱਤਰ ਹੀ ਨਹੀਂ, **ਉਤਪਾਦਨ ਸਮੇਂ ਆਪਣੀ ਮੌਜੂਦਗੀ** ਸਾਬਤ ਕਰਦਾ ਹੈ।

### 2) ਮਿਹਨਤ ਅਤੇ ਪ੍ਰਕਿਰਿਆ ਸਬੂਤ (Labor & Process Proof)

- **ਸਮੱਸਿਆ:** 2 ਸਕਿੰਟ ਵਿੱਚ ਤਿਆਰ AI ਦ੍ਰਿਸ਼ ਅਤੇ 2 ਮਹੀਨਿਆਂ ਵਿੱਚ ਬਣੀ ਪੇਂਟਿੰਗ ਦਾ ਇੱਕੋ "jpeg" ਵਾਂਗ ਪੇਸ਼ ਆਉਣਾ।
- **[PoArt] ਹੱਲ:** ਕਲਾਕ੍ਰਿਤੀ ਦੀ "ਗਰਭ ਅਤੇ ਜਨਮ" ਪ੍ਰਕਿਰਿਆ ਰਿਕਾਰਡ ਕੀਤੀ ਜਾਂਦੀ ਹੈ।

### 3) ਸੁਹਜ ਮੁੱਲ ਸਬੂਤ (Aesthetic Value Proof)

- **ਸਮੱਸਿਆ:** "Meme" ਸੱਭਿਆਚਾਰ ਸਿਰਫ਼ ਤੁਰੰਤ ਕਾਮੇਡੀ 'ਤੇ ਧਿਆਨ ਕੇਂਦਰਿਤ ਕਰਦਾ ਹੈ।
- **[PoArt] ਹੱਲ:** ਪ੍ਰੋਜੈਕਟ, ਅਕਾਦਮਿਕ ਕਲਾ ਮਿਆਰਾਂ, ਰੰਗ ਸਿਧਾਂਤ, ਰਚਨਾ ਨਿਯਮਾਂ ਦਾ ਮਾਲਕ ਹੋਣਾ ਚਾਹੀਦਾ ਹੈ।

### 4) ਵਿਚਾਰਕ ਨਵੀਨਤਾ (Conceptual Novelty)

- **ਸਮੱਸਿਆ:** ਇੱਕ ਦੂਜੇ ਦੀਆਂ ਨਕਲਾਂ, ਰਚਨਾਤਮਕਤਾ ਤੋਂ ਦੂਰ ਹਜ਼ਾਰਾਂ ਸਿੱਕੇ।
- **[PoArt] ਹੱਲ:** ਪ੍ਰੋਜੈਕਟ; ਕਲਾ, ਵਿਗਿਆਨ, ਦਰਸ਼ਨ ਜਾਂ ਟੈਕਨਾਲੋਜੀ ਨੂੰ ਅਰਥਪੂਰਨ ਢਾਂਚੇ ਵਿੱਚ ਜੋੜਨ ਵਾਲਾ ਨਵਾਂ ਪੁਲ ਬਣਾਉਣਾ ਚਾਹੀਦਾ ਹੈ।

### 5) ਐਲਗੋਰਿਦਮਿਕ-ਰਹਿਤ ਇੱਛਾ (Non-Algorithmic Agency)

- **ਸਮੱਸਿਆ:** ਸੰਪੂਰਨ ਪਰ ਆਤਮਾ-ਰਹਿਤ ਡਿਜੀਟਲ ਉਤਪਾਦਨ।
- **[PoArt] ਹੱਲ:** ਮਨੁੱਖ ਦੀ ਗਲਤੀ ਕਰ ਸਕਣ ਵਾਲੀ, ਜੋਖਮ ਲੈਣ ਵਾਲੀ ਮੌਲਿਕ ਇੱਛਾ ਕਲਾਕ੍ਰਿਤੀ ਵਿੱਚ ਮਹਿਸੂਸ ਹੋਣੀ ਚਾਹੀਦੀ ਹੈ।

---

## c) ਪ੍ਰਮਾਣਿਕਤਾ ਅਤੇ ਧੋਖਾਧੜੀ-ਵਿਰੋਧੀ ਵਿਧੀ

### 📦 ਸਬੂਤ ਪੈਕੇਜ (Evidence Pack)

ਹਰ [PoArt] ਪ੍ਰਮਾਣਿਤ ਕਲਾਕ੍ਰਿਤੀ ਦੇ ਪਿੱਛੇ, ਨਿਵੇਸ਼ਕਾਂ ਦੁਆਰਾ ਡਾਊਨਲੋਡ ਕੀਤੇ ਜਾ ਸਕਣ ਵਾਲਾ ਡੇਟਾ ਪੈਕੇਜ ਹੈ:

- **RAW ਵੀਡੀਓ ਰਿਕਾਰਡਿੰਗ:** ਉਤਪਾਦਨ ਪਲ ਦੀ ਲਗਾਤਾਰ ਕੱਚੀ ਤਸਵੀਰਾਂ
- **Metadata ਵਿਸ਼ਲੇਸ਼ਣ:** ਫਾਈਲ ਬਣਾਉਣ ਦੀ ਤਾਰੀਖ਼, ਯੰਤਰ ਜਾਣਕਾਰੀ
- **ਭੌਤਿਕ ਹਵਾਲੇ:** ਭੌਤਿਕ ਦੁਨੀਆ ਵਿੱਚ ਮੌਜੂਦਗੀ ਦੇ ਸਬੂਤ

### 🔄 365 ਦਿਨ ਨਵੀਨੀਕਰਣ (Sustainability Protocol)

- **ਕ੍ਰਾਂਤੀਕਾਰੀ ਵਿਸ਼ੇਸ਼ਤਾ:** "Verified Artist" ਰੁਤਬਾ ਜੀਵਨ ਭਰ ਦਾ ਨਹੀਂ। ਸਿਰਫ਼ **1 ਸਾਲ** ਵੈਧ।
- **ਨਿਯਮ:** ਕਲਾਕਾਰ/ਡਿਵੈਲਪਰ, ਹਰ 365 ਦਿਨਾਂ ਵਿੱਚ ਇੱਕ ਵਾਰ, ਨਵੀਂ ਪ੍ਰਮਾਣਿਤ ਕਲਾਕ੍ਰਿਤੀ ਪੇਸ਼ ਕਰਨ ਲਈ ਮਜਬੂਰ।

### 🚩 ਲਾਲ ਝੰਡਾ (Red Flag Protocol)

ਭਾਈਚਾਰੇ ਜਾਂ ਐਲਗੋਰਿਦਮ ਦੁਆਰਾ ਪਤਾ ਲਗਾਈ ਗਈ ਧੋਖਾਧੜੀ (AI ਵਰਤੋਂ, ਚੋਰੀ, ਹੇਰਾਫੇਰੀ):

1. ਸਰਟੀਫਿਕੇਟ **"VOID"** ਵਜੋਂ ਚਿੰਨ੍ਹਿਤ
2. ਸਬੂਤ ਪੈਕੇਜ **"ਨਕਲੀ"** ਵਜੋਂ ਟੈਗ
3. ਪ੍ਰੋਜੈਕਟ, [PoArt] ਕਾਲੀ ਸੂਚੀ ਵਿੱਚ
4. ਕਿਸੇ ਵੀ ਪ੍ਰਕਾਸ਼ਨ ਵਿੱਚ [PoArt] ਸ਼ਬਦ ਵਰਤਣ 'ਤੇ ਪਾਬੰਦੀ

---

## d) ਸਿੱਟਾ: ਜੂਆਘਰ ਨਹੀਂ, ਅਜਾਇਬਘਰ

**Pump.fun ਅਤੇ DEX ਹੁਣ ਬਦਕਿਸਮਤੀ ਨਾਲ ਜੂਆਘਰ ਹਨ। [PoArt], ਇਸ ਜੂਆਘਰ ਦੇ ਵਿਚਕਾਰ ਬਣਾਇਆ ਗਿਆ ਕਿਲ੍ਹਾ ਹੈ।**

- 🎰 ਜੂਆਘਰ ਕਾਗਜ਼ ਖੇਡਾਂ 'ਤੇ ਨਿਰਭਰ; ਅਸੀਂ **ਭੌਤਿਕ ਵਾਸਤਵਿਕਤਾ** 'ਤੇ
- 🃏 ਜੂਆਘਰ ਧੋਖੇ ਲਈ ਖੁੱਲ੍ਹਾ; ਅਸੀਂ **ਪਾਰਦਰਸ਼ੀ ਸਬੂਤਾਂ** ਲਈ ਖੁੱਲ੍ਹੇ
- ⏳ ਜੂਆਘਰ ਅਸਥਾਈ; ਅਸੀਂ **ਕਲਾ ਅਤੇ ਵਿਗਿਆਨ ਦੀ ਸਦੀਵਤਾ** 'ਤੇ ਕੇਂਦਰਿਤ

**ਇਸ ਪ੍ਰੋਟੋਕੋਲ ਨੂੰ ਵਰਤਣ ਵਾਲਾ ਟੋਕਨ, ਸਿਰਫ਼ "coin" ਨਹੀਂ; ਪਿੱਛੇ ਪਸੀਨਾ, ਰੰਗ, ਕੋਡ ਅਤੇ ਦਰਸ਼ਨ ਰੱਖਣ ਵਾਲਾ ਡਿਜੀਟਲ ਸ਼ੇਅਰ ਹੈ।**

---

**(ਭਾਗ 1 ਦਾ ਅੰਤ - ਭਾਗ 2 ਜਾਰੀ...)**
# PoArt ਪ੍ਰੋਟੋਕੋਲ - ਭਾਗ 2

## 🗳️ 6) ਯੋਨੇਸ਼ਿਮ ਅਤੇ ਜਨਤਕ ਰਜਿਸਟਰੀ (Governance & Public Registry)

**ਇਸ ਭਾਗ ਦਾ ਉਦੇਸ਼: [PoArt] ਮਿਆਰ ਨੂੰ "ਵਿਅਕਤੀਆਂ 'ਤੇ ਭਰੋਸਾ" ਦਿਸ਼ਾ ਤੋਂ ਕੱਢ ਕੇ, ਰਿਕਾਰਡ + ਪ੍ਰਮਾਣਿਕਤਾ + ਭਾਈਚਾਰਾ ਨਿਗਰਾਨੀ ਨਾਲ ਟਿਕਾਊ ਜਨਤਕ ਬੁਨਿਆਦ ਵਿੱਚ ਬਦਲਣਾ।**

### 6.1 Public Registry (ਜਨਤਕ ਰਜਿਸਟਰੀ)

- **Public Registry:** ਸਾਰੇ ਮਨਜ਼ੂਰ ਡੇਟਾ `ilhanart.org/registry` (ਜਾਂ GitHub Registry) 'ਤੇ ਰਿਕਾਰਡ ਕੀਤੇ ਜਾਂਦੇ ਹਨ।

**ਰਿਕਾਰਡ ਤਰਕ (ਸੁਝਾਈ ਮਿਆਰ - JSON path ਫਾਰਮੈਟ):**

ਰਜਿਸਟਰੀ ਵਿੱਚ ਹਰ ਰਿਕਾਰਡ, ਘੱਟੋ-ਘੱਟ ਇਹ ਪ੍ਰਮਾਣਿਤ ਕੇਂਦਰੀ ਖੇਤਰ ਰੱਖਦਾ ਹੈ:

- **ਪਛਾਣ ਅਤੇ ਸਥਿਤੀ:**
  - `certificate_id` (ਪੜ੍ਹਨਯੋਗ ਹਵਾਲਾ)
  - `status` (active / void)
  - `void_reason` (ਜੇਕਰ ਹੋਵੇ)
  - `visibility` (private / masked / public)
  - `created_at` (ਸਮਾਂ ਮੋਹਰ)

- **ਜਾਰੀਕਰਤਾ:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **ਕਲਾਕ੍ਰਿਤੀ ਜਾਣਕਾਰੀ:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet`
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **ਫੋਰੈਂਸਿਕ ਡੇਟਾ:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **ਕ੍ਰਿਪਟੋਗ੍ਰਾਫਿਕ ਸਬੂਤ:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **ਯੋਨੇਸ਼ਿਮ:**
  - `governance.decision`
  - `governance.review_notes`

---

### 6.2 PoArt Verified ਅਰਜ਼ੀ ਪ੍ਰਕਿਰਿਆ

**PoArt Verified ਅਰਜ਼ੀਆਂ, İlhanArt Gallery ਦੁਆਰਾ 5 PoArt ਮਿਆਰਾਂ ਅਨੁਸਾਰ ਮੁਲਾਂਕਣ ਕੀਤੀਆਂ ਜਾਂਦੀਆਂ ਹਨ।**

#### ਅਰਜ਼ੀ ਪ੍ਰਕਿਰਿਆ

**ਅਰਜ਼ੀ:**
- ਕਲਾਕਾਰ/ਪ੍ਰੋਜੈਕਟ PoArt Verified ਅਰਜ਼ੀ ਦਿੰਦਾ ਹੈ
- Evidence Pack ਤਿਆਰ ਕੀਤਾ ਜਾਂਦਾ ਹੈ
- ਅਰਜ਼ੀ İlhanArt Gallery ਨੂੰ ਭੇਜੀ ਜਾਂਦੀ ਹੈ

**ਜਾਂਚ (30 ਦਿਨ):**
- ਗੈਲਰੀ ਟੀਮ Evidence Pack ਦੀ ਵਿਸਤਾਰ ਨਾਲ ਜਾਂਚ
- ਸਾਰੇ 5 PoArt ਮਿਆਰ ਜਾਂਚੇ ਜਾਂਦੇ ਹਨ
- ਕਲਾਕਾਰ ਨਾਲ ਇੰਟਰਵਿਊ (ਵਿਕਲਪਿਕ)

**ਭਾਈਚਾਰਾ ਸਲਾਹ:**
- Evidence Pack ਜਨਤਾ ਨਾਲ ਸਾਂਝੀ
- ਭਾਈਚਾਰਾ ilhanart.org ਰਾਹੀਂ ਫੀਡਬੈਕ ਦੇ ਸਕਦਾ ਹੈ
- Token holder (ਘੱਟੋ-ਘੱਟ 10,000 $CULTURE) ਸੁਝਾਅ ਦੇ ਸਕਦੇ ਹਨ
- **ਸਾਰਾ ਫੀਡਬੈਕ ਜਾਂਚ ਵਿੱਚ ਧਿਆਨ ਵਿੱਚ ਰੱਖਿਆ ਜਾਂਦਾ ਹੈ**
- **ਪਰ ਅੰਤਮ ਫੈਸਲਾ, ਕਿਉਰੇਟੋਰੀਅਲ ਮੁਲਾਂਕਣ 'ਤੇ ਨਿਰਭਰ**

**ਫੈਸਲਾ:**
- ਗੈਲਰੀ, ਅਰਜ਼ੀ ਨੂੰ ਮਨਜ਼ੂਰ ਜਾਂ ਰੱਦ ਕਰਦੀ ਹੈ
- ਫੈਸਲੇ ਦਾ ਕਾਰਨ ਪਾਰਦਰਸ਼ੀ ਢੰਗ ਨਾਲ ਸਪੱਸ਼ਟ
- ਮਨਜ਼ੂਰ → PoArt Verified badge
- ਰੱਦ → 6 ਮਹੀਨੇ ਬਾਅਦ ਦੁਬਾਰਾ ਅਰਜ਼ੀ

**ਪਾਰਦਰਸ਼ਤਾ:**
- ਸਾਰੀਆਂ ਅਰਜ਼ੀਆਂ ਅਤੇ ਫੈਸਲੇ ilhanart.org/registry 'ਤੇ ਰਿਕਾਰਡ

#### ਕਿਉਂ ਕਿਉਰੇਟੋਰੀਅਲ ਫੈਸਲਾ?

**ਗੁਣਵੱਤਾ ਨਿਯੰਤਰਣ:**  
PoArt Verified ਸਥਿਤੀ, ਉੱਚ ਮਿਆਰਾਂ ਵਾਲੀ badge ਹੈ।

**ਕਿਆਸਅਰਾਈ ਹੇਰਾਫੇਰੀ ਰੋਕਥਾਮ:**  
Pump.fun ਟੋਕਨਾਂ ਨਾਲ ਪੂਰੀ on-chain governance ਤਕਨੀਕੀ ਤੌਰ 'ਤੇ ਸੰਭਵ ਨਹੀਂ।

**ਸੰਚਾਲਨ ਕੁਸ਼ਲਤਾ:**  
ਗੁੰਝਲਦਾਰ voting ਵਿਧੀਆਂ ਦੀ ਬਜਾਏ, ਤੇਜ਼ ਅਤੇ ਸਪੱਸ਼ਟ ਫੈਸਲਾ।

---

### 6.3 Token Utility (ਟੋਕਨ ਵਰਤੋਂ ਖੇਤਰ)

**$CULTURE token holder ਨੂੰ ਪ੍ਰਦਾਨ ਕੀਤੇ ਲਾਭ:**

**1. ਗੈਲਰੀ ਸਮਾਗਮਾਂ ਤਕ ਪਹਿਲੀ ਪਹੁੰਚ:**
- İlhanArt Gallery ਵਿੱਚ ਸਾਲ ਵਿੱਚ 1 ਹਫਤੇ ਪ੍ਰਦਰਸ਼ਨੀ ਕਰਨ ਦਾ ਅਧਿਕਾਰ (ਅਧਿਕਾਰ ਤਬਦੀਲਯੋਗ)
- Drop painting ਛੋਟਾਂ
- ਗੈਲਰੀ ਵਿੱਚ ਪੇਂਟਿੰਗਾਂ 'ਤੇ 10% ਤੋਂ 30% ਛੋਟ

**2. PoArt Registry ਪੂਰੀ ਪਹੁੰਚ:**
- ਸਾਰੀਆਂ authenticated artworks ਦੇ ਵਿਸਤ੍ਰਿਤ ਰਿਕਾਰਡ
- Evidence Pack ਦੇ ਪੂਰੇ ਸੰਸਕਰਣ
- Forensic verification ਸਾਧਨ

**3. Advisory Voting:**
- PoArt Verified ਅਰਜ਼ੀਆਂ ਵਿੱਚ ਸਲਾਹ ਅਧਿਕਾਰ
- ਭਾਈਚਾਰਾ ਫੀਡਬੈਕ ਚੈਨਲਾਂ ਤਕ ਪਹੁੰਚ

**4. Exclusive Content:**
- ਸਟੂਡੀਓ behind-the-scenes ਸਮੱਗਰੀ
- ਕਲਾਕਾਰ ਇੰਟਰਵਿਊ ਅਤੇ ਪ੍ਰਕਿਰਿਆ ਵੀਡੀਓ

---

### 6.4 Metadata Sync (ਭੌਤਿਕ ਦੁਨੀਆ ਨਾਲ ਮੇਲ)

**"100% ਮੇਲ" ਨੂੰ ਤਕਨੀਕੀ ਤੌਰ 'ਤੇ ਪਰਿਭਾਸ਼ਿਤ ਕਰਨਾ:**

- **ਘੱਟੋ-ਘੱਟ ਮੇਲ (ਲਾਜ਼ਮੀ):**
  - ਰਜਿਸਟਰੀ ਵਿੱਚ `asset.fingerprints.sha256/sha512` ਅਤੇ ਹੱਥ ਵਿੱਚ ਫਾਈਲ ਦਾ hash **ਬਿਲਕੁਲ ਇੱਕੋ**
  - ਰਜਿਸਟਰੀ ਵਿੱਚ `proof.notary_seal` ਦੁਬਾਰਾ ਤਿਆਰ ਕਰਨ 'ਤੇ **ਬਿਲਕੁਲ ਇੱਕੋ**

---

### 6.5 ਇਤਰਾਜ਼, ਜਾਂਚ ਅਤੇ ਰੱਦ (Dispute & Revocation)

ਰਜਿਸਟਰੀ, ਸਿਰਫ਼ "ਮਨਜ਼ੂਰੀ" ਵਿਧੀ ਨਹੀਂ; **ਧੋਖਾਧੜੀ ਦੇ ਵਿਰੁੱਧ ਜੀਵੰਤ ਨਿਗਰਾਨੀ** ਵਿਧੀ ਹੈ।

- ਇਤਰਾਜ਼ ਸ਼ੁਰੂ ਹੋਣ 'ਤੇ ਰਿਕਾਰਡ **"review"** ਮੋਡ ਵਿੱਚ
- ਧੋਖਾਧੜੀ ਪਤਾ ਲੱਗਣ 'ਤੇ `status: void` ਵਜੋਂ ਚਿੰਨ੍ਹਿਤ ਅਤੇ ਕਾਰਨ ਜੋੜਿਆ ਜਾਂਦਾ ਹੈ:
  - `void_reason` (AI ਵਰਤੋਂ / ਚੋਰੀ / ਹੇਰਾਫੇਰੀ ਆਦਿ)
  - `revoked_at` (ਰੱਦ ਸਮਾਂ)

---

### 6.6 ਉਦਾਹਰਨ ਰਜਿਸਟਰੀ ਰਿਕਾਰਡ (Machine-readable)

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

## 7) 🔐 ਤਕਨੀਕੀ ਮੋਹਰ (NOTARY SEAL)

**PoArt Forensic Engine (PFE) v1.0** ਦੁਆਰਾ ਤਿਆਰ ਕੀਤੀ ਅਟੱਲ ਮੋਹਰ ਐਲਗੋਰਿਦਮ:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

## 🛡️ ਵਰਤੋਂ ਖੇਤਰ ਅਤੇ ਲਾਭ

ਜੇਕਰ ਤੁਸੀਂ ਕਲਾਕਾਰ, ਲੇਖਕ ਜਾਂ ਡਿਜ਼ਾਈਨਰ ਹੋ, "ਮੈਂ ਇਹ ਪਹਿਲਾਂ ਕੀਤਾ ਸੀ" ਕਹਿਣਾ ਕਾਫ਼ੀ ਨਹੀਂ, ਸਾਬਤ ਕਰਨਾ ਜ਼ਰੂਰੀ ਹੈ।

**PoArt ਨਾਲ ਮੋਹਰਬੰਦ ਕਲਾਕ੍ਰਿਤੀ:**

- **ਗਣਿਤਿਕ ਸਬੂਤ:** ਤੁਹਾਡੀ ਫਾਈਲ ਦਾ ਇੱਕ pixel ਵੀ ਬਦਲੇ ਤਾਂ ਸਿਸਟਮ ਸਮਝ ਜਾਂਦਾ ਹੈ
- **ਕਾਨੂੰਨੀ ਅਧਾਰ:** ਕਲਾਕ੍ਰਿਤੀ ਕਿਸ ਤਾਰੀਖ਼, ਕਿਸ ਸ਼ਹਿਰ, ਕਿਸ ਯੰਤਰ ਤੋਂ ਮੋਹਰਬੰਦ ਕੀਤੀ, ਰਿਕਾਰਡ ਵਿੱਚ
- **ਤੁਰੰਤ ਸਰਟੀਫਿਕੇਟ:** ਸਕਿੰਟਾਂ ਵਿੱਚ ਤੁਹਾਡੇ ਲਈ ਖਾਸ, QR ਕੋਡ ਵਾਲਾ ਸਰਟੀਫਿਕੇਟ

---

## ⚙️ ਸਿਸਟਮ ਢਾਂਚਾ ਅਤੇ ਤਕਨੀਕੀ ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ

| ਪਰਤ | ਟੈਕਨਾਲੋਜੀ | ਵਰਣਨ |
|--------|-----------|----------|
| **Cryptography** | SHA-256 & SHA-512 | ਦੋ-ਪਰਤੀ ਕ੍ਰਿਪਟੋਗ੍ਰਾਫਿਕ ਸਾਰ |
| **Database** | Supabase (PostgreSQL) | JSONB ਡੇਟਾ ਢਾਂਚਾ |
| **Forensic Data** | ipapi.co API | IP/ਸਥਾਨ/ਸਮਾਂ ਤਿੰਨੇ |
| **Rendering** | html2canvas + jsPDF | Client-side PNG/PDF |
| **Frontend** | Vanilla JavaScript | ਜ਼ੀਰੋ framework dependency |
| **Security** | Client-side hashing | ਫਾਈਲ ਕਦੇ ਸਰਵਰ 'ਤੇ ਨਹੀਂ |

---

## 🗺️ ਰੋਡਮੈਪ: "Trustless" ਭਵਿੱਖ

### ਫੇਜ਼ 1: Beta v1.0 (ਹੁਣ ਲਾਈਵ)

**ਬੁਨਿਆਦ:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + IPFS backup)
- Gallery self-attestation

**ਟੋਕਨ:**
- Platform: Pump.fun
- Liquidity: Raydium (automatic)
- Governance: Advisory only

**ਉਦੇਸ਼:**
- ਰਫ਼ਤਾਰ, UX ਰੁਕਾਵਟਾਂ ਹਟਾਉਣਾ
- "ਰਗੜ-ਰਹਿਤ" ਸੁਰੱਖਿਆ
- ਭਾਈਚਾਰਾ ਬਣਾਉਣਾ

---

### 🚀 ਫੇਜ਼ 2: Decentralized Authority (2026 Q2-Q4)

| ਵਿਸ਼ੇਸ਼ਤਾ | ਕੀ ਦਿੰਦੀ ਹੈ? | Tech Stack | ETA |
|---------|---------------|------------|-----|
| **Edge Function INSERT** | Spam ਰੋਕ + API Key ਸੁਰੱਖਿਆ | Supabase Edge (Deno) | Q2 2026 |
| **Wallet ਦਸਤਖ਼ਤ** | Decentralized identity | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | Decentralized ਪੁਰਾਲੇਖ | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | ਨਕਲੀ ਸਰਟੀਫਿਕੇਟ ਰੱਦ | DB Schema Update | Q2 2026 |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain voting (x/web) + wallet signature
- Community representatives ਚੋਣ
- Multi-sig operations
- Weighted advisory voting (whale cap ਨਾਲ)

---

### ਫੇਜ਼ 3: ਪੂਰੀ ਵਿਕੇਂਦਰੀਕਰਣ (2027+)

| ਵਿਸ਼ੇਸ਼ਤਾ | ਟੀਚਾ | ETA |
|---------|-------|-----|
| **On-Chain Registry** | Solana on-chain ਰਿਕਾਰਡ | Q1 2027 |
| **Enhanced Token Utility** | NFT mint, advanced features | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **Legal Recognition** | ਤੁਰਕੀ ਦੀਆਂ ਅਦਾਲਤਾਂ ਵਿੱਚ ਵੈਧਤਾ | 2027-2028 |

---

## 🧬 ਪ੍ਰੋਟੋਕੋਲ ਡੇਟਾ ਢਾਂਚਾ (JSON Schema)

**ਹਰ [PoArt] ਸਰਟੀਫਿਕੇਟ, ਇਸ ਮਿਆਰ ਵਿੱਚ ਤਿਆਰ ਕੀਤਾ ਗਿਆ JSON ਪਛਾਣ ਪੱਤਰ ਹੈ:**

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
      "sha512": "41e5e0d007a2a77b6e0e3ebc548fbaa2788ea265193434f58d23e8c0f5bb20a0..."
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

## 🔬 ਤਕਨੀਕੀ ਡੂੰਘਾਈ: ਮੋਹਰ ਐਲਗੋਰਿਦਮ

### Deterministicਹੈਸ਼ ਫੰਕਸ਼ਨ

```javascript
// FileHash ਗਣਨਾ (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// EvidenceRoot ਬਣਾਉਣਾ
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// NotarySeal ਤਿਆਰ
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:{timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}
```

### ਪ੍ਰਮਾਣਿਕਤਾ ਵਹਾਅ (ਦੋ ਪੱਧਰ)

#### Quick Verify (ਤੇਜ਼ ਪ੍ਰਮਾਣਿਕਤਾ)

```javascript
// ਸਿਰਫ਼ ਫਾਈਲ hash ਜਾਂਚ (ਤੇਜ਼ ਲਾਲ ਝੰਡਾ)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  if (userFileHash === originalHash) {
    return { valid: true, message: "✅ ਅਸਲੀ - ਫਾਈਲ hash ਮੇਲ ਖਾਂਦੀ ਹੈ" };
  } else {
    return { valid: false, message: "❌ ਨਕਲੀ - ਫਾਈਲ ਹੇਰਾਫੇਰੀ ਕੀਤੀ ਗਈ" };
  }
}
```

#### Full Verify (ਪੂਰੀ ਪ੍ਰਮਾਣਿਕਤਾ)

```javascript
// EvidenceRoot ਅਤੇ NotarySeal ਦੁਬਾਰਾ ਤਿਆਰ ਕਰਕੇ ਪ੍ਰਮਾਣਿਤ
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash ਜਾਂਚ
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ ਨਕਲੀ - ਫਾਈਲ hash ਮੇਲ ਨਹੀਂ" };
  }

  // 2) EvidenceRoot ਦੁਬਾਰਾ ਤਿਆਰ
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ ਮੇਲ ਨਹੀਂ - EvidenceRoot" };
  }

  // 3) NotarySeal ਦੁਬਾਰਾ ਤਿਆਰ
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ ਮੇਲ ਨਹੀਂ - NotarySeal" };
  }

  return { valid: true, message: "✅ ਅਸਲੀ - ਪੂਰੀ ਪ੍ਰਮਾਣਿਕਤਾ ਪਾਸ" };
}
```

---

## 💬 ਅੰਤਮ ਨੋਟਸ

### Pump.fun ਅਤੇ ਵਾਸਤਵਿਕਤਾ

ਇਹ ਪ੍ਰੋਜੈਕਟ Pump.fun 'ਤੇ ਸ਼ੁਰੂ ਕੀਤਾ ਗਿਆ ਕਿਉਂਕਿ:
- ✅ ਤਰਲਤਾ ਪਹੁੰਚ (Raydium automatic migration)
- ✅ ਮੌਜੂਦਾ ਭਾਈਚਾਰੇ ਤਕ ਪਹੁੰਚ
- ✅ ਘੱਟ ਸ਼ੁਰੂਆਤੀ ਲਾਗਤ

ਪਰ ਸਪੱਸ਼ਟ ਕਰੀਏ:
- **ਟੋਕਨ ਕੀਮਤ**, ਕਲਾਤਮਕ ਸਫਲਤਾ ਦਾ ਸੂਚਕ ਨਹੀਂ
- **ਸੰਚਾਲਨ ਬਜਟ** ਲਈ ਟੋਕਨ ਮੁੱਲ ਮਹੱਤਵਪੂਰਨ (ਗੈਲਰੀ, ਪ੍ਰਦਰਸ਼ਨੀਆਂ, ਬੁਨਿਆਦ)
- **ਸਫਲਤਾ ਮੈਟ੍ਰਿਕਸ:** Authenticated artworks + community engagement + ਭੌਤਿਕ ਵਿਜ਼ਿਟਰ

### Governance ਅਤੇ ਵਿਕੇਂਦਰੀਕਰਣ

**v1.0 ਵਾਸਤਵਿਕਤਾ (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (ਕੇਂਦਰੀ ਪਰ ਪਾਰਦਰਸ਼ੀ)
- Governance: Advisory only (ਕਿਉਰੇਟੋਰੀਅਲ ਅੰਤਮ ਫੈਸਲਾ)

**v2.0+ ਦ੍ਰਿਸ਼ਟੀ (2027+):**
- Registry: On-chain (Solana)
- Signatures: Wallet-based (decentralized)
- Governance: Hybrid (community advisory + curatorial quality)

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // ਸੱਭਿਆਚਾਰ, ਪੂੰਜੀ ਤੋਂ ਵੱਡਾ*

## 🧾 License

MIT License © 2026 İlhan Art Gallery Initiative

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) 
![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) 
![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) 
![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**ਇਹ ਪ੍ਰੋਜੈਕਟ [İlhan Art Gallery] ਪਹਿਲਕਦਮੀ ਨਾਲ ਵਿਕਸਤ ਕੀਤਾ ਗਿਆ ਹੈ, ਸਰੋਤ ਕੋਡ ਪਾਰਦਰਸ਼ਤਾ ਲਈ ਜਨਤਾ ਲਈ ਖੁੱਲ੍ਹੇ ਹਨ।**

**ਪ੍ਰੋਟੋਕੋਲ V1.0 // SHA-512 ਨਾਲ ਮੋਹਰਬੰਦ**

*© 2026 İLHAN ART | ਕਲਾਕ੍ਰਿਤੀਆਂ, ਦ੍ਰਿਸ਼ਾਂ ਅਤੇ ਵਿਚਾਰਾਂ ਦੇ ਸਾਰੇ ਅਧਿਕਾਰ ਰਾਖਵੇਂ।*

---

**(ਭਾਗ 2 ਦਾ ਅੰਤ)**
