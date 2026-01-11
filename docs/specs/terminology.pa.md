| **ਸੁਰੱਖਿਆ** | ਕਲਾਇੰਟ-ਸਾਈਡ ਹੈਸ਼ਿੰਗ | ਫਾਇਲ ਕਦੇ ਵੀ ਸਰਵਰ 'ਤੇ ਨਹੀਂ ਜਾਂਦੀ |

### ਧਿਆਨ ਦੇਣ ਯੋਗ ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ

| ਵਿਸ਼ੇਸ਼ਤਾ | ਵੇਰਵਾ | ਪ੍ਰਤੀਯੋਗੀਆਂ ਵਿੱਚ? |
|---------|-------|-----------------|
| **UI ਡਰੈਗ ਐਂਡ ਡਰੌਪ** | ਫਾਇਲ ਘਸੀਟੋ ਅਤੇ ਛੱਡੋ, ਤੁਰੰਤ ਪੂਰਵਦਰਸ਼ਨ | ❌ ਜ਼ਿਆਦਾਤਰ ਵਿੱਚ ਨਹੀਂ |
| **ਬਹੁ-ਫਾਰਮੈਟ ਨਿਰਯਾਤ** | PNG, JSON, PDF - ਇੱਕ ਕਲਿੱਕ | ⚠️ ਸੀਮਤ |
| **ਰੀਅਲ-ਟਾਈਮ ਪੂਰਵਦਰਸ਼ਨ** | ਸਰਟੀਫਿਕੇਟ ਪੂਰਵਦਰਸ਼ਨ ਸਿੱਧਾ | ❌ ਕੋਈ ਨਹੀਂ |
| **ਗੋਪਨੀਯਤਾ ਨਿਯੰਤਰਣ** | ਨਿੱਜੀ/ਮਾਸਕ/ਜਨਤਕ ਵਿਕਲਪ | ❌ ਕੋਈ ਨਹੀਂ |
| **ਕਲਾਇੰਟ-ਸਾਈਡ ਹੈਸ਼** | ਫਾਇਲ ਕਦੇ ਵੀ ਸਰਵਰ 'ਤੇ ਨਹੀਂ ਜਾਂਦੀ | ✅ ਸਿਰਫ਼ ਕੁਝ ਵਿੱਚ |
| **ਫੋਰੈਂਸਿਕ ਮੈਟਾਡੇਟਾ** | IP, ਸਥਾਨ, ਯੰਤਰ, ਸਮਾਂ - ਸਾਰੇ ਇਕੱਠੇ | ❌ ਵੰਡਿਆ ਹੋਇਆ |
| **QR ਤਸਦੀਕ** | ਤੁਰੰਤ ਤਸਦੀਕ QR ਕੋਡ | ⚠️ ਸੀਮਤ |
| **ਰਫ਼ਤਾਰ ਸੀਮਾ** | ਸਪੈਮ ਸੁਰੱਖਿਆ (RLS + ਕਲਾਇੰਟ) | ❌ ਜ਼ਿਆਦਾਤਰ ਵਿੱਚ ਨਹੀਂ |

---

## 🗺️ ਰੋਡਮੈਪ: ਭਵਿੱਖ "ਵਿਸ਼ਵਾਸਹੀਣ"

ਮੌਜੂਦਾ ਸੰਸਕਰਨ **(Beta v1.0)** ਅੰਤਮ ਉਪਭੋਗਤਾਵਾਂ ਨੂੰ ਵੱਧ ਤੋਂ ਵੱਧ ਰਫ਼ਤਾਰ, ਆਸਾਨ ਇੰਟਰਫੇਸ ਅਤੇ ਮੁਫ਼ਤ ਪਹੁੰਚ ਦੇਣ ਲਈ ਡਿਜ਼ਾਈਨ ਕੀਤਾ ਗਿਆ ਹੈ। ਸਾਡੀ ਅੰਤਮ ਦ੍ਰਿਸ਼ਟੀ, ਹਾਲਾਂਕਿ, ਇੱਕ ਅਜਿਹੇ ਢਾਂਚੇ ਵਿੱਚ ਤਬਦੀਲੀ ਹੈ ਜਿੱਥੇ ਡੇਟਾਬੇਸ ਪ੍ਰਬੰਧਕ (ਅਸੀਂ) ਵੀ ਦਖਲ ਨਹੀਂ ਦੇ ਸਕਦੇ।

### ਪੜਾਅ 1: ਬੀਟਾ (ਹੁਣ ਸਿੱਧਾ)

- **ਬੁਨਿਆਦੀ ਢਾਂਚਾ:** ਕਲਾਊਡ ਡੇਟਾਬੇਸ (Supabase)।
- **ਉਦੇਸ਼:** ਰਫ਼ਤਾਰ, UX (ਉਪਭੋਗਤਾ ਅਨੁਭਵ) ਰੁਕਾਵਟਾਂ ਹਟਾਉਣਾ ਅਤੇ ਪਾਲਣਾ। "ਰਗੜ-ਰਹਿਤ" ਸੁਰੱਖਿਆ ਪ੍ਰਦਾਨ ਕਰਨਾ।

### 🚀 ਪੜਾਅ 2: (ਬੈਕਐਂਡ / ਐੱਜ ਫੰਕਸ਼ਨ ਲੋੜਾਂ)

ਇਸ ਪੜਾਅ ਵਿੱਚ "ਕਲਾਇੰਟ-ਸਾਈਡ" ਪੂਰਨ ਸੰਚਾਲਨ ਢਾਂਚੇ ਤੋਂ "ਸਰਵਰ-ਸਾਈਡ ਅਥਾਰਟੀ" ਢਾਂਚੇ ਵੱਲ ਤਬਦੀਲੀ ਸ਼ਾਮਲ ਹੈ ਜੋ ਵਧੇਰੇ ਸੁਰੱਖਿਅਤ ਅਤੇ ਨਿਯੰਤਰਣਯੋਗ ਹੈ।

| ਆਈਟਮ | ਇਹ ਕੀ ਲਿਆਉਂਦਾ ਹੈ? | ਤਕਨੀਕੀ ਸਟੈਕ | ਤਰਜੀਹ |
|-------|---------------|------------|---------|
| **`INSERT` → ਐੱਜ ਫੰਕਸ਼ਨ** | ਸਪੈਮ ਰੋਕੋ + API ਕੁੰਜੀ ਸੁਰੱਖਿਆ | Supabase Edge (Deno) | 🔴 ਉੱਚ |
| **ਵਾਲੇਟ ਦਸਤਖਤ** | ਕ੍ਰਿਪਟੋਗ੍ਰਾਫਿਕ ਤਸਦੀਕ | Solana Wallet Adapter | 🟡 ਮੱਧਮ |
| **IPFS/Arweave ਬੈਕਅੱਪ** | ਵਿਕੇਂਦਰੀਕ੍ਰਿਤ ਅਟੱਲਤਾ | IPFS SDK + Pinata | 🟢 ਘੱਟ |
| **ਰੱਦ ਪ੍ਰਕਿਰਿਆ** | ਝੂਠੇ ਸਰਟੀਫਿਕੇਟ ਰੱਦ ਕਰੋ | DB ਸਕੀਮਾ ਅੱਪਡੇਟ | 🔴 ਉੱਚ |
| **ਸਮੀਖਿਆ ਲੌਗ** | ਵਿਗਿਆਨਕ ਪੁੱਛਗਿੱਛ ਰਿਕਾਰਡ | ਵਿਸ਼ੇਸ਼ ਰਿਕਾਰਡ ਟੇਬਲ | 🟡 ਮੱਧਮ |
| **OpenTimestamps** | Bitcoin ਐਂਕਰ | OTS JavaScript | 🟢 ਘੱਟ |
| **DID ਏਕੀਕਰਨ** | ਵਿਕੇਂਦਰੀਕ੍ਰਿਤ ਪਛਾਣ | ION/Ceramic | 🟢 ਘੱਟ |

### ਪੜਾਅ 3: ਪੂਰਨ ਵਿਕੇਂਦਰੀਕਰਨ (ਲੰਬੀ-ਮਿਆਦ)

| ਵਿਸ਼ੇਸ਼ਤਾ | ਟੀਚਾ | ETA |
|---------|------|-----|
| **ਬਲਾਕਚੇਨ ਰਜਿਸਟਰ** | ਆਨ-ਚੇਨ Ethereum/Solana ਰਜਿਸਟ੍ਰੇਸ਼ਨ | Q4 2026 |
| **DAO ਪ੍ਰਸ਼ਾਸਨ** | ਕਮਿਊਨਿਟੀ ਪ੍ਰਸ਼ਾਸਨ | Q1 2027 |
| **ਬਹੁ-ਚੇਨ ਸਹਾਇਤਾ** | Polygon, Arbitrum, Base | Q2 2027 |
| **ਕਾਨੂੰਨੀ ਮਾਨਤਾ** | ਤੁਰਕੀ ਅਦਾਲਤਾਂ ਵਿੱਚ ਵੈਧਤਾ | 2027-2028 |
| **ਡਿਵੈਲਪਰਾਂ ਲਈ API** | ਜਨਤਕ API ਐਂਡਪੌਇੰਟ | Q3 2026 |

---

## 📊 ਪ੍ਰਤੀਯੋਗੀ ਵਿਸ਼ਲੇਸ਼ਣ (ਅੱਪਡੇਟ ਕੀਤਾ)

PoArt ਮੌਜੂਦਾ ਹੱਲਾਂ ਦੇ ਖਾਲੀ ਥਾਂ ਨੂੰ ਭਰਨ ਵਾਲੇ "Sweet Spot" ਵਿੱਚ ਖੜ੍ਹਾ ਹੈ।

| ਵਿਸ਼ੇਸ਼ਤਾ | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **ਲਾਗਤ** | 🆓 ਮੁਫ਼ਤ | 🆓 | 💰 ਭੁਗਤਾਨ ਕੀਤਾ | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI ਡਰੈਗ ਐਂਡ ਡਰੌਪ** | ✅ ਬਹੁਤ ਆਸਾਨ | ❌ CLI | ⚠️ ਮੱਧਮ | ⚠️ ਮੱਧਮ | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **ਬਹੁ-ਫਾਰਮੈਟ ਨਿਰਯਾਤ** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **ਰੀਅਲ-ਟਾਈਮ ਪੂਰਵਦਰਸ਼ਨ** | ✅ ਸਿੱਧਾ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **ਗੋਪਨੀਯਤਾ ਨਿਯੰਤਰਣ** | ✅ 3 ਮੋਡ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **ਕਲਾਇੰਟ-ਸਾਈਡ ਹੈਸ਼** | ✅ ਗੋਪਨੀਯਤਾ | ✅ | ❌ ਅੱਪਲੋਡ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **ਫੋਰੈਂਸਿਕ ਮੈਟਾਡੇਟਾ** | ✅ ਪੂਰਨ | ❌ | ❌ | ⚠️ ਸੀਮਤ | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR ਤਸਦੀਕ** | ✅ ਤੁਰੰਤ | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **ਰਫ਼ਤਾਰ ਸੀਮਾ** | ✅ RLS+ਕਲਾਇੰਟ | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **ਬਲਾਕਚੇਨ ਐਂਕਰ** | 🔄 ਰੋਡਮੈਪ | ✅ Bitcoin | ✅ Ethereum | ✅ ਕਈ | ✅ | ✅ | ✅ | ✅ |
| **ਓਪਨ ਸੋਰਸ** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **ਤੁਰਕੀ ਸਹਾਇਤਾ** | ✅ ਮੂਲ | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**ਕੁੰਜੀ:**
- ✅ : ਪੂਰਨ ਸਹਾਇਤਾ / ਉਪਲਬਧ
- ⚠️ : ਸੀਮਤ / ਭੁਗਤਾਨ ਯੋਜਨਾਵਾਂ ਵਿੱਚ
- ❌ : ਕੋਈ ਨਹੀਂ / ਸਮਰਥਿਤ ਨਹੀਂ
- 🔄 : ਰੋਡਮੈਪ ਵਿੱਚ (ਵਿਕਾਸ ਵਿੱਚ)
- 🆓 : ਪੂਰੀ ਤਰ੍ਹਾਂ ਮੁਫ਼ਤ
- 💰 : ਭੁਗਤਾਨ ਕੀਤਾ / ਰਜਿਸਟ੍ਰੇਸ਼ਨ ਲੋੜੀਂਦੀ

### ਪ੍ਰਤੀਯੋਗੀਆਂ ਦੇ ਖਾਲੀ ਥਾਂ, PoArt ਦੀ ਤਾਕਤ

| ਖਾਲੀ ਥਾਂ | ਪ੍ਰਤੀਯੋਗੀ | PoArt |
|-------|-------------|-------|
| **ਵਰਤੋਂ ਮੁਸ਼ਕਲ** | CLI, API ਗਿਆਨ, ਵਾਲੇਟ ਲੋੜੀਂਦਾ | ਘਸੀਟੋ ਅਤੇ ਛੱਡੋ, 3 ਕਲਿੱਕਾਂ ਨਾਲ ਤਿਆਰ |
| **ਲਾਗਤ ਰੁਕਾਵਟ** | ਰਜਿਸਟ੍ਰੇਸ਼ਨ $50-500/ਮਹੀਨਾ | 100% ਮੁਫ਼ਤ |
| **ਗੋਪਨੀਯਤਾ** | ਫਾਇਲ ਸਰਵਰ 'ਤੇ ਅੱਪਲੋਡ | ਕਲਾਇੰਟ-ਸਾਈਡ, ਫਾਇਲ ਕਦੇ ਨਹੀਂ ਜਾਂਦੀ |
| **ਫੋਰੈਂਸਿਕ ਡੇਟਾ** | ਸਿਰਫ਼ ਟਾਈਮ ਸਟੈਂਪ | IP, ਸਥਾਨ, ਯੰਤਰ, ਸਮਾਂ - ਸਾਰੇ |
| **ਤੁਰਕੀ ਸਹਾਇਤਾ** | ਕੋਈ ਨਹੀਂ ਜਾਂ ਬਹੁਤ ਸੀਮਤ | ਮੂਲ ਭਾਸ਼ਾ ਸਹਾਇਤਾ |
| **ਓਪਨ ਸੋਰਸ** | ਬੰਦ ਬਾਕਸ | ਸਾਰਾ ਕੋਡ GitHub 'ਤੇ ਖੁੱਲ੍ਹਾ |

---

## 🧬 ਪ੍ਰੋਟੋਕੋਲ ਡੇਟਾ ਢਾਂਚਾ (JSON Schema)

**ਹਰ [PoArt] ਸਰਟੀਫਿਕੇਟ ਵਿੱਚ ਹੇਠਾਂ ਦਿੱਤੇ ਮਿਆਰ ਅਨੁਸਾਰ ਬਣਾਇਆ ਗਿਆ ਪੋਰਟੇਬਲ ਅਤੇ ਤਸਦੀਕਯੋਗ JSON ਪਛਾਣ ਕਾਰਡ ਹੈ।**

> **ਨੋਟ:** ਇਹ JSON ਪਛਾਣ ਫਾਰਮੈਟ ਉਪਭੋਗਤਾਵਾਂ ਨੂੰ ਪੇਸ਼ ਕੀਤਾ ਸਰਟੀਫਿਕੇਟ ਫਾਰਮੈਟ ਹੈ। ਰਜਿਸਟਰ ਰਿਕਾਰਡਾਂ ਵਿੱਚ, `registry.asset` `identity.asset_data` ਦੀ ਥਾਂ ਵਰਤਿਆ ਜਾਂਦਾ ਹੈ (ਮੈਪਿੰਗ: `identity.asset_data` == `registry.asset`)।
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

## 🔬 ਤਕਨੀਕੀ ਡੂੰਘਾਈ: ਮੋਹਰ ਐਲਗੋਰਿਦਮ

### ਨਿਰਧਾਰਿਤ ਹੈਸ਼ ਫੰਕਸ਼ਨ
```javascript
// ਸਹਾਇਕ ਫੰਕਸ਼ਨ: ਸੰਖੇਪ ਨੂੰ ਹੈਕਸਾਡੈਸੀਮਲ ਸਟ੍ਰਿੰਗ ਵਿੱਚ ਬਦਲੋ
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// ਸਟ੍ਰਿੰਗ ਨੂੰ ਬਾਈਟ ਐਰੇ ਵਿੱਚ ਬਦਲੋ
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// ਕੈਨੋਨੀਕਲ ਫੋਰੈਂਸਿਕਸ ਸਟ੍ਰਿੰਗ ਸਿਰਜਣਾ (v1.0: ਸਥਿਰ ਫੀਲਡ ਕ੍ਰਮ + UTF-8 + ਡੀਲਿਮੀਟਰ \n)
// ਪੜਾਅ 2 ਸੱਚ: RFC 8785 (JCS) ਨਾਲ ਕੈਨੋਨੀਕਲ JSON ਵਿੱਚ ਤਬਦੀਲੀ
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal ਸਿਰਜਣਾ ਪ੍ਰਕਿਰਿਆ (ਪੂਰੀ ਤਰ੍ਹਾਂ ਨਿਰਧਾਰਿਤ)
```javascript
// 1. FileHash ਗਣਨਾ (ਕਲਾਇੰਟ-ਸਾਈਡ)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. ਫੋਰੈਂਸਿਕ ਡੇਟਾ ਇਕੱਠਾ ਕਰਨਾ (ਇੱਕਲੇ ਟਾਈਮ ਸਟੈਂਪ ਦੀ ਵਰਤੋਂ)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // ਇੱਕਲੇ ਟਾਈਮ ਸਟੈਂਪ ਸਿਰਜਣਾ
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // ਇੱਕੋ ਟਾਈਮ ਸਟੈਂਪ
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot ਨਿਰਮਾਣ (ਕੈਨੋਨੀਕਲ ਐਨਕ੍ਰਿਪਸ਼ਨ ਨਾਲ)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal ਸਿਰਜਣਾ (ਇੱਕੋ ਟਾਈਮ ਸਟੈਂਪ ਦੀ ਵਰਤੋਂ)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// ਮਾਸਕਿੰਗ ਸਹਾਇਕ ਫੰਕਸ਼ਨ (IPv4 ਅਤੇ IPv6 ਸਹਾਇਤਾ)
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4 ਜਾਂਚ
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 ਜਾਂ ਅਣਜਾਣ ਫਾਰਮੈਟ
  return "***";
}
```

### ਤਸਦੀਕ ਪ੍ਰਵਾਹ (ਦੋ ਪੱਧਰ)

#### Quick Verify (ਤੇਜ਼ ਤਸਦੀਕ)
```javascript
// ਸਿਰਫ਼ ਫਾਇਲ ਹੈਸ਼ ਤਸਦੀਕ ਕਰੋ (ਤੇਜ਼ ਲਾਲ ਝੰਡਾ)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // ਰਜਿਸਟਰ ਤੋਂ ਪ੍ਰਾਪਤ ਕਰੋ
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // ਹੈਸ਼ ਤੁਲਨਾ
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ ਅਸਲੀ - ਫਾਇਲ ਹੈਸ਼ ਮੇਲ ਖਾਂਦਾ ਹੈ"
    };
  } else {
    return {
      valid: false,
      message: "❌ ਝੂਠਾ - ਫਾਇਲ ਵਿੱਚ ਹੇਰਾਫੇਰੀ ਕੀਤੀ ਗਈ"
    };
  }
}
```

#### Full Verify (ਪੂਰਨ ਤਸਦੀਕ)
```javascript
// EvidenceRoot ਅਤੇ NotarySeal ਦੁਬਾਰਾ ਬਣਾਓ ਅਤੇ ਤਸਦੀਕ ਕਰੋ
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // ਰਜਿਸਟਰ ਤੋਂ ਪ੍ਰਾਪਤ ਕਰੋ
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash ਤਸਦੀਕ (ਤੇਜ਼ ਲਾਲ ਝੰਡਾ)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ ਝੂਠਾ - ਫਾਇਲ ਹੈਸ਼ ਮੇਲ ਨਹੀਂ ਖਾਂਦਾ" };
  }

  // 2) EvidenceRoot ਦੁਬਾਰਾ ਬਣਾਓ (ਰਜਿਸਟਰ ਵਿੱਚ ਸੰਭਾਲੇ ਫੋਰੈਂਸਿਕ ਡੇਟਾ ਨਾਲ)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ ਮੇਲ ਨਹੀਂ - EvidenceRoot ਖੜ੍ਹਾ ਨਹੀਂ" };
  }

  // 3) NotarySeal ਦੁਬਾਰਾ ਬਣਾਓ (ਇੱਕੋ ਟਾਈਮ ਸਟੈਂਪ + signer_sig ਨਾਲ)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ ਮੇਲ ਨਹੀਂ - NotarySeal ਖੜ੍ਹਾ ਨਹੀਂ" };
  }

  // ਵਿਕਲਪਿਕ: ਪੜਾਅ 2 ਵਿੱਚ, signer_sig ਵੀ attestation_pubkey ਨਾਲ ਤਸਦੀਕ ਕਰੋ
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ ਗਲਤ ਦਸਤਖਤ" };

  return { valid: true, message: "✅ ਅਸਲੀ - ਪੂਰਨ ਤਸਦੀਕ ਸਫਲ" };
}
```

> **ਮਹੱਤਵਪੂਰਨ ਸੱਚਾਈਆਂ:**
> - **Quick Verify:** ਤੇਜ਼ ਵਰਤੋਂ ਲਈ ਸਿਰਫ਼ ਫਾਇਲ ਹੈਸ਼ ਤਸਦੀਕ ਕਰਦਾ ਹੈ।
> - **Full Verify:** ਸਾਰੀਆਂ ਪ੍ਰੋਟੋਕੋਲ ਪਰਤਾਂ ਤਸਦੀਕ ਕਰਦਾ ਹੈ (EvidenceRoot + NotarySeal)।
> - ਸਾਰੀਆਂ ਹੈਸ਼ ਕਾਰਵਾਈਆਂ ਸਥਿਰ ਐਨਕ੍ਰਿਪਸ਼ਨ ਅਤੇ ਸਥਿਰ ਡੀਲਿਮੀਟਰਾਂ ਨਾਲ ਨਿਰਧਾਰਿਤ ਤਰੀਕੇ ਨਾਲ ਕੀਤੀਆਂ ਜਾਂਦੀਆਂ ਹਨ।
> - **ਮੌਜੂਦਾ ਮਿਆਰ v1.0:** ਸਥਿਰ ਫੀਲਡ ਕ੍ਰਮ + UTF-8 ਐਨਕ੍ਰਿਪਸ਼ਨ + ਡੀਲਿਮੀਟਰ `\n`।
> - **ਪੜਾਅ 2 ਯੋਜਨਾ:** RFC 8785 (JCS - JSON Canonicalization Scheme) ਨਾਲ ਕੈਨੋਨੀਕਲ JSON ਵਿੱਚ ਤਬਦੀਲੀ।
> - ਮਾਸਕ ਮੋਡ ਵਿੱਚ, EvidenceRoot ਅਤੇ NotarySeal ਗਣਨਾ ਮਾਸਕ ਕੀਤੇ ਫੋਰੈਂਸਿਕ ਡੇਟਾ ਨਾਲ ਕੀਤੀ ਜਾਂਦੀ ਹੈ; ਇਸਲਈ ਤਸਦੀਕ ਨਿਰਧਾਰਿਤ ਰਹਿੰਦੀ ਹੈ।
> - ਪੂਰੀ ਪ੍ਰਕਿਰਿਆ ਵਿੱਚ ਇੱਕਲਾ ਟਾਈਮ ਸਟੈਂਪ ਵਰਤਿਆ ਜਾਂਦਾ ਹੈ (ਫੋਰੈਂਸਿਕਸ + NotarySeal); ਨਿਰਧਾਰਣ ਗਾਰੰਟੀਸ਼ੁਦਾ।
> - **ਫੋਰੈਂਸਿਕ ਫੀਲਡ ਨਾਮ:** `ip_masked`, `location`, `device`, `timestamp` (ਕੋਡ ਅਤੇ ਰਜਿਸਟਰ ਬਿਲਕੁਲ ਮੇਲ ਖਾਂਦੇ ਹਨ)।
> - **ਰਜਿਸਟਰ ਮਾਰਗ:** `certificate.asset.fingerprints` (ਤਸਦੀਕ ਕੋਡ ਨਾਲ ਬਿਲਕੁਲ ਮੇਲ ਖਾਂਦਾ ਹੈ)।
> - **ਰਜਿਸਟਰ ਵਿੱਚ signer_sig:** ਪੂਰਨ ਤਸਦੀਕ ਲਈ `proof.signer_sig` ਫੀਲਡ ਲੋੜੀਂਦੀ।
> - SignerSignature ਪ੍ਰਕਿਰਿਆ ਪੜਾਅ 2 ਵਿੱਚ Solana Wallet Adapter ਨਾਲ ਸਰਗਰਮ ਕੀਤੀ ਜਾਵੇਗੀ; v1.0 ਵਿੱਚ, ਤਸਦੀਕ `attestation_pubkey` ਨਾਲ ਕੀਤੀ ਜਾ ਸਕਦੀ ਹੈ।

---

## 📈 ਵਰਤੋਂ ਅੰਕੜੇ (Q1 2026 ਟੀਚੇ)

| ਮੀਟ੍ਰਿਕ | ਟੀਚਾ | ਸਥਿਤੀ |
|--------|--------|--------|
| **ਕੁੱਲ ਸਰਟੀਫਿਕੇਟ** | 1,000 | 🔄 ਪ੍ਰਗਤੀ ਵਿੱਚ |
| **ਸਰਗਰਮ ਉਪਭੋਗਤਾ** | 500 | 🔄 ਪ੍ਰਗਤੀ ਵਿੱਚ |
| **ਤਸਦੀਕ ਸੰਖਿਆ** | 5,000 | 🔄 ਪ੍ਰਗਤੀ ਵਿੱਚ |
| **Uptime** | 99.9% | ✅ ਸਿੱਧਾ |
| **ਔਸਤ ਜਵਾਬ ਸਮਾਂ** | <200ms | ✅ ਸ਼ਾਨਦਾਰ |

---

## 🌍 ਕਮਿਊਨਿਟੀ ਅਤੇ ਸਹਾਇਤਾ

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **ਵੈੱਬਸਾਈਟ:** [ilhanart.org](https://ilhanart.org)
- **ਈਮੇਲ:** galeri@ilhanart.org

---

## 🙏 ਯੋਗਦਾਨੀ

PoArt ਪ੍ਰੋਟੋਕੋਲ ਓਪਨ ਸੋਰਸ ਕਮਿਊਨਿਟੀ ਤੋਂ ਯੋਗਦਾਨਾਂ ਨਾਲ ਵਧ ਰਿਹਾ ਹੈ।

**ਯੋਗਦਾਨ ਕਰਨ ਲਈ:**
1. ਰਿਪੋਜ਼ਿਟਰੀ Fork ਕਰੋ
2. ਫੀਚਰ ਬ੍ਰਾਂਚ ਬਣਾਓ (`git checkout -b feature/amazing-feature`)
3. Commit ਕਰੋ (`git commit -m 'Add amazing feature'`)
4. Push ਕਰੋ (`git push origin feature/amazing-feature`)
5. Pull Request ਖੋਲ੍ਹੋ

### 🛠️ ਸਾਨੂੰ ਹੁਣ ਕੀ ਚਾਹੀਦਾ ਹੈ? (ਮਦਦ ਦੀ ਕਾਲ)

PoArt ਪ੍ਰੋਟੋਕੋਲ **ਪੜਾਅ 2** ਵਿਕਾਸ ਲਈ ਹੇਠਾਂ ਦਿੱਤੇ ਖੇਤਰਾਂ ਵਿੱਚ ਅਨੁਭਵੀ ਡਿਵੈਲਪਰ ਲੱਭ ਰਿਹਾ ਹੈ:

* **Supabase Edge ਫੰਕਸ਼ਨ:** ਸਪੈਮ ਸੁਰੱਖਿਆ ਨੂੰ ਸਰਵਰ ਸਾਈਡ 'ਤੇ ਤਬਦੀਲ ਕਰਨਾ।
* **Solana Web3.js:** ਵਾਲੇਟ ਦਸਤਖਤ ਏਕੀਕਰਨ।
* **IPFS / Arweave:** ਸਟੋਰੇਜ ਅਤੇ ਪਿੰਨ ਸੇਵਾ ਏਕੀਕਰਨ।

> ਕਿਰਪਾ ਕਰਕੇ ਫੀਚਰ ਜੋੜਨ ਤੋਂ ਪਹਿਲਾਂ "Issues" ਟੈਬ ਵਿੱਚ ਚਰਚਾ ਸ਼ੁਰੂ ਕਰੋ।

---

**[PoArt] Proof of Art ਪ੍ਰੋਟੋਕੋਲ v1.0**  
*"ਸੱਭਿਆਚਾਰ > ਪੂੰਜੀ"*

## 🧾 ਲਾਇਸੈਂਸ

MIT ਲਾਇਸੈਂਸ © 2026 Ilhan Art Gallery Initiative

ਪੂਰੀਆਂ ਸ਼ਰਤਾਂ ਲਈ [![ਲਾਇਸੈਂਸ](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) ਦੇਖੋ।

---

## 💬 ਸਵੀਕ੍ਰਿਤੀ

![ਸੰਸਕਰਨ](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![ਸੁਰੱਖਿਆ](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![ਪਲੇਟਫਾਰਮ](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![ਲਾਇਸੈਂਸ](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**ਇਹ ਪ੍ਰੋਜੈਕਟ [Ilhan Art Gallery] ਪਹਿਲਕਦਮੀ ਦੁਆਰਾ ਵਿਕਸਤ ਕੀਤਾ ਗਿਆ ਹੈ, ਅਤੇ ਇਸਦਾ ਸਰੋਤ ਕੋਡ ਪਾਰਦਰਸ਼ਤਾ ਲਈ ਜਨਤਕ ਤੌਰ 'ਤੇ ਉਪਲਬਧ ਹੈ।**

**ਪ੍ਰੋਟੋਕੋਲ V1.0 // SHA-512 ਨਾਲ ਸੀਲ ਕੀਤਾ**

*© 2026 İLHAN ART | ਕਲਾਕ੍ਰਿਤੀਆਂ, ਤਸਵੀਰਾਂ ਅਤੇ ਵਿਚਾਰਾਂ ਲਈ ਸਾਰੇ ਅਧਿਕਾਰ ਰਾਖਵੇਂ ਹਨ।*

---
