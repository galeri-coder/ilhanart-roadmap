# 📚 ÌTÚMỌ̀ ÀTI ÀKÓJỌ ÈRÒ
> **"Láti mọ èdè ìlànà yìí túmọ̀ sí láti mọ ìran rẹ̀."**

## ⚙️ Ẹ̀rọ Ìwádìí PoArt (PFE) v1.0: Ìpìlẹ̀ Pàtàkì

**Ẹ̀rọ Ìwádìí PoArt (PFE)** jẹ́ ipele àkọ́kọ́ tí ó ń ṣojú ọgbọ́n àárín àti iṣẹ́ ìmọ̀-ẹ̀rọ lẹ́yìn ìlànà [PoArt]. Èyí ni "ẹ̀rọ ìwádìí" tí ó ń mú àwọn dátà títàn ti iṣẹ́ ọnà tí ó wà ní ojú-ìwé tí ó sì ń yí wọn padà sí **ẹ̀rí dájítà** tí a lè ṣàyẹ̀wò tí kò sì lè yí padà.

### 🧩 Kí ni ìdí "PoArt Forensic"?

- **PoArt (Ẹ̀rí Ọnà):** Èrò ẹ̀rọ náà ni láti so iye kadara dájítà kì í ṣe sí àsọtẹ́lẹ̀, ṣùgbọ́n sí **ìlànà ìṣèdá tí a lè ṣàyẹ̀wò**.
- **Forensic (Ìṣàyẹ̀wò Sáyẹ́ńsì):**
  - **Ìtúmọ̀ Ìmọ̀-ẹ̀rọ:** Ọ̀nà algorithm àti ìlànà àkọsílẹ̀ láti ṣàyẹ̀wò pé àwọn dátà ìlànà ìṣèdá (àwọn ìfàsẹ́ brush, vídíò àkókò, àkọsílẹ̀) kò ní ìdàrúdàpọ̀.
  - **Ipele Ìmọ̀-ọgbọ́n:** Ẹ̀rí láti yí **àkókò ènìyàn, ìgbìyànjú, àti iye ìpinnu** padà sí òtítọ́ tí a lè wọ̀n, lòdì sí ìṣèdá "èsì lẹ́sẹ̀kẹsẹ̀" AI.

> Àkíyèsí: Ìsopọ̀ blockchain (fún àpẹẹrẹ, Solana) kì í ṣe ọkàn PFE; a ó ṣàlàyé rẹ̀ lọ́tọ̀ gẹ́gẹ́ bí **Ipele Ìdásílẹ̀ Pùpọ̀** fún èrè ìṣàyẹ̀wò/ìforúkọsílẹ̀.

### 🛠️ Ìwọ̀n Ìmọ̀-ẹ̀rọ v1.0

**Ẹ̀rọ Ìwádìí PoArt (PFE) v1.0** jẹ́ kíkọ́ lórí **àwọn òpó mẹ́ta pàtàkì** wọ̀nyí dípò àwọn ìwé ìnáwó tí ó nira:

1. **Hashing & Sealing (Dídì):**  
   PFE ń ṣiṣẹ́ pẹ̀lú ìpinnu gbogbo àwọn nǹkan nínú Àpò Ẹ̀rí (fáìlì iṣẹ́, vídíò, JSON/àkọsílẹ̀, ìbúwọ́lù, àti bẹ́ẹ̀ bẹ́ẹ̀ lọ) tí ó sì ń ṣẹ̀dá iye **NotarySeal** pàtàkì kan.

   **Àwọn èrò pàtàkì (v1.0):**
   - **FileHash (ìtẹ̀sẹ́ ìka iṣẹ́):** Hash tí a ṣẹ̀dá láti bytes fáìlì iṣẹ́.
   - **EvidenceRoot (gbòǹgbò àpò ẹ̀rí):** Àkópọ̀ gbòǹgbò tí ó ń ṣojú òdodo Àpò Ẹ̀rí (gbòǹgbò Merkle tàbí hash àlàyé tó péye).
   - **NotarySeal (èdìdì ìparí / ìṣàkójáde PFE):** Èdìdì ìparí tí a ṣẹ̀dá láti àpapọ̀ EvidenceRoot + àkókò + ìbúwọ́lù.

   **Àwọn fọ́múlà (tí ó hàn kedere fún àwọn olùdókòwò):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Ìtúmọ̀ Ẹrù Pàtàkì (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Àkíyèsí: Iye tí a ń tọ́ka sí gẹ́gẹ́ bí ìṣàkójáde PFE ni **NotarySeal**. Ilana **SignerSignature** yóò di mímúṣẹ́ ní Ipele 2 (pẹ̀lú Solana Wallet Adapter); nínú v1.0 lọ́wọ́lọ́wọ́, a ń lo ìbúwọ́lù ẹ̀rí ètò. Wọ́n ń tẹ̀ jáde kọ́kọ́rọ́ gbogbogbò ẹ̀rí nínú ìforúkọsílẹ̀ lábẹ́ àyè `issuer.attestation_pubkey`.

2. **Indexing (Ìpamọ́):**  
   Ó ń kọ sílẹ̀ àpamọ́wọ́ wo, ní ọjọ́ wo, ló fi **Ẹ̀rí Iṣẹ́** ránṣẹ́ fún iṣẹ́ wo sí ipele ìforúkọsílẹ̀ tí ó hàn kedere tí a sì lè béèrè lọ́wọ́ rẹ̀.  
   *(Ipele yìí lè jẹ́ ibi ìpamọ́ dátà; ìsopọ̀ pùpọ̀ ní a ṣàlàyé lọ́tọ̀ gẹ́gẹ́ bí "Ipele Ìdásílẹ̀ Pùpọ̀".)*

3. **Verification (Ìṣàyẹ̀wò):**  
   Nígbà tí a bá ṣe ìyàsọ́tọ̀ nípa òdodo iṣẹ́ kan, PFE ń tún ṣiṣẹ́ àwọn ẹ̀rí títàn; ó ń ṣe ìdánwò ní ọ̀nà ìṣirò bóyá àwọn iye **EvidenceRoot / NotarySeal** tí a ṣèṣírò bá àwọn àkọsílẹ̀ ìpamọ́ mu.

---

### 🧮 Ìlànà Iye PoArt (The Value Theorem)

Ìlànà [PoArt] ń so iye ($V$) kadara dájítà kì í ṣe sí ìmọ̀ àìmọ́gbọ́nwá ọjà, ṣùgbọ́n sí **òtítọ́ ti ara ìlànà ìṣèdá**.

Ọgbọ́n Ìró (AI) ń ba ìlànà jẹ́ nípa fífa èsì jáde lẹ́sẹ̀kẹsẹ̀ ($t \to 0$). [PoArt], bí ó tilẹ̀ jẹ́ bẹ́ẹ̀, ń ṣe ìtọ́jú iye gẹ́gẹ́ bí àkójọpọ̀ àwọn apá **àkókò, iṣẹ́, àti ìfẹ́**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Ìtúmọ̀ Àwọn Ọ̀nà

- **$\int dt$ (Àkójọpọ̀ Ìlànà):**  
  Iye kì í ṣe "èsì" lẹ́sẹ̀kẹsẹ̀; **ìlànà** ni tí a kó jọ láàárín $t_{\text{start}}$ àti $t_{\text{end}}$. Bí gígùn bá ń dínkù (ìṣèdá AI), èsì integral náà ń súnmọ́ 0.

- **$P_{\text{labor}}(t)$ (Agbára Iṣẹ́ Lẹ́sẹ̀kẹsẹ̀):**  
  Ó ń ṣojú líle ìgbìyànjú ọpọlọ àti ti ara tí a ná ní àkókò ìṣèdá. Bí ìgbìyànjú tí a lè ṣàyẹ̀wò bá ń pọ̀ sí i, integrand náà ń dàgbà.  
  > Àkíyèsí: A lè ṣe àtúnṣe ọ̀rọ̀ yìí ní ìtẹ̀lọ́rùn nípa "àwọn àmì iṣẹ́ tí a lè wọ̀n/ṣàyẹ̀wò".

- **$I_{\text{agency}}(t)$ (Ìpín Ìfẹ́):**  
   Agbára olùṣèdá láti gba ewu àti ṣe ìpinnu. Ó ń gba iye láàárín $0$ àti $1$.
  - **AI ($I \approx 0$):** Ó ń ṣe àṣẹ, kò gba ewu, kò san iye owó.
  - **Ènìyàn ($I \to 1$):** Ń yí ìpinnu padà, ń ṣiyèméjì, ń gba ewu.

- **$U_{\text{irreversible}}$ (Àdánilójú Àìlèyípadà):**  
  Nígbà tí ìdásẹ́yìn (`Ctrl+Z`) ṣe é ṣe nínú ìṣèdá dájítà, nínú ìṣèdá ti ara (àwọ̀ tí a fi lé canvas, òkúta tí a gé, ìgbésẹ̀ nínú ìgbésíta taara) kò sí ọ̀nà ìpadàbọ̀. **Àìlèyípadà** yìí jẹ́ ọ̀rọ̀ àfikún tí ó ń ṣẹ̀dá "àdánilójú" (àbùdá àìlèpààrọ̀) nínú iṣẹ́ náà.

### 🔎 Àyẹ̀wò Ọ̀rọ̀: AI "Èsì Lẹ́sẹ̀kẹsẹ̀" vs. Ènìyàn "Ìlànà Tí A Ti Ṣàyẹ̀wò"

Ìṣẹ̀lẹ̀ tí ó tẹ̀le yìí ń ṣàfihàn bí **Ìlànà Iye PoArt** ṣe ń ṣiṣẹ́ ní ìtẹ̀lọ́rùn àti ìdí tí ìṣèdá AI fi ń gba àwọn àmì kékeré ní ìlànà [PoArt].

#### Ìṣẹ̀lẹ̀ A: Ìṣèdá Ríran ní Ìṣẹ́jú 10 pẹ̀lú AI

- **Gígùn ($\Delta t$):** $10$ ìṣẹ́jú (ìlànà kékeré)
- **Agbára Iṣẹ́ ($P_{\text{labor}}$):** $1$ ìwọ̀n (kìkọ àṣẹ nìkan)
- **Ìpín Ìfẹ́ ($I_{\text{agency}}$):** $0.01$ (kò sí ewu, kò sí iye owó)
- **Àìlèyípadà ($U_{\text{irreversible}}$):** $0$ (a lè yí padà / a lè ṣẹ̀dà)

**Èsì:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Àsọyé:** Bí èsì náà tilẹ̀ jẹ́ pípé; iye [PoArt] ń súnmọ́ $0$ nítorí a kò gbé ìlànà kankan ṣe kò sì sí ìfẹ́/ewu tí ó wà nínú rẹ̀.

#### Ìṣẹ̀lẹ̀ B: Ìṣèdá Ti Ara ti Wákàtí 6 ní Ìgbésíta Taara

- **Gígùn ($\Delta t$):** $6$ wákàtí ($21{,}600$ ìṣẹ́jú)
- **Agbára Iṣẹ́ ($P_{\text{labor}}$):** $0.5$ ìwọ̀n (ìtẹ̀síwájú ìgbìyànjú ti ara àti ọpọlọ)
- **Ìpín Ìfẹ́ ($I_{\text{agency}}$):** $0.9$ (yíyí ìpinnu padà, gbígba ewu, ìyàn àìlèyípadà)
- **Àìlèyípadà ($U_{\text{irreversible}}$):** $>0$ (àwọn àmì ti ara kò lè ṣe ìdásẹ́yìn)

**Èsì:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Àsọyé:** Bí ìlànà ṣe ń gùn àti bí ìfẹ́ (ewu) ṣe ń pọ̀ sí i, iye náà ń kó jọ ní àkójọpọ̀. Ọ̀rọ̀ $U_{\text{irreversible}}$ jẹ́ ìdásí àfikún tí ó ń ṣẹ̀dá "àdánilójú" (àbùdá àìlèpààrọ̀) nínú iṣẹ́ náà.

---

### ✅ Ìparí: Iye Tí A So Mọ́ Ẹ̀rí (Proof-Bound Value)

Ìlànà yìí ń mú ìjẹ́rìísí iye [PoArt] jáde láti jẹ́ "ìfẹ́ràn" tàbí "ìtàn ọjà" ó sì so ó mọ́ **òtítọ́ ìṣèdá tí a lè ṣàyẹ̀wò**.

1. **Kò Sí Ìlànà, Kò Sí Iye:**  
   AI ń ba ìlànà jẹ́ pẹ̀lú èsì lẹ́sẹ̀kẹsẹ̀ ($t \to 0$). Bí fèrèsé ìlànà ṣe ń dín, èsì integral náà dọ́gba láti dínkù:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Ìfẹ́ Àti Ewu Jẹ́ Aṣe-ìlọ́pọ̀:**  
   [PoArt] kì í ṣe kìkà "àkókò tí a ná" nìkan ṣùgbọ́n ipele òtítọ́ ìpinnu, ewu, àti iye owó nínú àkókò yẹn náà. Ìṣèdá láìgba ewu (AI) ní iye kékeré:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Àdánilójú Jẹ́ Ẹ̀rí Ti Ara, Kì í Ṣe Títà:**  
   Àwọn àmì àìlèyípadà nínú ìṣèdá ti ara (ìgbọ̀nsẹ̀ canvas, gígé òkúta) wà lóde ìmọ̀tò `Ctrl+Z` ti dájítà. Àìlèyípadà yìí ($U_{\text{irreversible}}$) ń ṣe àdánilójú iṣẹ́ náà ní ọ̀nà ontology.

> **🔐 ÀKÓPỌ̀:** Bí ìlànà iye tilẹ̀ lè dàbí àìnídìí gẹ́gẹ́ bí wíwọ̀n (bí ó tilẹ̀ jẹ́ pé àpẹẹrẹ rẹ̀ nínú ayé gidi kò lè ní wíwọ̀n ní kíkún), èrò fọ́múlà yìí ni láti ṣàfihàn ìṣètò àti itọ́sọ́nà àwọn ọ̀nà. Ní àkókò AI, ohun tí ó ṣòro ni kì í ṣe "àwòrán" ṣùgbọ́n **iṣẹ́ tí a lè ṣàyẹ̀wò, àkókò, àti ìfẹ́.** [PoArt] ń wọ̀n àìpọ̀ yìí ó sì ń kọ ọ́ sílẹ̀ pẹ̀lú **Àpò Ẹ̀rí**.

### 🏛️ Pàtàkì Èrò "Ẹ̀rọ"

Àwọn àmì tí ó ń yọ jáde láti Pump.fun tàbí àwọn pẹpẹ aláàjò ní ìgbà púpọ̀ jẹ́ **"àwọn tíkẹ́ẹ̀tì ìwọlé"** nìkan. **Ẹ̀rọ Ìwádìí PoArt (PFE)**, bí ó tilẹ̀ jẹ́ bẹ́ẹ̀, ni **ipele ìmọ̀tò ọgbọ́n òfin** tí ó ń pinnu àwọn ẹ̀tọ́ wo ni tíkẹ́ẹ̀tì yìí ń dáàbò bò, báwo ni a ṣe máa kọ iṣẹ́ náà sílẹ̀ àti báwo ni a ṣe máa tẹ̀síwájú ọnà/sáyẹ́ńsì/ìmọ̀-ẹ̀rọ.

> **Àkíyèsí:** Ìdí tí a fi ṣe ìfilọ́lẹ̀ iṣẹ́ yìí lórí Pumpfun ni pé a kò ní omi tó tó kò sì ní àwọn olùtẹ̀lé tó tó. Lílo dátà tí ó wà jẹ́ ìlànà ìgbésẹ̀ tó tọ́, bí ó tilẹ̀ jẹ́ pé kì í ṣe ìwọ̀n tó ga jù lọ. Láìka ìsúná àti àwọn ohun èlò sí i, ṣíṣàlàyé ìmọ̀tò ẹ̀rọ yìí lórí GitHub ń ṣe ẹ̀rí pé iṣẹ́ náà kì í ṣe àsọtẹ́lẹ̀ owó nìkan, ṣùgbọ́n ìran ìgbà pípẹ́ ti **ohun èlò sọ́fùtíwíà** àti **ilé-ìkàwé orílẹ̀-èdè dájítà**.

---

## 🎨 ÌLÀNÀ [PoArt] TI ẸRÍ IṢẸ́ (Proof of Art Protocol v1.0)

> **"Oníṣọ̀nà Gidi, Ìṣèdá Gidi, Iye Gidi."**

Ìlànà yìí jẹ́ **ìlànà ààbò ìbísí àti ọgbọ́n** tí a ṣẹ̀dá lòdì sí àwọn alárékérekè aláìmọ̀ tí ó yí ìṣesí crypto ká, àwọn àwòrán AI tí a ṣe ní ìṣẹ́jú 5, àti àṣà "Pump & Dump".

---

## a) Kí ni [PoArt]? (Ìtúmọ̀ Ìmọ̀-ọgbọ́n àti Ìmọ̀-ẹ̀rọ)

**Ẹ̀rí Ọnà [PoArt];** jẹ́ ìlànà ìṣàyẹ̀wò ilé-iṣẹ́ tí ó ń ṣe ìdánilójú pé iye lẹ́yìn kadara lórí blockchain kì í ṣe tó dá lórí àsọtẹ́lẹ̀, ṣùgbọ́n lórí **iṣẹ́ ènìyàn**, **àkókò**, àti **agbára ti ara** tí a lè ṣàyẹ̀wò.

Bí Bitcoin ṣe ń ṣẹ̀dá iye pẹ̀lú *"Iná Mànàmáná àti Agbára Processer"* **(Ẹ̀rí Iṣẹ́)**, àwọn iṣẹ́ aṣàmúlò tí ó bá [PoArt] mu ń ṣẹ̀dá iye pẹ̀lú *"Ọgbọ́n Ọnà àti Àkókò Ènìyàn"*.

Ó ń mú ewu *"Olùgbékalẹ̀ tà á, iṣẹ́ náà parí"* kúrò lórí àwọn pẹpẹ Pump.fun àti DEX; nítorí níbí iye kì í ṣe nínú kóòdù, ṣùgbọ́n nínú **ìtẹ̀síwájú ìṣèdá**.

> **[PoArt] kò sọ fún àwọn olùkópa "Ẹ gbà wá gbọ́"; ó ń sọ "Èyí ni ẹ̀rí, wò ó pẹ̀lú ojú rẹ, ṣàyẹ̀wò pẹ̀lú ìṣirò rẹ."**

---

## b) Ìlànà Òpó 5 [PoArt] (Àwọn Òpó 5 Ti Òtítọ́)

Àwọn nǹkan márùn-ún wọ̀nyí jẹ́ àwọn àṣẹ̀ tí a kò lè ṣèṣí tí iṣẹ́ gbọ́dọ̀ kọjá láti gba èdìdì [PoArt].

### 1) Ẹ̀rí Ìdánimọ̀ Taara

- **Ìṣòro:** Ayé crypto kún fún àwọn olùdásílẹ̀ aláìmọ̀ (Devs) pẹ̀lú ìdánimọ̀ àìmọ́ tí ó ń kó owó tí wọ́n sì ń fi iṣẹ́ sílẹ̀.
- **Ojútùú [PoArt]:** Olùṣèdá ń ṣe ẹ̀rí kì í ṣe ìwé ẹ̀rí nìkan, ṣùgbọ́n **ìwàláàyè ní àkókò ìṣèdá**. Èyí ní àwọn ìjókòó ìgbésíta taara níbi tí ìbáṣepọ̀ pẹ̀lú àwùjọ ń wáyé tí a sì ń pé àwọn ìbéèrè pàtàkì lẹ́sẹ̀kẹsẹ̀, kì í ṣe àwọn vídíò tí a ti ṣe àgbékalẹ̀ tẹ́lẹ̀.  
  (Fún àpẹẹrẹ, *"Kọ ọjọ́ òní àti nọ́mbà búlọ́ọ̀kù lọ́wọ́lọ́wọ́ ní igun ọ̀tún canvas"*)
- **Àkọlé:** *"Bots lè ya àwòrán ṣùgbọ́n bots kò lè gbẹ̀fún kò sì lè ṣe improvisation."*

### 2) Ẹ̀rí Iṣẹ́ Àti Ìlànà

- **Ìṣòro:** Àwọn àwòrán AI (Ọgbọ́n Ìró) tí a ṣe ní ìṣẹ́jú 2 tí ó ń gba ìtọ́jú "jpeg" kan náà bí àwòn ìyàwòrán epo tí a ṣe ní oṣù 2 ní ayé dájítà.
- **Ojútùú [PoArt]:** A ń kọ ìlànà "oyún àti ìbímọ" iṣẹ́ náà sílẹ̀. A ń kọ àwọn ìgbésẹ̀ sketch, àwọn ipele àwọ̀, àwọn wákàtí tí a kó jọ tí a ná àti ìlànà ti ara tí oníṣọ̀nà kọjá nígbà tí ó ń ṣẹ̀dá iṣẹ́ náà sílẹ̀. Èyí ń fi **"Iye Owó Àkókò"** kún àmì náà. Ìṣòro ìṣèdá kadara bó ṣe pọ̀ tó, iye rẹ̀ múra tó.

### 3) Ẹ̀rí Iye Ẹwà

- **Ìṣòro:** Àṣà "Meme" tí ó ń dójúkọ ẹ̀rín lẹ́sẹ̀kẹsẹ̀ nìkan nígbà tí ó ń fi ẹwà àti ìjìnlẹ̀ ọnà sílẹ̀, èyí tó ń fa àwọn iṣẹ́ "Hype" ìgbà kúkúrú.
- **Ojútùú [PoArt]:** Iṣẹ́ náà gbọ́dọ̀ ní àwọn ìlànà ọnà ẹ̀kọ́, ìlànà àwọ̀, òfin ìṣètò, àti ìmọ̀ ohun èlò (Impasto, Texture, àti bẹ́ẹ̀ bẹ́ẹ̀ lọ). Àkóónú kò gbọ́dọ̀ jẹ́ kí o rẹ́rìn-ín nìkan; ó gbọ́dọ̀ ru ìyanu sókè fún àwọn olùwòran ó sì gbọ́dọ̀ ní **iye ìkójọpọ̀**.

### 4) Tuntun Èrò

- **Ìṣòro:** Ẹgbẹ̀rún àwọn owó ajá/ológbò àdàkọ láìní ìṣẹ̀dá.
- **Ojútùú [PoArt]:** Iṣẹ́ náà gbọ́dọ̀ kọ́ afárá tuntun tí ó ń da ọnà, sáyẹ́ńsì, ìmọ̀-ọgbọ́n tàbí ìmọ̀-ẹ̀rọ pọ̀ nínú àgbékalẹ̀ tó ní ìtumọ̀.  
  (Fún àpẹẹrẹ, Dídapọ̀ ère atijọ́ David pẹ̀lú dátà ọjà crypto; ṣíṣe ìmúṣẹ èrò pé ìmọ̀ ènìyàn "ń di òkúta" nípa èyí tí a sì fi ìpìlẹ̀ẹ rẹ̀ múlẹ̀ pẹ̀lú àwọn orísun sáyẹ́ńsì.)  
  Iṣẹ́ náà kò gbọ́dọ̀ jẹ́ àjọ̀dún ríran nìkan ṣùgbọ́n tún ní ìpèníjà ọgbọ́n tí ó ń ru èrò sókè nípa **Sáyẹ́ńsì, Ìmọ̀-ọgbọ́n tàbí Ìmọ̀-ẹ̀rọ**.

> [!IMPORTANT]
> **Àpẹẹrẹ Ìrántí (Ipa Las Palmitas):** Ní àgbègbè Las Palmitas ní Mexico, tí ọ̀daràn ń pọ̀ sí i, wọ́n yí àwọn ilé tó lé ní 200 padà sí ìran òṣùmàrè ńlá kan. Nítorí ìṣediwọ́n ẹwà yìí, iye ọ̀daràn ní àgbègbè náà dínkù díẹ̀, àwọn ọ̀dọ́ sì bẹ̀rẹ̀ sí í ní ṣe ọnà dípò àwọn ẹgbẹ́ ọ̀daràn. Ìyípadà ẹwà náà tún kọ ọ̀wọ̀ ìbọ̀wọ̀ àwọn ènìyàn fún àyíká wọn àti ara wọn (Ìsopọ̀ Àwùjọ).
>
> **Ìrètí:** Iṣẹ́ tí ó bá wọ inú àtòjọ [PoArt] gbọ́dọ̀, bí nínú àpẹẹrẹ tó wà lókè, ní ìbátan ìdí-èsì àwùjọ, sáyẹ́ńsì tàbí ìmọ̀-ọgbọ́n ju ẹwà ríran lọ. Bí àkókò ṣe jẹ́ kadara kan ṣoṣo tí a kò lè rà pẹ̀lú owó, nínú ìlànà yìí a gbọ́dọ̀ ṣe ẹ̀rí àkókò nípa fífi rẹ̀ ṣe ìlérí gẹ́gẹ́ bí ààbò. Ìpìlẹ̀ èrò iṣẹ́ náà gbọ́dọ̀ jẹ́ alágbára àti ti ayé gbogbo tó bẹ́ẹ̀ tí àní nínú ìṣẹ̀lẹ̀ CTO (Ìgbà Àwùjọ Gbà) tó ṣeé ṣe lẹ́yìn ọdún, àwùjọ lè tẹ̀síwájú ní òmìnira agbára ìṣẹ̀dá iṣẹ́ náà nípa jogún ogún yìí.

### 5) Ìfẹ́ Tí Kì í Ṣe Ti Algorithm

- **Ìṣòro:** Àwọn ìṣèdá dájítà pípé ṣùgbọ́n aláìlẹ́mí tí ó ń tún ara wọn ṣe.
- **Ojútùú [PoArt]:** A gbọ́dọ̀ mọ ìfẹ́ àdáni ènìyàn tí ó lè ṣe àṣìṣe, gba ewu àti ní ìyípadà ìmọ̀lára nínú iṣẹ́ náà. Àìnídìí nínú àwọn ìgbọ̀nsẹ̀ brush, àwọn èsì àìrètí àwọn ohun èlò, àti àwọn ìpinnu lẹ́sẹ̀kẹsẹ̀ oníṣọ̀nà ni **Ìbúwọ́lù Ìbísí** tí ó ń yà iṣẹ́ náà sọ́tọ̀ kúrò ní "Ìṣèdá Ẹ̀rọ".

---

## c) Ìlànà Ìṣàyẹ̀wò Àti Ìdènà-Ẹ̀tàn

Ètò yìí ń ṣe ìdánilójú pé iṣẹ́ náà ń jẹ́ ìgbẹ́kẹ̀lé tí ó sì wà láàyè kì í ṣe "ní ìbẹ̀rẹ̀" nìkan ṣùgbọ́n "títí láé".

### 📦 Àpò Ẹ̀rí - Ìbejì Dájítà

Lẹ́yìn gbogbo iṣẹ́ tí [PoArt] ti fọwọ́sí ni àpò dátà tí a ti parọ́ tí ó sì ní àmì àkókò tí àwọn olùdókòwò lè gbà sọ̀kalẹ̀:

- **Àwọn Ìgbàsílẹ̀ Vídíò RAW:** Fíìmù títàn tí kò ní ìdásílẹ̀ ti àkókò ìṣèdá.
- **Àyẹ̀wò Metadata:** Ọjọ́ ìṣẹ̀dá fáìlì, àlàyé nípa ẹ̀rọ tí a lò àti dátà ipò.
- **Àwọn Ìtọ́kasí Ti Ara:** Ẹ̀rí pé iṣẹ́ náà wà ní ayé ti ara  
  (Fún àpẹẹrẹ, Ìwé ìròyìn lọ́wọ́lọ́wọ́ tàbí dátà blockchain ti àkókò yẹn lẹ́gbẹ̀ẹ́ iṣẹ́ náà).

> *Àkíyèsí ìbámu:* Ọ̀rọ̀ "àpò ẹ̀rí" ń sopọ̀ mọ́ pùpọ̀ **Àpò Ẹ̀rí → EvidenceRoot → NotarySeal** ní àwọn apá tó wà ṣáájú; èyí tó túmọ̀ sí pé, òdodo àpò náà ní wíwakọ́ nípa èdìdì tí a lè ṣàyẹ̀wò.

### 🔄 Ìmúdójúìwọ̀n Ọjọ́ 365 (Ìlànà Ìdúró Pẹ́)

- **Ẹ̀yà Ìyípadà:** Nínú àwọn iṣẹ́ crypto, "Dev" (Olùgbékalẹ̀) ń ṣe ìfilọ́lẹ̀ àmì tí ó sì gbogbo ìgbà ń parẹ́ lẹ́yìn oṣù 1-2 (Soft Rug). [PoArt] ń jẹ́ kí èyí má ṣeé ṣe.
- **Òfin:** Ipò "Oníṣọ̀nà Tí A Ti Ṣàyẹ̀wò" kì í ṣe fún gbogbo ayé. **Ọdún 1** nìkan ní ó wúlò.
- **Ìṣiṣẹ́:** Oníṣọ̀nà/olùgbékalẹ̀ gbọ́dọ̀ fi **iṣẹ́ tuntun pàtàkì tí a lè ṣàyẹ̀wò** hàn fún àwùjọ ní gbogbo ọjọ́ 365.
- **Àpẹẹrẹ Ìṣẹ̀lẹ̀:** O ṣe ìfilọ́lẹ̀ iṣẹ́ náà ní 2026. Ní January 2027, ètò náà ń fún ni ní ìkìlọ̀ "Àkókò Ẹ̀rí Ti Parí". Tí oníṣọ̀nà kò bá ṣàfihàn ìfihàn tuntun, iṣẹ́ ti ara tuntun tàbí ìsopọ̀ ìmọ̀-ẹ̀rọ tuntun, "Àmì Ìgbẹ́kẹ̀lé" iṣẹ́ náà ń ṣubú.
- **Èsì:** Ètò yìí ń ṣe ìdánilójú pé **àkóónú kò níí parẹ́ láé** àti pé olùdókòwò kò níí ní ìrìlárá ẹ̀rù *"Ṣé olùgbékalẹ̀ sì wà níbẹ̀?"*. Iṣẹ́ náà di ile-iṣẹ́ aláàyè.

### 🚩 Ìlànà Àsíá Pupa

**Ní ìṣẹ̀lẹ̀ ẹ̀tàn kankan tí àwùjọ tàbí algorithms bá ṣàwárí (lílo AI, iṣẹ́ jíjà, vídíò tí a ti dàrúdàpọ̀):**

1. Wọ́n ń fi àmì sí ìwé ẹ̀rí lẹ́sẹ̀kẹsẹ̀ bí **"VOID" (KÒ WÚLÒ)**.
2. Wọ́n ń fi àmì sí àwọn àpò ẹ̀rí ní gbangba bí **"Èké"**.
3. Wọ́n ń fi iṣẹ́ náà sínú àtòjọ dúdú [PoArt]. Èyí ń mú kí ó di mímọ̀ pé ní ayé aláìlákóso, **orúkọ rere ni owó kan ṣoṣo**.

---

## d) Ìparí: Kì í Ṣe Casino, Ṣùgbọ́n Ilé-Ìṣọ́

**Pump.fun àti Àwọn Pàṣípààrọ̀ Aláìlákóso (DEX) jẹ́ àníyàn casino báyìí; àwọn fìtílà ń tan, gbogbo ènìyàn ń lé èrè kíákíá lọ, ilé (àwọn alárékérekè) sì ń borí nígbà gbogbo. Ìdí tí a fi bẹ̀rẹ̀ iṣẹ́ náà níbí ni àìní ìsúná tó tó àti ní àyíká láti dé ọ̀dọ̀ àwọn olùgbọ́ tó wà nípa ìgbésíta taara.**

**[PoArt] jẹ́ odi tí a kọ́ láàárín casino yìí.**

- 🎰 Casino dá lórí eré kààdì; àwa dá lórí **òtítọ́ ti ara**.
- 🃏 Casino ṣí sílẹ̀ fún ẹ̀tàn; àwa ṣí sílẹ̀ fún **ẹ̀rí tó hàn kedere**.
- ⏳ Casino jẹ́ ìgbà díẹ̀; a dójúkọ **títí láé ọnà àti sáyẹ́ńsì**.

**Àmì tí ó bá lo ìlànà yìí kì í ṣe "owó" nìkan; ó jẹ́ ohun-ìní dájítà tó ní òógùn, àwọ̀, kóòdù àti ìmọ̀-ọgbọ́n.**

---

## 🗳️ 6) ÌṢÀKÓSO ÀTI ÌFORÚKỌSÍLẸ̀ GBOGBOGBÒ

**Èrò apá yìí ni: láti yí ìlànà [PoArt] padà láti ipele "ìgbẹ́kẹ̀lé nínú àwọn ènìyàn" sí ohun èlò gbogbogbò tí ó ní ìdúró pẹ́ pẹ̀lú ìforúkọsílẹ̀ + ìṣàyẹ̀wò + ìbójútó àwùjọ.**

### 6.1 Ìforúkọsílẹ̀ Gbogbogbò

- **Ìforúkọsílẹ̀ Gbogbogbò:** A ń kọ gbogbo dátà tí a fọwọ́sí sílẹ̀ ní `ilhanart.org/registry` (tàbí GitHub Registry).

**Ìmọ̀tò ìforúkọsílẹ̀ (ìlànà tí a ṣe ìmọ̀ràn - ní ọ̀nà ọ̀nà JSON):**

Gbogbo ìforúkọsílẹ̀ tí ó bá wọ inú ìforúkọsílẹ̀ ń gba àwọn àyè àárín wọ̀nyí tí a lè ṣàyẹ̀wò tó kéré jù:

- **Ìdánimọ̀ Àti Ipò:**
  - `certificate_id` (ìtọ́kasí tí a lè kà)
  - `status` (active / void)
  - `void_reason` (tí ó bá wúlò)
  - `visibility` (private / masked / public)
  - `created_at` (àmì àkókò)

- **Ilé-iṣẹ́ Ẹlẹ́rìí:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Àlàyé Iṣẹ́:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (tí ó bá ṣeé ṣe; fún ìdánimọ̀ pẹ̀lú ẹnu-ọ̀nà àmì)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Dátà Ìwádìí:**
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
  - `governance.veto_threshold`

Ìforúkọsílẹ̀ lè ní àwọn ipele méjì:
- **1)** Àtọ́kà tí ènìyàn lè kà (àtòjọ wẹ́ẹ̀bù / wíwá / àṣẹ̀)
- **2)** Àlàyé tí ẹ̀rọ lè kà (àwọn àkọsílẹ̀ JSON; fún ìṣàyẹ̀wò PFE)

**"Ìforúkọsílẹ̀" yìí di ẹni tí a lè ṣàyẹ̀wò nípa pùpọ̀ Àpò Ẹ̀rí → EvidenceRoot → NotarySeal ti PFE. Ìforúkọsílẹ̀ náà ń pèsè àwọn àfojúsùn ìṣàyẹ̀wò, kì í ṣe "ẹ̀sùn".**

---

### 6.2 Ìdílọ́wọ́ Àwùjọ 40% (Ìṣàkóso Pẹ̀lú Ẹnu-ọ̀nà Àmì)

- **Ìdílọ́wọ́ Àwùjọ 40%:** Ìdìbò ń bẹ̀rẹ̀ oṣù kan ṣáájú fífún ní ipò; ìdílọ́wọ́ 40% ti àwùjọ **pẹ̀lú Ẹnu-ọ̀nà Àmì (tí a ti ṣàyẹ̀wò Solana)** ń fagilee ìbéèrè náà.

**Ìlò ìdìbò (ìlànà tó hàn kedere tí a ṣe ìmọ̀ràn):**
- **Fèrèsé ìbéèrè:** Iṣẹ́ ọlọ́jà ń ṣí "ìforúkọsílẹ̀ ọlọ́jà PoArt" (àwọn àkọsílẹ̀ ọlọ́jà ń hàn ní ipò "dúró").
- **Àkókò àtúnyẹ̀wò:** Àwùjọ ń ṣàyẹ̀wò ẹ̀rí fún ọjọ́ 30 (Àpò Ẹ̀rí + àwọn ìgbàsílẹ̀ ìgbésíta taara + metadata).
- **Ìṣàyẹ̀wò pẹ̀lú ẹnu-ọ̀nà àmì:** A ń ṣe ìdìbò pẹ̀lú àwọn àpamọ́wọ́ Solana tí a ti ṣàyẹ̀wò (fún àpẹẹrẹ ohun-ìní àmì/NFT pàtàkì + ìbúwọ́lù àpamọ́wọ́).
- **Òfin ìdílọ́wọ́:** Tí 40% ti àwọn ìdìbò bá jẹ́ **ìdílọ́wọ́ (BẸẸ̀ KỌ́ / ÌDÍLỌ́WỌ́)**, a ń kọ̀ ìbéèrè náà.
- **Síṣíi:** A ń pa èsì ìdìbò mọ́ nínú ìforúkọsílẹ̀ bí "àkọsílẹ̀ ìpinnu" (ọjọ́, ìpín, ID àwòrán).

---

### 6.3 Ìdọ́gbà Metadata (Ìbámu Pẹ̀lú Ayé Ti Ara)

- **Ìdọ́gbà Metadata:** Dátà ìmọ̀-ẹ̀rọ nínú ìforúkọsílẹ̀ gbọ́dọ̀ bá nǹkan ti ara mu 100%.

**Ṣíṣàlàyé "ìbámu 100%" ní ọ̀nà ìmọ̀-ẹ̀rọ (ìṣípayá tí a ṣe ìmọ̀ràn):**
- **Ìbámu kékeré jù (dandan):**
  - `asset.fingerprints.sha256/sha512` nínú ìforúkọsílẹ̀ gbọ́dọ̀ jẹ́ **bákan náà** pẹ̀lú hash fáìlì tí a ń sọ̀rọ̀ nípa rẹ̀.
  - Nígbà tí a bá tún ṣe `proof.notary_seal` nínú ìforúkọsílẹ̀ (tí Àpò Ẹ̀rí bá wà), ó gbọ́dọ̀ jẹ́ **bákan náà**.
- **Ìbámu ìtọ́kasí ti ara (irú ẹ̀rí):**
  - Iṣẹ́ ti ara + ìtọ́kasí ọjọ́/búlọ́ọ̀kù tí a fi hàn nínú ìgbésíta taara àti ẹ̀rí bákan náà gbọ́dọ̀ bá Àpò Ẹ̀rí mu.
- **Ìgbọ́ràn àṣírí:**
  - Àwọn àyè bí IP/ipò ní ìríran `masked` ní wíwé jáde **gẹ́gẹ́ bí àwọn ìlànà ìbòjú**.

---

### 6.4 Ìjà Àti Ìfagilee

Ìforúkọsílẹ̀ kì í ṣe ìlànà "ìfọwọ́sí" nìkan; **ìlànà àyẹ̀wò aláàyè** ni lòdì sí ẹ̀tàn.

- Nígbà tí a bá bẹ̀rẹ̀ ìjà, a lè fi ìforúkọsílẹ̀ náà sí ipò **"review" (àtúnyẹ̀wò)**.
- Tí a bá rí ẹ̀tàn, a ń fi àmì sí i bí `status: void` pẹ̀lú ìdí tí a fi kùn:
  - `void_reason` (lílo AI / jíjà / dídàrúdàpọ̀, àti bẹ́ẹ̀ bẹ́ẹ̀ lọ)
  - `revoked_at` (àkókò ìfagilee)
- Orísun ìpinnu ìfagilee ń hàn kedere nínú ìforúkọsílẹ̀:
  - ìdìbò àwùjọ / ìgbìmọ̀ tí a fún ní àṣẹ / àkíyèsí ìwádìí sáyẹ́ńsì (èyí tó bá wúlò)

> **Apá yìí ni àkọ́kọ́ ìforúkọsílẹ̀ ti èrò VOID nínú apá "Ìlànà Àsíá Pupa".**

---

### 6.5 Àpẹẹrẹ Ìforúkọsílẹ̀ (Tí Ẹ̀rọ Lè Kà)
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
> *Àkíyèsí: `asset.fingerprints.sha512` àti àwọn iye hash mìíràn ní píkúrúkúrú fún àfihàn; nínú ìmúṣẹ gan-an, a ń lo àwọn okùn kíkún ọ̀rọ̀ hexadecimal.*

---

## 7) 🔐 ÈDÌDÌ ÌMỌ̀-ẸRỌ (NOTARY SEAL)

Algorithm èdìdì aláìyípadà tí **Ẹ̀rọ Ìwádìí PoArt (PFE) v1.0** ṣẹ̀dá:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Ìlànà [PoArt] Ti Notary Dájítà Àti Ẹ̀rí Sáyẹ́ńsì (Beta v1.0)

> **"Àṣà tóbi ju Owó lọ. Dáàbò bo àwọn iṣẹ́ rẹ lónìí, gbé wọn lọ sí ọ̀la."**

---

## Kí ni ìdí Gbogbogbò?

Ààbò òtítọ́ ń wá láti ìhàn kedere. Ọpẹ́ fún ètò **Ìforúkọsílẹ̀ Gbogbogbò** wa, ẹnikẹ́ni níbikíbi ní ayé lè ṣàyẹ̀wò pé fáìlì kan jẹ́ atọ́wọ́dọ́wọ́ ní ìṣẹ́jú, láì nílò ẹ̀rí kankan.

---

## 🧩 Kí ni ìdí "Àwọn Module Ìríran" Púpọ̀?

Èyí ni apá pàtàkì jù ti kóòdù (àtòjọ yíyàn ìríran). Àwọn àṣàyàn wọ̀nyí ń jẹ́ kí àwọn olùlò ṣe ìdọ́gbà **"Àṣírí vs. Ìhàn Kedere"**:

### 🔒 Àdání

- **Ìṣẹ̀lẹ̀:** Oníṣọ̀nà ò tíì fẹ́ tẹ̀ iṣẹ́ náà jáde, ṣùgbọ́n ó fẹ́ fi àmì àkókò sí i láti ṣe ẹ̀rí "mo ṣe èyí ní ọjọ́ yìí".
- **Kíni Kóòdù Náà Ń Ṣe:** Ó ń kọ dátà sínú ibi ìpamọ́ dátà ṣùgbọ́n ó ń fi àmì `visibility: "private"`. Lẹ́yìn àyè nígbà tí o bá kọ ìlànà "Kíkà Gbogbogbò", o lè fi àwọn àkọsílẹ̀ wọ̀nyí pamọ́ kúrò ní gbangba pẹ̀lú `WHERE visibility = 'public'`.

### 🕶️ Ìbòjú

- **Ìṣẹ̀lẹ̀:** Oníṣọ̀nà fẹ́ ìhàn kedere ṣùgbọ́n ó bẹ̀rù pé a máa rí àdírẹ́ẹ̀sì ilé rẹ̀ (ipò IP).
- **Kíni Kóòdù Náà Ń Ṣe:** Àwọn iṣẹ́ `maskIP` àti `maskLoc` ń ṣiṣẹ́ ní apá JavaScript. Ó ń yí àdírẹ́ẹ̀sì IP padà sí ọ̀nà `88.241.***.***`, ipò sí ọ̀nà `***/TR`, tí ó sì ń fi àtúntò tí a fi ìyàsọ́tọ̀ ránṣẹ́ sí ibi ìpamọ́ dátà.
- **Àkíyèsí Àṣírí:** A ń ṣe ìbòjú ní ẹ̀rọ àwárí, Supabase kò rí ipò gan-an. **Ṣùgbọ́n:** Tí a bá lo àwọn APIs ẹlòmíràn bí ipapi.co fún dátà ipò, àwọn olùpèsè wọ̀nyí ń rí àdírẹ́ẹ̀sì IP ní àkókò ìbéèrè.
- **Èdìdì ní Ọ̀nà Ìbòjú:** A ń ṣe ìṣirò EvidenceRoot àti NotarySeal pẹ̀lú dátà ìwádìí tí a fi ìbòjú; nítorí náà ìṣàyẹ̀wò ń jẹ́ ìpinnu.

### 🌍 Gbogbogbò

- **Ìṣẹ̀lẹ̀:** Ìhàn kedere kíkún. Gẹ́gẹ́ bí àwọn ìlànà [PoArt], níbo, nígbà wo, láti orí nẹ́tíwọ́ọ̀kì wo ni a ṣẹ̀dá iṣẹ́ náà ní kíkéde kedere.

---

## 💡 Ìṣẹ̀dá Ìmọ̀-ẹ̀rọ

PoArt kì í ṣe ètò ìgbékalẹ̀ fáìlì nìkan. Ó jẹ́ ẹ̀rọ **"Pùpọ̀ Ìtọ́jú Sáyẹ́ńsì"** tí ó ń mú ìlànà tuntun wá nípa dídàpọ̀ àwọn ipele ìmọ̀-ẹ̀rọ mẹ́ta tó yàtọ̀ sí ìkòkò kan.

**Ipele tí a ṣàlàyé gẹ́gẹ́ bí "ẹ̀rọ" nínú apá yìí ń bá ọkàn Ẹ̀rọ Ìwádìí PoArt (PFE) mu nínú ìṣàlàyé ṣáájú.**

### 1) Hashing Apá Oníbàárà (Àṣírí Tó Ga Jù)

A kò gbé àwọn fáìlì iṣẹ́ ọnà rẹ kalẹ̀ sórí ọ̀dọ̀. Ẹ̀rọ wa tó dá lórí ẹ̀rọ àwárí (apá oníbàárà) ń ṣe ìṣirò hash (àkópọ̀ dájítà) fáìlì náà lórí kọ̀mpútà tìrẹ. Ìtẹ̀sẹ́ ìka yìí àti metadata nìkan ni a ń fi ránṣẹ́ sí ọ̀dọ̀.

> **Àkíyèsí Àṣírí:** A kò gbé fáìlì iṣẹ́ náà kalẹ̀ sórí ọ̀dọ̀ a sì dáàbò bò ó báyìí. Bí ó tilẹ̀ jẹ́ bẹ́ẹ̀, a ń pín dátà ìwádìí (IP/ipò) gẹ́gẹ́ bí ọ̀nà ìríran tí a yàn (àdání/ìbòjú/gbogbogbò).

### 2) Àdàpọ̀ Dátà Ìwádìí (Agbára Sáyẹ́ńsì)

Púpọ̀ ju àmì àkókò déédé lọ. Ètò náà ń da àwọn dátà wọ̀nyí pọ̀ sínú "Èdìdì Ìbẹ̀rẹ̀" kan:

- **Àkópọ̀ Dájítà (SHA-512):** Ìtẹ̀sẹ́ ìka nípa lílo ìlànà àkópọ̀ cryptographic (SHA-512) tí yóò fọ́ tí kódà pixel kan bá yí padà nínú iṣẹ́ náà.
- **Ipò Àti Àkókò:** Ọjọ́ pẹ̀lú ìgbéléyìn milliseconds, orílẹ̀-èdè, ìlú àti dátà àgbègbè ìdúnàádúrà.
- **Ìdánimọ̀ Ẹ̀rọ:** Ètò ìṣiṣẹ́, ẹ̀rọ àwárí àti irú ẹ̀rọ (àyẹ̀wò User-Agent).

---

## 🛡️ Àwọn Ìlò Àti Àǹfàní

Tí o bá jẹ́ oníṣọ̀nà, onímọ̀kọ́wé tàbí aláṣẹ, sísọ "Mo ṣe èyí tẹ́lẹ̀" kò tó; o nílò láti ṣe ẹ̀rí.

**Iṣẹ́ tí o fi èdìdì pẹ̀lú PoArt:**

- **Ẹ̀rí Ìṣirò:** Tí kódà pixel kan bá yí padà nínú fáìlì rẹ, ètò náà mọ̀. Àìṣedéédéé kò ṣeé ṣe.
- **Ìpìlẹ̀ Òfin:** A ti kọ ọjọ́ wo, ìlú wo, láti ẹ̀rọ wo ni a fi èdìdì sí iṣẹ́ náà sílẹ̀.
- **Ìwé Ẹ̀rí Lẹ́sẹ̀kẹsẹ̀:** Ó ń ṣẹ̀dá **"Ìwé Ẹ̀rí Ìdánimọ̀ Kadara"** pàtàkì fún ọ ní ìṣẹ́jú, pẹ̀lú kóòdù QR tí a sì fi èdìdì sí i.

---

## ⚙️ Àgbékalẹ̀ Ètò Àti Àwọn Ẹ̀yà Ìmọ̀-ẹ̀rọ

A ṣe àgbékalẹ̀ ètò náà lórí àgbékalẹ̀ "Serverless", tí ó ń dójúkọ ìṣesí gíga àti agbára láti gbooro.

| Ipele | Ìmọ̀-ẹ̀rọ | Àlàyé |
|--------|-----------|-------------|
| **Ìparọ́** | SHA-256 & SHA-512 | Àkópọ̀ cryptographic ipele méjì |
| **Ibi Ìpamọ́ Dátà** | Supabase (PostgreSQL) | Àgbékalẹ̀ dátà JSONB, àwọn ìlànà RLS |
| **Dátà Ìwádìí** | ipapi.co API | Mẹ́ta IP/Ipò/Àkókò |
| **Ṣíṣe Àfihàn** | html2canvas + jsPDF | Ìṣẹ̀dá PNG/PDF apá oníbàárà |
| **Frontend** | Vanilla JavaScript | Ìgbẹ́kẹ̀lé lórí ilana òfò |
| **Ààbò** | Hashing apá oníbàárà | Fáìlì kò gbẹ̀dọ̀ lọ |

### Àwọn Ẹ̀yà Tó Hàn Kedere

| Ẹ̀yà | Àlàyé | Ní Àwọn Alámìíṣe? |
|---------|-------|-----------------|
| **UI Wọlé & Sọ̀kalẹ̀** | Wọlé àti sọ̀kalẹ̀ fáìlì, ìríran lẹ́sẹ̀kẹsẹ̀ | ❌ Kò sí ní ọ̀pọ̀ |
| **Ìgbéjáde Oríṣiríṣi** | PNG, JSON, PDF - tẹ̀ ẹyọkan | ⚠️ Àìtó |
| **Ìríran Àkókò Lára** | Ìríran ìwé ẹ̀rí taara | ❌ Kò sí |
| **Àwọn Ìṣàkóso Àṣírí** | Àwọn àṣàyàn Àdání/Ìbòjú/Gbogbogbò | ❌ Kò sí |
| **Hash Apá Oníbàárà** | Fáìlì kò gbẹ̀dọ̀ lọ | ✅ Nínú díẹ̀ nìkan |
| **Metadata Ìwádìí** | IP, ipò, ẹ̀rọ, àkókò - gbogbo wọn papọ̀ | ❌ Pínpín |
| **Ìṣàyẹ̀wò QR** | Kóòdù QR ìṣàyẹ̀wò lẹ́sẹ̀kẹsẹ̀ | ⚠️ Àìtó |
| **Ìdínà Iyára** | Ààbò lòdì sí spam (RLS + Oníbàárà) | ❌ Kò sí ní ọ̀pọ̀ |

---

## 🗺️ Àwòrán Ọ̀nà: Ọjọ́ Iwájú "Láì Ní Ìgbẹ́kẹ̀lé"

Àtúntò lọ́wọ́lọ́wọ́ **(Beta v1.0)** jẹ́ ìmúdára láti fún àwọn olùlò ìparí ní iyára tó ga jù, ẹ̀rọ tó rọrùn àti ìwọlé ọ̀fẹ́. Bí ó tilẹ̀ jẹ́ bẹ́ẹ̀, ìran wa ìparí ni àyípadà sí àgbékalẹ̀ níbi tí kódà alábòójútó ibi ìpamọ́ dátà (àwa) kò lè lọ́wọ́ sí i.

### Ipele 1: Beta (Ó Wà Lára Lọ́wọ́lọ́wọ́)

- **Ohun Èlò:** Ibi Ìpamọ́ Dátà Àwọsánmọ̀ (Supabase).
- **Èrò:** Iyára, ìmúkúrò àwọn ìdènà UX (Ìrírí Olùlò) àti ìbámu. Pípèsè ààbò "láì ní ìdènà".

### 🚀 Ipele 2: (Àwọn Ìbéèrè Backend / Iṣẹ́ Edge)

Ipele yìí ń bò àyípadà láti àgbékalẹ̀ iṣẹ́ "apá oníbàárà" pátápátá sí àgbékalẹ̀ "Àṣẹ Apá Ọ̀dọ̀" tó ní ààbò púpọ̀ tó sì lè ní ìṣàkóso.

| Nǹkan | Kíni Ó Ń Mú Wá? | Àpapọ̀ Ìmọ̀-ẹ̀rọ | Pàtàkì |
|-------|---------------|------------|---------|
| **`INSERT` → Iṣẹ́ Edge** | Ìdènà spam + ààbò kọ́kọ́rọ́ API | Supabase Edge (Deno) | 🔴 Gíga |
| **Ìbúwọ́lù Àpamọ́wọ́** | Ìṣàyẹ̀wò cryptographic | Solana Wallet Adapter | 🟡 Àárín |
| **Àdúgbò IPFS/Arweave** | Àìlèyípadà láì ní àkóso àárín | IPFS SDK + Pinata | 🟢 Kékeré |
| **Ìlànà Ìfagilee** | Ìfàgílé ìwé ẹ̀rí èké | Ìmúdójúìwọ̀n Àgbékalẹ̀ DB | 🔴 Gíga |
| **Àkọsílẹ̀ Àyẹ̀wò** | Àkọsílẹ̀ ìbéèrè sáyẹ́ńsì | Tábìlì àkọsílẹ̀ pàtàkì | 🟡 Àárín |
| **OpenTimestamps** | Ìdásílẹ̀ Bitcoin | OTS JavaScript | 🟢 Kékeré |
| **Ìsopọ̀ DID** | Ìdánimọ̀ Láì Ní Àkóso Àárín | ION/Ceramic | 🟢 Kékeré |

### Ipele 3: Àìní Àkóso Àárín Kíkún (Ìgbà Pípẹ́)

| Ẹ̀yà | Èrò | ETA |
|---------|------|-----|
| **Ìforúkọsílẹ̀ Blockchain** | Ìforúkọsílẹ̀ lórí pùpọ̀ Ethereum/Solana | Q4 2026 |
| **Ìṣàkóso DAO** | Ìṣàkóso àwùjọ | Q1 2027 |
| **Àtìlẹ́yìn Pùpọ̀ Púpọ̀** | Polygon, Arbitrum, Base | Q2 2027 |
| **Ìmọ̀ Òfin** | Ìwúlò ní àwọn ilé-ẹjọ́ Turkíì | 2027-2028 |
| **API Fún Àwọn Olùgbékalẹ̀** | Ìparí API gbogbogbò | Q3 2026 |

---

## 📊 Àyẹ̀wò Ìdíje (Tí A Ti Ṣe Ìmúdójúìwọ̀n)

PoArt wà ní "Sweet Spot" tí ó ń kun àwọn àìtó àwọn ojútùú tí ó wà.

| Ẹ̀yà | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Iye Owó** | 🆓 Ọ̀fẹ́ | 🆓 | 💰 Owó | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI Wọlé & Sọ̀kalẹ̀** | ✅ Rọrùn Gan-an | ❌ CLI | ⚠️ Àárín | ⚠️ Àárín | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Ìgbéjáde Oríṣiríṣi** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Ìríran Àkókò Lára** | ✅ Taara | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Àwọn Ìṣàkóso Àṣírí** | ✅ Ọ̀nà 3 | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Hash Apá Oníbàárà** | ✅ Àṣírí | ✅ | ❌ Ìgbékalẹ̀ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Metadata Ìwádìí** | ✅ Kíkún | ❌ | ❌ | ⚠️ Àìtó | ❌ | ⚠️ | ❌ | ⚠️ |
| **Ìṣàyẹ̀wò QR** | ✅ Lẹ́sẹ̀kẹsẹ̀ | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Ìdínà Iyára** | ✅ RLS+Oníbàárà | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Ìdásílẹ̀ Blockchain** | 🔄 Àwòrán Ọ̀nà | ✅ Bitcoin | ✅ Ethereum | ✅ Púpọ̀ | ✅ | ✅ | ✅ | ✅ |
| **Orísun Ṣíṣí** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Àtìlẹ́yìn Turkíì** | ✅ Ìbílẹ̀ | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Ìtumọ̀:**
- ✅ : Àtìlẹ́yìn kíkún / wà
- ⚠️ : Àìtó / nínú àwọn ètò owó
- ❌ : Kò sí / a kò tìlẹ́yìn
- 🔄 : Nínú àwòrán ọ̀nà (ń gbòòrò)
- 🆓 : Ọ̀fẹ́ pátápátá
- 💰 : Owó / ìforúkọsílẹ̀ ń bééré

### Àwọn Àìtó Àwọn Alámìíṣe, Àwọn Agbára PoArt

| Àìtó | Àwọn Alámìíṣe | PoArt |
|-------|-------------|-------|
| **Ìṣòro Ìlò** | CLI, ìmọ̀ API, àpamọ́wọ́ ń bééré | Wọlé àti sọ̀kalẹ̀, tán ní tẹ̀ 3 |
| **Ìdènà Iye Owó** | Ìforúkọsílẹ̀ $50-500/oṣù | 100% ọ̀fẹ́ |
| **Àṣírí** | A ń gbé fáìlì kalẹ̀ sórí ọ̀dọ̀ | Apá oníbàárà, fáìlì kò gbẹ̀dọ̀ lọ |
| **Dátà Ìwádìí** | Àmì àkókò nìkan | IP, ipò, ẹ̀rọ, àkókò - gbogbo |
| **Àtìlẹ́yìn Turkíì** | Kò sí tàbí àìtó púpọ̀ | Àtìlẹ́yìn èdè ìbílẹ̀ |
| **Orísun Ṣíṣí** | Àpótí títì | Gbogbo kóòdù ṣíṣí lórí GitHub |

---

## 🧬 Àgbékalẹ̀ Dátà Ìlànà (JSON Schema)

**Gbogbo ìwé ẹ̀rí [PoArt] ní kàádì ìdánimọ̀ JSON tí ó lè gbé tí a sì lè ṣàyẹ̀wò tí a ṣẹ̀dá ní ìlànà tó wà nísàlẹ̀.**

> **Àkíyèsí:** Àgbékalẹ̀ JSON ìdánimọ̀ yìí jẹ́ àgbékalẹ̀ ìwé ẹ̀rí tí a ń gbé kalẹ̀ fún àwọn olùlò. Nínú àwọn àkọsílẹ̀ ìforúkọsílẹ̀, a ń lo `registry.asset` dípò `identity.asset_data` (ìṣàpèjúwe: `identity.asset_data` == `registry.asset`).
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

## 🔬 Ìjìnlẹ̀ Ìmọ̀-ẹ̀rọ: Algorithm Èdìdì

### Àwọn Iṣẹ́ Hash Tí Ó Ní Ìpinnu
```javascript
// Àwọn Iṣẹ́ Ìrànlọ́wọ́: Yí àkópọ̀ padà sí okùn hexadecimal
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Yí okùn padà sí àkójọpọ̀ bytes
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Ìṣẹ̀dá okùn ìwádìí pàtàkì (v1.0: ètò àyè tí ó dúró + UTF-8 + pínpín \n)
// Àkíyèsí Ipele 2: Àyípadà sí JSON pàtàkì pẹ̀lú RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Ìlànà Ìṣẹ̀dá NotarySeal (Pẹ̀lú Ìpinnu Pátápátá)
```javascript
// 1. Ìṣirò FileHash (apá oníbàárà)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Kíkójọpọ̀ dátà ìwádìí (lílo àmì àkókò kan)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Ìṣẹ̀dá àmì àkókò kan
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Àmì àkókò kan náà
  };
  
  return { forensics, timestamp };
}

// 3. Ìṣẹ̀dá EvidenceRoot (pẹ̀lú ìparọ́ pàtàkì)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Ìṣẹ̀dá NotarySeal (lílo àmì àkókò kan náà)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Àwọn iṣẹ́ ìrànlọ́wọ́ ìbòjú (àtìlẹ́yìn IPv4 àti IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Àyẹ̀wò IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 tàbí àgbékalẹ̀ àìmọ̀
  return "***";
}
```

### Ìlò Ìṣàyẹ̀wò (Àwọn Ipele Méjì)

#### Quick Verify (Ìṣàyẹ̀wò Kíákíá)
```javascript
// Ṣàyẹ̀wò hash fáìlì nìkan (àsíá pupa kíákíá)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Gbà láti ìforúkọsílẹ̀
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Àfiwéra hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Atọ́wọ́dọ́wọ́ - Hash fáìlì bá ara mu"
    };
  } else {
    return {
      valid: false,
      message: "❌ Èké - A ti dàrúdàpọ̀ fáìlì náà"
    };
  }
}
```

#### Full Verify (Ìṣàyẹ̀wò Kíkún)
```javascript
// Tún ṣẹ̀dá kí o sì ṣàyẹ̀wò EvidenceRoot àti NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Gbà láti ìforúkọsílẹ̀
  const cert = await fetchFromRegistry(certificateId);

  // 1) Ìṣàyẹ̀wò FileHash (àsíá pupa kíákíá)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Èké - Hash fáìlì kò bá ara mu" };
  }

  // 2) Tún ṣẹ̀dá EvidenceRoot (pẹ̀lú dátà ìwádìí tí a pa mọ́ nínú ìforúkọsílẹ̀)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Kò bá ara mu - EvidenceRoot kò dúró" };
  }

  // 3) Tún ṣẹ̀dá NotarySeal (pẹ̀lú àmì àkókò kan náà + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Kò bá ara mu - NotarySeal kò dúró" };
  }

  // Àṣàyàn: Ní Ipele 2, tún ṣàyẹ̀wò signer_sig pẹ̀lú attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Ìbúwọ́lù tí kò wúlò" };

  return { valid: true, message: "✅ Atọ́wọ́dọ́wọ́ - Ìṣàyẹ̀wò kíkún kọjá" };
}
```

> **Àwọn Àkíyèsí Pàtàkì:**
> - **Quick Verify:** Ń ṣàyẹ̀wò hash fáìlì nìkan fún ìlò kíákíá.
> - **Full Verify:** Ń ṣàyẹ̀wò gbogbo àwọn ipele ìlànà (EvidenceRoot + NotarySeal).
> - A ń ṣe gbogbo àwọn iṣẹ́ hash ní ìpinnu pẹ̀lú ìparọ́ àti àwọn pínpín tó dúró.
> - **Ìlànà ṣíṣe pàtàkì v1.0:** Ètò àyè tó dúró + ìparọ́ UTF-8 + pínpín `\n`.
> - **Ètò Ipele 2:** Àyípadà sí JSON pàtàkì pẹ̀lú RFC 8785 (JCS - JSON Canonicalization Scheme).
> - Ní ọ̀nà ìbòjú, a ń ṣe ìṣirò EvidenceRoot àti NotarySeal pẹ̀lú dátà ìwádìí tí a fi ìbòjú; nítorí náà ìṣàyẹ̀wò ń jẹ́ ìpinnu.
> - A ń lo àmì àkókò kan náà jákèjádò ìlànà náà (ìwádìí + NotarySeal); a ti ṣe ìdánilójú ìpinnu.
> - **Àwọn orúkọ àyè ìwádìí:** `ip_masked`, `location`, `device`, `timestamp` (kóòdù àti ìforúkọsílẹ̀ bá ara mu pátápátá).
> - **Ọ̀nà ìforúkọsílẹ̀:** `certificate.asset.fingerprints` (bá kóòdù ìṣàyẹ̀wò mu pátápátá).
> - **signer_sig nínú ìforúkọsílẹ̀:** Àyè `proof.signer_sig` ń nílò fún Full Verify.
> - A ó mú ìlànà SignerSignature ṣiṣẹ́ ní Ipele 2 pẹ̀lú Solana Wallet Adapter; ní v1.0, a lè ṣe ìṣàyẹ̀wò pẹ̀lú `attestation_pubkey`.

---

## 📈 Àwọn Ìṣirò Ìlò (Àwọn Àfojúsùn Q1 2026)

| Òṣùwọ̀n | Àfojúsùn | Ipò |
|--------|--------|--------|
| **Àpapọ̀ Àwọn Ìwé Ẹ̀rí** | 1,000 | 🔄 Ìlọsíwájú |
| **Àwọn Olùlò Aláàyè** | 500 | 🔄 Ìlọsíwájú |
| **Iye Àwọn Ìṣàyẹ̀wò** | 5,000 | 🔄 Ìlọsíwájú |
| **Àkókò Ìwàláàyè** | 99.9% | ✅ Aláàyè |
| **Àpapọ̀ Àkókò Ìdáhùn** | <200ms | ✅ Dáradára |

---

## 🌍 Àwùjọ Àti Àtìlẹ́yìn

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Wẹ́ẹ̀bù:** [ilhanart.org](https://ilhanart.org)
- **Ímeèlì:** galeri@ilhanart.org

---

## 🙏 Àwọn Alábábọ̀

Ìlànà PoArt ń tẹ̀síwájú láti gbòòrò pẹ̀lú àwọn àbábọ̀ láti àwùjọ orísun ṣíṣí.

**Láti ṣe àbábọ̀:**
1. Fork àpamọ́wọ́ náà
2. Ṣẹ̀dá ẹ̀ka ẹ̀yà (`git checkout -b feature/amazing-feature`)
3. Ṣe Ìbúwọ́lù (`git commit -m 'Add amazing feature'`)
4. Títa (`git push origin feature/amazing-feature`)
5. Ṣí Ìbéèrè Wíwọ́lé

### 🛠️ Kí ni A Nílò Báyìí? (Ìpè Ìrànlọ́wọ́)

Ìlànà PoArt ń wá àwọn olùgbékalẹ̀ ọlọ́gbọ́n ní àwọn àgbègbè tó wà nísàlẹ̀ fún ìgbòòrò **Ipele 2**:

* **Àwọn Iṣẹ́ Edge Supabase:** Gbé ààbò spam lọ sí apá ọ̀dọ̀.
* **Solana Web3.js:** Ìsopọ̀ ìbúwọ́lù àpamọ́wọ́.
* **IPFS / Arweave:** Ìsopọ̀ àwọn iṣẹ́ ìpamọ́ àti píníní.

> Jọ̀wọ́ bẹ̀rẹ̀ ìjíròrò ní àkójọ "Issues" ṣáájú fífikún ẹ̀yà kan.

---

**Ìlànà [PoArt] Proof of Art v1.0**  
*"Àṣà > Owó"*

## 🧾 Ìwé-àṣẹ

Ìwé-àṣẹ MIT © 2026 Ilhan Art Gallery Initiative

Wo [![Ìwé-àṣẹ](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) fún àwọn òfin kíkún.

---

## 💬 Àwọn Ẹ̀tọ́

![Àtúntò](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Ààbò](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Pẹpẹ](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![Ìwé-àṣẹ](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**A ṣe ìgbòòrò iṣẹ́ yìí nípa ìgbàlódé [Ilhan Art Gallery], àwọn kóòdù orísun rẹ̀ sì wà ní gbangba fún ìhàn kedere.**

**ÌLÀNÀ V1.0 // TÍ A FI ÈDÌDÌ SHA-512 SÍ**

*© 2026 İLHAN ART | GBOGBO ẸTỌ́ NÍ ÌPAMỌ́ FÚN ÀW ỌN IṢẸ́ ỌNÀ, ÀWÒRÁN ÀTI ÈRÒ.*

---
