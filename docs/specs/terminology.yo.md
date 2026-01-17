# 📚 ÌTUMỌ̀ ÀTI ÀWỌN ÈRÒ ÌMỌ̀ ỌRỌ̀
> **"Láti mọ èdè ìlànà yìí ni láti mọ ìran rẹ̀."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Ìpìlẹ̀ Pàtàkì

**PoArt Forensic Engine (PFE)** jẹ́ ipele àkọ́kọ́ tí ó wà lábẹ́ ìlànà [PoArt], tí ó ń ṣàfihàn ìmọ̀ràn pàtàkì àti ìṣiṣẹ́ ìmọ̀-ẹ̀rọ tí ó wà lábẹ́ rẹ̀. Èyí ni "ẹ̀rọ àdájọ́" tí ó ń mú data ìṣẹ́dá gbòǹgbò iṣẹ́ ọnà tí ó yí i padà sí **ẹ̀rí oníróbótó** tí a lè ṣàyẹ̀wò tí kò sì lè yí padà.

### 🧩 Kí Ni Ìdí "PoArt Forensic"?

- **PoArt (Proof of Art - Ẹ̀rí Ọnà):** Ìfojúsùn ẹ̀rọ náà ni láti so iye ohun-ìní oníróbótó mọ́ **ìlànà ìṣẹ́dá tí a lè fihàn**, kì í ṣe sí àrokò owó.
- **Forensic (Ìdájọ́ Àdánwò):**
  - **Ìtumọ̀ Ìmọ̀-Ẹ̀rọ:** Ìlànà algorithm àti ìgbéléwọ́n ìforúkọsílẹ̀ láti ṣàyẹ̀wò pé data ìlànà ìṣẹ́dá (gbígbọ̀n fọ́ọ̀mù, timelapse, àwọn ìforúkọsílẹ̀) kò tí ṣe àyípadà.
  - **Ipele Ìmọ̀ Ọgbọ́n:** Lòdì sí ìṣẹ́dá "èsì lẹ́sẹ̀kẹsẹ̀" ti AI; ìfẹ́ láti yí **àkókò ènìyàn, agbára àti iye ìpinnu** padà sí òtítọ́ tí a lè wọ̀n.

> Àkíyèsí: Ìdàpọ̀ blockchain (bíi Solana) kìí ṣe àárín PFE; a máa tọ́ka sí rẹ̀ bíi **Chain Anchor Layer** fún ìdánwò/registry.

### 🛠️ v1.0 Ìbò Ìmọ̀-Ẹ̀rọ

**PoArt Forensic Engine (PFE) v1.0** kọ́ lórí àwọn **ọ̀wọ́n pàtàkì mẹ́ta** yìí dípò àwọn àpẹẹrẹ owó tó nira:

1. **Hashing & Sealing (Dídì Èdìdì):**  
   PFE ń ṣiṣẹ́ gbogbo ohun tó wà nínú Evidence Pack (fáìlì iṣẹ́ ọnà, video, JSON/log, ìbuwọ́lù àbáwọlé) ní ọ̀nà tó ṣeé ṣàkóso, ó sì máa ṣe àgbéjáde iye **NotarySeal** kan ṣoṣo.

   **Àwọn èrò pàtàkì (v1.0):**
   - **FileHash (ìtẹ̀ka iṣẹ́ ọnà):** Hash tí a ṣe láti bytes fáìlì iṣẹ́ ọnà náà.
   - **EvidenceRoot (gbòǹgbò àkójọ ẹ̀rí):** Àkópọ̀ gbòǹgbò tó dúró fún ìdọ́gba Evidence Pack (Merkle root tàbí kanonik manifest hash).
   - **NotarySeal (èdìdì ìparí / PFE Output):** Èdìdì ìkẹyìn tí a ṣe láti EvidenceRoot + àkókò + ìbuwọ́lù.

   **Àwọn Àgbékalẹ̀ (tí ó hàn kedere fún olùdókòwò):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Àwọn Ìtumọ̀ Canonical Payload (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Àkíyèsí: Iye tí PFE ń ṣe àgbéjáde ni **NotarySeal**. Ìlànà **SignerSignature** yóò wọlé ní Faz 2 (pẹ̀lú Solana Wallet Adapter); ní v1.0 tó wà báyìí, ìbuwọ́lù attestation ti ètò náà ni a ń lò. Attestation public key yóò hàn sí registry ní `issuer.attestation_pubkey`.

2. **Indexing (Ìforúkọsílẹ̀):**  
   Àpamọ́wọ́ wo ni, ní ọjọ́ wo ni, fún iṣẹ́ ọnà wo ni **Labor Proof (Ẹ̀rí Iṣẹ́)** fi hàn; ó ń fi sínú ipele ìforúkọsílẹ̀ tí ó ṣí sílẹ̀ tí a sì lè béèrè.  
   *(Ipele yìí lè jẹ́ ibi-ìpamọ́ data; ìdàpọ̀ chain yóò jẹ́ "Chain Anchor Layer" tó yàtọ̀.)*

3. **Verification (Ìdánwò):**  
   Nígbà tí wọ́n bá béèrè bóyá iṣẹ́ ọnà kan jẹ́ ọkọ̀ọ̀kan, PFE yóò tún ṣiṣẹ́ àwọn ẹ̀rí gbòǹgbò; yóò sì ṣe àyẹ̀wò pẹ̀lú ìdánilójú mathematiki bóyá àwọn iye **EvidenceRoot / NotarySeal** tí a ṣe ìṣirò bá àwọn tó wà nínú registry mu.

---

### 🧮 Ìlànà Iye PoArt (The Value Theorem)

Ìlànà [PoArt] so iye ohun-ìní oníróbótó ($V$) mọ́ **òtítọ́ ti ara ìlànà ìṣẹ́dá**, kì í ṣe mọ́ ìrò ojú ọjà tí ó lè yí padà.

Artificial Intelligence (AI) ń pa ìlànà rẹ̀ run nípa fífun ní èsì lẹ́sẹ̀kẹsẹ̀ ($t \to 0$). [PoArt] gbé iye kalẹ̀ lórí **àkójọpọ̀ àkókò, iṣẹ́, àti ìfẹ́** bíi ohun kan.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Ìtumọ̀ Àwọn Onísẹ́

- **$\int dt$ (Àkójọpọ̀ Ìlànà):**  
  Iye kìí ṣe "èsì" tí ó yára; ó jẹ́ **ìlànà** tí ó kójọpọ̀ láàárín $t_{\text{start}}$ àti $t_{\text{end}}$. Bí àkókò bá ń dínkù (ìṣẹ́dá AI), èsì integral náà yóò súnmọ́ 0.

- **$P_{\text{labor}}(t)$ (Agbára Iṣẹ́ Lọ́wọ́lọ́wọ́):**  
  Ó dúró fún kíkankíkan agbára inú àti ti ara tí a lò ní àkókò ìṣẹ́dá. Bí agbára tí a lè fihàn bá ń pọ̀ sí i, integrand náà yóò ń tóbi sí i.  
  > Àkíyèsí: A lè ṣe ìbámu ọ̀rọ̀ yìí ní ìṣe pẹ̀lú "àwọn àmì iṣẹ́ tí a lè wọ̀n/fihàn".

- **$I_{\text{agency}}(t)$ (Ìdínwọ̀n Ìfẹ́):**  
  Agbára olùṣẹ́dá láti gba ewu àti láti ṣe ìpinnu. Ó gbà iye láàárín $0$ àti $1$.
  - **AI ($I \approx 0$):** Ó ń ṣe àṣẹ, kò gba ewu, kò san iye kan.
  - **Ènìyàn ($I \to 1$):** Ó yí ìpinnu padà, ó ń ṣiyèméjì, ó ń gba ewu.

- **$U_{\text{irreversible}}$ (Àìlèyípadà Ọ̀tọ̀ọ̀tọ̀):**  
  Nínú ìṣẹ́dá oníróbótó, ìdápadà (`Ctrl+Z`) ṣeé ṣe; nínú ìṣẹ́dá ti ara (ìgbọ̀nwọ́ ewé sórí canvas, fífọ́ òkúta, ìṣesí ní ìṣafihàn láìkede), ìdápadà kò sí. **Àìlèyípadà** yìí ń dá "ọ̀tọ̀ọ̀tọ̀" (non-fungible character) sílẹ̀ nínú iṣẹ́ ọnà náà.

### 🔎 Ìtúpalẹ̀ Àpẹẹrẹ: AI "Èsì Lẹ́sẹ̀kẹsẹ̀" vs. Ènìyàn "Ìlànà Pẹ̀lú Ẹ̀rí"

Àpẹẹrẹ ìsàlẹ̀ yìí ń ṣàfihàn bí **Ìlànà Iye PoArt** ṣe ń ṣiṣẹ́ ní ìṣe àti ìdí tí ìṣẹ́dá AI fi ń gba àmì kékeré ní ìlànà [PoArt].

#### Àpẹẹrẹ A: Ìṣẹ́dá Àwòrán Pẹ̀lú AI Ní Ìṣẹ́jú Àáyá 10

- **Àkókò ($\Delta t$):** Ìṣẹ́jú àáyá $10$ (ìlànà kò sí fẹ́rẹ̀)
- **Agbára Iṣẹ́ ($P_{\text{labor}}$):** $1$ ìwọ̀n (kíkọ àṣẹ nìkan)
- **Ìdínwọ̀n Ìfẹ́ ($I_{\text{agency}}$):** $0.01$ (kò sí ewu, kò sí iye)
- **Àìlèyípadà ($U_{\text{irreversible}}$):** $0$ (a lè dá padà / a lè ṣẹ̀dà)

**Èsì:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Àsọyé:** Bí èsì náà tilẹ̀ jẹ́ pípé; nítorí pé ìlànà kò gbà lára rẹ̀ àti pé kò ní ìfẹ́/ewu, iye [PoArt] yóò súnmọ́ $0$.

#### ÀpẹẀrẹ B: Ìṣẹ́dá Ti Ara Ní Ìṣafihàn Láìkede Fún Wákàtí 6

- **Àkókò ($\Delta t$):** Wákàtí $6$ (ìṣẹ́jú àáyá $21{,}600$)
- **Agbára Iṣẹ́ ($P_{\text{labor}}$):** $0.5$ ìwọ̀n (ìtẹ̀síwájú agbára inú àti ti ara)
- **Ìdínwọ̀n Ìfẹ́ ($I_{\text{agency}}$):** $0.9$ (yíyí ìpinnu padà, gbígba ewu, àwọn ìpinnu àìlèyípadà)
- **Àìlèyípadà ($U_{\text{irreversible}}$):** $>0$ (àwọn àmì ti ara kò lè yí padà)

**Èsì:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Àsọyé:** Bí ìlànà bá ń gùn sí i àti bí ìfẹ́ (ewu) bá ń pọ̀ sí i, iye náà yóò ń kójọpọ̀. Ọ̀rọ̀ $U_{\text{irreversible}}$ ń ṣèrànwọ́ láti dá "ọ̀tọ̀ọ̀tọ̀" (non-fungible character) sílẹ̀ nínú iṣẹ́ ọnà náà.

---

### ✅ Ìparí: Dídì Iye Pẹ̀lú Ẹ̀rí (Proof-Bound Value)

Ìlànà yìí mú ìfẹ́ iye ti [PoArt] kúrò nínú "ìfẹ́ràn" tàbí "ìtàn ọjà" ó sì so ó mọ́ **òtítọ́ ìṣẹ́dá tí a lè fihàn**.

1. **Iye Kò Lè Wáyé Láìsí Ìlànà:**  
   AI ń pa ìlànà rẹ̀ run nínú èsì lẹ́sẹ̀kẹsẹ̀ ($t \to 0$). Bí fèrèsé ìlànà bá ń dín, èsì integral náà yóò dínkù pẹ̀lú ìdánilójú mathematiki:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Ìfẹ́ Àti Ewu Jẹ́ Olùṣàkóso:**  
   [PoArt] kì í ṣe "àkókò tí a lò" nìkan ni ó ń wọ̀n; ó tún ń wọ̀n ìpinnu òtítọ́, ewu àti iye nínú àkókò náà. Iye ìṣẹ́dá tí kò gba ewu (AI) kéré:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Ọ̀tọ̀ọ̀tọ̀ Jẹ́ Ẹ̀rí Ti Ara, Kì Í Ṣe Tí Títà:**  
   Àwọn àmì àìlèyípadà nínú ìṣẹ́dá ti ara (ìgbọ̀nwọ́ ewé, fífọ́ òkúta) wà lóde ìmọ̀ `Ctrl+Z` ti oníróbótó. Àìlèyípadà yìí ($U_{\text{irreversible}}$) ń ṣe ọ̀tọ̀ọ̀tọ̀ sí iṣẹ́ ọnà náà ní ọ̀nà ontolojiki.

> **🔐 ÀKÓPỌ̀:** Bí ìlànà iye tilẹ̀ dàbí ìdánwò tí kò ṣeé ṣàyẹ̀wò (nínú ayé gidi kò lè wọ̀n 100%), ète àgbékalẹ̀ yìí ni láti fi ìṣètò àti ọ̀nà àwọn onísẹ́ hàn. Nínú àkókò AI, ohun tí ó ṣọ̀wọ́n kì í ṣe "àwòrán"; ó jẹ́ **iṣẹ́ tí a lè fihàn, àkókò, àti ìfẹ́.** [PoArt] ń wọ̀n àìpọ̀ yìí ó sì fi **Evidence Pack** jẹ́rìí rẹ̀.

### 🏛️ Pàtàkì Èrò "Engine" (Ẹ̀rọ)

Àwọn token tí ó ti Pump.fun tàbí àwọn pẹpẹ ìrú rẹ̀ jáde sábà máa ń jẹ́ **"tíkẹ́ẹ̀tì ìwọlé"** nìkan. **PoArt Forensic Engine (PFE)** ṣùgbọ́n jẹ́ **ipele ìmọ̀ràn tí ó dàbí ìlànà òfin** tí ó ń pinnu àwọn ẹ̀tọ́ tí tíkẹ́ẹ̀tì náà ń dáàbò bò, bí a ṣe lè forúkọsílẹ̀ iṣẹ́, àti bí a ṣe lè ṣe ìdúróṣinṣin ọnà/ìmọ̀ sáyẹ́nsì/ìmọ̀-ẹ̀rọ.

> **Àkíyèsí:** Ìdí tí a fi bẹ̀rẹ̀ iṣẹ́ àkànṣe yìí ní Pump.fun ni pé a kò ní omi ọjà tó tó àti àwọn olùtẹ̀lé tó pọ̀. Lílo data tí a ní báyìí jẹ́ ìgbésẹ̀ tó tọ́ jùlọ ní ìlànà, bí ó tilẹ̀ jẹ́ pé kì í ṣe ti ọ̀gá jùlọ. Láìsí ọwọ́ ìṣúná tàbí àǹfààní, ṣíṣe àlàyé ìmọ̀ràn ẹ̀rọ yìí lórí GitHub fi hàn pé iṣẹ́ àkànṣe yìí kì í ṣe àrokò owó nìkan, ṣùgbọ́n **ìpìlẹ̀ sọ́fítìwíà** ìgbà pípẹ́ àti **ilé-ìkàwé oríìlú oníróbótó**.

---
## 🎨 [PoArt] ÌLÀNÀ Ẹ̀RÍ IṢẸ́ (Proof of Art Protocol v1.0)

> **"Oníṣọ̀nà Gidi, Ìṣẹ́dá Gidi, Iye Gidi."**

Ìlànà yìí jẹ́ **ẹ̀rọ ààbò ti ara àti ti ọgbọ́n** tí a ṣe lòdì sí àwọn alárékérekè aláìmọ̀ tó kárí eto crypto, àwọn àwòrán AI tí a ṣe ní ìṣẹ́jú 5, àti àṣà "Pump & Dump" (Fẹ́ẹ̀ Sókè Kó Sọnù).

---

## a) [PoArt] Kín Ni? (Ìtumọ̀ Ìmọ̀ Ọgbọ́n Àti Ìmọ̀-Ẹ̀rọ)

**Proof of Art [PoArt];** jẹ́ ìlànà ìdánwò ilé-iṣẹ́ tí ó ń dáàbò bò pé iye tí ó wà lẹ́yìn ohun-ìní kan lórí blockchain dúró lé **iṣẹ́ ènìyàn**, **àkókò** àti **agbára ti ara** tí a lè fihàn, kì í ṣe lórí àrokò.

Bí Bitcoin ṣe ń ṣe iye pẹ̀lú *"Iná Mànàmáná Àti Agbára Processor"* **(Proof of Work)**; àwọn iṣẹ́ àkànṣe tó bá mu [PoArt] náà ń ṣe iye pẹ̀lú *"Ọgbọ́n Àti Àkókò Ènìyàn Tó Lò"*. Wọ́n ń fi àkókò "Stake".

Ó ń pa ewu *"Olùṣe-sọ́fítìwíà (Dev) tà á, iṣẹ́ àkànṣe parí"* rẹ́ nínú Pump.fun àti àwọn pẹpẹ DEX; nítorí pé níbí, iye kì í wà nínú code, ó wà nínú **ìtẹ̀síwájú ìṣẹ́dá**.

> **[PoArt] kì í sọ fún olùkópa rẹ̀ pé "Ẹ gbà wá gbọ́"; ó sọ pé "Ẹ wò àwọn ẹ̀rí, ẹ fi ojú yín rí i, ẹ fi mathematiki yín ṣàyẹ̀wò."**

---

## b) Ìlànà 5-In-One [PoArt] (The 5 Pillars of Truth)

Àwọn mẹ́ta yìí jẹ́ àwọn àṣẹ̀ tí kò ṣeé ṣe àyípadà tí iṣẹ́ àkànṣe kan gbọ́dọ̀ kọjá kó tó lè gba èdìdì [PoArt].

### 1) Ẹ̀rí Ìdánimọ̀ Láìkede (Live Identity Proof)

- **Ìṣòro:** Ayé crypto kún fún àwọn olùdásílẹ̀ aláìmọ̀ (Dev) tó ń gba owó tó sì ń fi iṣẹ́ àkànṣe sílẹ̀.
- **Ojútùú [PoArt]:** Olùṣẹ́dá kì í fi **káàdì ìdánimọ̀** nìkan hàn, ṣùgbọ́n ó ń fi **ìwáyé rẹ̀ ní àkókò ìṣẹ́dá** hàn. Èyí kì í ṣe pẹ̀lú àwọn video tí a ti forúkọsílẹ̀ tẹ́lẹ̀, ṣùgbọ́n pẹ̀lú àwọn ìgbà ìṣafihàn láìkede níbi tí wọ́n ti ń bá àwùjọ lò pọ̀ tí wọ́n sì ń ṣe àwọn ìbéèrè pàtó lẹ́sẹ̀kẹsẹ̀.  
  (Fún àpẹẹrẹ: *"Kọ ọjọ́ òní àti nọ́mbà búlọ́ọ̀kù tó wà lọ́wọ́ sí apá ọ̀tún canvas"*)
- **Kókó Ọ̀rọ̀:** *"Àwọn bot lè ṣe àwòrán ṣùgbọ́n àwọn bot kò lè jẹ́gbẹ̀ẹ́ bẹ́ẹ̀ ni wọn kò lè ṣe àìróte."*

### 2) Ẹ̀rí Iṣẹ́ Àti Ìlànà (Labor & Process Proof)

- **Ìṣòro:** Àwọn àwòrán AI tí a ṣe ní ìṣẹ́jú àáyá 2 àti àwòrán oil painting tí a ṣe ní oṣù 2 ní ayé oníróbótó jọra bíi "jpeg" kan náà.
- **Ojútùú [PoArt]:** A forúkọsílẹ̀ ìlànà "ìlóyún àti ìbímọ" ti iṣẹ́ ọnà náà. Àwọn ìpele sketch, àwọn ipele ewé, àwọn wákàtí tí a kójọpọ̀ lò àti ìlànà ti ara tí oníṣọ̀nà náà kọjá láti dá iṣẹ́ ọnà náà ni a forúkọsílẹ̀. Èyí ń fi **"Iye Àkókò" (Time Cost)** kún token náà. Bí ìṣẹ́dá ohun-ìní kan bá ṣòro tó, iye rẹ̀ yóò ní ìdúróṣinṣin tó.

### 3) Ẹ̀rí Iye Ẹwà (Aesthetic Value Proof)

- **Ìṣòro:** Àṣà "Meme" tí ó ń kọjú àwọ̀ àti ìjìnlẹ̀ ọnà tí ó sì ń fọkàn sí àwọ̀ àpanilẹ́rìn nìkan, èyí tó ń fa àwọn iṣẹ́ àkànṣe "Hype" aláìpẹ́.
- **Ojútùú [PoArt]:** Iṣẹ́ àkànṣe gbọ́dọ̀ ní àwọn ìlànà ọnà ìwé-ẹ̀kọ́, ìlànà àwọ̀, àwọn òfin ìṣètò àti ìmọ̀ nípa àwọn ohun èlò (Impasto, Doku àti bẹ́ẹ̀ bẹ́ẹ̀ lọ). Àkóónú kì í yẹ kí ó ṣe àpanilẹ́rìn nìkan; ó yẹ kí ó ru ìyàlẹ́nu sókè nínú ẹni tó ń wò ó kó sì ní **iye àkójọpọ̀**.

### 4) Ìtúnṣe Èrò (Conceptual Novelty)

- **Ìṣòro:** Ẹgbẹẹgbẹ̀rún àwọn coin ajá/ológbò tó ń ṣẹ̀dà ara wọn tí kò sí ìmọ̀-ọ̀nà kankan.
- **Ojútùú [PoArt]:** Iṣẹ́ àkànṣe náà gbọ́dọ̀ kọ́ àfárá tuntun tó ní ìtumọ̀ tó ń so ọnà, sáyẹ́nsì, ìmọ̀ ọgbọ́n tàbí ìmọ̀-ẹ̀rọ pọ̀.  
  (Fún àpẹẹrẹ: Dídapọ̀ ère David àtijọ́ pẹ̀lú data ojú ọjà crypto; láti inú èyí láti ṣe àlàyé èrò "dí i di òkúta" ti ìmọ̀ ènìyàn kó sì fi àwọn orísun sáyẹ́nsì ṣe ìpìlẹ̀ rẹ̀.)  
  Iṣẹ́ ọnà kì í yẹ kí ó jẹ́ àjọyọ̀ àwòrán nìkan; ó tún gbọ́dọ̀ jẹ́ **ìjà ọgbọ́n** tó ń mú ènìyàn ronú lórí Sáyẹ́nsì, Ìmọ̀ Ọgbọ́n tàbí Ìmọ̀-Ẹ̀rọ.

> [!IMPORTANT]
> **Àpẹẹrẹ Ìtọ́kasí (Ipa Las Palmitas):**  
> Ní àgbègbè Las Palmitas ti Mexico tó kún fún ọ̀daràn, wọ́n yí ilé tó lé ní 200 padà sí àjọyọ̀ rainbow ńlá. Lẹ́yìn ìṣọwọ́-ìṣẹ̀wà yìí, ìwọ̀n ọ̀daràn ní àgbègbè náà dínkù díẹ̀, àwọn ọ̀dọ́ bẹ̀rẹ̀ sí ní ní àníyàn sí ọnà ju àwọn ẹgbẹ́ ọ̀daràn lọ. Ìyípadà ẹwà tún ṣe code sí ọ̀wọ̀ tí ènìyàn ń fi bọ̀wọ̀ fún àyíká wọn àti fún ara wọn (Social Cohesion).
>
> **Ìrètí:** Iṣẹ́ àkànṣe tó bá wọ àtòkọ [PoArt]; gẹ́gẹ́ bí àpẹẹrẹ òkè yìí, gbọ́dọ̀ ní ìbáṣepọ̀ ìdí-èsì tó kọjá ẹwà àwòrán lásán, ìbá à ṣe ti àwùjọ, sáyẹ́nsì tàbí ìmọ̀ ọgbọ́n. Nítorí pé "Àkókò" ni ohun kan ṣoṣo tí owó kò lè rà, nínú ìlànà yìí, a fi àkókò "stake" bíi ẹ̀rí. Ìpìlẹ̀ èrò ti iṣẹ́ àkànṣe náà gbọ́dọ̀ lágbára tó àti àgbáyé tó; pé kódà lẹ́yìn ọdún púpọ̀ nínú àpẹẹrẹ CTO (Community Take Over) tó ṣeé ṣe, àwùjọ lè gba ogún yìí kí wọ́n sì tẹ̀síwájú àǹfààní ìmọ̀-ọ̀nà ti iṣẹ́ àkànṣe náà ní ọ̀nà aládàáṣe.

### 5) Ìfẹ́ Tí Kì Í Ṣe Ti Algorithm (Non-Algorithmic Agency)

- **Ìṣòro:** Àwọn ìṣẹ́dá oníróbótó tó pé tí kò sì ní ẹ̀mí, tó ń ṣẹ̀dà ara wọn.
- **Ojútùú [PoArt]:** Ìfẹ́ àdáni ti ènìyàn tó lè ṣàṣìṣe, tó ń gba ewu tó sì ń ní ìyípadà ẹ̀mí gbọ́dọ̀ hàn nínú iṣẹ́ ọnà náà. Àìdánilójú nínú gbígbọ̀nwọ́ ewé, àwọn ìdáhùn àìrètí ti ohun èlò àti àwọn ìpinnu lẹ́sẹ̀kẹsẹ̀ ti oníṣọ̀nà ni **Ìbuwọ́lù Ti Ara** tó ń ya iṣẹ́ ọnà yìí sọ́tọ̀ kúrò nínú "Ìṣẹ́dá Ẹ̀rọ".

---

## c) Ẹ̀rọ Ìdánwò & Ààbò Lòdì Sí Èké

Ètò yìí ń ṣe àdánilójú pé iṣẹ́ àkànṣe náà kò ní "ìbẹ̀rẹ̀" nìkan ṣùgbọ́n tẹ̀síwájú láì parí láti jẹ́ ìgbẹ́kẹ̀lé àti láìkú.

### 📦 Àpò Ẹ̀rí (Evidence Pack - The Digital Twin)

Lẹ́yìn gbogbo iṣẹ́ ọnà tó ní ìwé-ẹ̀rí [PoArt], àpò data tó ní ìdí èdìdì àti àmì àkókò tí àwọn olùdókòwò lè gbà sílẹ̀:

- **Àwọn Ìforúkọsílẹ̀ Video RAW:** Àwọn àwòrán gbòǹgbò aláìdáwọ́ dúró ti àkókò ìṣẹ́dá náà.
- **Ìtúpalẹ̀ Metadata:** Ọjọ́ ìṣẹ̀dá fáìlì, àlàyé nípa ẹ̀rọ tí a lò àti data ipò (Ìlú-Orílẹ̀-èdè).
- **Àwọn Ìtọ́kasí Ti Ara:** Àwọn ẹ̀rí pé iṣẹ́ ọnà náà wà nínú ayé ti ara  
  (Fún àpẹẹrẹ: Ìwé ìròyìn àìkú tó wà lẹ́gbẹ̀ẹ́ iṣẹ́ ọnà náà tàbí data blockchain àkókò náà).

> *Àkíyèsí ìbámu:* Ọ̀rọ̀ "àpò ẹ̀rí" so mọ́ **Evidence Pack → EvidenceRoot → NotarySeal** tó wà ní àwọn apá tó kọjá; èyí túmọ̀ sí pé ìdọ́gba àpò náà ni a fi èdìdì tó ṣeé ṣàyẹ̀wò ṣe àpèjúwe.

### 🔄 Ìsọdọ̀tun 365 Ọjọ́ (The Sustainability Protocol)

- **Ìṣẹ̀ Ìyàlẹ́nu:** Nínú àwọn iṣẹ́ àkànṣe crypto, "Dev" (Olùṣe-sọ́fítìwíà) yóò fi token sí ojú ọjà yóò sì sábà máa parẹ́ lẹ́yìn oṣù 1-2 (Soft Rug). [PoArt] kọ̀ ó di aláìṣeéṣe.
- **Òfin:** Ipò "Verified Artist" (Oníṣọ̀nà Tó Ti Ní Ìjẹ́rìísí) kì í ṣe títí láé. Ọdún **kan** nìkan ni ó tó.
- **Bí Ó Ṣe Ń Ṣiṣẹ́:** Oníṣọ̀nà/Olùṣe-sọ́fítìwíà gbọ́dọ̀ máa fi **iṣẹ́ ọnà tuntun, ńlá tí a sì lè fihàn** sílẹ̀ fún àwùjọ ní gbogbo 365 ọjọ́.
- **Àpẹẹrẹ Ìṣẹ̀lẹ̀:** Ẹ bẹ̀rẹ̀ iṣẹ́ àkànṣe náà ní 2026. Ní January 2027, ètò náà yóò fún ni ìkilọ̀ "Àkókò Ẹ̀rí Ti Parí". Bí oníṣọ̀nà kò bá fi ìrísí tuntun, iṣẹ́ ọnà ti ara tuntun tàbí ìdàpọ̀ ìmọ̀-ẹ̀rọ tuntun sílẹ̀, "Báàjì Ìgbẹ́kẹ̀lé" ti iṣẹ́ àkànṣe náà yóò ṣubú.
- **Èsì:** Ètò yìí ń ṣe àdánilójú pé **àkóónú náà kò ní ọjọ́ gbẹ láé** àti pé olùdókòwò kò ní ní ìbẹ̀rù *"Ṣé Olùṣe-sọ́fítìwíà ṣì wà níbí?"* Iṣẹ́ àkànṣe náà di ilé-iṣẹ́ alààyè.

### 🚩 Àmì Pupa (Red Flag Protocol)

**Nígbà tí àwùjọ tàbí algorithms bá ṣe àwárí èké kankan (lílo AI, jíjà iṣẹ́ ọnà, ṣíṣe àyípadà video):**

1. Ìwé-ẹ̀rí yóò di "**FÀGÍLÉ" (VOID)** lẹ́sẹ̀kẹsẹ̀.
2. A yóò samisi àwọn àpò ẹ̀rí ní àti gbangba bíi **"Èké"**.
3. A yóò fi iṣẹ́ àkànṣe náà sínú àtòkọ dúdú [PoArt]. Èyí ń ṣe ìmúdára òtítọ́ pé nínú ayé aládàáṣe, **orúkọ rere ni owó kan ṣoṣo**.
4. A kò lè lo àwọn ọ̀rọ̀ [PoArt] nínú ìpolongo kankan, orísun tó tọ́ kan ṣoṣo ni https://www.ilhanart.org/public-registry

---

## d) Ìparí: Kì Í Ṣe Ilé-Ìṣeré, Ṣùgbọ́n Ilé-Ìṣọ́

**Pump.fun àti Àwọn Ọjà Aládàáṣe (DEX) jẹ́ ilé-ìṣeré báyìí lákọtọ́; àwọn iná ń yọ àti kú, gbogbo ènìyàn ń lépa èrè tó yára àti àpótí (àwọn alárékérekè) máa ń borí nígbà gbogbo. Ìdí tí a fi bẹ̀rẹ̀ iṣẹ́ àkànṣe níbí tún ni láti gbìyànjú láti ṣe ìtúnṣe sí ibẹ̀ àti pẹ̀lú data àti àwọn ìṣafihàn láìkede tí a ní, a lè dé ọ̀dọ̀ àwùjọ tó wà lọ́wọ́.**

**[PoArt] jẹ́ ilé-ìṣọ́ tí a kọ́ sí àárín ilé-ìṣeré yìí.**

- 🎰 Ilé-ìṣeré dúró lórí eré káàdì; àwa dúró lórí **òtítọ́ ti ara**.
- 🃏 Ilé-ìṣeré ṣí sílẹ̀ fún ẹ̀tàn; àwa ṣí sílẹ̀ fún **ẹ̀rí kedere**.
- ⏳ Ilé-ìṣeré jẹ́ ìgbà díẹ̀; àwa fọkàn sí **àìnípẹ̀kun ọnà àti sáyẹ́nsì**.

**Token tó ń lo ìlànà yìí kì í ṣe "coin" kan nìkan; ó jẹ́ ìpín oníróbótó kan tó ní bílẹ̀, ewé, code àti ìmọ̀ ọgbọ́n lẹ́yìn rẹ̀.**

---

## 🗳️ 6) ÌṢÀKÓSO ÀTI ÌFORÚKỌSÍLẸ̀ GBANGBA (Governance & Public Registry)

**Èrí-ìníkàn apá yìí ni: Mú ìlànà [PoArt] kúrò nínú ipele "ìgbẹ́kẹ̀lé sí ènìyàn" kí ó sì di ìpìlẹ̀ gbangba tó ní ìdúróṣinṣin pẹ̀lú ìforúkọsílẹ̀ + ìdánwò + ìṣàkóso àwùjọ.**

### 6.1 Public Registry (Ìforúkọsílẹ̀ Gbangba)

- **Public Registry:** Gbogbo data tó ti ní ìfọwọ́sí ni a forúkọsílẹ̀ sí `ilhanart.org/registry` (tàbí GitHub Registry).

**Ìmọ̀ ìforúkọsílẹ̀ (ìlànà tí a ṣe ìmọ̀ràn - ní ọ̀nà JSON path):**

Ìforúkọsílẹ̀ kọ̀ọ̀kan tó bá wọ inú registry gbọ́dọ̀ ní àwọn aaye pàtàkì tó ṣeé ṣàyẹ̀wò yìí:

- **Ìdánimọ̀ & Ipò:**
  - `certificate_id` (ìtọ́kasí tó ṣeé kà)
  - `status` (active / void)
  - `void_reason` (bí ó bá wà)
  - `visibility` (private / masked / public)
  - `created_at` (àmì àkókò)

- **Ilé-Iṣẹ́ Olùfúnni:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Àlàyé Iṣẹ́ Ọnà:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (bí ó bá ṣeé ṣe; fún ìdánimọ̀ olùdìímú token)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Data Àdájọ́:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Àwọn Ẹ̀rí Cryptographic:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Ìṣàkóso:**
  - `governance.decision`
  - `governance.review_notes`

Registry lè ní ipele méjì:
- **1)** Ìtọ́ka tí ènìyàn lè kà (àtòjọ wẹ́ẹ̀bù / wíwá / àṣẹ)
- **2)** Manifest tí ẹ̀rọ lè kà (àwọn ìforúkọsílẹ̀ JSON; fún ìdánwò PFE)

**"Ìforúkọsílẹ̀" níbí di ohun tó ṣeé ṣàyẹ̀wò pẹ̀lú ọ̀nà Evidence Pack → EvidenceRoot → NotarySeal ti PFE. Registry ń fún ni àfojúsùn ìdánwò, kì í ṣe "ìsọ" nìkan.**

---

### 6.2 Ìlànà Ìbéèrè PoArt Verified

**İlhanArt Gallery ló ń ṣàyẹ̀wò àwọn ìbéèrè PoArt Verified gẹ́gẹ́ bí 5 ìlànà PoArt. A máa ń kíyèsi ìdáhùn àwùjọ, ṣùgbọ́n ìpinnu ìparí wà lọ́wọ́ ẹgbẹ́ curatorial. A ṣàlàyé àwọn ìpinnu ní kedere a sì forúkọsílẹ̀ wọ́n sí ilhanart.org/registry.**

#### Ìlànà Ìbéèrè

**Ìbéèrè:**
- Oníṣọ̀nà/iṣẹ́ àkànṣe ṣe ìbéèrè PoArt Verified
- Ìgbaradì Evidence Pack (àwọn ìforúkọsílẹ̀ video, metadata, àwọn ọ̀nà asopọ̀ ìṣafihàn láìkede)
- Ìbéèrè ránṣẹ́ sí İlhanArt Gallery

**Ìṣàyẹ̀wò (Ọjọ́ 30):**
- Ẹgbẹ́ gallery ṣe àyẹ̀wò Evidence Pack ní ìkíni
- Wọ́n ṣàyẹ̀wò gbogbo 5 ìlànà PoArt:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Ìfọ̀rọ̀wánilẹ́nuwò pẹ̀lú oníṣọ̀nà (ìyàn)

**Ìmọ̀ràn Àwùjọ:**
- A máa ń pín Evidence Pack sí gbangba ní àkókò ìbéèrè
- Àwùjọ lè fún ni ìdáhùn lórí ilhanart.org
- Àwọn olùdìímú token (tó kéré jù 10,000 $CULTURE) lè ṣe ìmọ̀ràn pàtó
- **A máa ń kíyèsi gbogbo ìdáhùn ní àkókò ìṣàyẹ̀wò**
- **Ṣùgbọ́n ìpinnu ìparí wà lọ́wọ́ àyẹ̀wò curatorial**

**Ìpinnu:**
- Gallery fọwọ́sí tàbí kọ̀ ìbéèrè náà
- A ṣàlàyé ìdí ìpinnu ní kedere
- Bí a bá fọwọ́sí → Báàjì PoArt Verified
- Bí a bá kọ̀ → Ó lè tún béèrè lẹ́yìn oṣù 6

**Kedere:**
- A forúkọsílẹ̀ gbogbo ìbéèrè àti ìpinnu sí ilhanart.org/registry
- A ṣe àtẹ̀jáde ìforúkọsílẹ̀ ìpinnu sí gbangba:
  - Ọjọ́ ìbéèrè
  - Àkópọ̀ ìlànà ìṣàyẹ̀wò
  - Ìpinnu (Approved / Rejected)
  - Ìdí ìpinnu (àlàyé kúkúrú)
  - Àkópọ̀ ìdáhùn àwùjọ (aláìlórúkọ)

#### Kí Ni Ìdí Ìpinnu Curatorial?

**Ìṣàkóso Ìdárayá:**  
Ipò PoArt Verified ní àwọn ìlànà gíga. Àyẹ̀wò curatorial ń ṣe àdánilójú ìdúróṣinṣin àwọn ìlànà yìí.

**Ìdènà Ṣíṣe Àyípadà Àrokò:**  
Pẹ̀lú àwọn token Pump.fun, on-chain governance tó kún (bíi: Realms, DAO voting) kò ṣeé ṣe ní ọ̀nà ìmọ̀-ẹ̀rọ. Àwọn ètò ìdìbò off-chain sì ṣí sílẹ̀ fún ṣíṣe àyípadà whale àti ìkọlù tó ṣètò. Ìpinnu curatorial ń pa ewu yìí rẹ́.

**Ìmúṣiṣẹ́ Ṣíṣe:**  
Dípò àwọn ìlànà ìdìbò tó nira, ìlànà ìpinnu tó yára tó sì kedere. Àwọn oníṣọ̀nà máa ń gba èsì láàárín ọjọ́ 30.

**Ìkópa Àwùjọ:**  
A máa ń kíyèsi ìdáhùn àwùjọ pátápátá ó sì ń ní ipa lórí ìlànà ìpinnu. Ṣùgbọ́n ìpinnu ìparí wà lọ́wọ́ ẹgbẹ́ curatorial tí a ti dáàbò bò kúrò nínú ṣíṣe àyípadà.

**Ọjọ́ Iwájú:**  
Nígbà tí iṣẹ́ àkànṣe bá ti dàgbà (2027+), a lè mú ìlànà ìmọ̀ràn àwùjọ lágbára sí i. Ṣùgbọ́n ààbò ìlànà curatorial yóò wà títí láé.

---

### 6.3 Token Utility (Àwọn Àǹfààní Lílo Token)

**Àwọn àǹfààní tí a ń fún àwọn olùdìímú token $CULTURE:**

**1. Ìwọlé Àkọ́kọ́ Sí Àwọn Ìṣẹ̀lẹ̀ Gallery:**
- Ẹ̀tọ́ láti ṣe ìrísí ní İlhanArt Gallery fún ọ̀sẹ̀ kan ní ọdún (ẹ̀tọ́ tó ṣeé gbé)
- Ìdínkù fún drop painting
- Ẹ̀tọ́ ìdínkù láàárín 10% sí 30% fún àwọn àwòrán ní gallery

**2. Ìwọlé Kíkún Sí PoArt Registry:**
- Àwọn ìforúkọsílẹ̀ àlàyé kíkún ti gbogbo authenticated artworks
- Àwọn ẹ̀dà kíkún ti Evidence Pack
- Àwọn irinṣẹ́ ìdánwò forensic

**3. Advisory Voting:**
- Ẹ̀tọ́ ìmọ̀ràn nínú àwọn ìbéèrè PoArt Verified
- Ìwọlé sí àwọn ọ̀nà ìdáhùn àwùjọ
- Ìkópa nínú àwọn ìjíròrò ìṣàkóso

**4. Àkóónú Àkànṣe:**
- Àkóónú behind-the-scenes ti ilé-iṣẹ́
- Àwọn ìfọ̀rọ̀wérọ̀ oníṣọ̀nà àti àwọn video ìlànà
- Ìwọlé sí ìwé àlàyé ìmọ̀-ẹ̀rọ

**Àkíyèsí:**  
Àwọn olùdìímú token ń fún ni advisory vote (ìdìbò ìmọ̀ràn). Ìpinnu ìparí wà lọ́wọ́ ẹgbẹ́ curatorial. A yan ìṣètò yìí láti ṣe ìdènà ṣíṣe àyípadà whale àti ìkọlù àrokò. Kò sí èrè staking nítorí pé àwa ń wá àwọn olùkópa àṣà ìgbà pípẹ́, kì í ṣe mercenary capital ìgbà kúkúrú.

---

### 6.4 Metadata Sync (Ìbámu Pẹ̀lú Ayé Ti Ara)

- **Metadata Sync:** Data ìmọ̀-ẹ̀rọ nínú registry gbọ́dọ̀ bá ohun-ìní ti ara mu ní 100%.

**Ṣíṣe àlàyé "ìbámu 100%" ní ọ̀nà ìmọ̀-ẹ̀rọ (ìmọ̀ràn àlàyé):**

- **Ìbámu tó kéré jù (dandan):**
  - `asset.fingerprints.sha256/sha512` nínú registry àti hash ti fáìlì tó wà lọ́wọ́ gbọ́dọ̀ **jọra pátápátá**.
  - `proof.notary_seal` nínú registry nígbà tí a bá tún ṣe é (bí Evidence Pack bá wà) gbọ́dọ̀ **jọra pátápátá**.

- **Ìbámu ìtọ́kasí ti ara (irú ẹ̀rí):**
  - Iṣẹ́ ọnà ti ara tí a fi hàn ní ìṣafihàn láìkede + àwọn ẹ̀rí ọjọ́/búlọ́ọ̀kù gbọ́dọ̀ bá Evidence Pack mu.

- **Ìbámu ìkọ̀kọ̀:**
  - Ní ipò `masked`, àwọn aaye bíi IP/ipò gbọ́dọ̀ jáde gẹ́gẹ́ bí **ìlànà masking**.

---

### 6.5 Ìtakọ̀, Ìṣàyẹ̀wò Àti Fàgílé (Dispute & Revocation)

Registry kì í ṣe ẹ̀rọ "ìfọwọ́sí" nìkan; ó jẹ́ **ẹ̀rọ ìṣàkóso alààyè** lòdì sí èké.

- Nígbà tí ìtakọ̀ bá bẹ̀rẹ̀, a lè fi ìforúkọsílẹ̀ sí ipò **"review"**.
- Bí a bá rí èké, a máa samisi rẹ̀ bíi `status: void` a sì fi ìdí kún un:
  - `void_reason` (lílo AI / jíjà / ṣíṣe àyípadà àbáwọlé)
  - `revoked_at` (àkókò fàgílé)
- Orísun ìpinnu fàgílé yóò hàn kedere nínú registry:
  - àyẹ̀wò curatorial / ìtakọ̀ àwùjọ / àkíyèsí ìtúpalẹ̀ àdájọ́ (èyí tó bá wà)

> **Apá yìí jẹ́ ìbámu ti èrò VOID nínú apá "Red Flag Protocol" lórí registry.**

---

### 6.6 Àpẹẹrẹ Ìforúkọsílẹ̀ Registry (Tí ẹ̀rọ lè kà)
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

> *Àkíyèsí: `asset.fingerprints.sha512` àti àwọn iye hash míìràn di kúkúrú fún àpẹẹrẹ; nínú ìṣe gidi, a máa lò ọ̀rọ̀ hexadecimal tó kún.*

---

## 7) 🔐 ÈDÌDÌ ÌMỌ̀-ẸRỌ (NOTARY SEAL)

**Algorithm èdìdì tí kò lè yọ̀ tí PoArt Forensic Engine (PFE) v1.0 ṣe:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Ìlànà Akọ̀wé Oníróbótó & Ẹ̀rí Àdájọ́ (Beta v1.0)

> **"Àṣà tóbi ju Oluómìnira. Dáàbò bo àwọn iṣẹ́ yín láti òní, gbé wọn lọ sí ọ̀la."**

---

## Kí Ni Ìdí Sí Gbangba?

Ààbò tòótọ́ wá láti inú kedere. Pẹ̀lú ètò **Public Registry (Ìforúkọsílẹ̀ Gbangba)** wa, ẹnikẹ́ni ní ibikíbi láyé lè ṣàyẹ̀wò bóyá fáìlì tó wà lọ́wọ́ rẹ̀ jẹ́ ọkọ̀ọ̀kan láìsí aláṣẹ kankan láàárín ìṣẹ́jú àáyá díẹ̀.

---

## 🧩 Kí Ni Ìdí Púpọ̀ "Module Ìríran"?

Èyí ni apá tó ṣe pàtàkì jù nínú code (àtòjọ àṣàyàn visibility). Àwọn àṣàyàn yìí ń jẹ́ kí àwọn olùlò ṣètò ìdọ́gba **"Ìkọ̀kọ̀ vs. Kedere"**:

### 🔒 Àdáni (Private)

- **Àpẹẹrẹ:** Oníṣọ̀nà kò fẹ́ ṣe àtẹ̀jáde iṣẹ́ ọnà ṣìbẹ̀ ṣùgbọ́n ó fẹ́ fi àmì àkókò kùn ún kó lè fihàn pé "Mo ṣe èyí ní ọjọ́ yìí".
- **Ohun Tí Code Ń Ṣe:** Ó kọ data sínú ibi-ìpamọ́ ṣùgbọ́n ó fi àmì `visibility: "private"` sí i. Ní ọjọ́ iwájú nígbà tí a bá kọ "Public Read" policy, a lè sọ `WHERE visibility = 'public'` láti fi àwọn ìforúkọsílẹ̀ yìí pamọ́ kúrò lọ́dọ̀ àwùjọ.

### 🕶️ Aláàbò (Masked)

- **Àpẹẹrẹ:** Oníṣọ̀nà fẹ́ kedere ṣùgbọ́n ó bẹ̀rù pé wọ́n á rí àdírẹ́ẹ̀sì ilé rẹ̀ (ipò IP).
- **Ohun Tí Code Ń Ṣe:** Ní apá JavaScript, àwọn iṣẹ́ `maskIP` àti `maskLoc` ń ṣiṣẹ́. Ó yí àdírẹ́ẹ̀sì IP padà sí `88.241.***.***`, ipò sí `***/TR` ó sì fi ẹ̀dà tí a ti ṣe sansọ́ọ̀ sínú ibi-ìpamọ́.
- **Àkíyèsí Ìkọ̀kọ̀:** A ń ṣe masking ní apá browser, Supabase kò rí ipò tòótọ́. **Ṣùgbọ́n:** Bí a bá ń lo API ẹlẹ́gbẹ́ bíi ipapi.co fún data ipò, àwọn olùpèsè yìí yóò rí àdírẹ́ẹ̀sì IP ní àkókò ìbéèrè.
- **Mühürleme Ní Ipò Masked:** Ìṣírò EvidenceRoot àti NotarySeal ṣe pẹ̀lú data forensics tí a ti ṣe masking; báyìí ìdánwò yóò jẹ́ deterministik.

### 🌍 Sí Gbogbo Ènìyàn (Public)

- **Àpẹẹrẹ:** Kedere kíkún. Gẹ́gẹ́ bí ìlànà [PoArt], níbo, nígbà wo, láti orí nẹ́tíwọ̀ọ̀kì wo ni a ṣe iṣẹ́ ọnà náà ni a sọ kedere.

---
> **Àwọn Àkíyèsí Pàtàkì:**
> - **Quick Verify:** Ìṣàyẹ̀wò hash fáìlì nìkan fún lílo tó yára.
> - **Full Verify:** Ṣàyẹ̀wò gbogbo ipele ìlànà (EvidenceRoot + NotarySeal).
> - Gbogbo iṣẹ́ hash ṣe ní ọ̀nà deterministik, pẹ̀lú encoding tó dúró àti àwọn delimiter.
> - **Ìlànà canonicalization v1.0:** Ìtò aaye tó dúró + UTF-8 encoding + delimiter `\n`.
> - **Ètò Ipele 2:** Ìlọ sí canonical JSON pẹ̀lú RFC 8785 (JCS - JSON Canonicalization Scheme).
> - Ní ipò masked, ìṣírò EvidenceRoot àti NotarySeal ṣe pẹ̀lú data forensics tí a ti mask.
> - A lò timestamp kan kárí ìlànà náà (forensics + NotarySeal); determinism ni a ń ṣe àdánilójú.
> - **Àwọn orúkọ aaye forensics:** `ip_masked`, `location`, `device`, `timestamp` (code àti registry bá ara mu pátápátá).
> - **Ọ̀nà registry:** `certificate.asset.fingerprints` (bá code verify mu).
> - **signer_sig ní registry:** Aaye `proof.signer_sig` ṣe pàtàkì fún Full Verify.
> - Ìlànà SignerSignature yóò wọlé ní Ipele 2 pẹ̀lú Solana Wallet Adapter; ní v1.0, a lè ṣàyẹ̀wò pẹ̀lú `attestation_pubkey`.

---

## 📊 Ìtúpalẹ̀ Àwọn Aláfara (Tí A Ti Ṣe Ìmúdájú)

PoArt wà ní ipò "Sweet Spot" (Ipò Tó Dára Jù) tó ń kún àwọn àlàfo àwọn ojútùú tó wà.

| Àbùdá | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Owó Náà** | 🆓 Ọ̀fẹ́ | 🆓 | 💰 Owó Ń Wọlé | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Rọrùn Púpọ̀ | ❌ CLI | ⚠️ Àárín | ⚠️ Àárín | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Láìkú | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ Ipò 3 | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Ìkọ̀kọ̀ | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Kíkún | ❌ | ❌ | ⚠️ Níòpin | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Lẹ́sẹ̀kẹsẹ̀ | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Ìtìlẹ́yìn Yorùbá** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Àlàyé:**
- ✅ : Ìtìlẹ́yìn kíkún / wà
- ⚠️ : Níòpin / ní àwọn ètò tó ń gba owó
- ❌ : Kò sí / a kò ṣe ìtìlẹ́yìn
- 🔄 : Ní roadmap (a ń ṣiṣẹ́ lórí rẹ̀)
- 🆓 : Ọ̀fẹ́ pátápátá
- 💰 : Owó ń wọlé / ìforúkọsílẹ̀ ń wọlé

### Àwọn Àlàfo Àwọn Aláfara, Àwọn Agbára PoArt

| Àlàfo | Àwọn Aláfara | PoArt |
|------|----------|-------|
| **Ìṣòro Lílo** | CLI, ìmọ̀ API, àpamọ́wọ́ ń wọlé | Fà-jù, ó parí pẹ̀lú títẹ̀ mẹ́ta |
| **Ìdènà Owó** | Ìforúkọsílẹ̀ $50-500/oṣù | 100% ọ̀fẹ́ |
| **Ìkọ̀kọ̀** | Fáìlì lọ sórí server | Client-side, fáìlì kò lọ láé |
| **Data Forensic** | Timestamp nìkan | IP, ipò, ẹ̀rọ, àkókò - gbogbo rẹ̀ |
| **Ìtìlẹ́yìn Yorùbá** | Kò sí tàbí kékeré púpọ̀ | Ìtìlẹ́yìn èdè abínibí |
| **Open Source** | Àpótí tí a ti pa | Gbogbo code wà lórí GitHub |

---

## 📈 Ìṣirò Lílo (Àwọn Àfojúsùn 2026 Q1)

| Ìwọ̀n | Àfojúsùn | Ipò |
|--------|-------|-------|
| **Ìwé-Ẹ̀rí Lápapọ̀** | 1,000 | 🔄 Ń Lọ | 
| **Olùlò Tó Ń Ṣiṣẹ́** | 500 | 🔄 Ń Lọ |
| **Nọ́mbà Ìdánwò** | 5,000 | 🔄 Ń Lọ |
| **Uptime** | %99.9 | ✅ Ń Ṣiṣẹ́ |
| **Avg Response Time** | <200ms | ✅ Tó Dára |

---

## 🌍 Àwùjọ & Ìtìlẹ́yìn

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Àwọn Olùkópa

Ìlànà PoArt ń tẹ̀síwájú pẹ̀lú àwọn ìkópa láti àwùjọ open source.

**Láti kópa:**
1. Ṣe Fork
2. Ṣẹ̀dá feature branch (`git checkout -b feature/amazing-feature`)
3. Ṣe Commit (`git commit -m 'Add amazing feature'`)
4. Ṣe Push (`git push origin feature/amazing-feature`)
5. Ṣí Pull Request

### 🛠️ Kí Ni A Nílò Báyìí? (Ìpè Fún Ìrànlọ́wọ́)

Fún àwọn ìdàgbàsókè **Ipele 2** ti Ìlànà PoArt, a ń retí àwọn ìkópa láti ọ̀dọ̀ àwọn olùṣẹ̀dá tó ní ìmọ̀ nínú àwọn kókó yìí:

* **Supabase Edge Functions:** Gbígbé ààbò spam sí apá server.
* **Solana Web3.js:** Ìdàpọ̀ ìbuwọ́lù àpamọ́wọ́ (Wallet Signing).
* **IPFS / Arweave:** Ìdàpọ̀ ìforúkọsílẹ̀ àti àwọn iṣẹ́ pinning.
* **Community Tools:** Ìdìbò X, àwọn ètò ìdìbò, dashboard analytics.

> Ẹ jọ̀wọ́ bẹ̀rẹ̀ ìjíròrò ní "Issues" kí ẹ tó fi àbùdá kan kún un.

---

## 💬 Àwọn Àkíyèsí Ìparí

### Pump.fun Àti Òtítọ́

A bẹ̀rẹ̀ iṣẹ́ àkànṣe yìí ní Pump.fun nítorí pé:
- ✅ Ìwọlé sí omi (Raydium automatic migration)
- ✅ Ìwọlé sí àwùjọ tó wà
- ✅ Iye ìbẹ̀rẹ̀ tó kéré

Ṣùgbọ́n ẹ jẹ́ ká ṣàlàyé èyí:
- **Iye token** kì í ṣe àpẹẹrẹ àṣeyọrí ọnà
- Iye token ṣe pàtàkì fún **ìṣúná ṣíṣe** (gallery, àwọn ìrísí, ìpìlẹ̀)
- **Àwọn ìwọ̀n àṣeyọrí:** Authenticated artworks + ìkópa àwùjọ + àwọn alábèwò ti ara

### Ìṣàkóso Àti Aládàáṣe

**Òtítọ́ v1.0 (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (àárín ṣùgbọ́n kedere)
- Governance: Advisory nìkan (ìpinnu curatorial ìparí)
- Token utility: Ìwọlé gallery + registry + àkọ́kọ́ NFT

**Ìran v2.0+ (2027+):**
- Registry: On-chain (Solana)
- Àwọn Ìbuwọ́lù: Dídúró lórí àpamọ́wọ́ (aládàáṣe)
- Governance: Híbrídì (ìmọ̀ràn àwùjọ + ìdárayá curatorial)
- Token utility: Àwọn àbùdá tó ga + ìwọlé tó ga

Ìṣètò yìí ń fún ni **ìmúṣiṣẹ́ ṣíṣe** àti **ìṣàkóso ìdárayá** ní ìbẹ̀rẹ̀, bó tilẹ̀ jẹ́ pé ó ń ṣí ọ̀nà sílẹ̀ fún **ìkópa àwùjọ** tó pọ̀ sí i ní ọjọ́ iwájú.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Àṣà Tóbi Ju Oluómìnira*

## 🧾 Ìwé-Àṣẹ

MIT License © 2026 İlhan Art Gallery Initiative

Wò [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) fún àwọn ọ̀rọ̀ kíkún.

---

## 💬 Ọpẹ́

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**A ti ṣe iṣẹ́ àkànṣe yìí pẹ̀lú ìgbìmọ̀ [İlhan Art Gallery], gbogbo code sì wà ní gbangba fún kedere.**

**ÌLÀNÀ V1.0 // A FI SHA-512 DÌ ÈDÌ**

*© 2026 İLHAN ART | GBOGBO ẸTỌ́ TI ÀWỌN IṢẸ́ ỌNÀ, ÀWÒRÁN ÀTI ÈRÒ JẸ́ TI WA.*

---
