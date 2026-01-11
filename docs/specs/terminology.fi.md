# 📚 TERMINOLOGIAN JA KÄSITTEIDEN SANASTO
> **"Tämän protokollan kielen ymmärtäminen tarkoittaa sen vision ymmärtämistä."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Perusinfrastruktuuri

**PoArt Forensic Engine (PFE)** on peruskerros, joka edustaa [PoArt]-protokollan taustalla olevaa peruslogiikkaa ja teknistä toimintaa. Se on "rikostekniikkamoottori", joka muuntaa taideteoksen tuotannon raakatiedot todennettavaksi ja muuttumattomaksi **digitaaliseksi todisteeksi**.

### 🧩 Miksi "PoArt Forensic"?

- **PoArt (Proof of Art):** Moottorin painopiste on digitaalisen omaisuuden arvon sitominen ei spekulaatioon, vaan **todennettavaan tuotantoprosessiin**.
- **Forensic (Rikostekniikka Todentaminen):**
  - **Tekninen Määritelmä:** Algoritminen lähestymistapa ja todistusketju sen todentamiseksi, että tuotantoprosessin tietoja (siveltimenvedot, timelapse, lokit) ei ole manipuloitu.
  - **Filosofinen Taso:** Tekoälyn "välitöntä tuotantoa" vastaan; väite inhimillisen tuotannon, joka sisältää **aikaa, vaivaa ja päätösten kustannuksia**, muuntamisesta mitattavaksi todellisuudeksi.

> Huomautus: Blockchain-integraatio (esim. Solana) ei ole PFE:n ydin; se määritellään erikseen **Chain Anchor Layer**:ksi todentamista/rekisteriä varten.

### 🛠️ Tekninen Laajuus v1.0

**PoArt Forensic Engine (PFE) v1.0** on rakennettu **3 peruspilarille** monimutkaisten rahoitusmallien sijaan:

1. **Hashing & Sealing (Sinetöinti):**  
   PFE käsittelee deterministisesti kaikki Evidence Pack -paketin elementit (teosfiedosto, video, JSON/loki, allekirjoitus jne.) ja generoi ainutlaatuisen **NotarySeal**-arvon.

   **Avainkäsitteet (v1.0):**
   - **FileHash (teoksen sormenjälki):** Teosfiedoston tavuista generoitu hash.
   - **EvidenceRoot (todistepaketin juuri):** Juuren digest, joka edustaa Evidence Pack -paketin eheyttä (Merkle-juuri tai kanonisen manifestin hash).
   - **NotarySeal (lopullinen sinetti / PFE:n tuloste):** Lopullinen sinetti, joka on generoitu EvidenceRoot + aika + allekirjoitus -yhdistelmästä.

   **Kaavat (sijoittajille ymmärrettävässä muodossa):**
   
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
   
   > Huomautus: PFE:n tulosteena pidetty arvo on **NotarySeal**. **SignerSignature**-mekanismi aktivoidaan vaiheessa 2 (Solana Wallet Adapter -sovittimella); nykyisessä v1.0:ssa käytetään järjestelmän omaa todennusallekirjoitusta. Todennuksen julkinen avain julkaistaan rekisterissä `issuer.attestation_pubkey`-kentässä.

2. **Indexing (Arkistointi):**  
   Kirjaa, mikä lompakko, minä päivänä, esitti **Labor Proof (Työn Todisteen)** mille teokselle; läpinäkyvässä ja kyselykelpoisessa rekisterikerroksessa.  
   *(Tämä kerros voi olla tietokanta; blockchain-integraatio määritellään erikseen "Chain Anchor Layer":ksi.)*

3. **Verification (Todentaminen):**  
   Kun teoksen aitous kyseenalaistetaan, PFE käsittelee raakadodisteet uudelleen; testaa matemaattisella varmuudella, vastaako lasketut **EvidenceRoot / NotarySeal**-arvot arkiston tietueita.

---

### 🧮 PoArt-arvoteoreema (The Value Theorem)

[PoArt]-protokolla sitoo digitaalisen omaisuuden arvon ($V$) ei subjektiiviseen markkinakäsitykseen, vaan **tuotantoprosessin fyysiseen todellisuuteen**.

Tekoäly (AI) kumoaa prosessin tarjoamalla välittömiä tuloksia ($t \to 0$). [PoArt] pitää sen sijaan arvoa **ajan, työn ja tahdon** komponenttien kertymänä.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Muuttujien Määritelmä

- **$\int dt$ (Prosessin Kertyminen):**  
  Arvo ei ole hetkellinen "tuloste"; se on **prosessi**, joka kertyy $t_{\text{start}}$:n ja $t_{\text{end}}$:n välillä. Kun aika vähenee (AI-tuotanto), integraalin tulos lähestyy nollaa.

- **$P_{\text{labor}}(t)$ (Hetkellinen Työn Intensiteetti):**  
   Edustaa tuotantohetkellä käytetyn henkisen ja fyysisen ponnistelun intensiteettiä. Kun todennettu ponnistelu kasvaa, integroitava kasvaa.  
  > Huomautus: Tämä termi voidaan käytännössä normalisoida "mitattaviksi/todennettaviksi työsignaaleiksi".

- **$I_{\text{agency}}(t)$ (Tahdon Kerroin):**  
  Tämä on tuottajan kyky ottaa riskejä ja tehdä päätöksiä. Saa arvoja $0$:n ja $1$:n välillä.
  - **AI ($I \approx 0$):** Suorittaa käskyjä, ei ota riskejä, ei maksa kustannuksia.
  - **Ihminen ($I \to 1$):** Muuttaa päätöksiä, epäröi, ottaa riskejä.

- **$U_{\text{irreversible}}$ (Peruuttamaton Ainutlaatuisuus):**  
  Kun digitaalisessa tuotannossa voi peruuttaa (`Ctrl+Z`); fyysisessä tuotannossa (kankaalle levitetty maali, veistetty marmori, ele live-lähetyksen aikana) ei ole paluuta. Tämä **peruuttamattomuus** on lisätermi, joka luo "ainutlaatuisuuden" (ei-vaihdettavan luonteen) teokseen.

### 🔎 Tapausanalyysi: AI "Välitön Tuloste" vs Ihminen "Todennettu Prosessi"

Seuraava skenaario näyttää, miten **PoArt-arvoteoreema** toimii käytännössä ja miksi AI-tuotannot saavat alhaisia pisteitä [PoArt]-standardissa.

#### Skenaario A: Visuaalinen Tuotanto AI:lla 10 Sekunnissa

- **Kesto ($\Delta t$):** $10$ sekuntia (prosessi käytännössä olematon)
- **Työn Intensiteetti ($P_{\text{labor}}$):** $1$ yksikkö (vain komennon kirjoitus)
- **Tahdon Kerroin ($I_{\text{agency}}$):** $0.01$ (ei riskiä, ei kustannuksia)
- **Peruuttamattomuus ($U_{\text{irreversible}}$):** $0$ (peruutettavissa / kopioitavissa)

**Tulos:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Kommentti:** Vaikka tuloste olisi täydellinen; koska prosessia ei ole koettu eikä se sisällä tahtoa/riskiä, [PoArt]-arvo lähestyy $0$:aa.

#### Skenaario B: Fyysinen Tuotanto Live-lähetyksessä 6 Tunnin Ajan

- **Kesto ($\Delta t$):** $6$ tuntia ($21{,}600$ sekuntia)
- **Työn Intensiteetti ($P_{\text{labor}}$):** $0.5$ yksikköä (fyysisen ja henkisen ponnistelun jatkuvuus)
- **Tahdon Kerroin ($I_{\text{agency}}$):** $0.9$ (päätösten muuttaminen, riskien ottaminen, peruuttamattomat valinnat)
- **Peruuttamattomuus ($U_{\text{irreversible}}$):** $>0$ (fyysisiä jälkiä ei voi peruuttaa)

**Tulos:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Kommentti:** Kun prosessi pitenee ja tahto (riski) kasvaa, arvo kertyy kumulatiivisesti. $U_{\text{irreversible}}$-termi on lisäpanos, joka luo "ainutlaatuisuuden" (ei-vaihdettavan luonteen) teokseen.

---

### ✅ Johtopäätös: Todisteeseen Sidottu Arvo (Proof-Bound Value)

Tämä teoreema poistaa [PoArt]-arvoväitteen olemasta "tykkäys" tai "markkinatarina" ja sitoo sen **todennettuun tuotannon todellisuuteen**.

1. **Ilman Prosessia Ei Synny Arvoa:**  
   AI kumoaa prosessin välittömässä tulosteessa ($t \to 0$). Kun prosessin ikkuna kapenee, integraalin tulos pienenee matemaattisesta välttämättömyydestä:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Tahto ja Riski Ovat Kertoimia:**  
   [PoArt] mittaa ei vain "käytettyä aikaa", vaan myös todellista päätöksen, riskin ja kustannusten tasoa tuona aikana. Riskejä ottamattoman tuotannon (AI) arvo on alhainen:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Ainutlaatuisuus On Fyysinen Todiste, Ei Markkinointi:**  
   Fyysisessä tuotannossa peruuttamattomat jäljet (siveltimenvetostisä kankaalla, murtunut marmori) ovat digitaalisen `Ctrl+Z`-logiikan ulkopuolella. Tämä peruuttamattomuus ($U_{\text{irreversible}}$) tekee teoksesta ontologisesti ainutlaatuisen.

> **🔐 YHTEENVETO:** Vaikka arvoteoreema saattaa vaikuttaa epämääräiseltä mittauksena (vaikka sitä ei voida mitata 100% todellisessa elämässä), tämän kaavan tarkoitus on näyttää muuttujien rakenne ja suunta. Se, mikä on harvinaista AI-aikakaudella, ei ole "kuva", vaan **todennettu työ, aika ja tahto.** [PoArt] mittaa tätä harvinaisuutta ja tallentaa sen **Evidence Pack**:n kautta.

### 🏛️ "Engine" (Moottori) -käsitteen Merkitys

Pump.fun:n kaltaisilta alustoilta peräisin olevat tokenit ovat usein vain **"pääsylippuja"**. **PoArt Forensic Engine (PFE)** on sen sijaan **perustuslaillinen looginen kerros**, joka määrittelee, mitä oikeuksia tämä lippu suojaa, miten työ kirjataan ja miten taide/tiede/teknologia tulevat pysyviksi.

> **Huomautus:** Syy, miksi aloitimme tämän projektin Pumpfun:ssa, on se, että meillä ei ollut tarpeeksi likviditeettiä ja seuraajia. Olemassa olevien tietojen käyttö oli strategisesti oikea askel, vaikkakin ei laadukkain. Tämän moottorin logiikan määrittely GitHubissa, budjetista ja resursseista riippumatta, todistaa, että projekti ei ole vain rahoitusspekulaatiota, vaan pitkän aikavälin visio **ohjelmistoinfrastruktuurista** ja **digitaalisesta kansalliskirjastosta**.

---

## 🎨 [PoArt] PROOF OF ART -PROTOKOLLA (Proof of Art Protocol v1.0)

> **"Aito Taiteilija, Aito Tuotanto, Aito Arvo."**

Tämä protokolla on **biologinen ja älyllinen puolustusmekanismi**, joka on suunniteltu kryptovaluuttaekosysteemin täyttäneitä nimettömiä huijareita, 5 minuutissa tuotettuja AI-kuvia ja "Pump & Dump" -kulttuuria vastaan.

---

## a) Mikä On [PoArt]? (Filosofinen ja Tekninen Määritelmä)

**Proof of Art [PoArt];** on institutionaalinen todennusstandardi, joka takaa, että blockchain-omaisuuden taustalla oleva arvo perustuu ei spekulaatioon, vaan todennettuun **inhimilliseen työhön**, **aikaan** ja **fyysiseen energiaan**.

Kuten Bitcoin tuottaa arvoa *"Sähköllä ja Laskentateholla"* **(Proof of Work)**; [PoArt]-yhteensopivat projektit tuottavat arvoa *"Taiteellisella Taidolla ja Inhimillisellä Ajalla"*.

Eliminoi *"Dev myi, projekti päättyi"* -riskin, joka on läsnä Pump.fun:ssa ja DEX-alustoilla; koska täällä arvo ei ole koodissa, vaan **tuotannon jatkuvuudessa**.

> **[PoArt] ei sano osallistujalle "Luota meihin"; se sanoo "Tässä todisteet, katso omin silmin, todenna omalla matematiikallasi".**

---

## b) [PoArt] 5-Pilarinen Standardi (The 5 Pillars of Truth)

Nämä 5 kohtaa ovat manipuloimattomia suodattimia, jotka projektin on läpäistävä saadakseen [PoArt]-sinetin.

### 1) Live-identiteetin Todistus (Live Identity Proof)

- **Ongelma:** Kryptomaailma on täynnä nimettömiä perustajia (Dev), joiden henkilöllisyys on määrittelemätön ja jotka keräävät rahaa ja hylkäävät projektin.
- **[PoArt]-ratkaisu:** Tuottaja todistaa ei vain henkilöllisyytensä, vaan **läsnäolonsa tuotannon aikana**. Tämä sisältää live-istuntoja, joissa he ovat vuorovaikutuksessa yhteisön kanssa ja täyttävät tiettyjä välittömiä vaatimuksia, eivät ennalta nauhoitettuja videoita.  
  (Esimerkiksi: *"Kirjoita tämän päivän päivämäärä ja nykyinen lohkonumero kankaan oikeaan kulmaan"*)
- **Motto:** *"Robotit voivat maalata, mutta robotit eivät hikoile eivätkä improvisoi."*

### 2) Työn ja Prosessin Todistus (Labor & Process Proof)

- **Ongelma:** 2 sekunnissa tuotetut AI-kuvat ja 2 kuukaudessa tehdyt öljymaalaukset katsotaan samaksi "jpegiksi" digitaalisessa maailmassa.
- **[PoArt]-ratkaisu:** Teoksen "raskaus- ja syntymäprosessi" tallennetaan. Luonnosvaiheet, maalikerrokset, kertyneet käytetyt tunnit ja taiteilijan kokema fyysinen prosessi teoksen luomisen aikana dokumentoidaan. Tämä lisää **"Aikakustannuksen" (Time Cost)** tokeniin. Mitä vaikeampi omaisuutta on tuottaa, sitä vahvempi sen arvo.

### 3) Esteettisen Arvon Todistus (Aesthetic Value Proof)

- **Ongelma:** "Meme"-kulttuurin estetiikka ja taiteellinen syvyys, joka sivuuttaa kaiken ja keskittyy vain hetkelliseen komediaan, ja siitä seuraavat lyhytaikaiset "Hype"-projektit.
- **[PoArt]-ratkaisu:** Projektilla on oltava akateemiset taidestandardit, väriteoria, sommittelusäännöt ja materiaalien tuntemus (Impasto, Tekstuuri jne.). Sisällön ei pidä vain naurattaa; sen on herätettävä ihailua katsojassa ja sillä on oltava **keräilyarvoa**.

### 4) Käsitteellinen Innovaatio (Conceptual Novelty)

- **Ongelma:** Tuhansia identtisiä dog/cat coin, kaukana luovuudesta.
- **[PoArt]-ratkaisu:** Projektin on rakennettava uusi silta, joka yhdistää merkitsevästi taiteen, tieteen, filosofian tai teknologian.  
  (Esimerkiksi: Klassisen Daavid-patsaan yhdistäminen kryptovaluuttamarkkinoiden tietoihin; tämän kautta ihmisen havaintojen "kivettymisen" idean käsittely ja mahdollisuus perustella tämä tieteellisillä lähteillä.)  
  Teoksen on oltava ei vain visuaalinen juhla, vaan myös älyllinen haaste, joka kannustaa ajattelemaan **Tiedettä, Filosofiaa tai Teknologiaa**.

> [!IMPORTANT]
> **Viiteesimerkki (Las Palmitas -ilmiö):** Meksikon Las Palmitas -alueella, joka kamppailee rikollisuuden kanssa, yli 200 taloa muutettiin jättimäiseksi >sateenkaarijuhlaksi. Tämän esteettisen väliintulon seurauksena alueen rikollisuustilastot laskivat tietyissä määrin, nuoret alkoivat kiinnostua taiteesta jengien sijaan. >Esteettinen muutos uudelleenkoodasi ihmisten kunnioituksen ympäristöä ja toisiaan kohtaan (Sosiaalinen Koheesio).
>
> **Odotus:** [PoArt]-listalle pääsevällä projektilla; kuten yllä olevassa esimerkissä, on oltava sosiologinen, tieteellinen tai filosofinen syy-seuraussuhde >visuaalisen estetiikan lisäksi. Koska ainoa asia, jota ei voi ostaa rahalla, on "Aika", tässä protokollassa aika on todistettava takuuna staking-menetelmällä. Projektin >käsitteellisen perustan on oltava niin vahva ja yleispätevä; että jopa mahdollisessa CTO (Community Take Over) -skenaariossa vuosia myöhemmin, yhteisö voi >autonomisesti ylläpitää projektin innovatiivista potentiaalia periessään tämän perinnön.

### 5) Ei-Algoritminen Tahto (Non-Algorithmic Agency)

- **Ongelma:** Täydelliset mutta sieluttomat, toistuvat digitaaliset tuotannot.
- **[PoArt]-ratkaisu:** Inhimillisen olennon alkuperäisen tahdon, joka voi tehdä virheitä, ottaa riskejä ja tuntea emotionaalisia vaihteluita, on tunnuttava teoksessa. Siveltimenvetojen epävarmuus, materiaalin odottamattomat reaktiot ja taiteilijan hetkelliset päätökset ovat **Biologinen Allekirjoitus**, joka erottaa teoksen "Mekaanisesta Tuotannosta".

---

## c) Todennusmekanismi ja Väärentämisen Esto

Tämä järjestelmä varmistaa, että projekti pysyy luotettavana ja elävänä ei vain "alussa", vaan "ikuisesti".

### 📦 Todistepaketti (Evidence Pack - The Digital Twin)

Jokaisen [PoArt]-sertifioidun teoksen takana on salattu ja aikaleimallinen datapaketti, jonka sijoittajat voivat ladata:

- **RAW-videotallenteet:** Jatkuvat raakatallenteet tuotantohetkestä.
- **Metadata-analyysi:** Tiedoston luontipäivä, käytetystä laitteesta tiedot ja sijaintitiedot.
- **Fyysiset Viitteet:** Todisteet siitä, että teos on olemassa fyysisessä maailmassa  
  (Esimerkiksi: Nykyinen sanomalehti tai nykyiset blockchain-tiedot teoksen vieressä).

> *Huomautus johdonmukaisuudesta:* Ilmaus "todistepaketti" liittyy aiemmista osista **Evidence Pack → EvidenceRoot → NotarySeal** -linjaan; eli paketin eheys esitetään todennetulla sinetillä.

### 🔄 365 Päivän Päivitys (The Sustainability Protocol)

- **Vallankumouksellinen Ominaisuus:** Kryptoprojekteissa "Dev" (Kehittäjä) lanseeraa tokenin markkinoille ja yleensä katoaa 1-2 kuukauden kuluttua (Soft Rug). [PoArt] tekee tämän mahdottomaksi.
- **Sääntö:** "Verified Artist" (Todennettu Taiteilija) -status ei ole elinikäinen. Se on voimassa vain **1 vuoden**.
- **Toiminta:** Taiteilijan/kehittäjän on esitettävä yhteisölle joka 365. päivä **uusi, suuri ja todennettu teos**.
- **Esimerkkiskenaario:** Aloitit projektin vuonna 2026. Tammikuussa 2027 järjestelmä antaa varoituksen "Todistusaika Päättynyt". Jos taiteilija ei esitä uutta näyttelyä, uutta fyysistä teosta tai uutta teknologista integraatiota, projektin "Luottamusmerkki" laskee.
- **Tulos:** Tämä järjestelmä varmistaa, että **sisältö ei koskaan menetä relevanssiaan** ja että sijoittaja ei elä pelossa *"Onko kehittäjä vielä täällä?"*. Projekti tulee eläväksi studioksi.

### 🚩 Punainen Lippu (Red Flag Protocol)

**Mikäli yhteisö tai algoritmit havaitsevat väärentämisen (AI:n käyttö, varastettu työ, manipuloitu video):**

1. Sertifikaatti merkitään välittömästi **"MITÄTÖIDYKSI" (VOID)**.
2. Todistuspaketit merkitään julkisesti **"Vääriksi"**.
3. Projekti lisätään [PoArt]-mustalle listalle. Tämä vahvistaa tosiasiaa, että hajautetussa maailmassa **maine on ainoa valuutta**.

---

## d) Johtopäätös: Ei Kasino, Museo

**Pump.fun ja Hajautetut Pörssit (DEX) ovat valitettavasti nyt kasinoita; valot vilkkuvat, kaikki etsivät nopeita voittoja, ja kasino (huijarit) voittaa aina. Syy, miksi aloitimme projektin täällä, on riittämättömän budjetin puute ja olemassa olevan yleisön olemassaolo live-lähetysten kautta.**

**[PoArt] on linnoitus, joka on rakennettu tämän kasinon keskelle.**

- 🎰 Kasinot perustuvat kortteihin; me perustumme **fyysiseen todellisuuteen**.
- 🃏 Kasinot ovat avoimia petoksille; me olemme avoimia **läpinäkyville todisteille**.
- ⏳ Kasinot ovat väliaikaisia; me keskitymme **taiteen ja tieteen ikuisuuteen**.

**Tätä protokollaa käyttävä token ei ole vain "kolikko"; se on digitaalinen arvopaperi, joka sisältää hikeä, maalia, koodia ja filosofiaa.**

---

## 🗳️ 6) HALLINTO JA JULKINEN REKISTERI (Governance & Public Registry)

**Tämän osion tarkoitus on: [PoArt]-standardin poistaminen "ihmisiin luottamisen" piiristä ja sen muuttaminen kestäväksi julkiseksi infrastruktuuriksi rekisterin + todennuksen + yhteisön valvonnan kanssa.**

### 6.1 Julkinen Rekisteri (Public Registry)

- **Public Registry:** Kaikki hyväksytyt tiedot tallennetaan osoitteeseen `ilhanart.org/registry` (tai GitHub Registry).

**Rekisteröintilogiikka (suositeltu standardi - JSON-polun muoto):**

Jokainen rekisteriin tuleva merkintä sisältää vähintään nämä todennetut peruskentät:

- **Identiteetti ja Tila:**
  - `certificate_id` (luettava viite)
  - `status` (active / void)
  - `void_reason` (jos olemassa)
  - `visibility` (private / masked / public)
  - `created_at` (aikaleima)

- **Myöntäjäorganisaatio:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Tiedot Teoksesta:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (jos mahdollista; token-gated identiteettiin)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Rikostekniset Tiedot:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Kryptografiset Todisteet:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Hallinto:**
  - `governance.decision`
  - `governance.veto_threshold`

Rekisterillä voi olla kaksi tasoa:
- **1)** Ihmisluettava hakemisto (web-lista / haku / suodatin)
- **2)** Koneluettava manifesti (JSON-merkinnät; PFE-todennusta varten)

**Tässä "rekisteröinti" tulee todennetuksi PFE:n Evidence Pack → EvidenceRoot → NotarySeal -ketjusta. Rekisteri tarjoaa todennuksen tarkoituksen, ei "väitettä".**

---

### 6.2 40 % Yhteisön Veto (Token-Gated Governance)

- **40 % Yhteisön Veto:** Äänestys alkaa kuukautta ennen statuksen saamista; **Token-Gated (Solana-Verified)** -yhteisön 40 %:n vastalause mitätöi hakemuksen.

**Äänestysvirtaus (suositeltu puhdas prosessi):**
- **Ehdokasikkuna:** Ehdokasprojekti avaa "PoArt-ehdokasrekisteröinnin" (ehdokasrekisteröinnit näkyvät "pending"-tilassa).
- **Tarkistusjakso:** 30 päivän ajan yhteisö tutkii todisteita (Evidence Pack + live-tallenteet + metadata).
- **Token-gated todentaminen:** Äänestys tapahtuu Solanassa todennetuilla lompakoilla (esim. tietyn tokenin/NFT:n omistus + lompakon allekirjoitus).
- **Veto-sääntö:** Jos 40 % äänistä on **vastalause (NO / VETO)**, hakemus hylätään.
- **Läpinäkyvyys:** Äänestysten tulos tallennetaan rekisteriin "decision record":ksi (päivämäärä, suhde, snapshot ID).

---

### 6.3 Metadatan Synkronointi (Fyysisen Maailman Vastaavuus)

- **Metadata Sync:** Rekisterin tekniset tiedot on vastattava 100 % fyysistä omaisuutta.

**"100 % vastaavuuden" tekninen määrittely (suositeltu selvyys):**
- **Vähimmäisvastaavuus (pakollinen):**
  - Rekisterin `asset.fingerprints.sha256/sha512`:n on oltava **täsmälleen sama** kuin käsillä olevan tiedoston hash.
  - Rekisterin `proof.notary_seal`:n, kun se toistetaan (jos Evidence Pack on olemassa), on oltava **täsmälleen sama**.
- **Fyysisen viittauksen vastaavuus (todistustyyppi):**
  - Todisteet, kuten live-lähetyksessä näkyvä fyysinen teos + päivä/lohko-viittaus, on oltava yhdenmukaisia Evidence Pack:n kanssa.
- **Yksityisyyden vastaavuus:**
  - Kentät, kuten IP/sijainti `masked`-näkyvyydessä, julkaistaan **peittämisstandardin mukaisesti**.

---

### 6.4 Riita, Tarkistus ja Peruutus (Dispute & Revocation)

Rekisteri ei ole vain "hyväksymismekanismi"; se on **elävä valvontamekanismi väärentämistä vastaan**.

- Kun riita aloitetaan, merkintä voidaan asettaa **"review"**-tilaan.
- Jos väärentäminen havaitaan, se merkitään `status: void`:ksi ja lisätään syy:
  - `void_reason` (AI:n käyttö / plagiointi / manipulointi jne.)
  - `revoked_at` (peruutushetki)
- Peruutuspäätöksen lähde on selvästi näkyvissä rekisterissä:
  - yhteisön äänestys / valtuutettu neuvosto / rikostekniikkatutkimuksen muistiinpano (riippuen sovellettavasta)

> **Tämä osio on rekisterin vastine "Red Flag Protocol" -osion VOID-käsitteelle.**

---

### 6.5 Esimerkki Rekisterimerkinnästä (Koneluettava)
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
    "title": "Nimetön",
    "creator": "Anonyymi",
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
> *Huomautus: `asset.fingerprints.sha512` ja muut hash-arvot on lyhennetty esittelytarkoituksiin; todellisessa sovelluksessa käytetään täyden pituista heksadesimaalimerkkijonoa.*

---

## 7) 🔐 TEKNINEN SINETTI (NOTARY SEAL)

**PoArt Forensic Engine (PFE) v1.0** järkkymätön sinetöintialgoritmi tuotettu:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt]-protokolla Digitaalinen Notaari ja Rikostekniikka Todistus (Beta v1.0)

> **"Kulttuuri Suurempi kuin Pääoma. Suojaa teoksesi tänään, vie ne huomiseen."**

---

## Miksi Julkinen?

Todellinen turvallisuus tulee läpinäkyvyydestä. **Public Registry (Julkinen Rekisteri)** -järjestelmämme ansiosta henkilö missä päin maailmaa tahansa voi todentaa muutamassa sekunnissa, onko hänen kädessään oleva tiedosto alkuperäinen, ilman minkäänlaista viranomaista.

---

## 🧩 Miksi On Useampi "Näkyvyysmoduuli"?

Kriittisin osa koodista on tässä (näkyvyyden valintavalikko). Nämä vaihtoehdot antavat käyttäjille mahdollisuuden tasapainottaa **"Yksityisyys vs Läpinäkyvyys"**:

### 🔒 Yksityinen (Private)

- **Skenaario:** Taiteilija ei halua vielä julkaista teosta, mutta haluaa aikatestata sen ja todistaa "tein tämän tänä päivänä".
- **Mitä Koodi Tekee:** Tallentaa tiedot tietokantaan, mutta käyttää tagia `visibility: "private"`. Tulevaisuudessa, kun kirjoitat "Public Read" -käytännön, voit piilottaa nämä merkinnät julkiselta sanomalla `WHERE visibility = 'public'`.

### 🕶️ Peitetty (Masked)

- **Skenaario:** Taiteilija haluaa läpinäkyvyyttä, mutta pelkää kodin osoitteen löytyvän (IP-sijainti).
- **Mitä Koodi Tekee:** JavaScript-puolella toimivat `maskIP`- ja `maskLoc`-funktiot. Muuntaa IP-osoitteen muotoon `88.241.***.***` ja sijainnin muotoon `***/TR` ja lähettää sensuroitua versiota tietokantaan.
- **Huomautus Yksityisyydestä:** Peittäminen tapahtuu selaimessa, Supabase ei näe todellista sijaintia. **Kuitenkin:** Jos käytetään kolmannen osapuolen API:ita, kuten ipapi.co, sijaintitietoihin, nämä toimittajat näkevät IP-osoitteen pyynnön hetkellä.
- **Sinetöinti Masked-tilassa:** EvidenceRoot:n ja NotarySeal:n laskenta tehdään peitetyillä forensics-tiedoilla; näin todentaminen pysyy deterministisenä.

### 🌍 Julkinen (Public)

- **Skenaario:** Täysi läpinäkyvyys. [PoArt]-standardin mukaan missä, milloin ja mistä verkosta teos tuotettiin, julistetaan nimenomaisesti.

---

## 💡 Teknologinen Innovaatio

PoArt ei ole vain tiedostojen latausjärjestelmä. Se on **"Forensic Chain of Custody"** -moottori, joka sulattaa kolme eri teknologista kerrosta yhdeksi sulatuspataksi ja tuo uuden standardin.

**Tässä osiossa "moottori"ksi kuvattu kerros vastaa aiemmassa terminologiassa PoArt Forensic Engine (PFE) -ydintä.**

### 1) Client-Side Hashing (Maksimaalinen Yksityisyys)

Teostesi tiedostoja ei koskaan ladata palvelimelle. Selainpohjainen (Client-side) moottori laskee tiedoston hash:n (digitaalisen tiivisteen) tietokoneellasi. Vain tämä sormenjälki ja metadata lähetetään palvelimelle.

> **Huomautus Yksityisyydestä:** Teosfiedostoa ei ladata palvelimelle ja se on näin suojattu. Kuitenkin forensics-tiedot (IP/sijainti) jaetaan valitun näkyvyystilan mukaan (private/masked/public).

### 2) Forensic Data Fusion (Rikostekniikka Voima)

Tämä on paljon enemmän kuin pelkkä aikaleima. Järjestelmä yhdistää seuraavat tiedot yhdeksi "Genesis Seal":ksi:

- **Digitaalinen Tiiviste (SHA-512):** Kryptografisen tiivisteen (SHA-512) standardia käyttäen digitaalinen sormenjälki, joka hajoaa, vaikka yhden pikselin teosta muutetaan.
- **Sijainti ja Aika:** Päivämäärä millisekunnin tarkkuudella, maa, kaupunki ja alue, jossa kauppa tehtiin.
- **Laitteen Identiteetti:** Käyttöjärjestelmä, selain ja laitetyyppi (User-Agent-analyysi).

---

## 🛡️ Sovellusalueet ja Edut

Jos olet taiteilija, kirjailija tai suunnittelija, ei riitä, että sanot "Tein tämän aiemmin", sinun on todistettava se.

**PoArt:lla sinetöity teos:**

- **Matemaattinen Todiste:** Järjestelmä havaitsee tämän, vaikka yhden pikselin tiedostosta muutettaisiin. Manipulointi on mahdotonta.
- **Oikeudellinen Perusta:** On tallennettu, minä päivänä, missä kaupungissa, mistä laitteesta teos sinetöitiin.
- **Välitön Sertifikaatti:** Muutamassa sekunnissa generoi henkilökohtaisen **"Omaisuuden Identiteettisertifikaatin"** QR-koodilla ja sinetöitynä.

---

## ⚙️ Järjestelmäarkkitehtuuri ja Tekniset Spesifikaatiot

Järjestelmä on suunniteltu "Serverless" (Palvelimeton) -arkkitehtuurilla, keskittyen korkeaan suorituskykyyn ja skaalautuvuuteen.

| Kerros | Teknologia | Kuvaus |
|--------|-----------|----------|
| **Kryptografia** | SHA-256 & SHA-512 | Kaksikerroksinen kryptografinen tiiviste |
| **Tietokanta** | Supabase (PostgreSQL) | JSONB-tietorakenne, RLS-käytännöt |
| **Rikostekniset Tiedot** | ipapi.co API | IP/Sijainti/Aika-kolmikko |
| **Renderöinti** | html2canvas + jsPDF | PNG/PDF-generointi asiakaspuolella |
| **Frontend** | Vanilla JavaScript | Nolla framework-riippuvuuksia |
| **Turvallisuus** | Client-side hashing | Tiedosto ei koskaan saavu palvelimelle |

### Erottuvat Ominaisuudet

| Ominaisuus | Yksityiskohta | Kilpailijoilla? |
|---------|-------|-------------|
| **Drag & Drop UI** | Vedä ja pudota tiedosto, välitön esikatselu | ❌ Puuttuu useimmista |
| **Multi-Format Export** | PNG, JSON, PDF - yksi napsautus | ⚠️ Rajoitettu |
| **Real-Time Preview** | Sertifikaatin esikatselu reaaliajassa | ❌ Puuttuu |
| **Privacy Controls** | Private/Masked/Public -vaihtoehdot | ❌ Puuttuu |
| **Client-Side Hashing** | Tiedosto ei koskaan saavu palvelimelle | ✅ Vain joillakin |
| **Forensic Metadata** | IP, sijainti, laite, aika - kaikki yhdessä | ❌ Hajanainen |
| **QR Verification** | QR-koodi välitöntä todennusta varten | ⚠️ Rajoitettu |
| **Rate Limiting** | Roskapostisuojaus (RLS + Client) | ❌ Puuttuu useimmista |

---

## 🗺️ Tiekartta: "Trustless" Tulevaisuus

Nykyinen versio **(Beta v1.0)** on optimoitu tarjoamaan loppukäyttäjälle maksimaalinen nopeus, helppo käyttöliittymä ja ilmainen pääsy. Kuitenkin lopullinen visiomme on siirtyminen rakenteeseen, jossa edes tietokannan ylläpitäjä (me) ei voi puuttua asiaan.

### Vaihe 1: Beta (Nyt Saatavilla)

- **Infrastruktuuri:** Cloud Database (Supabase).
- **Tarkoitus:** Nopeus, UX (Käyttäjäkokemus) -esteiden poistaminen ja mukautuminen. "Kitkattoman" turvallisuuden varmistaminen.

### 🚀 Vaihe 2: (Mitä Vaatii Backend / Edge Function)

Tämä vaihe kattaa siirtymisen järjestelmän täysin "Client-Side" toimivasta rakenteesta turvallisempaan ja hallitumpaan "Server-Side Authority" -rakenteeseen.

| Elementti | Mitä Tuo? | Tech Stack | Prioriteetti |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Function** | Roskapostin esto + API-avaimen turvallisuus | Supabase Edge (Deno) | 🔴 Korkea |
| **Lompakon Allekirjoitus** | Kryptografisen identiteetin todentaminen | Solana Wallet Adapter | 🟡 Keskitaso |
| **IPFS/Arweave Varmuuskopio** | Hajautettu muuttumattomuus | IPFS SDK + Pinata | 🟢 Matala |
| **Peruutusmekanismi** | Väärien sertifikaattien mitätöinti | DB Schema päivitys | 🔴 Korkea |
| **Audit Log** | Rikostekniikkatutkimuksen tallentaminen | Mukautettu lokitaulukko | 🟡 Keskitaso |
| **OpenTimestamps** | Bitcoin-ankkurointi | OTS JavaScript | 🟢 Matala |
| **DID-integraatio** | Decentralized Identity | ION/Ceramic | 🟢 Matala |

### Vaihe 3: Täysi Hajauttaminen (Pitkällä Aikavälillä)

| Ominaisuus | Tarkoitus | ETA |
|---------|-------|-----|
| **Blockchain Registry** | On-chain rekisteröinti Ethereum/Solana | Q4 2026 |
| **DAO Governance** | Yhteisöhallinto | Q1 2027 |
| **Multi-Chain Support** | Polygon, Arbitrum, Base | Q2 2027 |
| **Legal Recognition** | Pätevyys Turkin tuomioistuimissa | 2027-2028 |
| **API for Developers** | Julkinen API-päätepiste | Q3 2026 |

---

## 📊 Kilpailijoiden Analyysi (Päivitetty)

PoArt on sijoitettu "Sweet Spot" (Optimaalinen Ideaalipiste) -kohtaan, joka täydentää olemassa olevien ratkaisujen aukkoja.

| Ominaisuus | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 証 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Hinta** | 🆓 Ilmainen | 🆓 | 💰 Maksullinen | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Erittäin Helppo | ❌ CLI | ⚠️ Keskitaso | ⚠️ Keskitaso | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Reaaliajassa | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Tilaa | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Yksityisyys | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Täydellinen | ❌ | ❌ | ⚠️ Rajoitettu | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Välitön | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Tiekartta | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Suomen Tuki** | 🔄 Kehityksessä | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Selite:**
- ✅ : Täysi tuki / saatavilla
- ⚠️ : Rajoitettu / maksullisissa suunnitelmissa
- ❌ : Puuttuu / ei tueta
- 🔄 : Tiekartalla (kehityksessä)
- 🆓 : Täysin ilmainen
- 💰 : Maksullinen / tilaus vaaditaan

### Kilpailijoiden Haitat, PoArt:n Vahvuudet

| Miinus | Kilpailijat | PoArt |
|------|----------|-------|
| **Käytön Monimutkaisuus** | CLI, API-tietämys, lompakko vaaditaan | Vedä ja pudota, päättyy 3 napsautuksessa |
| **Kustannuseste** | Tilaus $50-500/kk | 100 % ilmainen |
| **Yksityisyys** | Tiedosto ladataan palvelimelle | Client-side, tiedosto ei koskaan lähde |
| **Rikostekniset Tiedot** | Vain aikaleima | IP, sijainti, laite, aika - kaikki |
| **Suomen Tuki** | Puuttuu tai hyvin rajoitettu | Natiivi kielituki |
| **Open Source** | Suljettu laatikko | Kaikki koodi avoinna GitHubissa |

---

## 🧬 Protokollan Tietorakenne (JSON Schema)

**Jokaisella [PoArt]-sertifikaatilla on siirrettävä ja todennettava JSON-identiteetti, joka tuotetaan seuraavan standardin mukaisesti.**

> **Huomautus:** Tämä Identity JSON -muoto on käyttäjälle esitettävä sertifikaattimuoto. Rekisterimerkinnöissä `identity.asset_data`:n sijasta käytetään `registry.asset` (kartoitus: `identity.asset_data` == `registry.asset`).
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
    "title": "Virallinen Whitepaper",
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

## 🔬 Tekninen Syvyys: Sinetöintialgoritmi

### Deterministiset Hash-funktiot
```javascript
// Apufunktiot: Muunna digest hex-merkkijonoksi
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Muunna merkkijono tavutaulukoksi
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Kanonisen forensics-merkkijonon generointi (v1.0: kiinteä kenttäjärjestys + UTF-8 + \n erotin)
// Vaiheen 2 huomautus: Siirtyminen kanoniseen JSON:iin RFC 8785 (JCS) kanssa
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal-tuotantoprosessi (Täysin Deterministinen)
```javascript
// 1. FileHash-laskenta (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Rikostekniikkatietojen kerääminen (käyttäen yhtä aikaleimaa)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Yhden aikaleiman generointi
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

// 4. NotarySeal-tuotanto (käyttäen samaa aikaleimaa)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Peittämisen apufunktiot (IPv4- ja IPv6-tuki)
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

### Todennusvirtaus (Kaksi Tasoa)

#### Quick Verify (Nopea Todentaminen)
```javascript
// Tarkistaa vain tiedoston hashin (nopea punainen lippu)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Hae Rekisteristä
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Hash-vertailu
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Aito - Tiedoston hash täsmää"
    };
  } else {
    return {
      valid: false,
      message: "❌ Väärä - Tiedostoa on manipuloitu"
    };
  }
}
```

#### Full Verify (Täysi Todentaminen)
```javascript
// Toistaa ja todentaa EvidenceRoot:n ja NotarySeal:n
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Hae Rekisteristä
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash-tarkistus (nopea punainen lippu)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Väärä - Tiedoston hash ei täsmää" };
  }

  // 2) EvidenceRoot-toisto (rekisteriin tallennetuilla forensics-tiedoilla)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Ei täsmää - EvidenceRoot virheellinen" };
  }

  // 3) NotarySeal-toisto (samalla aikaleimalla + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Ei täsmää - NotarySeal virheellinen" };
  }

  // Valinnainen: Vaiheessa 2 todenna myös signer_sig attestation_pubkey:llä
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Allekirjoitus virheellinen" };

  return { valid: true, message: "✅ Aito - Full Verify läpäisty" };
}
```

> **Tärkeät Huomautukset:**
> - **Quick Verify:** Tarkistaa vain tiedoston hashin nopeaa käyttöä varten.
> - **Full Verify:** Todentaa kaikki protokollan kerrokset (EvidenceRoot + NotarySeal).
> - Kaikki hash-operaatiot suoritetaan deterministisesti, kiinteällä koodauksella ja erottimilla.
> - **v1.0 kanonisointistandardi:** Kiinteä kenttäjärjestys + UTF-8 koodaus + `\n` erotin.
> - **Vaiheen 2 suunnitelma:** Siirtyminen kanoniseen JSON:iin RFC 8785 (JCS - JSON Canonicalization Scheme) kanssa.
> - Masked-tilassa EvidenceRoot- ja NotarySeal-laskenta tehdään peitetyillä forensics-tiedoilla.
> - Käytetään yhtä aikaleimaa koko prosessissa (forensics + NotarySeal); determinismi taattu.
> - **Forensics-kenttien nimet:** `ip_masked`, `location`, `device`, `timestamp` (koodi ja rekisteri täysin yhteensopivia).
> - **Rekisterin polku:** `certificate.asset.fingerprints` (täysin yhteensopiva todennuskoodin kanssa).
> - **signer_sig Rekisterissä:** `proof.signer_sig`-kenttä tarvitaan Full Verify:lle.
> - SignerSignature-mekanismi aktivoidaan vaiheessa 2 Solana Wallet Adapter:lla; v1.0:ssa voidaan suorittaa todentaminen `attestation_pubkey`:llä.

---

## 📈 Käyttötilastot (Q1 2026 Tavoitteet)

| Mittari | Tavoite | Tila |
|--------|-------|-------|
| **Sertifikaatteja Yhteensä** | 1,000 | 🔄 Käynnissä |
| **Aktiivisia Käyttäjiä** | 500 | 🔄 Käynnissä |
| **Todentamisten Määrä** | 5,000 | 🔄 Käynnissä |
| **Uptime** | %99.9 | ✅ Aktiivinen |
| **Keskimääräinen Vastausaika** | <200ms | ✅ Optimaalinen |

---

## 🌍 Yhteisö ja Tuki

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 Osallistujat

PoArt-protokolla kehittyy avoimen lähdekoodin yhteisön panosten ansiosta.

**Osallistumiseksi:**
1. Tee fork
2. Luo ominaisuushaara (`git checkout -b feature/amazing-feature`)
3. Tee commit (`git commit -m 'Add amazing feature'`)
4. Tee push (`git push origin feature/amazing-feature`)
5. Avaa Pull Request

### 🛠️ Mitä Tarvitsemme Nyt? (Avunpyyntö)

Etsimme kokeneita kehittäjiä osallistumaan seuraaviin aiheisiin PoArt-protokollan **Vaiheen 2** kehityksessä:

* **Supabase Edge Functions:** Roskapostisuojauksen siirtäminen palvelinpuolelle.
* **Solana Web3.js:** Lompakon allekirjoituksen (Wallet Signing) integrointi.
* **IPFS / Arweave:** Arkistointi- ja ankkurointipalveluiden integrointi.

> Ennen ominaisuuden lisäämistä, aloita keskustelu "Issues"-osiossa.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Kulttuuri Suurempi kuin Pääoma*

## 🧾 Lisenssi

MIT License © 2026 İlhan Art Gallery Initiative

Katso [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) täydellisistä ehdoista.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Tämä projekti on kehitetty [İlhan Art Gallery] -aloitteella ja lähdekoodi on julkisesti saatavilla läpinäkyvyyden vuoksi.**

**PROTOKOLLA V1.0 // SINETÖITY SHA-512:LLA.**

*© 2026 İLHAN ART | KAIKKI OIKEUDET TEOKSIIN, KUVIIN JA IDEOIHIN SUOJATTU.*

---
