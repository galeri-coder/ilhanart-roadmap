# 📚 KAMUSI YA ISTILAHI NA DHANA
> **"Kuelewa lugha ya itifaki hii ni kuelewa dira yake."**

## ⚙️ Injini ya Uchunguzi ya PoArt (PFE) v1.0: Miundombinu ya Msingi

**Injini ya Uchunguzi ya PoArt (PFE)** ni safu kuu inayowakilisha mantiki ya kati na utendaji wa kiufundi nyuma ya itifaki ya [PoArt]. Hii ndio "injini ya uchunguzi" inayochukua data ghafi za uzalishaji wa kazi ya sanaa na kuzibadilisha kuwa **ushahidi wa kidijitali** unaoweza kuthibitishwa na usiobadilikana.

### 🧩 Kwa Nini "PoArt Forensic"?

- **PoArt (Uthibitisho wa Sanaa):** Lengo la injini ni kuunganisha thamani ya mali ya kidijitali si kwa ubashiri, bali kwa **mchakato wa uzalishaji unaoweza kuthibitishwa**.
- **Forensic (Uthibitisho wa Kisayansi):**
  - **Ufafanuzi wa Kiufundi:** Mbinu ya algorithm na mlolongo wa rekodi kwa kuthibitisha kwamba data za mchakato wa uzalishaji (mistari ya brashi, video ya muda, kumbukumbu) hazijaguswa.
  - **Safu ya Kifalsafa:** Madai ya kubadilisha **muda wa kibinadamu, juhudi, na gharama za uamuzi** kuwa ukweli unaoweza kupimwa, dhidi ya uzalishaji wa "matokeo ya papo hapo" wa AI.

> Kumbuka: Ujumuishaji wa blockchain (mfano, Solana) sio kiini cha PFE; utafafanuliwa tofauti kama **Safu ya Nanga ya Mlolongo** kwa madhumuni ya uthibitisho/usajili.

### 🛠️ Upeo wa Kiufundi v1.0

**Injini ya Uchunguzi ya PoArt (PFE) v1.0** imejengwa juu ya **nguzo 3 kuu** zifuatazo badala ya mifano ngumu ya kifedha:

1. **Hashing & Sealing (Muhuri):**  
   PFE inachakata kwa njia ya kuhakikisha vipengele vyote katika Kifurushi cha Ushahidi (faili la kazi, video, JSON/kumbukumbu, saini, nk.) na kuzalisha thamani ya kipekee ya **NotarySeal**.

   **Dhana za Msingi (v1.0):**
   - **FileHash (alama ya vidole ya kazi):** Hash iliyozalishwa kutoka kwa baiti za faili la kazi.
   - **EvidenceRoot (mzizi wa kifurushi cha ushahidi):** Muhtasari wa mzizi unaosimamia uadilifu wa Kifurushi cha Ushahidi (mzizi wa Merkle au hash ya maelezo halisi).
   - **NotarySeal (muhuri wa mwisho / matokeo ya PFE):** Muhuri wa mwisho uliozalishwa kutoka kwa mchanganyiko wa EvidenceRoot + muda + saini.

   **Fomula (zinaonekana wazi kwa wawekezaji):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Ufafanuzi wa Mizigo Halisi (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Kumbuka: Thamani inayorejelewa kama matokeo ya PFE ni **NotarySeal**. Utaratibu wa **SignerSignature** utaamilishwa katika Awamu ya 2 (na Solana Wallet Adapter); katika v1.0 ya sasa, saini ya uthibitisho wa mfumo inatumika. Ufunguo wa umma wa uthibitisho unachapishwa katika rejista chini ya sehemu ya `issuer.attestation_pubkey`.

2. **Indexing (Uhifadhi):**  
   Inaandika ni pochi gani, tarehe gani, ilisukuma **Uthibitisho wa Kazi** kwa kazi gani kwenye safu ya rejista inayoonekana na inayoweza kuulizwa.  
   *(Safu hii inaweza kuwa hifadhidata; ujumuishaji wa mlolongo unafafanuliwa tofauti kama "Safu ya Nanga ya Mlolongo".)*

3. **Verification (Uthibitisho):**  
   Wakati uhalali wa kazi unahojiwa, PFE inachakata upya ushahidi ghafi; inajaribu kihesabu kama thamani zilizokokotolewa za **EvidenceRoot / NotarySeal** zinalingana na kumbukumbu za kumbukumbu.

---

### 🧮 Nadharia ya Thamani ya PoArt (The Value Theorem)

Itifaki ya [PoArt] inaunganisha thamani ($V$) ya mali ya kidijitali si kwa mtazamo wa kibinafsi wa soko, bali kwa **ukweli wa kimwili wa mchakato wa uzalishaji**.

Akili Bandia (AI) inaharibu mchakato kwa kutoa matokeo mara moja ($t \to 0$). [PoArt], hata hivyo, inashughulikia thamani kama ukusanyaji wa vipengele vya **muda, kazi, na nia**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Ufafanuzi wa Vigezo

- **$\int dt$ (Ukusanyaji wa Mchakato):**  
   Thamani si "matokeo" ya papo hapo; ni **mchakato** unaokusanywa kati ya $t_{\text{start}}$ na $t_{\text{end}}$. Muda unavyopungua (uzalishaji wa AI), matokeo ya integral yanakaribia 0.

- **$P_{\text{labor}}(t)$ (Nguvu ya Kazi ya Papo Hapo):**  
   Inawakilisha ukali wa juhudi za kiakili na kimwili zilizotumika wakati wa uzalishaji. Juhudi zinazoweza kuthibitishwa zinavyoongezeka, integrand inakua.  
   > Kumbuka: Neno hili linaweza kukawaida kwa vitendo kupitia "ishara za kazi zinazoweza kupimwa/kuthibitishwa".

- **$I_{\text{agency}}(t)$ (Mgawo wa Nia):**  
   Uwezo wa mzalishaji kuchukua hatari na kufanya maamuzi. Inachukua thamani kati ya $0$ na $1$.
  - **AI ($I \approx 0$):** Inatekeleza amri, haichukui hatari, halipi gharama.
  - **Binadamu ($I \to 1$):** Hubadilisha maamuzi, husita, huchukua hatari.

- **$U_{\text{irreversible}}$ (Kipekee Kisichoweza Kugeuzwa):**  
   Wakati kutendua (`Ctrl+Z`) kunawezekana katika uzalishaji wa kidijitali, katika uzalishaji wa kimwili (rangi iliyowekwa kwenye canvas, marumaru iliyochongwa, ishara katika utangazaji wa moja kwa moja) hakuna njia ya kurudi. **Kutoweza kugeuzwa** huku ni neno la ziada linaloundua "kipekee" (sifa isiyoweza kubadilishwa) katika kazi.

### 🔎 Uchambuzi wa Kesi: AI "Matokeo ya Papo Hapo" dhidi ya Binadamu "Mchakato Uliothibitishwa"

Hali ifuatayo inaonyesha jinsi **Nadharia ya Thamani ya PoArt** inavyofanya kazi kwa vitendo na kwa nini uzalishaji wa AI unapata alama za chini katika kiwango cha [PoArt].

#### Hali A: Uzalishaji wa Kuona kwa Sekunde 10 na AI

- **Muda ($\Delta t$):** $10$ sekunde (mchakato mdogo)
- **Nguvu ya Kazi ($P_{\text{labor}}$):** $1$ kipimo (tu kuandika amri)
- **Mgawo wa Nia ($I_{\text{agency}}$):** $0.01$ (hakuna hatari, hakuna gharama)
- **Kutoweza Kugeuzwa ($U_{\text{irreversible}}$):** $0$ (inaweza kugeuzwa / inaweza kunakiliwa)

**Matokeo:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Maoni:** Hata kama matokeo ni kamili; thamani ya [PoArt] inakaribia $0$ kwa sababu hakuna mchakato ulioshiwa na hakuna nia/hatari iliyohusika.

#### Hali B: Uzalishaji wa Kimwili wa Saa 6 katika Utangazaji wa Moja kwa Moja

- **Muda ($\Delta t$):** $6$ saa ($21{,}600$ sekunde)
- **Nguvu ya Kazi ($P_{\text{labor}}$):** $0.5$ vipimo (kuendelea kwa juhudi za kimwili na kiakili)
- **Mgawo wa Nia ($I_{\text{agency}}$):** $0.9$ (kubadilisha maamuzi, kuchukua hatari, uchaguzi usioweza kugeuzwa)
- **Kutoweza Kugeuzwa ($U_{\text{irreversible}}$):** $>0$ (alama za kimwili haziwezi kutenduliwa)

**Matokeo:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Maoni:** Mchakato unavyorefuka na nia (hatari) inavyoongezeka, thamani inakusanyika kwa kukusanya. Neno $U_{\text{irreversible}}$ ni mchango wa ziada unaoundua "kipekee" (sifa isiyoweza kubadilishwa) katika kazi.

---

### ✅ Hitimisho: Thamani Iliyofungwa kwa Ushahidi (Proof-Bound Value)

Nadharia hii inatoa dai la thamani la [PoArt] kutoka kuwa "kipendwa" au "hadithi ya soko" na kuliunganisha na **ukweli wa uzalishaji unaoweza kuthibitishwa**.

1. **Hakuna Mchakato, Hakuna Thamani:**  
   AI inaharibu mchakato kwa matokeo ya papo hapo ($t \to 0$). Dirisha la mchakato linavyopungua, matokeo ya integral lazima yapungue:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Nia na Hatari ni Vyozidisha:**  
   [PoArt] haipimi tu "muda uliotumika" bali pia safu ya kweli ya uamuzi, hatari, na gharama katika muda huo. Uzalishaji bila kuchukua hatari (AI) una thamani ya chini:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Kipekee ni Ushahidi wa Kimwili, Sio Uuzaji:**  
   Alama zisizoweza kugeuzwa katika uzalishaji wa kimwili (mstari wa canvas, kipande cha marumaru) ziko nje ya mantiki ya `Ctrl+Z` ya kidijitali. Kutoweza kugeuzwa huku ($U_{\text{irreversible}}$) kunaundua kazi kwa ontolojia.

> **🔐 MUHTASARI:** Ingawa nadharia ya thamani inaweza kuonekana kuwa haihakikishi kama kipimo (hata kama sawa yake ya ulimwengu halisi haiwezi kupimwa kikamilifu), lengo la fomula hii ni kuonyesha usanidi na mwelekeo wa vigezo. Katika enzi ya AI, kilicho nadir si "picha" bali **kazi inayoweza kuthibitishwa, muda, na nia.** [PoArt] inapima uhaba huu na kuiandika na **Kifurushi cha Ushahidi**.

### 🏛️ Umuhimu wa Dhana ya "Injini"

Ishara zinazotokea kutoka Pump.fun au majukwaa sawa mara nyingi ni **"tiketi za ufikiaji"** tu. **Injini ya Uchunguzi ya PoArt (PFE)**, hata hivyo, ni **safu ya mantiki ya kikatiba** inayoamua haki zipi tiketi hii inalinda, jinsi kazi itaandikwa na jinsi sanaa/sayansi/teknolojia itaendelezwa.

> **Kumbuka:** Sababu tulizindua mradi huu kwenye Pumpfun ni kwamba hatukuwa na ukwasi wa kutosha wala wafuasi wa kutosha. Kutumia data iliyopo ilikuwa kimkakati hatua sahihi, hata kama haikuwa ya ubora wa juu zaidi. Bila kujali bajeti na rasilimali, kufafanua mantiki ya injini hii kwenye GitHub inathibitisha kwamba mradi si ubashiri wa kifedha tu, bali dira ya muda mrefu ya **miundombinu ya programu** na **maktaba ya kitaifa ya kidijitali**.

---

## 🎨 ITIFAKI YA [PoArt] YA UTHIBITISHO WA KAZI (Proof of Art Protocol v1.0)

> **"Msanii Halisi, Uzalishaji Halisi, Thamani Halisi."**

Itifaki hii ni **utaratibu wa ulinzi wa kibiolojia na kiakili** uliotengenezwa dhidi ya wadanganyifu wasiojulikana wanaozunguka ikolojia ya crypto, taswira za AI zilizozalishwa kwa dakika 5, na utamaduni wa "Pump & Dump".

---

## a) [PoArt] ni Nini? (Ufafanuzi wa Kifalsafa na Kiufundi)

**Uthibitisho wa Sanaa [PoArt];** ni kiwango cha uthibitisho wa kitaasisi kinachohakikisha kwamba thamani nyuma ya mali kwenye blockchain inategemea si kwa ubashiri, bali kwa **kazi ya kibinadamu**, **muda**, na **nishati ya kimwili** inayoweza kuthibitishwa.

Kama vile Bitcoin inavyozalisha thamani na *"Umeme na Nguvu ya Processer"* **(Uthibitisho wa Kazi)**, miradi inayolingana na [PoArt] inazalisha thamani na *"Ustadi wa Kisanaa na Muda wa Kibinadamu"*.

Inaondoa hatari ya *"Msanidi programu aliuza, mradi umeisha"* kwenye majukwaa ya Pump.fun na DEX; kwa sababu hapa thamani sio katika msimbo, bali katika **kuendelea kwa uzalishaji**.

> **[PoArt] haimwambii washiriki "Utuamini"; inasema "Hapa kuna ushahidi, ona kwa macho yako, thibitisha kwa hisabati yako."**

---

## b) Kiwango cha Nguzo 5 cha [PoArt] (Nguzo 5 za Ukweli)

Vipengele hivi 5 ni vichujio visivyoweza kubadilishwa ambavyo mradi lazima upite kupokea muhuri wa [PoArt].

### 1) Uthibitisho wa Kitambulisho wa Moja kwa Moja

- **Tatizo:** Ulimwengu wa crypto umejaa waanzilishi wasiojulikana (Wasanidi programu) wenye vitambulisho visivyo wazi wanaokusanya pesa na kusahau miradi.
- **Suluhisho la [PoArt]:** Mzalishaji anathibitisha si tu kitambulisho, bali **uwepo wakati wa uzalishaji**. Hii inajumuisha vikao vya utangazaji wa moja kwa moja ambapo mwingiliano na jamii hufanyika na maombi maalum ya papo hapo yanatekelezwa, si video zilizorekodiwa mapema.  
  (Kwa mfano, *"Andika tarehe ya leo na nambari ya bloku ya sasa kwenye kona ya kulia ya canvas"*)
- **Kauli:** *"Bots zinaweza kupaka rangi lakini bots hazitoi jasho na haziwezi kufanya improvisation."*

### 2) Uthibitisho wa Kazi na Mchakato

- **Tatizo:** Taswira za AI (Akili Bandia) zilizozalishwa kwa sekunde 2 zinapokea matibabu sawa ya "jpeg" na uchoraji wa mafuta uliofanywa kwa miezi 2 katika ulimwengu wa kidijitali.
- **Suluhisho la [PoArt]:** Mchakato wa "ujauzito na kuzaliwa" wa kazi unaandikwa. Hatua za mchoraji, safu za rangi, saa zilizokusanywa zilizotumika na mchakato wa kimwili ambao msanii aliupitia wakati wa kuunda kazi zinaandikwa. Hii inaongeza **"Gharama ya Muda"** kwa ishara. Uzalishaji wa mali unavyokuwa mgumu zaidi, thamani yake ni imara zaidi.

### 3) Uthibitisho wa Thamani ya Urembo

- **Tatizo:** Utamaduni wa "Meme" unaozingatia tu ucheshi wa papo hapo wakati ukipuuza urembo na kina cha kisanaa, unaosababisha miradi ya "Hype" ya muda mfupi.
- **Suluhisho la [PoArt]:** Mradi lazima uwe na viwango vya sanaa ya kitaaluma, nadharia ya rangi, sheria za muundo, na maarifa ya vifaa (Impasto, Muundo, nk.). Maudhui hayapaswi kufanya tu ucheke; yanapaswa kuchochea mshangao kwa watazamaji na kuwa na **thamani ya kukusanywa**.

### 4) Upya wa Dhana

- **Tatizo:** Maelfu ya sarafu za mbwa/paka nakala bila ubunifu.
- **Suluhisho la [PoArt]:** Mradi lazima ujenga daraja jipya linalounganisha sanaa, sayansi, falsafa au teknolojia katika muundo wenye maana.  
  (Kwa mfano, Kuchanganya sanamu ya kale ya David na data ya soko la crypto; kuchakata wazo kwamba mtazamo wa kibinadamu "unageuka kuwa jiwe" kupitia hii na kuisimamia na vyanzo vya kisayansi.)  
  Kazi haipaswi kuwa tu karamu ya kuona bali pia changamoto ya kiakili inayochochea mawazo kuhusu **Sayansi, Falsafa au Teknolojia**.

> [!IMPORTANT]
> **Mfano wa Kumbukumbu (Athari ya Las Palmitas):** Katika mtaa wa Las Palmitas nchini Mexico, uliosumbuliwa na uhalifu, zaidi ya nyumba 200 zilibadilishwa kuwa tamasha kubwa la upinde wa mvua. Kama matokeo ya uingiliaji huu wa urembo, viwango vya uhalifu katika mtaa vilipungua kwa kiasi fulani, na vijana walianza kushughulika na sanaa badala ya makundi ya uhalifu. Mabadiliko ya urembo yaliandika upya heshima ya watu kwa mazingira yao na kwa kila mmoja (Ushirikiano wa Kijamii).
>
> **Matarajio:** Mradi unaoingia kwenye orodha ya [PoArt] lazima, kama katika mfano hapo juu, uwe na uhusiano wa sababu na athari za kijamii, kisayansi au kifalsafa zaidi ya urembo wa kuona tu. Kwa kuwa muda ni mali pekee ambayo haiwezi kununuliwa kwa pesa, katika itifaki hii muda lazima uthibitishwe kwa kuwekewa dhamana kama usalama. Msingi wa dhana wa mradi lazima uwe imara na wa ulimwengu wote kiasi kwamba hata katika hali ya uwezekano wa CTO (Jamii Kuchukua Udhibiti) miaka baadaye, jamii inaweza kuendelea kwa uhuru uwezekano wa ubunifu wa mradi kwa kurithi urithi huu.

### 5) Nia Isiyokuwa ya Algorithm

- **Tatizo:** Uzalishaji wa kidijitali kamili lakini bila roho unaojirudia.
- **Suluhisho la [PoArt]:** Nia ya kipekee ya binadamu anayeweza kufanya makosa, kuchukua hatari na kupata mabadiliko ya kihisia lazima ihisiwe katika kazi. Kutokuwa na uhakika katika mistari ya brashi, athari zisizotarajiwa za vifaa, na maamuzi ya papo hapo ya msanii ni **Saini ya Kibiolojia** inayotenganisha kazi na "Uzalishaji wa Mashine".

---

## c) Utaratibu wa Uthibitisho na Kuzuia Udanganyifu

Mfumo huu unahakikisha kwamba mradi unabaki wa kuaminika na hai si tu "mwanzoni" bali "milele".

### 📦 Kifurushi cha Ushahidi - Pacha ya Kidijitali

Nyuma ya kila kazi iliyoidhinishwa na [PoArt] kuna kifurushi cha data kilichosimbwa na chenye muhuri wa muda ambacho wawekezaji wanaweza kuipakua:

- **Rekodi za Video RAW:** Filamu ghafi isiyo na kukatika ya wakati wa uzalishaji.
- **Uchambuzi wa Metadata:** Tarehe ya uundaji wa faili, maelezo ya kifaa kilichotumika na data ya eneo.
- **Marejeleo ya Kimwili:** Ushahidi kwamba kazi ipo katika ulimwengu wa kimwili  
  (Kwa mfano, Gazeti la sasa au data ya blockchain ya wakati huo karibu na kazi).

> *Kumbuka ya uthabiti:* Neno "kifurushi cha ushahidi" linaunganisha na mlolongo **Kifurushi cha Ushahidi → EvidenceRoot → NotarySeal** katika sehemu za awali; yaani, uadilifu wa kifurushi unawakilishwa na muhuri unaoweza kuthibitishwa.

### 🔄 Ufanyaji Upya wa Siku 365 (Itifaki ya Uendelevu)

- **Kipengele cha Mapinduzi:** Katika miradi ya crypto, "Dev" (Msanidi programu) hutoa ishara na kawaida hutoweka baada ya miezi 1-2 (Soft Rug). [PoArt] inafanya hii iwe haiwezekani.
- **Sheria:** Hadhi ya "Msanii Aliyethibitishwa" si ya maisha yote. **Mwaka 1** tu ni halali.
- **Uendeshaji:** Msanii/msanidi programu lazima awasilishe kwa jamii **kazi mpya muhimu na inayoweza kuthibitishwa** kila siku 365.
- **Hali ya Mfano:** Ulizindua mradi mnamo 2026. Mnamo Januari 2027, mfumo unatoa onyo "Kipindi cha Ushahidi Kimeisha". Ikiwa msanii hatawasilisha maonyesho mapya, kazi mpya ya kimwili au ujumuishaji mpya wa teknolojia, "Beji ya Imani" ya mradi inashuka.
- **Matokeo:** Mfumo huu unahakikisha kwamba **maudhui kamwe hayapotezi umuhimu** na kwamba mwekezaji kamwe hajapata hofu ya *"Je, msanidi programu bado yupo?"*. Mradi unakuwa studio hai.

### 🚩 Itifaki ya Bendera Nyekundu

**Katika hali ya udanganyifu wowote uliogundulika na jamii au algorithm (matumizi ya AI, kazi iliyoibiwa, video iliyodanganywa):**

1. Hati inawekewa alama mara moja kama **"VOID" (BATILI)**.
2. Vifurushi vya ushahidi vinawekewa lebo hadharani kama **"Bandia"**.
3. Mradi unawekwa kwenye orodha nyeusi ya [PoArt]. Hii inaimarisha kwamba katika ulimwengu usio na utawala wa kati, **sifa njema ni sarafu pekee**.

---

## d) Hitimisho: Sio Kasino, Bali Makumbusho

**Pump.fun na Mabadilishano Yasiyo na Utawala wa Kati (DEX) kwa bahati mbaya ni kasino sasa hivi; taa zinapepesa, kila mtu anafuata faida za haraka, na nyumba (wadanganyifu) inashinda kila wakati. Sababu tulianza mradi hapa ni ukosefu wa bajeti ya kutosha na kuwa na mazingira ya kufikia hadhira iliyopo kupitia utangazaji wa moja kwa moja.**

**[PoArt] ni ngome iliyojengwa katikati ya kasino hii.**

- 🎰 Kasino inategemea michezo ya karata; sisi tunategemea **ukweli wa kimwili**.
- 🃏 Kasino imefunguliwa kwa udanganyifu; sisi tumefunguliwa kwa **ushahidi ulio wazi**.
- ⏳ Kasino ni ya muda; tunazingatia **milele ya sanaa na sayansi**.

**Ishara inayotumia itifaki hii si "sarafu" tu; ni mtaji wa kidijitali wenye jasho, rangi, msimbo na falsafa.**

---

## 🗳️ 6) UTAWALA NA REJISTA YA UMMA

**Lengo la sehemu hii ni: kubadilisha kiwango cha [PoArt] kutoka kiwango cha "kuamini watu binafsi" hadi miundombinu endelevu ya umma yenye rejista + uthibitisho + usimamizi wa jamii.**

### 6.1 Rejista ya Umma

- **Rejista ya Umma:** Data zote zilizoidhinishwa zinaandikwa kwenye `ilhanart.org/registry` (au GitHub Registry).

**Mantiki ya rejista (kiwango kilichopendekezwa - katika muundo wa njia ya JSON):**

Kila uandikishaji unaoingia kwenye rejista unabeba sehemu hizi za msingi zinazoweza kuthibitishwa za chini:

- **Kitambulisho na Hadhi:**
  - `certificate_id` (kumbukumbu inayoweza kusomwa)
  - `status` (active / void)
  - `void_reason` (ikiwa inatumika)
  - `visibility` (private / masked / public)
  - `created_at` (muhuri wa muda)

- **Taasisi Inayotoa:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Maelezo ya Kazi:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (ikiwa inawezekana; kwa kitambulisho chenye lango la ishara)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Data za Uchunguzi:**
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
  - `governance.veto_threshold`

Rejista inaweza kuwa na safu mbili:
- **1)** Fahrasa inayoweza kusomwa na wanadamu (orodha ya wavuti / utafutaji / kichujio)
- **2)** Maelezo yanayoweza kusomwa na mashine (rekodi za JSON; kwa uthibitisho wa PFE)

**"Uandikishaji" huu unakuwa unaweza kuthibitishwa kupitia mnyororo Kifurushi cha Ushahidi → EvidenceRoot → NotarySeal wa PFE. Rejista inatoa malengo ya uthibitisho, si "madai".**

---

### 6.2 Veto ya Jamii ya 40% (Utawala wenye Lango la Ishara)

- **Veto ya Jamii ya 40%:** Kura inaanza mwezi mmoja kabla ya kutoa hadhi; pingamizi la 40% la jamii **yenye Lango la Ishara (iliyothibitishwa na Solana)** inabatilisha ombi.

**Mtiririko wa kura (mchakato ulio wazi uliop endekezwa):**
- **Dirisha la maombi:** Mradi wa mgombea unafungua "usajili wa mgombea wa PoArt" (rekodi za wagombea zinaonekana katika hadhi ya "inasubiri").
- **Kipindi cha ukaguzi:** Jamii inachunguza ushahidi kwa siku 30 (Kifurushi cha Ushahidi + rekodi za utangazaji wa moja kwa moja + metadata).
- **Uthibitisho wenye lango la ishara:** Kura inafanywa na pochi zilizothibitishwa za Solana (mfano umiliki wa ishara/NFT maalum + saini ya pochi).
- **Sheria ya veto:** Ikiwa 40% ya kura ni **pingamizi (HAPANA / VETO)**, ombi linakataliwa.
- **Uwazi:** Matokeo ya kura yanahifadhiwa katika rejista kama "uandikishaji wa uamuzi" (tarehe, uwiano, kitambulisho cha picha).

---

### 6.3 Usawazishaji wa Metadata (Upatanisho na Ulimwengu wa Kimwili)

- **Usawazishaji wa Metadata:** Data za kiufundi katika rejista lazima zilingane 100% na huluki ya kimwili.

**Kufafanua kwa kiufundi "upatanisho wa 100%" (uwazi uliop endekezwa):**
- **Upatanisho wa chini (lazima):**
  - `asset.fingerprints.sha256/sha512` katika rejista lazima iwe **sawa** na hash ya faili linalohusika.
  - Wakati `proof.notary_seal` katika rejista inazalishwa upya (ikiwa Kifurushi cha Ushahidi kipo), lazima iwe **sawa**.
- **Upatanisho wa kumbukumbu ya kimwili (aina ya ushahidi):**
  - Kazi ya kimwili + kumbukumbu ya tarehe/bloku iliyoonyeshwa katika utangazaji wa moja kwa moja na ushahidi sawa lazima uwe na uthabiti na Kifurushi cha Ushahidi.
- **Kufuata faragha:**
  - Sehemu kama IP/eneo katika uwazi wa `masked` zinachapishwa **kulingana na viwango vya kuficha**.

---

### 6.4 Ugomvi na Kubatilisha

Rejista sio utaratibu wa "idhini" tu; ni **utaratibu wa ukaguzi hai dhidi ya udanganyifu**.

- Ugomvi unapoanzishwa, uandikishaji unaweza kuwekwa katika hali ya **"review" (ukaguzi)**.
- Udanganyifu unapogunduliwa, unawekewa alama kama `status: void` na sababu imeongezwa:
  - `void_reason` (matumizi ya AI / wizi / udanganyaji, nk.)
  - `revoked_at` (muda wa kubatilisha)
- Chanzo cha uamuzi wa kubatilisha kinaonekana wazi katika rejista:
  - kura ya jamii / kamati iliyoidhinishwa / kumbukumbu ya uchunguzi wa kisayansi (kinachotumika)

> **Sehemu hii ni sawa na rejista ya dhana ya VOID katika sehemu ya "Itifaki ya Bendera Nyekundu".**

---

### 6.5 Mfano wa Uandikishaji wa Rejista (Unaweza Kusomwa na Mashine)
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
> *Kumbuka: `asset.fingerprints.sha512` na thamani zingine za hash zimefupishwa kwa madhumuni ya kuonyesha; katika utekelezaji halisi, tungo za herufi za hexadecimal za urefu kamili zinatumika.*

---

## 7) 🔐 MUHURI WA KIUFUNDI (NOTARY SEAL)

Algorithm ya muhuri isiyotikisika iliyozalishwa na **Injini ya Uchunguzi ya PoArt (PFE) v1.0**:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Itifaki ya [PoArt] ya Notary ya Kidijitali na Ushahidi wa Kisayansi (Beta v1.0)

> **"Utamaduni ni mkubwa kuliko mtaji. Linda kazi zako leo, zibebe kesho."**

---

## Kwa Nini Umma?

Usalama wa kweli unatoka kwa uwazi. Shukrani kwa mfumo wetu wa **Rejista ya Umma**, mtu yeyote mahali popote duniani anaweza kuthibitisha kama faili ni asili kwa sekunde, bila kuhitaji mamlaka yoyote.

---

## 🧩 Kwa Nini "Moduli Nyingi za Mwonekano"?

Hii ni sehemu muhimu zaidi ya msimbo (menyu ya uchaguzi wa mwonekano). Chaguo hizi zinaruhusu watumiaji kusawazisha **"Faragha dhidi ya Uwazi"**:

### 🔒 Binafsi

- **Hali:** Msanii bado hataki kuchapisha kazi, lakini anataka kuiweka muhuri wa muda kuthibitisha "nilifanya hii tarehe hii".
- **Msimbo Unafanya Nini:** Inaandika data katika hifadhidata lakini inaweka muhuri `visibility: "private"`. Baadaye wakati wa kuandika sera ya "Kusoma kwa Umma", unaweza kuficha rekodi hizi kutoka kwa umma na `WHERE visibility = 'public'`.

### 🕶️ Imefichwa

- **Hali:** Msanii anataka uwazi lakini anaogopa anwani yake ya nyumbani (eneo la IP) itapatikana.
- **Msimbo Unafanya Nini:** Kazi za `maskIP` na `maskLoc` zinafanya kazi upande wa JavaScript. Inabadilisha anwani ya IP kuwa muundo `88.241.***.***`, eneo kuwa muundo `***/TR`, na kutuma toleo lililocensored kwa hifadhidata.
- **Kumbuka ya Faragha:** Kuficha kunafanywa kwenye kivinjari, Supabase haiioni eneo halisi. **Hata hivyo:** Ikiwa API za watu wengine kama ipapi.co zinatumika kwa data za eneo, watoa huduma hawa wanaona anwani ya IP wakati wa ombi.
- **Muhuri katika Hali ya Kufichwa:** Hesabu ya EvidenceRoot na NotarySeal inafanywa na data za uchunguzi zilizofichwa; kwa hivyo uthibitisho unabaki wa kuhakikisha.

### 🌍 Umma

- **Hali:** Uwazi kamili. Kulingana na viwango vya [PoArt], wapi, lini, kutoka kwenye mtandao gani kazi ilizalishwa inatangazwa wazi.

---

## 💡 Ubunifu wa Teknolojia

PoArt si mfumo wa kupakia faili tu. Ni injini ya **"Mlolongo wa Ulinzi wa Kisayansi"** inayoleta kiwango kipya kwa kuunganisha safu tatu tofauti za teknolojia katika sufuria moja.

**Safu inayoelezewa kama "injini" katika sehemu hii inalingana na kiini cha Injini ya Uchunguzi ya PoArt (PFE) katika istilahi za awali.**

### 1) Hashing ya Upande wa Mteja (Faragha ya Juu Zaidi)

Faili zako za kazi za sanaa kamwe hazipakuliwi kwenye seva. Injini yetu inayotegemea kivinjari (upande wa mteja) inahesabu hash (muhtasari wa kidijitali) wa faili kwenye kompyuta yako mwenyewe. Alama hii ya vidole na metadata tu zinapelekwa kwa seva.

> **Kumbuka ya Faragha:** Faili la kazi halipakiwi kwenye seva na linalindwa kwa njia hii. Hata hivyo, data za uchunguzi (IP/eneo) zinashirikiwa kulingana na hali ya mwonekano uliochaguliwa (binafsi/kufichwa/umma).

### 2) Muunganisho wa Data za Uchunguzi (Nguvu ya Kisayansi)

Zaidi ya muhuri wa muda wa kawaida. Mfumo unaunganisha data hizi katika "Muhuri wa Mwanzo" mmoja:

- **Muhtasari wa Kidijitali (SHA-512):** Alama ya kidole kwa kutumia kiwango cha muhtasari wa cryptographic (SHA-512) ambacho kitavunjika ikiwa hata pixel moja ya kazi itabadilika.
- **Eneo na Muda:** Tarehe ya usahihi wa millisekunde, nchi, jiji na data za wilaya za muamala.
- **Kitambulisho cha Kifaa:** Mfumo wa uendeshaji, kivinjari na aina ya kifaa (uchambuzi wa User-Agent).

---

## 🛡️ Matumizi na Faida

Ikiwa wewe ni msanii, mwandishi au mbuni, kusema "Nilifanya hii mapema" haitoshi; unahitaji kuthibitisha.

**Kazi unayoiweka muhuri na PoArt:**

- **Ushahidi wa Kihesabu:** Ikiwa hata pixel moja ya faili lako itabadilika, mfumo unajua. Udanganyifu hauwezekani.
- **Msingi wa Kisheria:** Tarehe gani, jiji gani, kutoka kifaa gani kazi iliwekwa muhuri imeandikwa.
- **Hati ya Papo Hapo:** Inazalisha **"Hati ya Kitambulisho cha Mali"** maalum kwako kwa sekunde, yenye msimbo wa QR na yenye muhuri.

---

## ⚙️ Usanifu wa Mfumo na Vipengele vya Kiufundi

Mfumo umebuniwa kwenye usanifu wa "Serverless", ukizingatia utendaji wa juu na uwezekano wa kupanua.

| Safu | Teknolojia | Maelezo |
|--------|-----------|-------------|
| **Usimbaji** | SHA-256 & SHA-512 | Muhtasari wa cryptographic wa safu mbili |
| **Hifadhidata** | Supabase (PostgreSQL) | Muundo wa data ya JSONB, sera za RLS |
| **Data za Uchunguzi** | ipapi.co API | Utatu wa IP/Eneo/Muda |
| **Uwasilishaji** | html2canvas + jsPDF | Uzalishaji wa PNG/PDF wa upande wa mteja |
| **Frontend** | Vanilla JavaScript | Utegemezi wa mfumo sifuri |
| **Usalama** | Hashing ya upande wa mteja | Faili kamwe haliendi kwenye seva |

### Vipengele Vinavyoonekana

| Kipengele | Maelezo | Kwa Washindani? |
|---------|-------|-----------------|
| **UI ya Buruta na Acha** | Buruta na acha faili, onyesho la papo hapo | ❌ Hakipo kwa wengi |
| **Usafirishaji wa Muundo Mwingi** | PNG, JSON, PDF - bofya moja | ⚠️ Kikomo |
| **Onyesho la Wakati Halisi** | Onyesho la hati moja kwa moja | ❌ Hakuna |
| **Vidhibiti vya Faragha** | Chaguo la Binafsi/Kufichwa/Umma | ❌ Hakuna |
| **Hash ya Upande wa Mteja** | Faili kamwe haliendi kwenye seva | ✅ Tu kwa wachache |
| **Metadata za Uchunguzi** | IP, eneo, kifaa, muda - vyote pamoja | ❌ Vimegawanyika |
| **Uthibitisho wa QR** | Msimbo wa QR wa uthibitisho wa papo hapo | ⚠️ Kikomo |
| **Kiwango cha Kasi** | Ulinzi dhidi ya spam (RLS + Mteja) | ❌ Hakipo kwa wengi |

---

## 🗺️ Ramani ya Barabara: Siku zijazo "Bila Kuamini"

Toleo la sasa **(Beta v1.0)** limebuniwa kutoa watumiaji wa mwisho kasi ya juu, kiolesura rahisi na ufikiaji bure. Hata hivyo, dira yetu ya mwisho ni mpito hadi muundo ambapo hata msimamizi wa hifadhidata (sisi) hawawezi kuingilia.

### Awamu ya 1: Beta (Iko Moja kwa Moja Sasa)

- **Miundombinu:** Hifadhidata ya Wingu (Supabase).
- **Lengo:** Kasi, kuondoa vizuizi vya UX (Uzoefu wa Mtumiaji) na upatanisho. Kutoa usalama "bila msuguano".

### 🚀 Awamu ya 2: (Mahitaji ya Backend / Kazi ya Edge)

Awamu hii inashughulikia mpito kutoka kwa muundo unaotefanya "upande wa mteja" kabisa hadi muundo wa "Mamlaka ya Upande wa Seva" wenye usalama zaidi na unaoweza kudhibitiwa.

| Kipengele | Kinaleta Nini? | Rundo la Teknolojia | Kipaumbele |
|-------|---------------|------------|---------|
| **`INSERT` → Kazi ya Edge** | Kuzuia spam + usalama wa ufunguo wa API | Supabase Edge (Deno) | 🔴 Juu |
| **Saini ya Pochi** | Uthibitisho wa cryptographic | Solana Wallet Adapter | 🟡 Wastani |
| **Hifadhi ya IPFS/Arweave** | Kutobadilika bila utawala wa kati | IPFS SDK + Pinata | 🟢 Chini |
| **Utaratibu wa Kubatilisha** | Kufuta hati bandia | Sasisha Mpango wa DB | 🔴 Juu |
| **Kumbukumbu ya Ukaguzi** | Rekodi ya ulizo wa kisayansi | Jedwali maalum la kumbukumbu | 🟡 Wastani |
| **OpenTimestamps** | Nanga ya Bitcoin | OTS JavaScript | 🟢 Chini |
| **Ujumuishaji wa DID** | Kitambulisho bila Utawala wa Kati | ION/Ceramic | 🟢 Chini |

### Awamu ya 3: Kutokuwa na Utawala wa Kati Kabisa (Muda Mrefu)

| Kipengele | Lengo | ETA |
|---------|------|-----|
| **Rejista ya Blockchain** | Usajili wa kwenye mlolongo wa Ethereum/Solana | Q4 2026 |
| **Utawala wa DAO** | Usimamizi wa jamii | Q1 2027 |
| **Usaidizi wa Mlolongo Mwingi** | Polygon, Arbitrum, Base | Q2 2027 |
| **Utambuzi wa Kisheria** | Uhalali katika mahakama za Uturuki | 2027-2028 |
| **API kwa Wasanidi programu** | Mwisho wa API ya umma | Q3 2026 |

---

## 📊 Uchambuzi wa Ushindani (Imesasishwa)

PoArt iko katika "Sweet Spot" inayokamilisha upungufu wa suluhisho zilizopo.

| Kipengele | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Gharama** | 🆓 Bure | 🆓 | 💰 Malipo | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI ya Buruta na Acha** | ✅ Rahisi Sana | ❌ CLI | ⚠️ Wastani | ⚠️ Wastani | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Usafirishaji wa Muundo Mwingi** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Onyesho la Wakati Halisi** | ✅ Moja kwa Moja | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Vidhibiti vya Faragha** | ✅ Hali 3 | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Hash ya Upande wa Mteja** | ✅ Faragha | ✅ | ❌ Pakia | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Metadata za Uchunguzi** | ✅ Kamili | ❌ | ❌ | ⚠️ Kikomo | ❌ | ⚠️ | ❌ | ⚠️ |
| **Uthibitisho wa QR** | ✅ Papo Hapo | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Kiwango cha Kasi** | ✅ RLS+Mteja | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Nanga ya Blockchain** | 🔄 Ramani ya Barabara | ✅ Bitcoin | ✅ Ethereum | ✅ Mwingi | ✅ | ✅ | ✅ | ✅ |
| **Chanzo Wazi** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Usaidizi wa Kituruki** | ✅ Asili | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Ufafanuzi:**
- ✅ : Usaidizi kamili / inapatikana
- ⚠️ : Kikomo / katika mipango ya malipo
- ❌ : Hakuna / haitegemezwi
- 🔄 : Katika ramani ya barabara (inaendelezwa)
- 🆓 : Kabisa bure
- 💰 : Malipo / usajili unahitajika

### Upungufu wa Washindani, Nguvu za PoArt

| Kasoro | Washindani | PoArt |
|-------|-------------|-------|
| **Ugumu wa Matumizi** | CLI, maarifa ya API, pochi inahitajika | Buruta na acha, tayari kwa mibofyo 3 |
| **Kizuizi cha Gharama** | Usajili wa $50-500/mwezi | 100% bure |
| **Faragha** | Faili linapakiwa kwenye seva | Upande wa mteja, faili kamwe haliendi |
| **Data za Uchunguzi** | Muhuri wa muda tu | IP, eneo, kifaa, muda - vyote |
| **Usaidizi wa Kituruki** | Hakuna au kikomo sana | Usaidizi wa lugha asili |
| **Chanzo Wazi** | Sanduku liliofungwa | Msimbo wote wazi kwenye GitHub |

---

## 🧬 Muundo wa Data wa Itifaki (JSON Schema)

**Kila hati ya [PoArt] ina kitambulisho cha JSON kinachobeba na kinachoweza kuthibitishwa kilichozalishwa kwa kiwango kifuatacho.**

> **Kumbuka:** Muundo huu wa JSON wa kitambulisho ni muundo wa hati unaotolewa kwa watumiaji. Katika rekodi za rejista, `registry.asset` inatumika badala ya `identity.asset_data` (ramani: `identity.asset_data` == `registry.asset`).
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

### Kazi za Hash za Kuhakikisha
```javascript
// Kazi za Kusaidia: Badilisha muhtasari kuwa tungo ya hexadecimal
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Badilisha tungo kuwa safu ya baiti
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Uzalishaji wa tungo halisi ya uchunguzi (v1.0: mpangilio wa sehemu wa kudumu + UTF-8 + kitenganishi \n)
// Kumbuka ya Awamu ya 2: Mpito hadi JSON halisi na RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Mchakato wa Uzalishaji wa NotarySeal (Kuhakikisha Kabisa)
```javascript
// 1. Hesabu ya FileHash (upande wa mteja)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Ukusanyaji wa data za uchunguzi (matumizi ya muhuri mmoja wa muda)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Uzalishaji wa muhuri mmoja wa muda
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

// 3. Uundaji wa EvidenceRoot (na usimbaji halisi)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Uzalishaji wa NotarySeal (matumizi ya muhuri sawa wa muda)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Kazi za kusaidia za kuficha (usaidizi wa IPv4 na IPv6)
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

#### Quick Verify (Uthibitisho wa Haraka)
```javascript
// Thibitisha tu hash ya faili (bendera nyekundu ya haraka)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Pata kutoka rejista
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Ulinganisho wa hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Asili - Hash ya faili inafanana"
    };
  } else {
    return {
      valid: false,
      message: "❌ Bandia - Faili limedanganywa"
    };
  }
}
```

#### Full Verify (Uthibitisho Kamili)
```javascript
// Zalisha upya na thibitisha EvidenceRoot na NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Pata kutoka rejista
  const cert = await fetchFromRegistry(certificateId);

  // 1) Uthibitisho wa FileHash (bendera nyekundu ya haraka)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Bandia - Hash ya faili haifanani" };
  }

  // 2) Zalisha upya EvidenceRoot (na data za uchunguzi zilizohifadhiwa kwenye rejista)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Haifanani - EvidenceRoot haisimami" };
  }

  // 3) Zalisha upya NotarySeal (na muhuri sawa wa muda + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Haifanani - NotarySeal haisimami" };
  }

  // Hiari: Katika Awamu ya 2, pia thibitisha signer_sig na attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Saini batili" };

  return { valid: true, message: "✅ Asili - Uthibitisho kamili umepita" };
}
```

> **Vidokezo Muhimu:**
> - **Quick Verify:** Inathibitisha tu hash ya faili kwa matumizi ya haraka.
> - **Full Verify:** Inathibitisha safu zote za itifaki (EvidenceRoot + NotarySeal).
> - Operesheni zote za hash zinatekelezwa kwa kuhakikisha na usimbaji na vitenganishi vya kudumu.
> - **Kiwango cha kukawaida v1.0:** Mpangilio wa sehemu wa kudumu + usimbaji wa UTF-8 + kitenganishi `\n`.
> - **Mpango wa Awamu ya 2:** Mpito hadi JSON halisi na RFC 8785 (JCS - JSON Canonicalization Scheme).
> - Katika hali ya kufichwa, hesabu ya EvidenceRoot na NotarySeal inafanywa na data za uchunguzi zilizofichwa; kwa hivyo uthibitisho unabaki wa kuhakikisha.
> - Muhuri mmoja wa muda unatumika katika mchakato wote (uchunguzi + NotarySeal); kuhakikisha kumehakikishwa.
> - **Majina ya sehemu za uchunguzi:** `ip_masked`, `location`, `device`, `timestamp` (msimbo na rejista zinafanana kabisa).
> - **Njia ya rejista:** `certificate.asset.fingerprints` (inafanana kabisa na msimbo wa uthibitisho).
> - **signer_sig katika rejista:** Sehemu ya `proof.signer_sig` inahitajika kwa Full Verify.
> - Utaratibu wa SignerSignature utaamilishwa katika Awamu ya 2 na Solana Wallet Adapter; katika v1.0, uthibitisho unaweza kufanywa na `attestation_pubkey`.

---

## 📈 Takwimu za Matumizi (Malengo ya Q1 2026)

| Kipimo | Lengo | Hadhi |
|--------|--------|--------|
| **Jumla ya Hati** | 1,000 | 🔄 Inaendelea |
| **Watumiaji Hai** | 500 | 🔄 Inaendelea |
| **Idadi ya Uthibitisho** | 5,000 | 🔄 Inaendelea |
| **Wakati wa Kuwa Hai** | 99.9% | ✅ Hai |
| **Wastani wa Muda wa Majibu** | <200ms | ✅ Bora |

---

## 🌍 Jamii na Usaidizi

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Wavuti:** [ilhanart.org](https://ilhanart.org)
- **Barua pepe:** galeri@ilhanart.org

---

## 🙏 Wachangiaji

Itifaki ya PoArt inaendelea kukua na michango kutoka kwa jamii ya chanzo wazi.

**Kuchangia:**
1. Fork hifadhi
2. Unda tawi la kipengele (`git checkout -b feature/amazing-feature`)
3. Commit (`git commit -m 'Add amazing feature'`)
4. Sukuma (`git push origin feature/amazing-feature`)
5. Fungua Ombi la Kuvuta

### 🛠️ Tunahitaji Nini Sasa? (Wito wa Msaada)

Itifaki ya PoArt inatafuta wasanidi programu wenye uzoefu katika maeneo yafuatayo kwa maendeleo ya **Awamu ya 2**:

* **Kazi za Supabase Edge:** Hamisha ulinzi wa spam kwenye upande wa seva.
* **Solana Web3.js:** Ujumuishaji wa saini ya pochi.
* **IPFS / Arweave:** Ujumuishaji wa huduma za kuhifadhi na kupachika.

> Tafadhali anzisha mjadala katika kichupo cha "Masuala" kabla ya kuongeza kipengele.

---

**Itifaki ya [PoArt] Proof of Art v1.0**  
*"Utamaduni > Mtaji"*

## 🧾 Leseni

Leseni ya MIT © 2026 Ilhan Art Gallery Initiative

Angalia [![Leseni](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) kwa masharti kamili.

---

## 💬 Sifa

![Toleo](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Usalama](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Jukwaa](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![Leseni](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Mradi huu umetengenezwa na mpango wa [Ilhan Art Gallery], na msimbo wake wa chanzo unapatikana hadharani kwa uwazi.**

**ITIFAKI V1.0 // IMEWEKWA MUHURI NA SHA-512**

*© 2026 İLHAN ART | HAKI ZOTE ZIMEHIFADHIWA KWA KAZI ZA SANAA, TASWIRA NA MAWAZO.*

---
