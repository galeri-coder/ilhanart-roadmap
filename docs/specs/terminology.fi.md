# 📚 TERMINOLOGIA JA KÄSITTEET -SANASTO
> **"Tämän protokollan kielen ymmärtäminen on sen vision ymmärtämistä."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Ydininfrastruktuuri

**PoArt Forensic Engine (PFE)** edustaa [PoArt]-protokollan taustalla olevaa ydinlogiikkaa ja teknistä toimintaa. Tämä on "forensinen moottori", joka ottaa taideteoksen raakadatan ja muuntaa sen todennettavaksi ja muuttumattomaksi **digitaaliseksi todisteeksi**.

### 🧩 Miksi "PoArt Forensic"?

- **PoArt (Proof of Art):** Moottorin keskiössä on digitaalisen omaisuuserän arvon sitominen spekulaation sijaan **todennettavissa olevaan tuotantoprosessiin**.
- **Forensic (Oikeustieteellinen todentaminen):**
  - **Tekninen määritelmä:** Algoritmi- ja kirjausketjulähestymistapa, jolla todennetaan, ettei tuotantoprosessin dataa (siveltimenvedot, timelapse, lokit) ole manipuloitu.
  - **Filosofinen taso:** Väite, jolla tekoälyn "välitön tuotos" muunnetaan mitattavaksi todellisuudeksi; **ihmisen aikaa, vaivannäköä ja päätöksenteon hintaa** sisältävä tuotanto.

> Huom: Lohkoketjuintegraatio (esim. Solana) ei ole PFE:n ydin; se käsitellään erikseen **Chain Anchor Layer** -kerroksena todentamista/rekisteröintiä varten.

### 🛠️ v1.0 Tekninen laajuus

**PoArt Forensic Engine (PFE) v1.0** on rakennettu monimutkaisten rahoitusmallien sijaan näiden **3 pääpilarin** varaan:

1. **Hashing & Sealing (Sinetöinti):**  
   PFE käsittelee Evidence Pack -paketin kaikki elementit (teostiedosto, video, JSON/loki, allekirjoitus jne.) deterministisesti ja tuottaa yksilöllisen **NotarySeal**-arvon.

   **Ydinkäsitteet (v1.0):**
   - **FileHash (teoksen sormenjälki):** Teostiedoston tavuista tuotettu tiiviste.
   - **EvidenceRoot (todistuspaketin juuri):** Evidence Pack -paketin eheyttä edustava juuriyhteenveto (Merkle root tai kanoninen manifest-tiiviste).
   - **NotarySeal (lopullinen sinetti / PFE Output):** EvidenceRoot + aika + allekirjoitus -yhdistelmästä tuotettu lopullinen sinetti.

   **Kaavat (sijoittajalle selkeästi näkyvässä muodossa):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload -määritelmät (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Huom: PFE-tuotoksena tarkoitettu arvo on **NotarySeal**. **SignerSignature**-mekanismi otetaan käyttöön vaiheessa 2 (Solana Wallet Adapter -integraatiolla); nykyisessä v1.0:ssa käytetään järjestelmän omaa attestation-allekirjoitusta. Attestation public key julkaistaan rekisterissä `issuer.attestation_pubkey`-kentässä.

2. **Indexing (Arkistointi):**  
   Kirjaa läpinäkyvään ja kyselykelpoiseen rekisterikerrokseen, mikä lompakko, milloin ja mille teokselle on esittänyt **Labor Proof (Työtodiste)** -dokumentin.  
   *(Tämä kerros voi olla tietokanta; lohkoketjuintegraatio määritellään erikseen "Chain Anchor Layer" -kerroksena.)*

3. **Verification (Todentaminen):**  
   Kun teoksen aitous kyseenalaistetaan, PFE käsittelee raakadatan uudelleen; testaa matemaattisella varmuudella, vastaavatko lasketut **EvidenceRoot / NotarySeal** -arvot arkiston tietueita.

---

### 🧮 PoArt-arvoteoreema (The Value Theorem)

[PoArt]-protokolla yhdistää digitaalisen omaisuuserän arvon ($V$) subjektiivisen markkinakäsityksen sijaan **tuotantoprosessin fyysiseen todellisuuteen**.

Tekoäly (AI) tuhoaa prosessin tuottamalla tuloksen välittömästi ($t \to 0$). [PoArt] käsittelee arvoa **ajan, työn ja tahdon** komponenttien kertymänä.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Muuttujien määritelmät

- **$\int dt$ (Prosessin kertymä):**  
  Arvo ei ole välitön "tuotos" (output); se on **prosessi**, joka kertyy $t_{\text{start}}$:n ja $t_{\text{end}}$:n välillä. Kun aika lyhenee (tekoälytuotanto), integraalin tulos lähestyy nollaa.

- **$P_{\text{labor}}(t)$ (Hetkellinen työpanos):**  
  Edustaa tuotantohetkellä käytetyn henkisen ja fyysisen ponnistuksen intensiteettiä. Kun todennettavissa oleva ponnistus kasvaa, integrandi kasvaa.  
  > Huom: Tätä termiä voidaan käytännössä normalisoida "mitattavissa/todennettavissa olevien työsignaalien" perusteella.

- **$I_{\text{agency}}(t)$ (Tahtokerroin):**  
  Tuottajan riskinotto- ja päätöksentekokyky. Saa arvon välillä $0$ ja $1$.
  - **AI ($I \approx 0$):** Suorittaa komentoja, ei ota riskejä, ei maksa hintaa.
  - **Ihminen ($I \to 1$):** Muuttaa päätöksiä, epäröi, ottaa riskejä.

- **$U_{\text{irreversible}}$ (Peruuttamaton ainutlaatuisuus):**  
  Digitaalisessa tuotannossa kumous (`Ctrl+Z`) on mahdollinen; fyysisessä tuotannossa (kankaalle levitetty maali, veistetty marmori, suoran lähetyksen ele) ei ole paluuta. Tämä **peruuttamattomuus** on lisätermi, joka luo teokseen "ainutlaatuisuuden" (non-fungible-luonteen).

### 🔎 Tapausanalyysi: AI "Välitön tuotos" vs. Ihmisen "Todennettu prosessi"

Seuraava skenaario osoittaa, miten **PoArt-arvoteoreema** toimii käytännössä ja miksi tekoälytuotokset saavat alhaisen pistemäärän [PoArt]-standardissa.

#### Skenaario A: Kuvan tuottaminen tekoälyllä 10 sekunnissa

- **Kesto ($\Delta t$):** $10$ sekuntia (prosessia ei käytännössä ole)
- **Työpanos ($P_{\text{labor}}$):** $1$ yksikkö (vain komennon kirjoittaminen)
- **Tahtokerroin ($I_{\text{agency}}$):** $0.01$ (ei riskiä, ei hintaa)
- **Peruuttamattomuus ($U_{\text{irreversible}}$):** $0$ (kumottavissa / kopioitavissa)

**Tulos:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Tulkinta:** Vaikka tuotos olisi virheetön; koska prosessia ei koettu eikä se sisällä tahtoa/riskiä, [PoArt]-arvo lähestyy $0$:aa.

#### Skenaario B: 6 tunnin fyysinen tuotanto suorassa lähetyksessä

- **Kesto ($\Delta t$):** $6$ tuntia ($21{,}600$ sekuntia)
- **Työpanos ($P_{\text{labor}}$):** $0.5$ yksikköä (fyysisen ja henkisen ponnistuksen jatkuvuus)
- **Tahtokerroin ($I_{\text{agency}}$):** $0.9$ (päätösten muuttaminen, riskinotto, peruuttamattomat valinnat)
- **Peruuttamattomuus ($U_{\text{irreversible}}$):** $>0$ (fyysisiä jälkiä ei voi kumota)

**Tulos:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Tulkinta:** Kun prosessi pitenee ja tahto (riski) kasvaa, arvo kertyy kumulatiivisesti. $U_{\text{irreversible}}$-termi on lisäpanos, joka luo teokseen "ainutlaatuisuuden" (non-fungible-luonteen).

---

### ✅ Johtopäätös: Arvon lukitseminen todisteeseen (Proof-Bound Value)

Tämä teoreema muuttaa [PoArt]:n arvoväitteen "tykkäyksestä" tai "markkinatarinasta" **todistettavissa olevaksi tuotantotodellisuudeksi**.

1. **Ilman prosessia ei synny arvoa:**  
   Tekoäly tuhoaa prosessin välittömällä tuotoksella ($t \to 0$). Kun prosessin aikaikkuna kapenee, integraalin tulos pienenee matemaattisena välttämättömyytenä:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Tahto ja riski ovat kertoimia:**  
   [PoArt] ei mittaa vain "kulutettua aikaa"; se mittaa myös todellista päätöksentekoa, riskiä ja hintakerrosta tuon ajan sisällä. Riskinottoa välttävän (AI) tuotannon arvo on alhainen:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Ainutlaatuisuus on fyysinen todiste, ei markkinointia:**  
   Fyysisessä tuotannossa peruuttamattomat jäljet (kankaan isku, marmorin halkeama) ovat digitaalisen `Ctrl+Z`-logiikan ulkopuolella. Tämä peruuttamattomuus ($U_{\text{irreversible}}$) tekee teoksesta ontologisesti ainutlaatuisen.

> **🔐 YHTEENVETO:** Vaikka arvoteoreema vaikuttaa mittauksellisesti epävarmalta (vaikka sen tarkkaa vastinetta ei voida 100% mitata todellisessa elämässä), tämän kaavan tarkoitus on osoittaa muuttujien rakenne ja suunta. Tekoälyaikakaudella harvinaista ei ole "kuva"; **se on todennettavissa oleva työ, aika ja tahto.** [PoArt] mittaa tätä niukkuutta ja rekisteröi sen **Evidence Pack** -paketilla.

### 🏛️ "Engine" (Moottori) -käsitteen merkitys

Pump.fun:sta tai vastaavista alustoista tulevat tokenit ovat usein vain **"pääsylippuja"**. **PoArt Forensic Engine (PFE)** on **perustuslaillinen logiikkakerros**, joka määrittelee, mitä oikeuksia tuo lippu suojaa, miten työ kirjataan ja miten taide/tiede/teknologia säilytetään.

> **Huom:** Syy tämän projektin aloittamiseen Pump.fun:ssa on se, ettemme saavuttaneet riittävää likviditeettiä ja seuraajamäärää. Vaikka olemassa olevan datan käyttäminen ei ole strategisesti optimaalista, voimme sanoa, että se oli oikea liike. Budjetista ja resursseista riippumatta tämän moottorin logiikan määrittely GitHubissa todistaa, että projekti ei ole vain taloudellinen spekulaatio, vaan pitkän aikavälin **ohjelmistoinfrastruktuuri** ja **digitaalinen kansalliskirjasto** -visio.

---

## 🎨 [PoArt] TYÖTODISTE-PROTOKOLLA (Proof of Art Protocol v1.0)

> **"Todellinen taiteilija, todellinen tuotanto, todellinen arvo."**

Tämä protokolla on **biologinen ja älyllinen puolustusmekanismi**, joka on kehitetty kryptoekosysteemiä ympäröiviä anonyymeja huijareita, 5 minuutissa tuotettuja tekoälykuvia ja "Pump & Dump" (Pumppaa ja dumppaa) -kulttuuria vastaan.

---

## a) Mikä on [PoArt]? (Filosofinen ja tekninen määritelmä)

**Proof of Art [PoArt];** on institutionaalinen todentamisstandardi, joka takaa, että lohkoketjussa olevan omaisuuserän taustalla oleva arvo perustuu spekulaation sijaan todennettavissa olevaan **ihmistyöhön**, **aikaan** ja **fyysiseen energiaan**.

Kuten Bitcoin tuottaa arvoa *"Sähköllä ja prosessoriteholla"* **(Proof of Work)**, myös [PoArt]-yhteensopivat projektit tuottavat arvoa *"Käytetyllä taidolla ja ihmisajalla"*. Ne "stakettavat" aikaa.

Se eliminoi Pump.fun:n ja DEX-alustojen *"Kehittäjä (Dev) myi, projekti päättyi"* -riskin; sillä tässä arvo ei ole koodissa, vaan **tuotannon jatkuvuudessa**.

> **[PoArt] ei sano osallistujalleen "Luottakaa meihin"; se sanoo "Tässä ovat todisteet, näe omin silmin, todenna matematiikallasi".**

---

## b) [PoArt] 5-osainen standardi (The 5 Pillars of Truth)

Nämä 5 kohtaa ovat manipuloimattomia suodattimia, jotka projektin on läpäistävä saadakseen [PoArt]-sinetin.

### 1) Reaaliaikainen henkilöllisyystodiste (Live Identity Proof)

- **Ongelma:** Kryptomaailma on täynnä tuntemattomia anonyymeja perustajia (Devejä), jotka keräävät rahat ja hylkäävät projektin.
- **[PoArt]-ratkaisu:** Tuottaja todistaa paitsi henkilöllisyystodistuksensa, myös **läsnäolonsa tuotantohetkellä**. Tähän sisältyy suoria lähetyksiä, joissa ollaan vuorovaikutuksessa yhteisön kanssa ja täytetään välittömiä erityispyyntöjä – ei ennalta nauhoitettuja videoita.  
  (Esim: *"Kirjoita kankaan oikeaan kulmaan tämän päivän päivämäärä ja nykyinen lohkonumero"*)
- **Motto:** *"Botit voivat maalata, mutta botit eivät hikoile eivätkä improvisoi."*

### 2) Työ- ja prosessitodiste (Labor & Process Proof)

- **Ongelma:** 2 sekunnissa tuotetut tekoälykuvat ja 2 kuukaudessa tehty öljymaalaus saavat saman "jpeg"-kohtelun digitaalisessa maailmassa.
- **[PoArt]-ratkaisu:** Teoksen "raskaus- ja syntymäprosessi" dokumentoidaan. Luonnosvaiheet, maalikerrokset, kertyneet tunnit ja taiteilijan fyysinen prosessi teosta luodessa dokumentoidaan. Tämä lisää tokeniin **"Aikakustannuksen" (Time Cost)**. Mitä vaikeampi omaisuuserän tuottaminen, sitä vakaampi sen arvo.

### 3) Esteettinen arvotodiste (Aesthetic Value Proof)

- **Ongelma:** "Meemi"-kulttuuri, joka sivuuttaa estetiikan ja taiteellisen syvyyden keskittyen vain hetkelliseen huumoriin, ja tästä johtuvat lyhytikäiset "Hype"-projektit.
- **[PoArt]-ratkaisu:** Projektilla on oltava akateemiset taidestandardit, väriteoria, sommittelusäännöt ja materiaalituntemus (Impasto, tekstuuri jne.). Sisällön ei pidä vain naurattaa; sen pitää herättää ihailua katsojassa ja olla **keräilyarvoinen**.

### 4) Käsitteellinen innovaatio (Conceptual Novelty)

- **Ongelma:** Tuhansia toistensa kopioita olevia koira/kissa-kolikoita vailla luovuutta.
- **[PoArt]-ratkaisu:** Projektin on rakennettava uusi silta, joka yhdistää taiteen, tieteen, filosofian tai teknologian mielekkäällä tavalla.  
  (Esim: Klassisen Daavidin veistoksen yhdistäminen kryptomarkkinadataan; ihmisten käsityksen "kiveytymisen" käsittely ja sen perustaminen tieteellisiin lähteisiin.)  
  Teoksen on oltava paitsi visuaalinen juhla, myös älyllinen haaste, joka saa pohtimaan **tiedettä, filosofiaa tai teknologiaa**.

> [!IMPORTANT]
> **Referenssiesimerkki (Las Palmitas -vaikutus):**  
> Meksikon rikollisuudesta kärsivässä Las Palmitasin naapurustossa yli 200 taloa muutettiin massiiviseksi sateenkaaren juhlaksi. Tämän esteettisen intervention seurauksena alueen rikollisuusaste laski tietyssä määrin, ja nuoret alkoivat kiinnostua taiteesta jengien sijaan. Esteettinen muutos koodasi uudelleen ihmisten kunnioituksen ympäristöään ja toisiaan kohtaan (Social Cohesion).
>
> **Odotus:** [PoArt]-listalle pääsevän projektin on, aivan kuten yllä olevassa esimerkissä, sisällettävä pelkän visuaalisen estetiikan lisäksi sosiologinen, tieteellinen tai filosofinen syy-seuraus-suhde. Koska aika on ainoa omaisuuserä, jota ei voi ostaa rahalla, tässä protokollassa aika on stakettava vakuutena ja todistettava. Projektin käsitteellisen perustan on oltava niin vahva ja universaali, että mahdollisessa CTO (Community Take Over) -skenaariossa vuosien päästä yhteisö voi periä tämän perinnön ja jatkaa projektin innovatiivista potentiaalia autonomisesti.

### 5) Ei-algoritminen tahto (Non-Algorithmic Agency)

- **Ongelma:** Virheettömät mutta sieluttomat, toisiaan toistavat digitaaliset tuotokset.
- **[PoArt]-ratkaisu:** Ihmisen ainutlaatuisen tahdon, joka voi tehdä virheitä, ottaa riskejä ja kokea tunnevaihteluja, on oltava aistittavissa teoksessa. Siveltimenvetojen epävarmuus, materiaalin odottamattomat reaktiot ja taiteilijan hetkelliset päätökset ovat **Biologinen allekirjoitus**, joka erottaa teoksen "Konetuotannosta".

---

## c) Todentamis- ja huijauksenestomekanismi

Tämä järjestelmä varmistaa, että projekti pysyy luotettavana ja elävänä paitsi "alussa", myös "ikuisesti".

### 📦 Todistuspaketti (Evidence Pack - The Digital Twin)

Jokaisen [PoArt]-sertifioidun teoksen takana on salattu ja aikaleimalla varustettu datapaketti, jonka sijoittajat voivat ladata:

- **RAW-videotallenteet:** Tuotantohetken keskeytymättömät raakakuvat.
- **Metadata-analyysi:** Tiedoston luontipäivä, käytetyn laitteen tiedot ja sijaintitiedot (Kaupunki-Maa).
- **Fyysiset viitteet:** Todisteet siitä, että teos on olemassa fyysisessä maailmassa  
  (Esim: Teoksen vieressä oleva päivän sanomalehti tai sen hetkinen lohkoketjudata).

> *Johdonmukaisuushuomautus:* "todistuspaketti"-ilmaisu yhdistyy edellisten osioiden **Evidence Pack → EvidenceRoot → NotarySeal** -ketjuun; eli paketin eheys edustetaan todennettavalla sinetillä.

### 🔄 365 päivän uusiminen (The Sustainability Protocol)

- **Vallankumouksellinen ominaisuus:** Kryptoprojekteissa "Dev" (Kehittäjä) lanseeraa tokenin ja yleensä katoaa 1-2 kuukauden kuluttua (Soft Rug). [PoArt] tekee tästä mahdotonta.
- **Sääntö:** "Verified Artist" (Todennettu taiteilija) -status ei ole elinikäinen. Se on voimassa vain **1 vuoden**.
- **Toiminta:** Taiteilijan/kehittäjän on esitettävä yhteisölle joka 365. päivä **uusi, merkittävä ja todennettavissa oleva teos**.
- **Esimerkkiskenaario:** Aloititte projektin vuonna 2026. Tammikuussa 2027 järjestelmä antaa "Todistusaika päättynyt" -varoituksen. Jos taiteilija ei esitä uutta näyttelyä, uutta fyysistä teosta tai uutta teknologista integraatiota, projektin "Luottamusmerkki" laskee.
- **Tulos:** Tämä järjestelmä varmistaa, että **sisältö ei koskaan vanhene** ja sijoittajan ei tarvitse pelätä *"Onko kehittäjä vielä täällä?"*. Projekti muuttuu eläväksi studioksi.

### 🚩 Punainen lippu (Red Flag Protocol)

**Kun yhteisö tai algoritmit havaitsevat huijauksen (tekoälyn käyttö, varastettu teos, manipuloitu video):**

1. Sertifikaatti merkitään välittömästi **"MITÄTÖN" (VOID)**.
2. Todistuspaketit merkitään julkisesti **"Väärennös"**.
3. Projekti lisätään [PoArt]-mustalle listalle. Tämä vahvistaa todellisuutta, jonka mukaan hajautetussa maailmassa **maine on ainoa valuutta**.
4. Missään julkaisussa ei saa käyttää [PoArt]-ilmaisuja, ainoa kelvollinen lähde on https://www.ilhanart.org/public-registry

---

## d) Johtopäätös: Kasino vai museo

**Pump.fun ja hajautetut pörssit (DEX) ovat valitettavasti tällä hetkellä kasinoita; valot vilkkuvat, kaikki tavoittelevat nopeita voittoja ja talo (huijarit) voittaa aina. Syy projektin aloittamiseen täällä on myös yritys parantaa tätä paikkaa, ja meillä on nykyinen datamme ja suorat lähetykset tavoittaaksemme nykyisen yleisön.**

**[PoArt] on linnoitus, joka on rakennettu tämän kasinon keskelle.**

- 🎰 Kasino perustuu korttipeleihin; me perustumme **fyysiseen todellisuuteen**.
- 🃏 Kasino on altis huijaukselle; me olemme avoimia **läpinäkyville todisteille**.
- ⏳ Kasino on väliaikainen; me keskitymme **taiteen ja tieteen ikuisuuteen**.

**Tätä protokollaa käyttävä token ei ole vain "kolikko"; se on digitaalinen osake, jonka takana on hikeä, maalia, koodia ja filosofiaa.**

---

## 🗳️ 6) HALLINTO JA JULKINEN REKISTERI (Governance & Public Registry)

**Tämän osion tarkoitus on: muuttaa [PoArt]-standardi "henkilöihin luottamisesta" kestäväksi julkiseksi infrastruktuuriksi rekisteröinnin + todentamisen + yhteisövalvonnan avulla.**

### 6.1 Public Registry (Julkinen rekisteri)

- **Public Registry:** Kaikki hyväksytyt tiedot tallennetaan osoitteeseen `ilhanart.org/registry` (tai GitHub Registry).

**Rekisteröintilogiikka (ehdotettu standardi - JSON-polkumuodossa):**

Jokainen rekisteriin tuleva merkintä sisältää vähintään seuraavat todennettavat ydinkentät:

- **Identiteetti ja status:**
  - `certificate_id` (luettava viite)
  - `status` (active / void)
  - `void_reason` (jos on)
  - `visibility` (private / masked / public)
  - `created_at` (aikaleima)

- **Myöntävä taho:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Teostiedot:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (jos mahdollista; tokenin haltijan tunnistamiseen)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Forensiset tiedot:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Kryptografiset todisteet:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Hallinto:**
  - `governance.decision`
  - `governance.review_notes`

Rekisterillä voi olla kaksi kerrosta:
- **1)** Ihmisen luettava indeksi (web-listaus / haku / suodatus)
- **2)** Koneluettava manifesti (JSON-tietueet; PFE-todentamiseen)

**Tässä oleva "rekisteri" tulee todennettavaksi PFE:n Evidence Pack → EvidenceRoot → NotarySeal -ketjulla. Rekisteri tarjoaa todentamiskohteen, ei "väitettä".**

---

### 6.2 PoArt Verified -hakuprosessi

**PoArt Verified -hakemukset arvioidaan İlhanArt Galleryn toimesta 5 PoArt-standardin mukaisesti. Yhteisön palaute otetaan huomioon, mutta lopullinen päätös on kuratoriaalisella tiimillä. Päätökset julkistetaan läpinäkyvästi ja tallennetaan ilhanart.org/registry-rekisteriin.**

#### Hakuprosessi

**Hakemus:**
- Taiteilija/projekti tekee PoArt Verified -hakemuksen
- Evidence Pack valmistellaan (videotallenteet, metadata, suorien lähetysten linkit)
- Hakemus lähetetään İlhanArt Gallerylle

**Arviointi (30 päivää):**
- Gallerian tiimi arvioi Evidence Pack -paketin yksityiskohtaisesti
- Kaikki 5 PoArt-standardia tarkistetaan:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Haastattelu taiteilijan kanssa (valinnainen)

**Yhteisön konsultointi:**
- Evidence Pack jaetaan julkisesti hakuprosessin aikana
- Yhteisö voi antaa palautetta ilhanart.org:n kautta
- Tokenin haltijat (vähintään 10 000 $CULTURE) voivat erityisesti antaa ehdotuksia
- **Kaikki palaute otetaan huomioon arviointiprosessissa**
- **Lopullinen päätös perustuu kuitenkin kuratoriaaliseen arviointiin**

**Päätös:**
- Galleria hyväksyy tai hylkää hakemuksen
- Päätöksen perustelu julkistetaan läpinäkyvästi
- Jos hyväksytään → PoArt Verified -merkki
- Jos hylätään → Uuden hakemuksen voi tehdä 6 kuukauden kuluttua

**Läpinäkyvyys:**
- Kaikki hakemukset ja päätökset tallennetaan ilhanart.org/registry-rekisteriin
- Päätöstietue julkaistaan:
  - Hakemuspäivä
  - Arviointiprosessin yhteenveto
  - Päätös (Approved / Rejected)
  - Päätöksen perustelu (lyhyt selitys)
  - Yhteisön palautteen yhteenveto (anonyymi)

#### Miksi kuratoriaalinen päätös?

**Laadunvalvonta:**  
PoArt Verified -status on korkeiden standardien merkki. Kuratoriaalinen arviointi takaa näiden standardien säilymisen.

**Spekulatiivisen manipuloinnin estäminen:**  
Pump.fun-tokeneilla täysin ketjussa tapahtuva hallinto (esim: Realms, DAO-äänestys) ei ole teknisesti mahdollista. Ketjun ulkopuoliset äänestysjärjestelmät ovat alttiita valasmanipulaatiolle ja koordinoiduille hyökkäyksille. Kuratoriaalinen päätös poistaa tämän riskin.

**Operatiivinen tehokkuus:**  
Monimutkaisten äänestysmekanismien sijaan nopea ja selkeä päätösprosessi. Taiteilijat saavat tuloksen 30 päivän kuluessa.

**Yhteisön osallistuminen:**  
Yhteisön palaute otetaan täysin huomioon ja vaikuttaa päätösprosessiin. Lopullinen päätös on kuitenkin manipulaatiolta suojatulla kuratoriaalisella tiimillä.

**Tulevaisuus:**  
Kun projekti kypsyy (2027+), yhteisön konsultointimekanismia voidaan vahvistaa. Kuratoriaalinen standardisuoja säilyy kuitenkin pysyvänä.

---

### 6.3 Token Utility (Tokenin käyttötarkoitukset)

**$CULTURE-tokenin haltijoille tarjotut edut:**

**1. Galleriatilaisuuksien prioriteettipääsy:**
- Oikeus 1 viikon näyttelyyn vuodessa İlhanArt Galleryssa (oikeus siirrettävissä)
- Drop painting -alennukset
- 10-30% alennus gallerian maalauksista

**2. PoArt Registry -täysi pääsy:**
- Kaikkien todennettujen teosten yksityiskohtaiset tietueet
- Evidence Pack -pakettien täydet versiot
- Forensic-todentamistyökalut

**3. Neuvoa-antava äänestys:**
- Neuvoa-antava oikeus PoArt Verified -hakemuksissa
- Pääsy yhteisön palautekanaviin
- Osallistuminen hallintokeskusteluihin

**4. Eksklusiivinen sisältö:**
- Studio behind-the-scenes -sisällöt
- Taiteilijoiden haastattelut ja prosessivideot
- Pääsy tekniseen dokumentaatioon

**Huom:**  
Tokenin haltijat antavat advisory vote (neuvoa-antava ääni). Lopullinen päätös kuuluu kuratoriaaliselle tiimille. Tämä rakenne on valittu valasmanipulaation ja spekulatiivisten hyökkäysten estämiseksi. Staking-palkkioita ei ole, koska etsimme pitkäaikaisia kulttuurisia osallistujia, emme lyhytaikaista palkkasoturipääomaa.

---

### 6.4 Metadata Sync (Synkronointi fyysisen maailman kanssa)

- **Metadata Sync:** Rekisterin teknisten tietojen on vastattava 100% fyysistä omaisuuserää.

**"100% vastaavuuden" tekninen määrittely (ehdotettu selkeys):**

- **Minimivastaavuus (pakollinen):**
  - Rekisterin `asset.fingerprints.sha256/sha512` ja käsillä olevan tiedoston tiiviste ovat **täsmälleen samat**.
  - Rekisterin `proof.notary_seal` uudelleen tuotettuna (jos Evidence Pack on käytettävissä) on **täsmälleen sama**.

- **Fyysisen viitteen vastaavuus (todistetyyppi):**
  - Suorassa lähetyksessä näytetyn fyysisen teoksen + päivämäärä/lohkoviitteen kaltaisten todisteiden on oltava johdonmukaisia Evidence Pack -paketin kanssa.

- **Yksityisyysyhteensopivuus:**
  - `masked`-näkyvyydessä IP/sijainti-kaltaiset kentät julkaistaan **maskausstandardin mukaisesti**.

---

### 6.5 Valitus, tarkistus ja peruutus (Dispute & Revocation)

Rekisteri ei ole vain "hyväksyntämekanismi"; se on **elävä valvontamekanismi huijausta vastaan**.

- Kun valitus käynnistetään, tietue voidaan asettaa **"review"**-tilaan.
- Jos huijaus havaitaan, se merkitään `status: void` ja perustelu lisätään:
  - `void_reason` (tekoälyn käyttö / varastettu / manipuloitu jne.)
  - `revoked_at` (peruutusaika)
- Peruutuspäätöksen lähde näkyy selvästi rekisterissä:
  - kuratoriaalinen arviointi / yhteisön valitus / forensinen analyysimerkintä (kumpi soveltuu)

> **Tämä osio on "Red Flag Protocol" -osion VOID-käsitteen rekisterivastine.**

---

### 6.6 Esimerkkirekisteritietue (Koneluettava)
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

> *Huom: `asset.fingerprints.sha512` ja muut tiivistearvot on lyhennetty esitystarkoituksessa; todellisessa sovelluksessa käytetään täyspitkää heksadesimaalimerkkijonoa.*

---

## 7) 🔐 TEKNINEN SINETTI (NOTARY SEAL)

**PoArt Forensic Engine (PFE) v1.0:n** tuottama horjumaton sinettialgoritmi:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Digitaalinen notaari ja forensinen todistusprotokolla (Beta v1.0)

> **"Kulttuuri on suurempi kuin pääoma. Suojaa teoksesi tänään, vie ne huomiseen."**

---

## Miksi julkinen?

Todellinen turvallisuus tulee läpinäkyvyydestä. **Public Registry (Julkinen rekisteri)** -järjestelmämme ansiosta kuka tahansa missä päin maailmaa voi sekuntien kuluessa todentaa, onko hänen hallussa oleva tiedosto aito, ilman mitään viranomaista.

---

## 🧩 Miksi on useita "Näkyvyysmoduuleja"?

Koodin kriittisin osa on tässä (visibility select -valikko). Nämä vaihtoehdot mahdollistavat käyttäjien **"Yksityisyys vs. Läpinäkyvyys"** -tasapainon:

### 🔒 Yksityinen (Private)

- **Skenaario:** Taiteilija ei halua vielä julkaista teosta, mutta haluaa asettaa aikaleiman ja todistaa "tein tämän tänä päivänä".
- **Mitä koodi tekee:** Kirjoittaa datan tietokantaan mutta asettaa `visibility: "private"` -tunnisteen. Tulevaisuudessa "Public Read" -käytäntöä kirjoittaessa voit käyttää `WHERE visibility = 'public'` piilottaaksesi nämä tietueet yleisöltä.

### 🕶️ Maskattu (Masked)

- **Skenaario:** Taiteilija haluaa läpinäkyvyyttä mutta pelkää kotiosoitteensa (IP-sijainnin) löytymistä.
- **Mitä koodi tekee:** JavaScript-puolella `maskIP`- ja `maskLoc`-funktiot suoritetaan. Muuntaa IP-osoitteen muotoon `88.241.***.***` ja sijainnin muotoon `***/TR` ja lähettää sensuroituna tietokantaan.
- **Yksityisyyshuomautus:** Maskaus tehdään selaimessa, Supabase ei näe todellista sijaintia. **Kuitenkin:** Jos sijaintidataan käytetään kolmannen osapuolen API:eja kuten ipapi.co, nämä palveluntarjoajat näkevät IP-osoitteen pyynnön hetkellä.
- **Sinetöinti Masked-tilassa:** EvidenceRoot- ja NotarySeal-laskenta tehdään maskatulla forensics-datalla; näin todentaminen pysyy deterministisenä.

### 🌍 Julkinen (Public)

- **Skenaario:** Täysi läpinäkyvyys. [PoArt]-standardin mukaisesti ilmoitetaan selvästi, missä, milloin ja mistä verkosta teos on sinetöity.

---

## 💡 Teknologinen innovaatio

PoArt ei ole vain tiedostonlatausjärjestelmä. Se on **"Forensinen todistusketju" (Forensic Chain of Custody)** -moottori, joka sulattaa kolme eri teknologiakerrosta yhteen ja tuo uuden standardin.

**Tässä osiossa "moottorina" kuvattu kerros vastaa aiemman terminologian PoArt Forensic Engine (PFE) -ydintä.**

### 1) Client-Side Hashing (Maksimaalinen yksityisyys)

Teostiedostojasi ei koskaan ladata palvelimelle. Selainpohjainen (Client-side) moottorimme laskee tiedoston tiivisteen (digitaalisen yhteenvedon) omalla tietokoneellasi. Palvelimelle lähetetään vain tämä sormenjälki ja metatiedot.

> **Yksityisyyshuomautus:** Teostiedostoa ei ladata palvelimelle ja se suojataan näin. Forensics-data (IP/sijainti) jaetaan kuitenkin valitun näkyvyystilan (private/masked/public) mukaan.

### 2) Forensic Data Fusion (Forensinen voima)

Se on paljon enemmän kuin tavallinen aikaleima (Timestamp). Järjestelmä yhdistää seuraavat tiedot yhteen "Genesis-sinettiin":

- **Digitaalinen yhteenveto (SHA-512):** Kryptografinen tiiviste (SHA-512) -standardia käyttäen digitaalinen sormenjälki, joka rikkoutuu, jos yksikin pikseli teoksessa muuttuu.
- **Sijainti ja aika:** Tapahtuman millisekunnin tarkkuudella oleva päivämäärä, maa, kaupunki ja alue.
- **Laitetunnus:** Käyttöjärjestelmä, selain ja laitetyyppi (User-Agent-analyysi).

---

## 🛡️ Käyttötarkoitukset ja hyödyt

Jos olet taiteilija, kirjailija tai suunnittelija, "Tein tämän aiemmin" sanominen ei riitä, sinun on todistettava se.

**PoArt:lla sinetöity teos:**

- **Matemaattinen todiste:** Järjestelmä huomaa, jos yksikin pikseli tiedostossasi muuttuu. Manipulointi on mahdotonta.
- **Oikeudellinen perusta:** On kirjattu, minä päivänä, missä kaupungissa ja millä laitteella teos on sinetöity.
- **Välitön sertifikaatti:** Tuottaa sekunneissa sinulle erityisen, QR-koodilla ja sinetillä varustetun **"Omaisuuserän identiteettisertifikaatin"**.

---

## ⚙️ Järjestelmäarkkitehtuuri ja tekniset ominaisuudet

Järjestelmä on suunniteltu "Serverless" (Palvelimeton) -arkkitehtuurille, keskittyen korkeaan suorituskykyyn ja skaalautuvuuteen.

| Kerros | Teknologia | Selitys |
|--------|-----------|----------|
| **Kryptografia** | SHA-256 & SHA-512 | Kaksikerroksinen kryptografinen tiiviste |
| **Tietokanta** | Supabase (PostgreSQL) | JSONB-datarakenne, RLS-käytännöt |
| **Forensinen data** | ipapi.co API | IP/Sijainti/Aika-kolmikko |
| **Renderöinti** | html2canvas + jsPDF | Client-side PNG/PDF-tuotanto |
| **Frontend** | Vanilla JavaScript | Nolla framework-riippuvuutta |
| **Turvallisuus** | Client-side hashing | Tiedosto ei koskaan lähde palvelimelle |

### Korostetut ominaisuudet

| Ominaisuus | Yksityiskohta | Kilpailijoilla? |
|---------|-------|-------------|
| **Vedä ja pudota UI** | Vedä ja pudota tiedosto, välitön esikatselu | ❌ Useimmilla ei |
| **Moniformaattivienti** | PNG, JSON, PDF - yhdellä napsautuksella | ⚠️ Rajoitettu |
| **Reaaliaikainen esikatselu** | Sertifikaatin live-esikatselu | ❌ Ei |
| **Yksityisyysasetukset** | Private/Masked/Public-vaihtoehdot | ❌ Ei |
| **Client-Side Hashing** | Tiedosto ei koskaan mene palvelimelle | ✅ Vain muutamalla |
| **Forensinen metadata** | IP, sijainti, laite, aika - kaikki yhdessä | ❌ Hajallaan |
| **QR-todentaminen** | Välitön todentamis-QR-koodi | ⚠️ Rajoitettu |
| **Rate Limiting** | Roskapostisuojaus (RLS + Client) | ❌ Useimmilla ei |

---

## 🗺️ Tiekartta: "Trustless"-tulevaisuus

Nykyinen versio **(Beta v1.0)** on optimoitu tarjoamaan loppukäyttäjälle maksimaalinen nopeus, helppo käyttöliittymä ja ilmainen pääsy. Lopullinen visiomme on kuitenkin siirtyä rakenteeseen, johon edes tietokantahallinnoija (me) ei voi puuttua.

### Vaihe 1: Beta v1.0 (Nyt julkaistu)

**Infrastruktuuri:**
- Cloud Database (Supabase)
- Off-chain-rekisteri (PostgreSQL + IPFS-varmuuskopio)
- Gallerian oma-attestointi (keskitetty mutta läpinäkyvä)

**Token:**
- Alusta: Pump.fun
- Likviditeetti: Raydium (automaattinen)
- Hallinto: Vain neuvoa-antava (yhteisön konsultointi)

**Tavoite:**
- Nopeus, UX-esteiden poistaminen
- "Kitkaton" turvallisuus
- Yhteisön rakentaminen

**Token Utility (v1.0):**
- Galleriatilaisuuksien prioriteettipääsy
- PoArt Registry -katselu
- Neuvoa-antava äänestysoikeus

---

### 🚀 Vaihe 2: Hajautettu auktoriteetti (2026 Q2-Q4)

Tämä vaihe kattaa siirtymän järjestelmän täysin "Client-Side" -rakenteesta turvallisempaan ja hajautetumpaan rakenteeseen.

| Ominaisuus | Mitä se tuo? | Tech Stack | Arvio |
|---------|---------------|------------|-----|
| **Edge Function INSERT** | Roskapostiesto + API Key -turvallisuus | Supabase Edge (Deno) | Q2 2026 |
| **Lompakkoallekirjoitus** | Hajautettu identiteetti | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave-varmuuskopio** | Hajautettu arkisto | IPFS SDK + Pinata | Q3 2026 |
| **Peruutusmekanismi** | Väärennetyn sertifikaatin peruutus | DB Schema Update | Q2 2026 |
| **Audit Log** | Forensinen kyselyloki | Custom logs -taulu | Q3 2026 |
| **OpenTimestamps** | Bitcoin-ankkurointi | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain-äänestys (x/web) + lompakkoallekirjoitus
- Yhteisön edustajien valinta (ensimmäiset 90 päivää)
- Multi-sig-operaatiolompakkojen hallinta
- Painotettu neuvoa-antava äänestys (valaskatto)

**Muuttumattomuus:**
- Rekisterin varmuuskopio IPFS-tiivisteillä
- Bitcoin-aikaleima-ankkurointi
- Cross-chain-todentamisen valmistelu

---

### Vaihe 3: Täysi hajauttaminen (2027+)

| Ominaisuus | Tavoite | Arvio |
|---------|-------|-----|
| **On-Chain-rekisteri** | Solana on-chain -tallennus | Q1 2027 |
| **Laajennettu Token Utility** | NFT-lyönti, edistyneet ominaisuudet | Q1 2027 |
| **Multi-Chain-tuki** | Ethereum, Polygon, Base | Q2 2027 |
| **DID-integraatio** | Hajautettu identiteetti | Q3 2027 |
| **Yhteisöhallinto** | Vahvistettu neuvoa-antava järjestelmä | Q4 2027 |
| **Oikeudellinen tunnustus** | Kelpoisuus Turkin tuomioistuimissa | 2027-2028 |
| **API kehittäjille** | Julkinen API-päätepiste | Q3 2027 |

**Hallinnon kehitys:**
- v3.0: Hybridimalli (kuratoriaalinen + yhteisön painotettu)
- 2028+: Täysi yhteisöhallinto (valinnainen)
- Kuratoriaalinen laadunvalvonta säilyy aina

---

## 🧬 Protokollan datarakenne (JSON Schema)

**Jokaisella [PoArt]-sertifikaatilla on siirrettävä ja todennettava JSON-henkilökortti, joka tuotetaan seuraavan standardin mukaisesti.**

> **Huom:** Tämä Identity JSON -formaatti on käyttäjälle esitettävä sertifikaattimuoto. Rekisteritietueissa käytetään `identity.asset_data`:n sijaan `registry.asset`:ia (vastaavuus: `identity.asset_data` == `registry.asset`).
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

## 🔬 Tekninen syvyys: Sinettialgoritmi

### Deterministiset tiivistefunktiot
```javascript
// Apufunktiot: Muunna tiiviste heksamerkkijonoksi
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Muunna merkkijono tavutaulukoksi
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Kanoninen forensics-merkkijonon tuotanto (v1.0: kiinteä kenttäjärjestys + UTF-8 + \n-erotin)
// Vaihe 2 -huomio: Siirretään RFC 8785 (JCS) -kanoniseen JSON:iin
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal-tuotantoprosessi (Täysin deterministinen)
```javascript
// 1. FileHash-laskenta (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Forensisen datan kerääminen (yksittäinen aikaleima)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Yksittäinen aikaleiman tuotanto
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Sama aikaleima
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot-luonti (kanonisella koodauksella)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal-tuotanto (sama aikaleima)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Maskauksen apufunktiot (IPv4- ja IPv6-tuki)
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4-tarkistus
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 tai tuntematon muoto
  return "***";
}
```

### Todentamisvirta (Kaksi tasoa)

#### Quick Verify (Nopea todentaminen)
```javascript
// Tarkistaa vain tiedoston tiivisteen (nopea punainen lippu)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Hae rekisteristä
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Tiivisteen vertailu
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Aito - Tiedoston tiiviste täsmää"
    };
  } else {
    return {
      valid: false,
      message: "❌ Väärennös - Tiedostoa on manipuloitu"
    };
  }
}
```

#### Full Verify (Täysi todentaminen)
```javascript
// Tuottaa EvidenceRoot:n ja NotarySeal:n uudelleen ja todentaa
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Hae rekisteristä
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash-tarkistus (nopea punainen lippu)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Väärennös - Tiedoston tiiviste ei täsmää" };
  }

  // 2) Tuota EvidenceRoot uudelleen (rekisteriin tallennetulla forensics-datalla)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Ei täsmää - EvidenceRoot ei vastaa" };
  }

  // 3) Tuota NotarySeal uudelleen (sama aikaleima + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Ei täsmää - NotarySeal ei vastaa" };
  }

  // Valinnainen: Vaiheessa 2 todenna signer_sig myös attestation_pubkey:llä
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Allekirjoitus virheellinen" };

  return { valid: true, message: "✅ Aito - Full Verify läpäisty" };
}
```

> **Tärkeät huomiot:**
> - **Quick Verify:** Tarkistaa vain tiedoston tiivisteen nopeaan käyttöön.
> - **Full Verify:** Todentaa kaikki protokollan kerrokset (EvidenceRoot + NotarySeal).
> - Kaikki tiivisteoperaatiot tehdään deterministisesti, kiinteällä koodauksella ja erottimilla.
> - **v1.0-kanonisointistandardi:** Kiinteä kenttäjärjestys + UTF-8-koodaus + `\n`-erotin.
> - **Vaihe 2 -suunnitelma:** Siirtyminen RFC 8785 (JCS - JSON Canonicalization Scheme) -kanoniseen JSON:iin.
> - Masked-tilassa EvidenceRoot- ja NotarySeal-laskenta tehdään maskatulla forensics-datalla.
> - Yksittäistä aikaleimaa käytetään koko prosessissa (forensics + NotarySeal); deterministisyys taataan.
> - **Forensics-kenttänimet:** `ip_masked`, `location`, `device`, `timestamp` (koodi ja rekisteri täysin yhteensopivia).
> - **Rekisteripolku:** `certificate.asset.fingerprints` (todentamiskoodi täysin yhteensopiva).
> - **Rekisterin signer_sig:** `proof.signer_sig`-kenttä tarvitaan Full Verify -todentamiseen.
> - SignerSignature-mekanismi otetaan käyttöön vaiheessa 2 Solana Wallet Adapter -integraatiolla; v1.0:ssa todentaminen voidaan tehdä `attestation_pubkey`:llä.

---

## 📊 Kilpailija-analyysi (Päivitetty)

PoArt on sijoitettu "Sweet Spot" (Ihanteellinen piste) -kohtaan, joka täydentää nykyisten ratkaisujen puutteita.

| Ominaisuus | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Hinta** | 🆓 Ilmainen | 🆓 | 💰 Maksullinen | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Vedä ja pudota UI** | ✅ Erittäin helppo | ❌ CLI | ⚠️ Keskitaso | ⚠️ Keskitaso | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Moniformaattivienti** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Reaaliaikainen esikatselu** | ✅ Live | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Yksityisyysasetukset** | ✅ 3 tilaa | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Yksityisyys | ✅ | ❌ Lataus | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensinen metadata** | ✅ Täysi | ❌ | ❌ | ⚠️ Rajoitettu | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR-todentaminen** | ✅ Välitön | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Lohkoketjuankkuri** | 🔄 Tiekartassa | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Avoin lähdekoodi** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Suomen kielen tuki** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Selitys:**
- ✅ : Täysi tuki / saatavilla
- ⚠️ : Rajoitettu / maksullisissa suunnitelmissa
- ❌ : Ei / ei tueta
- 🔄 : Tiekartassa (kehitteillä)
- 🆓 : Täysin ilmainen
- 💰 : Maksullinen / tilaus vaaditaan

### Kilpailijoiden puutteet, PoArt:n vahvuudet

| Puute | Kilpailijat | PoArt |
|------|----------|-------|
| **Käytön vaikeus** | CLI, API-osaaminen, lompakko vaaditaan | Vedä ja pudota, 3 napsautuksella valmis |
| **Hintaeste** | 50-500$/kk tilaus | 100% ilmainen |
| **Yksityisyys** | Tiedosto ladataan palvelimelle | Client-side, tiedosto ei koskaan lähde |
| **Forensinen data** | Vain aikaleima | IP, sijainti, laite, aika - kaikki |
| **Turkin kielen tuki** | Ei tai hyvin rajoitettu | Natiivi kielituki |
| **Avoin lähdekoodi** | Suljettu laatikko | Kaikki koodi avoinna GitHubissa |

---

## 📈 Käyttötilastot (2026 Q1 -tavoitteet)

| Mittari | Tavoite | Tila |
|--------|-------|-------|
| **Sertifikaatteja yhteensä** | 1 000 | 🔄 Edistyminen |
| **Aktiivisia käyttäjiä** | 500 | 🔄 Edistyminen |
| **Todentamismäärä** | 5 000 | 🔄 Edistyminen |
| **Uptime** | 99,9% | ✅ Aktiivinen |
| **Keskim. vasteaika** | <200ms | ✅ Optimaalinen |

---

## 🌍 Yhteisö ja tuki

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Sähköposti:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Osallistujat

PoArt-protokolla kehittyy edelleen avoimen lähdekoodin yhteisön panoksella.

**Osallistuaksesi:**
1. Tee fork
2. Luo feature branch (`git checkout -b feature/amazing-feature`)
3. Tee commit (`git commit -m 'Add amazing feature'`)
4. Tee push (`git push origin feature/amazing-feature`)
5. Avaa Pull Request

### 🛠️ Mitä tällä hetkellä tarvitsemme? (Avunpyyntö)

PoArt-protokollan **Vaihe 2** -kehityksissä odotamme kokeneita kehittäjiä seuraavilla alueilla:

* **Supabase Edge Functions:** Roskapostisuojauksen siirtäminen palvelinpuolelle.
* **Solana Web3.js:** Lompakkoallekirjoitus (Wallet Signing) -integraatio.
* **IPFS / Arweave:** Arkistointi- ja pinning-palvelujen integraatio.
* **Community Tools:** X-äänestys, voting systems, analytics dashboard.

> Ennen ominaisuuden lisäämistä aloita keskustelu "Issues"-välilehdellä.

---

## 💬 Loppuhuomautukset

### Pump.fun ja todellisuus

Tämä projekti aloitettiin Pump.fun:ssa koska:
- ✅ Likviditeettipääsy (Raydium automatic migration)
- ✅ Pääsy nykyiseen yhteisöön
- ✅ Alhainen aloituskustannus

Selvennetään kuitenkin:
- **Tokenin hinta** ei ole taiteellisen menestyksen mittari
- **Operatiivinen budjetti** tokenin arvo on tärkeä (galleria, näyttelyt, infrastruktuuri)
- **Menestysmittarit:** Todennetut teokset + yhteisön sitoutuminen + fyysiset vierailijat

### Hallinto ja hajauttaminen

**v1.0 Todellisuus (2026):**
- Rekisteri: Off-chain (PostgreSQL + IPFS-varmuuskopio)
- Attestointi: Gallerian oma-allekirjoitus (keskitetty mutta läpinäkyvä)
- Hallinto: Vain neuvoa-antava (kuratoriaalinen lopullinen päätös)
- Token utility: Galleriaccesss + rekisteri + NFT-prioriteetti

**v2.0+ Visio (2027+):**
- Rekisteri: On-chain (Solana)
- Allekirjoitukset: Lompakkopohjainen (hajautettu)
- Hallinto: Hybridi (yhteisön neuvoa-antava + kuratoriaalinen laatu)
- Token utility: Laajennetut ominaisuudet + edistynyt pääsy

Tämä rakenne tarjoaa **operatiivisen tehokkuuden** ja **laadunvalvonnan** varhaisessa vaiheessa, pitäen samalla avoinna tien **yhteisön osallistumisen** lisäämiseen tulevaisuudessa.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Kulttuuri on suurempi kuin pääoma*

## 🧾 Lisenssi

MIT-lisenssi © 2026 İlhan Art Gallery Initiative

Katso täydelliset ehdot [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE)

---

## 💬 Tekijätiedot

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Tämä projekti on kehitetty [İlhan Art Gallery] -aloitteella, ja lähdekoodi on avoinna läpinäkyvyyden vuoksi.**

**PROTOKOLLA V1.0 // SINETÖITY SHA-512:LLA.**

*© 2026 İLHAN ART | KAIKKI OIKEUDET TEOKSIIN, KUVIIN JA IDEOIHIN PIDÄTETÄÄN.*

---
