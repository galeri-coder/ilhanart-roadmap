# 📚 KAMUSI YA ISTILAHI NA DHANA
> **"Kuelewa lugha ya itifaki hii, ni kuelewa dira yake."**

## ⚙️ Injini ya Uchunguzi wa Kisayansi ya PoArt (PFE) v1.0: Miundombinu ya Msingi

**Injini ya Uchunguzi wa Kisayansi ya PoArt (PFE)**, ni safu kuu inayowakilisha mantiki ya msingi na utendaji wa kiufundi unaosimamia itifaki ya [PoArt]. Hii ndiyo "injini ya kisayansi" inayochukua data ghafi ya uzalishaji wa kazi ya sanaa na kuibadilisha kuwa **ushahidi wa kidijitali unaoweza kuthibitishwa na usioweza kubadilishwa**.

### 🧩 Kwa Nini "PoArt Forensic"?

- **PoArt (Uthibitisho wa Sanaa):** Lengo la injini ni kuunganisha thamani ya mali ya kidijitali si kwa ubashiri; bali kwa **mchakato wa uzalishaji unaoweza kuthibitishwa**.
- **Forensic (Uthibitisho wa Kisheria):**
  - **Ufafanuzi wa Kiufundi:** Mbinu ya algorithm na mnyororo wa kumbukumbu inayolenga kuthibitisha kuwa data zinazohusiana na mchakato wa uzalishaji (mistari ya brashi, timelapse, logs) hazijadadilishwa.
  - **Safu ya Kifalsafa:** Dhidi ya uzalishaji wa "matokeo ya papo hapo" wa AI; dai la kubadilisha uzalishaji wa binadamu unaohusisha **muda, jitihada na gharama ya uamuzi** kuwa ukweli unaoweza kupimwa.

> Kumbuka: Ujumuishaji wa blockchain (mfano Solana) sio msingi wa PFE; utafafanuliwa kando kama **Safu ya Nanga ya Mnyororo (Chain Anchor Layer)** kwa uthibitisho/usajili.

### 🛠️ Upeo wa Kiufundi wa v1.0

**Injini ya Uchunguzi wa Kisayansi ya PoArt (PFE) v1.0** imejengwa juu ya **nguzo 3 kuu** hizi badala ya mifano ngumu ya kifedha:

1. **Hashing & Sealing (Kutia Muhuri):**  
   PFE inachakata vipengele vyote ndani ya Furushi ya Ushahidi (faili la kazi, video, JSON/log, saini n.k.) kwa namna ya kimakadirio na kuzalisha thamani ya kipekee ya **NotarySeal**.

   **Dhana za msingi (v1.0):**
   - **FileHash (alama ya kidole ya kazi):** Hash iliyozalishwa kutoka kwa bytes za faili la kazi.
   - **EvidenceRoot (mzizi wa furushi ya ushahidi):** Muhtasari wa mzizi unawakilisha uthabiti wa Furushi ya Ushahidi (Merkle root au canonical manifest hash).
   - **NotarySeal (muhuri wa mwisho / Matokeo ya PFE):** Muhuri wa mwisho uliozalishwa kutoka kwa muunganiko wa EvidenceRoot + muda + saini.

   **Fomula (wazi kwa wawekezaji):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Ufafanuzi wa Canonical Payload (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Kumbuka: Thamani inayokusudiana kama matokeo ya PFE ni **NotarySeal**. Utaratibu wa **SignerSignature** utawashwa katika Awamu ya 2 (na Solana Wallet Adapter); katika v1.0 ya sasa, saini ya uthibitisho wa mfumo inatumika. Ufunguo wa umma wa uthibitisho unachapishwa katika usajili kwenye sehemu ya `issuer.attestation_pubkey`.

2. **Indexing (Uhifadhi):**  
   Inasajili kwa safu inayoweza kufuatiliwa na kuulizwa ni pochi gani, tarehe gani, kwa kazi gani imetoa **Uthibitisho wa Kazi (Labor Proof)**.  
   *(Safu hii inaweza kuwa hifadhidata; ujumuishaji wa mnyororo unafafanuliwa kando kama "Safu ya Nanga ya Mnyororo".)*

3. **Verification (Uthibitisho):**  
   Uhalisi wa kazi unapohojiwa, PFE inachakata upya ushahidi ghafi; inajaribu kwa uhakika wa kihesabu kama thamani zilizokokotolewa za **EvidenceRoot / NotarySeal** zinaendana na kumbukumbu zilizo kwenye kumbukumbu.

---

### 🧮 Nadharia ya Thamani ya PoArt (The Value Theorem)

Itifaki ya [PoArt] inaunganisha thamani ya mali ya kidijitali ($V$) si kwa mtazamo wa kibinadamu wa soko; bali kwa **ukweli wa kimwili wa mchakato wa uzalishaji**.

Akili Bandia (AI) inaharibu mchakato kwa kutoa matokeo mara moja ($t \to 0$). [PoArt] inachukulia thamani kama ukusanyaji wa vipengele vya **muda, jitihada na nia**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Ufafanuzi wa Vigeuzi

- **$\int dt$ (Ukusanyaji wa Mchakato):**  
  Thamani si "matokeo" ya papo hapo; ni **mchakato** unaokusanywa kati ya $t_{\text{start}}$ na $t_{\text{end}}$. Kadri muda unavyopungua (uzalishaji wa AI), matokeo ya integral yanakaribia sifuri.

- **$P_{\text{labor}}(t)$ (Nguvu ya Kazi ya Papo Hapo):**  
  Inawakilisha msukumo wa jitihada za kiakili na kimwili zinazotumiwa wakati wa uzalishaji. Kadri jitihada inayoweza kuthibitishwa inavyoongezeka, integrand inakua.  
  > Kumbuka: Neno hili linaweza kusawazishwa kimtindo kwa kupitia "ishara za kazi zinazoweza kupimwa/kuthibitishwa".

- **$I_{\text{agency}}(t)$ (Mgawo wa Nia):**  
  Uwezo wa mzalishaji wa kuchukua hatari na kufanya maamuzi. Inachukua thamani kati ya $0$ na $1$.
  - **AI ($I \approx 0$):** Inatekeleza maagizo, haichukui hatari, halipi gharama.
  - **Binadamu ($I \to 1$):** Inabadilisha maamuzi, inasita, inachukua hatari.

- **$U_{\text{irreversible}}$ (Kipekee Kisichoweza Kurudishwa):**  
  Katika uzalishaji wa kidijitali kurudi nyuma (`Ctrl+Z`) kunawezekana; katika uzalishaji wa kimwili (rangi iliyopakwa kwenye turuba, jiwe lililochongwa, tabia katika onyesho burudani) hakuna kurudi. **Kutoweza kurudishwa** huku ni neno la ziada linalozalisha "kipekee" (sifa ya non-fungible) katika kazi.

### 🔎 Uchambuzi wa Kesi: AI "Matokeo ya Papo Hapo" dhidi ya Binadamu "Mchakato Uliothibitishwa"

Hali ifuatayo inaonyesha jinsi **Nadharia ya Thamani ya PoArt** inavyofanya kazi kimtindo na kwa nini uzalishaji wa AI unapata alama chini katika kiwango cha [PoArt].

#### Hali A: Uzalishaji wa Picha kwa AI kwa Sekunde 10

- **Muda ($\Delta t$):** Sekunde $10$ (mchakato karibu sifuri)
- **Nguvu ya Kazi ($P_{\text{labor}}$):** Kitengo $1$ (kuandika amri tu)
- **Mgawo wa Nia ($I_{\text{agency}}$):** $0.01$ (hakuna hatari, hakuna gharama)
- **Kutoweza Kurudishwa ($U_{\text{irreversible}}$):** $0$ (inaweza kurudishwa / kunakiliwa)

**Matokeo:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Tafsiri:** Hata kama matokeo ni kamili; kwa sababu mchakato haukupitwa na haujabinadimu hatari/nia, thamani ya [PoArt] inakaribia sifuri.

#### Hali B: Uzalishaji wa Kimwili wa Saa 6 Kwenye Onyesho Burudani

- **Muda ($\Delta t$):** Saa $6$ (sekunde $21{,}600$)
- **Nguvu ya Kazi ($P_{\text{labor}}$):** Kitengo $0.5$ (uendelevu wa jitihada za kimwili na kiakili)
- **Mgawo wa Nia ($I_{\text{agency}}$):** $0.9$ (kubadilisha maamuzi, kuchukua hatari, chaguzi zisizoweza kurudishwa)
- **Kutoweza Kurudishwa ($U_{\text{irreversible}}$):** $>0$ (alama za kimwili haziwezi kurudishwa)

**Matokeo:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Tafsiri:** Kadri mchakato unavyoongezeka na nia (hatari) inavyoongezeka, thamani inaongezeka kwa ukusanyaji. Neno la $U_{\text{irreversible}}$ ni mchango wa ziada unaozalisha "kipekee" (sifa ya non-fungible) katika kazi.

---

### ✅ Hitimisho: Kufungwa kwa Thamani kwa Uthibitisho (Proof-Bound Value)

Nadharia hii inatoa dai la thamani ya [PoArt] kutoka kwa "kupendwa" au "hadithi ya soko" na kuiunganisha na **ukweli wa uzalishaji unaoweza kuthibitishwa**.

1. **Bila Mchakato Hakuna Thamani:**  
   AI inaharibu mchakato katika matokeo ya papo hapo ($t \to 0$). Kadri dirisha la mchakato linavyopungua, matokeo ya integral yanapungua kwa lazima la kihesabu:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Nia na Hatari ni Kuzidisha:**  
   [PoArt] haipimi tu "muda uliotumika"; bali pia safu halisi ya uamuzi, hatari na gharama katika muda huo. Thamani ya uzalishaji usiochukua hatari (AI) ni chini:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Kipekee si Masoko bali Uthibitisho wa Kimwili:**  
   Alama zisizoweza kurudishwa katika uzalishaji wa kimwili (mapigo ya turuba, kuvunjika kwa marumaru), ziko nje ya mantiki ya `Ctrl+Z` ya kidijitali. **Kutoweza kurudishwa** huku ($U_{\text{irreversible}}$), kinazalisha kazi kuwa kipekee kiontolojia.

> **🔐 MUHTASARI:** Ingawa nadharia ya thamani inaonekana kutokuwa wazi kama kipimo (hata kama katika maisha halisi sawa kabisa ya 100% haiwezi kupimwa kikamilifu) lengo la fomula hii ni kuonyesha muundo na mwelekeo wa vigeuzi. Kitu kigumu katika enzi ya AI si "picha"; bali **kazi, muda na nia zinazoweza kuthibitishwa.** [PoArt] inapima uhaba huu na kuuthibitisha na **Furushi ya Ushahidi**.

### 🏛️ Umuhimu wa Dhana ya "Injini" (Engine)

Ishara zinazotoka kwa mifumo kama Pump.fun, mara nyingi ni **"tikiti ya upatikanaji"** tu. **Injini ya Uchunguzi wa Kisayansi ya PoArt (PFE)** ndiyo **safu ya mantiki ya kikatiba** inayoamua ni haki gani tikiti hiyo inalinda, jinsi kazi inavyorekodiwa na jinsi sanaa/sayansi/teknolojia inavyoweza kudumu.

> **Kumbuka:** Sababu ya kuanzisha mradi huu kwenye Pump.fun ni kwa sababu hatukuwa na ukwasi wa kutosha na idadi ya wafuasi. Kutumia data iliyopo kilikuwa kimkakati si ubora bora zaidi lakini tunaweza kusema ilikuwa hatua sahihi. Kufafanua mantiki ya injini hii kwenye GitHub, bila kujitegemea kwa bajeti na rasilimali, inathibitisha kuwa mradi si ubashiri wa kifedha tu, bali maono ya muda mrefu ya **miundombinu ya programu** na **maktaba ya kitaifa ya kidijitali**.

---

## 🎨 ITIFAKI YA UTHIBITISHO WA KAZI YA [PoArt] (Proof of Art Protocol v1.0)

> **"Msanii Halisi, Uzalishaji Halisi, Thamani Halisi."**

Itifaki hii; ni **utaratibu wa ulinzi wa kibiolojia na kiakili** uliotengenezwa dhidi ya wadanganyifu wasio na utambulisho wanaozunguka ikolojia ya crypto, picha za akili bandia zinazozalishwa kwa dakika 5 na utamaduni wa "Pump & Dump" (Pumba na Tupa).

---

## a) [PoArt] ni Nini? (Ufafanuzi wa Kifalsafa na Kiufundi)

**Uthibitisho wa Sanaa [PoArt];** ni kiwango cha uthibitisho cha kitaasisi kinachohakikisha kuwa thamani nyuma ya mali kwenye blockchain inategemea **kazi ya binadamu** inayoweza kuthibitishwa, **muda** na **nishati ya kimwili**, si ubashiri.

Kama Bitcoin inavyozalisha thamani kwa *"Umeme na Nguvu ya Processor"* **(Uthibitisho wa Kazi)**; miradi inayoendana na [PoArt] pia inazalisha thamani kwa *"Kipawa na Muda wa Binadamu Uliotumika"*. Wana "Stake" muda.

Inaondoa hatari ya *"Msanidi Programu (Dev) aliuza, mradi umekwisha"* kwenye mifumo ya Pump.fun na DEX; kwa sababu hapa thamani haiko kwenye msimbo, iko katika **uendelevu wa uzalishaji**.

> **[PoArt] haimwambii mshiriki "Tuamini sisi"; inasema "Huu ni ushahidi, ona kwa macho yako, thibitisha kwa hisabati yako."**

---

## b) Kiwango cha Nguzo 5 cha [PoArt] (Nguzo 5 za Ukweli)

Vipengele hivi 5 ni vichujio visivyoweza kudanganywa ambavyo mradi lazima upite ili kupata muhuri wa [PoArt].

### 1) Uthibitisho wa Utambulisho Burudani (Live Identity Proof)

- **Tatizo:** Dunia ya crypto imejaa waanzilishi wasio na utambulisho (Dev) wanaokusanya pesa na kuiacha miradi.
- **Suluhisho la [PoArt]:** Mzalishaji anathibitisha si kitambulisho tu, bali **uwepo wake wakati wa uzalishaji**. Hii inajumuisha vikao vya onyesho burudani ambapo anawasiliana na jamii na maombi maalum ya papo hapo yanatekelezwa, si video zilizorekodiwa mapema.  
  (Mfano: *"Andika tarehe ya leo na nambari ya block ya sasa kwenye kona ya kulia ya turuba"*)
- **Kauli:** *"Boti zinaweza kupiga picha lakini boti hazitoi jasho na hazifanyi improvisation."*

### 2) Uthibitisho wa Kazi na Mchakato (Labor & Process Proof)

- **Tatizo:** Picha za AI (Akili Bandia) zinazozalishwa kwa sekunde 2 na mchoraji wa mafuta uliofanywa kwa miezi 2 zinachukuliwa kama "jpeg" sawa katika dunia ya kidijitali.
- **Suluhisho la [PoArt]:** Mchakato wa "ujauzito na kuzaliwa" wa kazi unaandikwa. Hatua za sketch, safu za rangi, masaa ya jumla yaliyotumika na mchakato wa kimwili ambao msanii aliupitia wakati wa kuumba kazi hiyo unarekodiwa. Hii inaongeza **"Gharama ya Muda" (Time Cost)** kwa ishara. Kadri uzalishaji wa mali unavyokuwa mgumu, thamani yake inakuwa imara.

### 3) Uthibitisho wa Thamani ya Urembo (Aesthetic Value Proof)

- **Tatizo:** Utamaduni wa "Meme" unaopuuza urembo na kina cha kisanaa na kuzingatia tu ucheshi wa papo hapo na matokeo yake miradi mifupi ya "Hype".
- **Suluhisho la [PoArt]:** Mradi lazima uwe na viwango vya sanaa vya kitaaluma, nadharia ya rangi, kanuni za muundo na ujuzi wa nyenzo (Impasto, Texture nk.). Maudhui hayapaswi kuchekesha tu; yanapaswa kuzalisha mshangao kwa mtazamaji na kuwa na **thamani ya mkusanyiko**.

### 4) Ubunifu wa Kiakili (Conceptual Novelty)

- **Tatizo:** Maelfu ya sarafu za mbwa/paka ambazo ni nakala za kila mmoja, zisizo na ubunifu.
- **Suluhisho la [PoArt]:** Mradi lazima ujenga daraja jipya linalounganisha sanaa, sayansi, falsafa au teknolojia katika muundo wenye maana.  
  (Mfano: Kuunganisha sanamu ya kawaida ya Daudi na data ya soko la crypto; kuchakata wazo la "kuwa jiwe" la mtazamo wa binadamu kupitia hii na kuiweka msingi kwa vyanzo vya kisayansi.)  
  Kazi haipaswi kuwa karamu ya kuona tu; bali pia lazima iwe **changamoto ya kiakili** inayowafanya watu wafikiri juu ya **Sayansi, Falsafa au Teknolojia**.

> [!IMPORTANT]
> **Mfano wa Kumbukumbu (Athari ya Las Palmitas):**  
> Katika mtaa wa Las Palmitas nchini Mexico unaopambana na uhalifu, zaidi ya nyumba 200 zilibadilishwa kuwa karamu kubwa ya upinde wa mvua. Kama matokeo ya uingiliaji huu wa urembo, viwango vya uhalifu katika mtaa vilipungua kwa kiasi fulani, vijana walianza kuvutiwa na sanaa badala ya makundi. Mabadiliko ya urembo yalibadilisha upya heshima ya watu kwa mazingira yao na kwa kila mmoja (Muungano wa Kijamii).
>
> **Matarajio:** Mradi utakaoingia kwenye orodha ya [PoArt]; kama mfano hapo juu, lazima uwe na uhusiano wa sababu-matokeo wa kijamii, kisayansi au kifalsafa, zaidi ya urembo wa kuona tu. Kwa kuwa mali pekee isiyoweza kununuliwa kwa pesa ni "Muda", katika itifaki hii muda lazima u-stake kama dhamana na kuthibitishwa. Msingi wa kiakili wa mradi lazima uwe imara na wa kimataifa kiasi kwamba; miaka baadaye hata katika hali ya CTO (Uchukuaji wa Jamii), jamii inaweza kurithi urithi huu na kuendelea uwezo wa ubunifu wa mradi kwa njia ya kujitegemea.

### 5) Nia Isiyo ya Algorithmic (Non-Algorithmic Agency)

- **Tatizo:** Uzalishaji wa kidijitali kamili lakini usio na roho, unarudia.
- **Suluhisho la [PoArt]:** Nia ya kipekee ya binadamu inayoweza kukosea, kuchukua hatari na kupitia mabadiliko ya kihisia lazima ihisiwe katika kazi. Kutokuwa na uhakika katika mapigo ya brashi, majibu yasiyo ya matarajio ya nyenzo na maamuzi ya papo hapo ya msanii, ni **Saini ya Kibiolojia** inayotofautisha kazi kutoka "Uzalishaji wa Mashine".

---

## c) Utaratibu wa Uthibitisho na Kupinga Ulaghai

Mfumo huu unahakikisha kuwa mradi unabaki wa kuaminika na hai si tu "mwanzoni" bali "milele".

### 📦 Furushi ya Ushahidi (Evidence Pack - The Digital Twin)

Nyuma ya kila kazi iliyothibitishwa na [PoArt], kuna furushi ya data iliyosimbwa na yenye muhuri wa muda ambayo wawekezaji wanaweza kupakua:

- **Rekodi za Video za RAW:** Picha ghafi zisizovunjika za wakati wa uzalishaji.
- **Uchambuzi wa Metadata:** Tarehe ya kuundwa kwa faili, taarifa za kifaa kilichotumiwa na data za eneo (Jiji-Nchi).
- **Marejeleo ya Kimwili:** Ushahidi kuwa kazi ipo ulimwenguni wa kimwili  
  (Mfano: Gazeti la sasa au data ya blockchain ya wakati huo karibu na kazi).

> *Kumbukumbu ya uthabiti:* Neno "furushi ya ushahidi" linaunganishwa na mstari wa **Evidence Pack → EvidenceRoot → NotarySeal** katika sehemu za awali; yaani uthabiti wa furushi unawakilishwa kwa muhuri unaoweza kuthibitishwa.

### 🔄 Upyaji wa Siku 365 (Itifaki ya Uendelevu)

- **Kipengele cha Mapinduzi:** Katika miradi ya crypto "Dev" (Msanidi Programu), hutoa ishara sokoni na kwa kawaida hutoweka baada ya miezi 1-2 (Soft Rug). [PoArt] inafanya hili liwe haliwezekani.
- **Sheria:** Hadhi ya "Msanii Aliyethibitishwa" (Verified Artist) si ya maisha yote. Ni halali kwa **mwaka 1** tu.
- **Utendaji:** Msanii/Msanidi Programu, kila siku 365, lazima atoe **kazi mpya, kubwa na inayoweza kuthibitishwa** kwa jamii.
- **Hali ya Mfano:** Ulianzisha mradi mnamo 2026. Mnamo Januari 2027 mfumo unatoa onyo "Muda wa Uthibitisho Umeisha". Ikiwa msanii hatoi maonyesho mapya, kazi mpya ya kimwili au ujumuishaji mpya wa teknolojia, "Badge ya Kuamini" ya mradi inashuka.
- **Matokeo:** Mfumo huu unahakikisha kuwa **maudhui hayawezi kamwe kupoteza umuhimu** na mwekezaji hasumbuliwi na hofu ya *"Je Msanidi Programu bado yuko hapa?"*. Mradi unabadilika kuwa studio inayoishi.

### 🚩 Itifaki ya Bendera Nyekundu (Red Flag Protocol)

**Katika hali yoyote ya ulaghai uliog undulika na jamii au algorithms (matumizi ya AI, kazi iliyoibiwa, video iliyodadilishwa):**

1. Cheti linawekewa alama mara moja kama **"BATILI" (VOID)**.
2. Furushi za ushahidi zinawekewa lebo hadharani kama **"Bandia"**.
3. Mradi unawekwa kwenye orodha nyeusi ya [PoArt]. Hii inaimarisha ukweli kwamba katika dunia isiyokuwa na kituo **sifa ni sarafu pekee**.
4. Katika uchapishaji wowote haiwezi kutumika misemo ya [PoArt], chanzo halali pekee ni https://www.ilhanart.org/public-registry

---

## d) Hitimisho: Si Kasino, bali Makumbusho

**Pump.fun na Masoko Yasiyo na Kituo (DEX) kwa sasa ni kasino tu; taa zinawaka na kuzima, kila mtu anatafuta faida ya haraka na mfuko (wadanganyifu) daima anashinda. Sababu ya kuanzisha mradi hapa pia ni jitihada yetu ya kuboresha mahali hapa na kutokana na data yetu iliyopo na mazingira yetu ya kufikia hadhira iliyopo kupitia onyesho burudani.**

**[PoArt] ni ngome iliyojengwa katikati ya kasino hii.**

- 🎰 Kasino inategemea michezo ya karatasi; sisi tunategemea **ukweli wa kimwili**.
- 🃏 Kasino imewazi kwa udanganyifu; sisi tupo wazi kwa **ushahidi ulio wazi**.
- ⏳ Kasino ni ya muda; sisi tunazingatia **milele ya sanaa na sayansi**.

**Ishara inayotumia itifaki hii si "coin" tu; ni hisa ya kidijitali yenye jasho, rangi, msimbo na falsafa nyuma yake.**

---

## 🗳️ 6) UTAWALA NA USAJILI WA UMMA (Governance & Public Registry)

**Lengo la sehemu hii ni: Kutoa kiwango cha [PoArt] kutoka ngazi ya "kuamini watu" na kuibadilisha kuwa miundombinu ya umma endelevu kwa kusajili + kuthibitisha + ufuatiliaji wa jamii.**

### 6.1 Usajili wa Umma (Public Registry)

- **Usajili wa Umma:** Data zote zilizosidir zinaandikwa kwenye `ilhanart.org/registry` (au GitHub Registry).

**Mantiki ya usajili (kiwango kinachopendekezwa - muundo wa njia ya JSON):**

Kila rekodi inayoingia kwenye usajili inabeba angalau sehemu hizi za msingi zinazoweza kuthibitishwa:

- **Utambulisho & Hadhi:**
  - `certificate_id` (rejea inayosomeka)
  - `status` (active / void)
  - `void_reason` (ikiwa ipo)
  - `visibility` (private / masked / public)
  - `created_at` (muhuri wa muda)

- **Taasisi Inayotoa:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Taarifa za Kazi:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (ikiwezekana; kwa utambulisho wa mmiliki wa ishara)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Data za Kisheria:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Ushahidi wa Cryptographic:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Utawala:**
  - `governance.decision`
  - `governance.review_notes`

Usajili unaweza kuwa na safu mbili:
- **1)** Fahrasa inayosomwa na binadamu (orodhesha/tafuta/chuja wavuti)
- **2)** Manifest inayosomwa na mashine (rekodi za JSON; kwa uthibitisho wa PFE)

**"Usajili" hapa unaweza kuthibitishwa na mnyororo wa Evidence Pack → EvidenceRoot → NotarySeal wa PFE. Usajili unatoa lengo la uthibitisho, si dai.**

---

### 6.2 Mchakato wa Maombi ya PoArt Verified

**Maombi ya PoArt Verified yanatathminiwa na İlhan Art Gallery kulingana na viwango 5 vya PoArt. Maoni ya jamii yanazingatiwa, lakini uamuzi wa mwisho unategemea timu ya curate. Maamuzi yanafafanuliwa kwa uwazi na kuandikwa kwenye ilhanart.org/registry.**

#### Mchakato wa Maombi

**Ombi:**
- Msanii/mradi anatuma ombi la PoArt Verified
- Furushi ya Ushahidi inatengenezwa (rekodi za video, metadata, viungo vya onyesho burudani)
- Ombi linatumwa kwa İlhan Art Gallery

**Ukaguzi (Siku 30):**
- Timu ya galeri inachunguza kwa undani Furushi ya Ushahidi
- Viwango vyote 5 vya PoArt vinakaguliwa:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Mazungumzo na msanii (ya hiari)

**Ushauri wa Jamii:**
- Furushi ya Ushahidi inashirikiwa hadharani wakati wa mchakato wa maombi
- Jamii inaweza kutoa maoni kupitia ilhanart.org
- Wamiliki wa ishara (chini ya 10,000 $CULTURE) wanaweza kutoa mapendekezo hasa
- **Maoni yote yanazingatiwa katika mchakato wa ukaguzi**
- **Lakini uamuzi wa mwisho unategemea tathmini ya curate**

**Uamuzi:**
- Galeri inaidhinisha au kukataa ombi
- Sababu ya uamuzi inafafanuliwa kwa uwazi
- Ikiwa imeidhinishwa → badge ya PoArt Verified
- Ikiwa imekataliwa → Ombi jipya linaweza kufanywa baada ya miezi 6

**Uwazi:**
- Maombi yote na maamuzi yanaandikwa kwenye ilhanart.org/registry
- Rekodi ya uamuzi inachapishwa hadharani:
  - Tarehe ya ombi
  - Muhtasari wa mchakato wa ukaguzi
  - Uamuzi (Umeidhinishwa / Umekataliwa)
  - Sababu ya uamuzi (ufafanuzi mfupi)
  - Muhtasari wa maoni ya jamii (bila jina)

#### Kwa Nini Uamuzi wa Curate?

**Udhibiti wa Ubora:**  
Hadhi ya PoArt Verified ni badge yenye viwango vya juu. Tathmini ya curate inahakikisha kuwa viwango hivi vinalindwa.

**Kuzuia Udadisi wa Ubashiri:**  
Utawala kamili juu ya mnyororo (mfano: Realms, kura za DAO) na ishara za Pump.fun haiwezekani kiufundi. Mifumo ya kura ya nje ya mnyororo pia iko katika hatari ya udadisi wa whale na mashambulio yanayoratibiwa. Uamuzi wa curate unaondoa hatari hii.

**Ufanisi wa Uendeshaji:**  
Badala ya taratibu ngumu za kura, mchakato wa uamuzi wa haraka na wazi. Wasanii wanapata matokeo ndani ya siku 30.

**Ushiriki wa Jamii:**  
Maoni ya jamii yanazingatiwa kikamilifu na kuathiri mchakato wa uamuzi. Lakini uamuzi wa mwisho unategemea timu ya curate iliyolindwa kutoka udadisi.

**Baadaye:**  
Mradi ukikomaa (2027+), utaratibu wa ushauri wa jamii unaweza kuimarishwa. Lakini ulinzi wa kiwango cha curate ni wa kudumu.

---

### 6.3 Matumizi ya Ishara (Token Utility)

**Faida zinazotolewa kwa wamiliki wa ishara ya $CULTURE:**

**1. Upatikanaji wa Kipaumbele kwa Matukio ya Galeri:**
- Haki ya kufanya maonyesho ya wiki 1 kwa mwaka kwenye İlhan Art Gallery (haki inaweza kuhamishwa)
- Punguzo la Drop painting
- Haki ya punguzo la 10% hadi 30% kwenye picha kwenye galeri

**2. Upatikanaji Kamili wa PoArt Registry:**
- Rekodi za kina za kazi zote za sanaa zilizothibitishwa
- Matoleo kamili ya Furushi za Ushahidi
- Zana za uthibitisho wa kisheria

**3. Kura ya Ushauri:**
- Haki ya ushauri katika maombi ya PoArt Verified
- Upatikanaji wa njia za maoni ya jamii
- Ushiriki katika majadiliano ya utawala

**4. Maudhui ya Kipekee:**
- Maudhui ya nyuma ya pazia ya studio
- Mahojiano ya msanii na video za mchakato
- Upatikanaji wa nyaraka za kiufundi

**Kumbuka:**  
Wamiliki wa ishara wanatoa kura ya ushauri (advisory vote). Uamuzi wa mwisho ni wa timu ya curate. Muundo huu umependelewa ili kuzuia udadisi wa whale na mashambulizi ya ubashiri. Hakuna tuzo za staking kwa sababu tunafuta washiriki wa kitamaduni wa muda mrefu, si mtaji wa askari wa muda mfupi.

---

### 6.4 Usawazishaji wa Metadata (Metadata Sync)

- **Usawazishaji wa Metadata:** Data za kiufundi kwenye usajili lazima ziendane 100% na mali ya kimwili.

**Kufafanua kiufundi "uendano wa 100%" (uwazi unaop

endekezwa):**

- **Uendano wa chini (lazima):**
  - `asset.fingerprints.sha256/sha512` kwenye usajili na hash ya faili lililopo lazima ziwe **sawa kabisa**.
  - `proof.notary_seal` kwenye usajili inapozalishwa upya (ikiwa Furushi ya Ushahidi ipo) lazima iwe **sawa kabisa**.

- **Uendano wa rejea ya kimwili (aina ya ushahidi):**
  - Ushahidi kama kazi ya kimwili iliyoonyeshwa kwenye onyesho burudani + rejea ya tarehe/block lazima iendane na Furushi ya Ushahidi.

- **Uendano wa faragha:**
  - Sehemu kama IP/eneo katika kuonekana kwa `masked` lazima zichapishwe **kulingana na kiwango cha kufunika**.

---

### 6.5 Pingamizi, Ukaguzi na Kufutwa (Dispute & Revocation)

Usajili si utaratibu wa "idhini" tu; ni **utaratibu wa ufuatiliaji hai dhidi ya ulaghai**.

- Pingamizi linapoanzishwa, rekodi inaweza kuchukua hali ya **"ukaguzi"**.
- Ulaghai ukigunduliwa, unawekwa alama kama `status: void` na sababu inaongezwa:
  - `void_reason` (matumizi ya AI / wizi / udadisi n.k.)
  - `revoked_at` (muda wa kufutwa)
- Chanzo cha uamuzi wa kufutwa kinaonekana wazi kwenye usajili:
  - ukaguzi wa curate / pingamizi la jamii / kumbukumbu ya uchambuzi wa kisheria (chochote kinachotumika)

> **Sehemu hii ni sawa na dhana ya VOID kwenye usajili kutoka sehemu ya "Itifaki ya Bendera Nyekundu".**

---

### 6.6 Mfano wa Rekodi ya Usajili (Inayosomwa na Mashine)
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

> *Kumbuka: `asset.fingerprints.sha512` na thamani zingine za hash zimefupishwa kwa madhumuni ya uwasilishaji; katika utekelezaji halisi, mfuatano kamili wa herufi za hexadecimal unatumika.*

---

## 7) 🔐 MUHURI WA KIUFUNDI (NOTARY SEAL)

**Algorithm ya muhuri usiotikisika iliyozalishwa na Injini ya Uchunguzi wa Kisayansi ya PoArt (PFE) v1.0:**

# Itifaki ya [PoArt] ya Notari ya Kidijitali & Ushahidi wa Kisheria (Beta v1.0)

> **"Utamaduni ni mkubwa kuliko mtaji. Linda kazi zako leo, zipitishe kesho."**

---

## Kwa Nini Hadharani?

Usalama halisi unatoka kwa uwazi. Kwa sababu ya mfumo wetu wa **Usajili wa Umma (Public Registry)**, mtu yeyote duniani kote anaweza; kuthibitisha kama faili lililopo mkononi mwake ni asili, ndani ya sekunde, bila kuhitaji mamlaka yoyote.

---

## 🧩 Kwa Nini Kuna "Moduli Nyingi za Kuonekana"?

Hii ndiyo sehemu muhimu zaidi ya msimbo (menyu ya kuchagua visibility). Chaguo hizi huruhusu watumiaji kuweka usawa wa **"Faragha dhidi ya Uwazi"**:

### 🔒 Binafsi (Private)

- **Hali:** Msanii bado hataki kuchapisha kazi lakini anataka kuweka muhuri wa tarehe na kuthibitisha "nilifanya hii tarehe hii".
- **Msimbo Unafanya Nini:** Unaandika data kwenye hifadhidata lakini unaweka lebo ya `visibility: "private"`. Baadaye wakati wa kuandika sera ya "Kusoma kwa Umma" unaweza kwa kusema `WHERE visibility = 'public'` kuficha rekodi hizi kutoka kwa umma.

### 🕶️ Iliyofunikwa (Masked)

- **Hali:** Msanii anataka uwazi lakini anaogopa anwani ya nyumbani (eneo la IP) kugunduliwa.
- **Msimbo Unafanya Nini:** Kazi za `maskIP` na `maskLoc` zinafanya kazi upande wa JavaScript. Inabadilisha anwani ya IP kuwa muundo wa `88.241.***.***`, eneo kuwa muundo wa `***/TR` na inatuma toleo lililosenswa kwenye hifadhidata.
- **Kumbukumbu ya Faragha:** Kufunika kunafanywa kwenye kivinjari, Supabase haioni eneo halisi. **Lakini:** Ikiwa API za watu wengine kama ipapi.co zinatumika kwa data za eneo, watoaji hawa huona anwani ya IP wakati wa ombi.
- **Kuweka Muhuri katika Hali ya Masked:** Hesabu ya EvidenceRoot na NotarySeal inafanywa kwa data ya forensics iliyofunikwa; kwa hivyo uthibitisho unabaki deterministic.

### 🌍 Hadharani (Public)

- **Hali:** Uwazi kamili. Kulingana na kiwango cha [PoArt], eneo, wakati na mtandao ambao kazi ilizalishwa hutangazwa wazi.

---

## 💡 Ubunifu wa Teknolojia

PoArt si mfumo wa kupakia faili tu. Ni injini ya **"Mnyororo wa Ulinzi wa Ushahidi wa Kisheria" (Forensic Chain of Custody)** inayoyeyusha safu tatu tofauti za teknolojia katika sufuria moja na kuleta kiwango kipya.

**Safu inayoelezwa katika sehemu hii kama "injini" inaendana na kiini cha Injini ya Uchunguzi wa Kisayansi ya PoArt (PFE) katika istilahi ya awali.**

### 1) Hashing ya Upande wa Mteja (Client-Side Hashing) - Faragha ya Juu Zaidi

Faili za kazi zako hazipakiwi kwenye seva kamwe. Injini yetu inayofanya kazi kwenye kivinjari (Client-side), inahesabu hash (muhtasari wa kidijitali) wa faili kwenye kompyuta yako mwenyewe. Alama hii ya kidole na metadata tu ndizo zinatumwa kwenye seva.

> **Kumbukumbu ya Faragha:** Faili la kazi halipakiwi kwenye seva na kwa hivyo linalindwa. Hata hivyo, data za forensics (IP/eneo) zinashirikiwa kulingana na hali ya kuonekana iliyochaguliwa (private/masked/public).

### 2) Kuchanganya Data za Kisheria (Forensic Data Fusion) - Nguvu ya Kisheria

Ni zaidi ya muhuri wa muda wa kawaida (Timestamp). Mfumo unachanganya data hizi kwenye "Muhuri wa Genesis" mmoja:

- **Muhtasari wa Kidijitali (SHA-512):** Alama ya kidole ya kidijitali kwa kutumia kiwango cha muhtasari wa cryptographic (SHA-512) ambayo itavunjika hata kama pikseli moja ya kazi ikibadilika.
- **Eneo na Muda:** Tarehe yenye usahihi wa millisecond, nchi, jiji na data ya wilaya ambapo operesheni ilifanywa.
- **Utambulisho wa Kifaa:** Mfumo wa uendeshaji, kivinjari na aina ya kifaa (uchambuzi wa User-Agent).

---

## 🛡️ Matumizi na Faida

Ikiwa wewe ni msanii, mwandishi au msanifu, kusema tu "Nilifanya hii awali" haitoshi, lazima uthibitishe.

**Kazi uliyoweka muhuri na PoArt:**

- **Uthibitisho wa Kihesabu:** Hata kama pikseli moja ya faili lako ikibadilika, mfumo unafahamu. Udadisi hauwezekani.
- **Msingi wa Kisheria:** Imeandikwa kazi ilipowekwa muhuri tarehe gani, jiji gani, kutoka kifaa gani.
- **Cheti cha Papo Hapo:** Ndani ya sekunde inazalisha **"Cheti cha Utambulisho wa Mali"** maalum kwako, chenye msimbo wa QR na muhuri.

---

## ⚙️ Usanifu wa Mfumo na Sifa za Kiufundi

Mfumo umebuniwa juu ya usanifu wa "Serverless" (Bila Seva), ukizingatia utendaji wa juu na uwezo wa kupanuka.

| Safu | Teknolojia | Maelezo |
|------|-----------|---------|
| **Cryptography** | SHA-256 & SHA-512 | Muhtasari wa cryptographic wa safu mbili |
| **Hifadhidata** | Supabase (PostgreSQL) | Muundo wa data wa JSONB, sera za RLS |
| **Data za Kisheria** | ipapi.co API | Tatu za IP/Eneo/Muda |
| **Rendering** | html2canvas + jsPDF | Uzalishaji wa PNG/PDF upande wa mteja |
| **Frontend** | Vanilla JavaScript | Hakuna utegemezi wa mfumo |
| **Usalama** | Client-side hashing | Faili halijawahi kwenda kwenye seva |

### Sifa Zinazoonekana

| Sifa | Maelezo | Kwa Washindani? |
|------|---------|----------------|
| **UI ya Buruta & Acha** | Buruta faili na kuacha, onyesho la papo hapo | ❌ Katika wengi hayupo |
| **Utoaji wa Aina Nyingi** | PNG, JSON, PDF - kwa kibonyezo kimoja | ⚠️ Mdogo |
| **Onyesho la Wakati Halisi** | Onyesho la papo hapo la cheti | ❌ Hayupo |
| **Udhibiti wa Faragha** | Chaguo za Private/Masked/Public | ❌ Hayupo |
| **Hashing ya Upande wa Mteja** | Faili halijawahi kwenda kwenye seva | ✅ Katika wachache tu |
| **Metadata ya Kisheria** | IP, eneo, kifaa, muda - vyote pamoja | ❌ Vipande vipande |
| **Uthibitisho wa QR** | Msimbo wa QR wa uthibitisho wa papo hapo | ⚠️ Mdogo |
| **Ukomo wa Kiwango** | Ulinzi wa spam (RLS + Client) | ❌ Katika wengi hayupo |

---

## 🗺️ Ramani ya Njia: Baadaye ya "Bila Kuamini" (Trustless)

Toleo la sasa **(Beta v1.0)** limeboreshwa kutoa kasi ya juu, kiolesura rahisi na upatikanaji wa bure kwa mtumiaji wa mwisho. Hata hivyo, dira yetu ya mwisho ni kuhamia muundo ambao hata msimamizi wa hifadhidata (sisi) hawezi kuingilia.

### Awamu ya 1: Beta v1.0 (Sasa Iko Mtandaoni)

**Miundombinu:**
- Hifadhidata ya Cloud (Supabase)
- Usajili wa nje ya mnyororo (PostgreSQL + nakala rudufu ya IPFS)
- Uthibitisho wa galeri kwa kujiamini (kituo lakini wazi)

**Ishara:**
- Jukwaa: Pump.fun
- Ukwasi: Raydium (kiotomatiki)
- Utawala: Ushauri tu (ushauri wa jamii)

**Lengo:**
- Kasi, kuondoa vizuizi vya UX
- Kutoa usalama "bila msuguano"
- Kuunda jamii

**Matumizi ya Ishara (v1.0):**
- Upatikanaji wa kipaumbele kwa matukio ya galeri
- Kuangalia PoArt Registry
- Haki ya kura ya ushauri

---

### 🚀 Awamu ya 2: Mamlaka Isiyokuwa na Kituo (Decentralized Authority) (2026 Q2-Q4)

Awamu hii inashughulikia mpito kutoka muundo unaofanya kazi kabisa "Upande wa Mteja" wa mfumo, hadi muundo salama zaidi na usio na kituo.

| Sifa | Inaleta Nini? | Tech Stack | ETA |
|------|--------------|------------|-----|
| **Edge Function INSERT** | Kizuizi cha spam + usalama wa ufunguo wa API | Supabase Edge (Deno) | Q2 2026 |
| **Saini ya Pochi** | Utambulisho usio na kituo | Solana Wallet Adapter | Q2 2026 |
| **Nakala Rudufu ya IPFS/Arweave** | Uhifadhi usio na kituo | IPFS SDK + Pinata | Q3 2026 |
| **Utaratibu wa Kufutwa** | Kufutwa kwa cheti bandia | Usasishaji wa Mchoro wa DB | Q2 2026 |
| **Logi ya Ukaguzi** | Kumbukumbu ya ulizo wa kisheria | Jedwali la logi maalum | Q3 2026 |
| **OpenTimestamps** | Kunga kwenye Bitcoin | OTS JavaScript | Q4 2026 |

**Utawala wa Ishara (v2.0):**
- Kura ya nje ya mnyororo (x/web) + saini ya pochi
- Uchaguzi wa wawakilishi wa jamii (siku za kwanza 90)
- Udhibiti wa pochi ya operesheni za saini nyingi
- Kura ya ushauri ya uzito (na kizuizi cha whale)

**Kutobadilika:**
- Nakala rudufu ya usajili na hash za IPFS
- Kunga kwa muhuri wa muda wa Bitcoin
- Maandalizi ya uthibitisho wa kati ya minyororo

---

### Awamu ya 3: Kutokuwa na Kituo Kikamilifu (2027+)

| Sifa | Lengo | ETA |
|------|-------|-----|
| **Usajili Juu ya Mnyororo** | Usajili juu ya mnyororo wa Solana | Q1 2027 |
| **Matumizi ya Ishara Yaliyoimarishwa** | Chapisha NFT, sifa za juu | Q1 2027 |
| **Msaada wa Minyororo Mingi** | Ethereum, Polygon, Base | Q2 2027 |
| **Ujumuishaji wa DID** | Utambulisho Usio na Kituo | Q3 2027 |
| **Utawala wa Jamii** | Mfumo wa ushauri ulioboreshwa | Q4 2027 |
| **Kutambuliwa Kisheria** | Uhalali katika mahakama za Uturuki | 2027-2028 |
| **API kwa Wasanidi Programu** | Mwisho wa API wa umma | Q3 2027 |

**Mabadiliko ya Utawala:**
- v3.0: Mfano wa kuchanganya (curate + jamii yenye uzito)
- 2028+: Utawala kamili wa jamii (hiari)
- Udhibiti wa ubora wa curate daima unalindwa

---

## 🧬 Muundo wa Data wa Itifaki (JSON Schema)

**Kila cheti cha [PoArt] kina kadi ya utambulisho wa JSON inayoweza kusafirisha na kuthibitishwa iliyozalishwa katika kiwango kifuatacho.**

> **Kumbuka:** Muundo huu wa Identity JSON ni muundo wa cheti unaowasilishwa kwa mtumiaji. Katika rekodi za usajili, `registry.asset` inatumika badala ya `identity.asset_data` (ramani: `identity.asset_data` == `registry.asset`).
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

## 🔬 Kina cha Kiufundi: Algorithm ya Muhuri

### Kazi za Hash za Deterministic
```javascript
// Kazi za Kusaidia: Badilisha Digest kuwa mfuatano wa hex
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Badilisha mfuatano kuwa safu ya byte
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Uzalishaji wa mfuatano wa forensics canonical (v1.0: mpangilio thabiti wa sehemu + UTF-8 + kitenganishi \n)
// Kumbukumbu ya Awamu ya 2: Mpito kwa JSON canonical na RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Mchakato wa Uzalishaji wa NotarySeal (Deterministic Kabisa)
```javascript
// 1. Hesabu ya FileHash (upande wa mteja)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Ukusanyaji wa data ya forensic (matumizi ya muhuri wa muda mmoja)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Uzalishaji wa muhuri wa muda mmoja
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Muhuri sawa wa muda
  };
  
  return { forensics, timestamp };
}

// 3. Kuunda EvidenceRoot (kwa canonical encoding)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Uzalishaji wa NotarySeal (matumizi ya muhuri sawa wa muda)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Kazi za kusaidia za kufunika (msaada wa IPv4 na IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Ukaguzi wa IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 au muundo usiojulikana
  return "***";
}
```

### Mtiririko wa Uthibitisho (Viwango Viwili)

#### Uthibitisho wa Haraka (Quick Verify)
```javascript
// Inakagua hash ya faili tu (bendera nyekundu ya haraka)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Pata kutoka kwa usajili
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Ulinganisho wa hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Asili - Hash ya faili inaendana"
    };
  } else {
    return {
      valid: false,
      message: "❌ Bandia - Faili limedadilishwa"
    };
  }
}
```

#### Uthibitisho Kamili (Full Verify)
```javascript
// Inazalisha upya na kuthibitisha EvidenceRoot na NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Pata kutoka kwa usajili
  const cert = await fetchFromRegistry(certificateId);

  // 1) Ukaguzi wa FileHash (bendera nyekundu ya haraka)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Bandia - Hash ya faili haiendani" };
  }

  // 2) Zalisha upya EvidenceRoot (kwa forensics iliyohifadhiwa kwenye usajili)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Haiendani - EvidenceRoot haiendani" };
  }

  // 3) Zalisha upya NotarySeal (kwa muhuri sawa wa muda + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Haiendani - NotarySeal haiendani" };
  }

  // Hiari: Katika Awamu ya 2 thibitisha pia signer_sig na attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Saini ni batili" };

  return { valid: true, message: "✅ Asili - Full Verify imepita" };
}
```

> **Vidokezo Muhimu:**
> - **Uthibitisho wa Haraka:** Inakagua hash ya faili tu kwa matumizi ya haraka.
> - **Uthibitisho Kamili:** Inathibitisha safu zote za itifaki (EvidenceRoot + NotarySeal).
> - Operesheni zote za hash zinafanywa kwa njia ya deterministic, kwa encoding thabiti na vitenganishi.
> - **Kiwango cha canonicalization cha v1.0:** Mpangilio thabiti wa sehemu + encoding ya UTF-8 + kitenganishi cha `\n`.
> - **Mpango wa Awamu ya 2:** Mpito kwa JSON canonical na RFC 8785 (JCS - JSON Canonicalization Scheme).
> - Katika hali ya Masked, hesabu ya EvidenceRoot na NotarySeal inafanywa kwa forensics iliyofunikwa.
> - Muhuri mmoja wa muda unatumika katika mchakato wote (forensics + NotarySeal); deterministic imehakikishwa.
> - **Majina ya sehemu za Forensics:** `ip_masked`, `location`, `device`, `timestamp` (msimbo na usajili vimeendana kikamilifu).
> - **Njia ya usajili:** `certificate.asset.fingerprints` (imeendana kikamilifu na msimbo wa verify).
> - **signer_sig kwenye usajili:** Sehemu ya `proof.signer_sig` inahitajika kwa Full Verify.
> - Utaratibu wa SignerSignature utawashwa katika Awamu ya 2 na Solana Wallet Adapter; katika v1.0 uthibitisho unaweza kufanywa na `attestation_pubkey`.

---

## 📊 Uchambuzi wa Washindani (Umesasishwa)

PoArt imewekwa juu ya "Mahali Pazuri Zaidi" (Sweet Spot) kinachokamilisha mapungufu ya suluhisho zilizopo.

| Sifa | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Gharama** | 🆓 Bure | 🆓 | 💰 Kulipwa | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI ya Buruta & Acha** | ✅ Rahisi Sana | ❌ CLI | ⚠️ Wastani | ⚠️ Wastani | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Utoaji wa Aina Nyingi** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Onyesho la Wakati Halisi** | ✅ Burudani | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Udhibiti wa Faragha** | ✅ Hali 3 | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Hash ya Upande wa Mteja** | ✅ Faragha | ✅ | ❌ Pakia | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Metadata ya Kisheria** | ✅ Kamili | ❌ | ❌ | ⚠️ Mdogo | ❌ | ⚠️ | ❌ | ⚠️ |
| **Uthibitisho wa QR** | ✅ Papo Hapo | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Ukomo wa Kiwango** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Nanga ya Blockchain** | 🔄 Ramani ya Njia | ✅ Bitcoin | ✅ Ethereum | ✅ Nyingi | ✅ | ✅ | ✅ | ✅ |
| **Chanzo Wazi** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Msaada wa Kiswahili** | ✅ Asili | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Maelezo:**
- ✅ : Msaada kamili / upo
- ⚠️ : Mdogo / katika mipango ya kulipwa
- ❌ | Hayupo / hauhimizwi
- 🔄 : Kwenye ramani ya njia (inatengenezwa)
- 🆓 : Kabisa bure
- 💰 : Kulipwa / kujiunga kunahitajika

### Mapungufu ya Washindani, Nguvu za PoArt

| Hasara | Washindani | PoArt |
|--------|-----------|-------|
| **Ugumu wa Matumizi** | CLI, ujuzi wa API, pochi inahitajika | Buruta-acha, inaisha kwa vibonyezo 3 |
| **Kizuizi cha Gharama** | Kujiunga kwa $50-500/mwezi | 100% bure |
| **Faragha** | Faili inapakiwa kwenye seva | Upande wa mteja, faili halijawahi kwenda |
| **Data ya Kisheria** | Muhuri wa muda tu | IP, eneo, kifaa, muda - vyote |
| **Msaada wa Kiswahili** | Hayupo au mdogo sana | Msaada wa lugha asili |
| **Chanzo Wazi** | Sanduku liliofungwa | Msimbo wote wazi kwenye GitHub |

---

## 📈 Takwimu za Matumizi (Malengo ya Q1 2026)

| Kipimo | Lengo | Hali |
|--------|-------|------|
| **Cheti Jumla** | 1,000 | 🔄 Inaendelea |
| **Mtumiaji Hai** | 500 | 🔄 Inaendelea |
| **Idadi ya Uthibitisho** | 5,000 | 🔄 Inaendelea |
| **Uptime** | %99.9 | ✅ Hai |
| **Wastani wa Muda wa Majibu** | <200ms | ✅ Bora |

---

## 🌍 Jamii na Msaada

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Wavuti:** [ilhanart.org](https://ilhanart.org)
- **Barua pepe:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Wachangiaji

Itifaki ya PoArt inaendelea kukua kwa michango ya jamii ya chanzo wazi.

**Kwa kuchangia:**
1. Fanya Fork
2. Unda tawi la kipengele (`git checkout -b feature/amazing-feature`)
3. Commit (`git commit -m 'Add amazing feature'`)
4. Push (`git push origin feature/amazing-feature`)
5. Fungua Pull Request

### 🛠️ Tunahitaji Nini Sasa? (Wito wa Msaada)

Itifaki ya PoArt inasubiri michango ya wasanidi wenye uzoefu katika maeneo yafuatayo kwa maendeleo ya **Awamu ya 2**:

* **Supabase Edge Functions:** Kuhamisha ulinzi wa spam kwa upande wa seva.
* **Solana Web3.js:** Ujumuishaji wa saini ya pochi (Wallet Signing).
* **IPFS / Arweave:** Ujumuishaji wa huduma za uhifadhi na pinning.
* **Zana za Jamii:** Mifumo ya kura ya X, dashibodi ya uchambuzi.

> Tafadhali anzisha mjadala kwenye kichupo cha "Issues" kabla ya kuongeza kipengele.

---

## 💬 Vidokezo vya Mwisho

### Pump.fun na Ukweli

Mradi huu ulianzishwa kwenye Pump.fun kwa sababu:
- ✅ Upatikanaji wa ukwasi (uhamiaji wa kiotomatiki wa Raydium)
- ✅ Upatikanaji wa jamii iliyopo
- ✅ Gharama ya chini ya kuanza

Lakini hebu tufafanue hili:
- **Bei ya ishara** si kiashiria cha mafanikio ya kisanaa
- **Bajeti ya uendeshaji** kwa thamani ya ishara ni muhimu (galeri, maonyesho, miundombinu)
- **Vipimo vya mafanikio:** Kazi zilizothibitishwa + ushirikiano wa jamii + wageni wa kimwili

### Utawala na Kutokuwa na Kituo

**Ukweli wa v1.0 (2026):**
- Usajili: Nje ya mnyororo (PostgreSQL + nakala rudufu ya IPFS)
- Uthibitisho: Saini ya galeri (kituo lakini wazi)
- Utawala: Ushauri tu (uamuzi wa mwisho wa curate)
- Matumizi ya ishara: Upatikanaji wa galeri + usajili + kipaumbele cha NFT

**Dira ya v2.0+ (2027+):**
- Usajili: Juu ya mnyororo (Solana)
- Saini: Kuzingatia pochi (kutokuwa na kituo)
- Utawala: Mchanganyiko (ushauri wa jamii + ubora wa curate)
- Matumizi ya ishara: Sifa zilizoimarishwa + upatikanaji wa juu

Muundo huu, katika hatua za mapema unahakikisha **ufanisi wa uendeshaji** na **udhibiti wa ubora**, huku ukifungua njia ya **kuongeza ushiriki wa jamii** baadaye.

---

**Itifaki ya [PoArt] Uthibitisho wa Sanaa v1.0**  
*"Utamaduni > Mtaji" // Culture > Capital // Kültür, Sermayeden Büyüktür*

## 🧾 Leseni

Leseni ya MIT © 2026 Mpango wa İlhan Art Gallery

Angalia [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) kwa masharti kamili.

---

## 💬 Sifa

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Mradi huu umetengenezwa kwa mpango wa [İlhan Art Gallery] na msimbo wa chanzo upo wazi kwa uwazi.**

**ITIFAKI V1.0 // IMEWEKWA MUHURI NA SHA-512.**

*© 2026 İLHAN ART | HAKI ZOTE ZA KAZI, PICHA NA MAWAZO ZIMEHIFADHIWA.*

---
$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---
