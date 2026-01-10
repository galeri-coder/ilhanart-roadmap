# 📚 GLOSSAIRE DE TERMINOLOGIE ET CONCEPTS
> **"Comprendre le langage de ce protocole, c'est comprendre sa vision."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0 : Infrastructure de Base

**PoArt Forensic Engine (PFE)** est la couche principale représentant la logique centrale et le fonctionnement technique derrière le protocole [PoArt]. C'est le "moteur forensique" qui prend les données brutes de production d'une œuvre d'art et les transforme en **preuves numériques** vérifiables et immuables.

### 🧩 Pourquoi "PoArt Forensic" ?

- **PoArt (Proof of Art) :** L'objectif du moteur est de lier la valeur d'un actif numérique non à la spéculation, mais au **processus de production démontrable**.
- **Forensic (Vérification Forensique) :**
  - **Définition Technique :** Une approche algorithmique et de chaîne d'enregistrement pour vérifier que les données du processus de production (coups de pinceau, timelapse, journaux) n'ont pas été manipulées.
  - **Couche Philosophique :** L'affirmation de transformer **le temps humain, l'effort et le coût de décision** en une réalité mesurable, contre la production de "sortie instantanée" de l'IA.

> Note : L'intégration blockchain (par ex. Solana) n'est pas le cœur du PFE ; elle sera définie séparément comme une **Chain Anchor Layer** à des fins de vérification/registre.

### 🛠️ Portée Technique v1.0

**PoArt Forensic Engine (PFE) v1.0** est construit sur les **3 piliers principaux** suivants plutôt que sur des modèles financiers complexes :

1. **Hashing & Sealing (Scellement) :**  
   Le PFE traite de manière déterministe tous les éléments du Pack de Preuves (fichier d'œuvre, vidéo, JSON/log, signature, etc.) et génère une valeur unique de **NotarySeal**.

   **Concepts centraux (v1.0) :**
   - **FileHash (empreinte de l'œuvre) :** Hash généré à partir des octets du fichier de l'œuvre.
   - **EvidenceRoot (racine du pack de preuves) :** Résumé racine représentant l'intégrité du Pack de Preuves (racine Merkle ou hash de manifeste canonique).
   - **NotarySeal (sceau final / sortie PFE) :** Sceau final généré à partir de la combinaison EvidenceRoot + temps + signature.

   **Formules (clairement visibles pour les investisseurs) :**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Définitions de Payload Canonique (v1.0) :**
   
   - **EvidenceRootPayload :**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload :**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Note : La valeur référencée comme sortie PFE est **NotarySeal**. Le mécanisme **SignerSignature** sera activé en Phase 2 (avec Solana Wallet Adapter) ; dans la v1.0 actuelle, la signature d'attestation propre au système est utilisée. La clé publique d'attestation est publiée dans le registre sous le champ `issuer.attestation_pubkey`.

2. **Indexing (Archivage) :**  
   Enregistre quel portefeuille, à quelle date, a soumis **Proof of Labor (Preuve de Travail)** pour quelle œuvre dans une couche de registre transparente et interrogeable.  
   *(Cette couche peut être une base de données ; l'intégration de chaîne est définie séparément comme "Chain Anchor Layer".)*

3. **Verification (Vérification) :**  
   Lorsque l'authenticité d'une œuvre est remise en question, le PFE retraite les preuves brutes ; il teste mathématiquement si les valeurs calculées de **EvidenceRoot / NotarySeal** correspondent aux enregistrements d'archive.

---

### 🧮 Théorème de Valeur PoArt (The Value Theorem)

Le protocole [PoArt] relie la valeur ($V$) d'un actif numérique non à la perception subjective du marché, mais à **la réalité physique du processus de production**.

L'Intelligence Artificielle (IA) détruit le processus en livrant le résultat instantanément ($t \to 0$). [PoArt], cependant, traite la valeur comme l'accumulation de composantes de **temps, travail et volonté**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Définitions des Variables

- **$\int dt$ (Accumulation de Processus) :**  
  La valeur n'est pas une "sortie" instantanée ; c'est un **processus** accumulé entre $t_{\text{start}}$ et $t_{\text{end}}$. À mesure que la durée diminue (production IA), le résultat de l'intégrale approche 0.

- **$P_{\text{labor}}(t)$ (Puissance de Travail Instantanée) :**  
  Représente l'intensité de l'effort mental et physique dépensé au moment de la production. À mesure que l'effort démontrable augmente, l'intégrande croît.  
  > Note : Ce terme peut être normalisé en pratique à travers des "signaux de travail mesurables/démontrables".

- **$I_{\text{agency}}(t)$ (Coefficient de Volonté) :**  
  La capacité du producteur à prendre des risques et à prendre des décisions. Prend une valeur entre $0$ et $1$.
  - **IA ($I \approx 0$) :** Exécute des commandes, ne prend pas de risques, ne paie pas de coûts.
  - **Humain ($I \to 1$) :** Change de décisions, hésite, prend des risques.

- **$U_{\text{irreversible}}$ (Singularité Irréversible) :**  
  Bien que l'annulation (`Ctrl+Z`) soit possible dans la production numérique, dans la production physique (peinture appliquée sur la toile, marbre taillé, geste en direct) il n'y a pas de retour en arrière. Cette **irréversibilité** est un terme supplémentaire créant la "singularité" (caractère non fongible) dans l'œuvre.

### 🔎 Analyse de Cas : IA "Sortie Instantanée" vs. Humain "Processus Prouvé"

Le scénario suivant démontre comment le **Théorème de Valeur PoArt** fonctionne en pratique et pourquoi les productions IA obtiennent de faibles scores dans la norme [PoArt].

#### Scénario A : Production Visuelle en 10 Secondes avec IA

- **Durée ($\Delta t$) :** $10$ secondes (processus négligeable)
- **Puissance de Travail ($P_{\text{labor}}$) :** $1$ unité (uniquement écrire des commandes)
- **Coefficient de Volonté ($I_{\text{agency}}$) :** $0.01$ (pas de risque, pas de coût)
- **Irréversibilité ($U_{\text{irreversible}}$) :** $0$ (réversible / copiable)

**Résultat :**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Commentaire :** Même si la sortie est parfaite ; la valeur [PoArt] approche $0$ car aucun processus n'a été vécu et aucune volonté/risque n'a été impliqué.

#### Scénario B : Production Physique de 6 Heures en Direct

- **Durée ($\Delta t$) :** $6$ heures ($21{,}600$ secondes)
- **Puissance de Travail ($P_{\text{labor}}$) :** $0.5$ unités (continuité de l'effort physique et mental)
- **Coefficient de Volonté ($I_{\text{agency}}$) :** $0.9$ (changer de décisions, prendre des risques, choix irréversibles)
- **Irréversibilité ($U_{\text{irreversible}}$) :** $>0$ (les traces physiques ne peuvent être annulées)

**Résultat :**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Commentaire :** À mesure que le processus s'allonge et que la volonté (risque) augmente, la valeur s'accumule cumulativement. Le terme $U_{\text{irreversible}}$ est une contribution supplémentaire créant la "singularité" (caractère non fongible) dans l'œuvre.

---

### ✅ Conclusion : Valeur Liée à la Preuve (Proof-Bound Value)

Ce théorème extrait l'affirmation de valeur de [PoArt] d'être un "like" ou un "récit de marché" et la lie à **une réalité de production démontrable**.

1. **Pas de Processus, Pas de Valeur :**  
   L'IA détruit le processus avec une sortie instantanée ($t \to 0$). À mesure que la fenêtre de processus se rétrécit, le résultat de l'intégrale se réduit nécessairement :
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **La Volonté et le Risque sont des Multiplicateurs :**  
   [PoArt] ne mesure pas seulement le "temps passé" mais aussi la couche réelle de décision, risque et coût dans ce temps. Une production sans prise de risque (IA) a une faible valeur :
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **La Singularité est une Preuve Physique, Pas du Marketing :**  
   Les traces irréversibles dans la production physique (trait de toile, éclat de marbre) sont en dehors de la logique `Ctrl+Z` du numérique. Cette irréversibilité ($U_{\text{irreversible}}$) singularise ontologiquement l'œuvre.

> **🔐 RÉSUMÉ :** Bien que le théorème de valeur puisse sembler incertain en tant que mesure (même si son équivalent dans le monde réel ne peut être entièrement mesuré), le but de cette formule est de montrer la configuration et la direction des variables. À l'ère de l'IA, ce qui est rare n'est pas "l'image" mais **le travail démontrable, le temps et la volonté.** [PoArt] mesure cette rareté et l'enregistre avec **Pack de Preuves**.

### 🏛️ L'Importance du Concept de "Moteur"

Les tokens émergeant de Pump.fun ou de plateformes similaires sont souvent de simples **"billets d'accès"**. **PoArt Forensic Engine (PFE)**, cependant, est la **couche logique constitutionnelle** qui détermine quels droits ce billet protège, comment le travail sera enregistré et comment l'art/science/technologie sera perpétué.

> **Note :** La raison pour laquelle nous avons lancé ce projet sur Pumpfun est que nous n'avions pas suffisamment de liquidité ni suffisamment d'abonnés. Utiliser les données existantes était stratégiquement le bon mouvement, même si ce n'était pas de la plus haute qualité. Indépendamment du budget et des ressources, définir la logique de ce moteur sur GitHub prouve que le projet n'est pas seulement de la spéculation financière, mais une vision d'**infrastructure logicielle** et de **bibliothèque nationale numérique** à long terme.

---

## 🎨 [PoArt] PROTOCOLE DE PREUVE DE TRAVAIL (Proof of Art Protocol v1.0)

> **"Artiste Réel, Production Réelle, Valeur Réelle."**

Ce protocole est un **mécanisme de défense biologique et intellectuelle** développé contre les escrocs anonymes entourant l'écosystème crypto, les visuels IA produits en 5 minutes et la culture "Pump & Dump".

---

## a) Qu'est-ce que [PoArt] ? (Définition Philosophique et Technique)

**Proof of Art [PoArt] ;** est une norme de vérification institutionnelle qui garantit que la valeur derrière un actif sur la blockchain est basée non sur la spéculation, mais sur le **travail humain**, le **temps** et l'**énergie physique** vérifiables.

Tout comme Bitcoin génère de la valeur avec *"Électricité et Puissance de Processeur"* **(Proof of Work)**, les projets conformes à [PoArt] génèrent de la valeur avec *"Compétence Artistique et Temps Humain"*.

Il élimine le risque de *"Le développeur a vendu, le projet est terminé"* sur les plateformes Pump.fun et DEX ; car ici la valeur n'est pas dans le code, mais dans la **continuité de la production**.

> **[PoArt] ne dit pas aux participants "Faites-nous confiance" ; il dit "Voici les preuves, voyez avec vos yeux, vérifiez avec vos mathématiques."**

---

## b) Norme à 5 Piliers [PoArt] (Les 5 Piliers de la Vérité)

Ces 5 éléments sont des filtres non manipulables qu'un projet doit passer pour recevoir le sceau [PoArt].

### 1) Preuve d'Identité en Direct

- **Problème :** Le monde crypto est rempli de fondateurs anonymes (Devs) avec des identités peu claires qui collectent de l'argent et abandonnent les projets.
- **Solution [PoArt] :** Le producteur prouve non seulement une carte d'identité, mais **la présence au moment de la production**. Cela inclut des sessions de diffusion en direct où l'interaction avec la communauté se produit et des demandes instantanées spécifiques sont satisfaites, pas des vidéos préenregistrées.  
  (Par ex., *"Écris la date d'aujourd'hui et le numéro de bloc actuel dans le coin droit de la toile"*)
- **Devise :** *"Les bots peuvent peindre mais les bots ne transpirent pas et ne peuvent pas improviser."*

### 2) Preuve de Travail et de Processus

- **Problème :** Des visuels IA (Intelligence Artificielle) produits en 2 secondes recevant le même traitement "jpeg" que des peintures à l'huile faites en 2 mois dans le monde numérique.
- **Solution [PoArt] :** Le processus de "grossesse et de naissance" de l'œuvre est enregistré. Les étapes d'esquisse, les couches de peinture, les heures cumulées passées et le processus physique que l'artiste a vécu en créant l'œuvre sont documentés. Cela ajoute un **"Coût de Temps"** au token. Plus la production d'un actif est difficile, plus sa valeur est solide.

### 3) Preuve de Valeur Esthétique

- **Problème :** Culture "Mème" se concentrant uniquement sur la comédie instantanée tout en ignorant l'esthétique et la profondeur artistique, résultant en des projets "Hype" de courte durée.
- **Solution [PoArt] :** Le projet doit avoir des normes d'art académiques, une théorie des couleurs, des règles de composition et une connaissance des matériaux (Impasto, Texture, etc.). Le contenu ne doit pas seulement faire rire ; il doit inspirer l'admiration chez les spectateurs et avoir une **valeur collectionnable**.

### 4) Nouveauté Conceptuelle

- **Problème :** Des milliers de pièces chien/chat copies dépourvues de créativité.
- **Solution [PoArt] :** Le projet doit construire un nouveau pont combinant art, science, philosophie ou technologie dans une structure significative.  
  (Par ex., Combiner la sculpture classique de David avec les données du marché crypto ; traiter l'idée que la perception humaine "se transforme en pierre" à travers cela et la fonder avec des sources scientifiques.)  
  L'œuvre ne doit pas seulement être une fête visuelle mais aussi un défi intellectuel qui provoque la réflexion sur **Science, Philosophie ou Technologie**.

> [!IMPORTANT]
> **Exemple de Référence (Effet Las Palmitas) :** Dans le quartier de Las Palmitas au Mexique, en proie au crime, plus de 200 maisons ont été transformées en un spectacle arc-en-ciel massif. Suite à cette intervention esthétique, les taux de criminalité dans le quartier ont diminué dans une certaine mesure, et les jeunes ont commencé à s'engager dans l'art au lieu des gangs. Le changement esthétique a recodé le respect des gens pour leur environnement et les uns envers les autres (Cohésion Sociale).
>
> **Attente :** Un projet entrant dans la liste [PoArt] doit, comme dans l'exemple ci-dessus, contenir une relation de cause à effet sociologique, scientifique ou philosophique au-delà de l'esthétique visuelle pure. Puisque le temps est le seul actif qui ne peut être acheté avec de l'argent, dans ce protocole le temps doit être prouvé en étant mis en jeu comme garantie. La base conceptuelle du projet doit être si forte et universelle que même dans un éventuel scénario CTO (Community Take Over) des années plus tard, la communauté puisse continuer de manière autonome le potentiel innovant du projet en héritant de cet héritage.

### 5) Volonté Non Algorithmique

- **Problème :** Productions numériques parfaites mais sans âme qui se répètent entre elles.
- **Solution [PoArt] :** La volonté unique de l'humain qui peut faire des erreurs, prendre des risques et vivre des fluctuations émotionnelles doit être ressentie dans l'œuvre. L'incertitude dans les coups de pinceau, les réactions inattendues des matériaux et les décisions instantanées de l'artiste sont la **Signature Biologique** qui sépare l'œuvre de la "Production Machine".

---

## c) Mécanisme de Vérification et Anti-Fraude

Ce système garantit que le projet reste fiable et vivant non seulement "au début" mais "pour toujours".

### 📦 Pack de Preuves - Le Jumeau Numérique

Derrière chaque œuvre certifiée [PoArt] se trouve un paquet de données crypté et horodaté que les investisseurs peuvent télécharger :

- **Enregistrements Vidéo RAW :** Séquences brutes ininterrompues du moment de production.
- **Analyse des Métadonnées :** Date de création du fichier, informations sur l'appareil utilisé et données de localisation.
- **Références Physiques :** Preuves que l'œuvre existe dans le monde physique  
  (Par ex., Journal actuel ou données blockchain de ce moment à côté de l'œuvre).

> *Note de cohérence :* Le terme "pack de preuves" se connecte à la chaîne **Pack de Preuves → EvidenceRoot → NotarySeal** dans les sections précédentes ; c'est-à-dire que l'intégrité du paquet est représentée par un sceau vérifiable.

### 🔄 Renouvellement de 365 Jours (Le Protocole de Durabilité)

- **Caractéristique Révolutionnaire :** Dans les projets crypto, le "Dev" (Développeur) lance le token et disparaît généralement après 1-2 mois (Soft Rug). [PoArt] rend cela impossible.
- **Règle :** Le statut d'"Artiste Vérifié" n'est pas à vie. Seulement **1 an** est valide.
- **Opération :** L'artiste/développeur doit présenter à la communauté **une nouvelle œuvre importante et démontrable** tous les 365 jours.
- **Scénario d'Exemple :** Vous avez lancé le projet en 2026. En janvier 2027, le système donne un avertissement "Période de Preuve Expirée". Si l'artiste ne présente pas une nouvelle exposition, une nouvelle œuvre physique ou une nouvelle intégration technologique, le "Badge de Confiance" du projet baisse.
- **Résultat :** Ce système garantit que **le contenu ne perd jamais sa pertinence** et que l'investisseur ne connaît jamais la peur de *"Le développeur est-il toujours là ?"*. Le projet devient un studio vivant.

### 🚩 Protocole de Drapeau Rouge

**En cas de fraude détectée par la communauté ou les algorithmes (utilisation d'IA, œuvre volée, vidéo manipulée) :**

1. Le certificat est immédiatement marqué comme **"VOID" (NUL)**.
2. Les packs de preuves sont étiquetés publiquement comme **"Faux"**.
3. Le projet est placé sur la liste noire [PoArt]. Cela renforce que dans un monde décentralisé, **la réputation est la seule monnaie**.

---

## d) Conclusion : Pas un Casino, Mais un Musée

**Pump.fun et les Échanges Décentralisés (DEX) sont malheureusement des casinos en ce moment ; les lumières clignotent, tout le monde poursuit les gains rapides, et la maison (escrocs) gagne toujours. La raison pour laquelle nous avons commencé le projet ici est le manque de budget suffisant et avoir un environnement pour atteindre le public existant via des diffusions en direct.**

**[PoArt] est une forteresse construite au milieu de ce casino.**

- 🎰 Le casino est basé sur les jeux de cartes ; nous sommes basés sur la **réalité physique**.
- 🃏 Le casino est ouvert à la triche ; nous sommes ouverts aux **preuves transparentes**.
- ⏳ Le casino est temporaire ; nous nous concentrons sur **l'éternité de l'art et de la science**.

**Un token utilisant ce protocole n'est pas seulement une "pièce" ; c'est une équité numérique contenant sueur, peinture, code et philosophie.**

---

## 🗳️ 6) GOUVERNANCE ET REGISTRE PUBLIC

**Le but de cette section est : transformer la norme [PoArt] du plan de "confiance en les individus" vers une infrastructure publique durable avec registre + vérification + supervision communautaire.**

### 6.1 Registre Public

- **Registre Public :** Toutes les données approuvées sont enregistrées sur `ilhanart.org/registry` (ou GitHub Registry).

**Logique de registre (norme recommandée - en format de chemin JSON) :**

Chaque enregistrement entrant dans le registre porte ces champs centraux vérifiables minimaux :

- **Identité et Statut :**
  - `certificate_id` (référence lisible)
  - `status` (active / void)
  - `void_reason` (si applicable)
  - `visibility` (private / masked / public)
  - `created_at` (horodatage)

- **Institution Émettrice :**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informations sur l'Œuvre :**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (si possible ; pour l'identité avec porte de token)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Données Forensiques :**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Preuves Cryptographiques :**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Gouvernance :**
  - `governance.decision`
  - `governance.veto_threshold`

Le registre peut avoir deux couches :
- **1)** Index lisible par l'humain (liste web / recherche / filtre)
- **2)** Manifeste lisible par machine (enregistrements JSON ; pour vérification PFE)

**Cet "enregistrement" devient vérifiable via la chaîne Pack de Preuves → EvidenceRoot → NotarySeal du PFE. Le registre offre des objectifs de vérification, pas des "affirmations".**

---

### 6.2 Veto Communautaire de 40% (Gouvernance avec Porte de Token)

- **Veto Communautaire de 40% :** Le vote commence un mois avant l'octroi du statut ; 40% d'objection de la communauté **avec Porte de Token (vérifiée Solana)** invalide la demande.

**Flux de vote (processus clair recommandé) :**
- **Fenêtre de candidature :** Le projet candidat ouvre "l'enregistrement de candidat PoArt" (les enregistrements de candidats apparaissent en statut "en attente").
- **Période d'examen :** La communauté examine les preuves pendant 30 jours (Pack de Preuves + enregistrements de diffusion en direct + métadonnées).
- **Vérification avec porte de token :** Le vote se fait avec des portefeuilles vérifiés Solana (par ex. propriété de token/NFT spécifique + signature de portefeuille).
- **Règle de veto :** Si 40% des votes sont **objection (NON / VETO)**, la demande est rejetée.
- **Transparence :** Le résultat du vote est stocké dans le registre comme "enregistrement de décision" (date, ratio, ID de snapshot).

---

### 6.3 Synchronisation des Métadonnées (Alignement avec le Monde Physique)

- **Synchronisation des Métadonnées :** Les données techniques dans le registre doivent correspondre à 100% avec l'entité physique.

**Définir techniquement la "correspondance à 100%" (clarté recommandée) :**
- **Correspondance minimale (obligatoire) :**
  - Le `asset.fingerprints.sha256/sha512` dans le registre doit être **identique** au hash du fichier en question.
  - Lorsque le `proof.notary_seal` dans le registre est reproduit (si le Pack de Preuves existe), il doit être **identique**.
- **Correspondance de référence physique (type de preuve) :**
  - L'œuvre physique + référence de date/bloc montrée dans la diffusion en direct et preuves similaires doivent être cohérentes avec le Pack de Preuves.
- **Conformité à la vie privée :**
  - Les champs comme IP/localisation en visibilité `masked` sont publiés **selon les normes de masquage**.

---

### 6.4 Litige et Révocation

Le registre n'est pas seulement un mécanisme d'"approbation" ; c'est un **mécanisme d'audit vivant contre la fraude**.

- Lorsqu'un litige est initié, l'enregistrement peut être placé en mode **"review" (révision)**.
- Si une fraude est détectée, il est marqué comme `status: void` avec raison ajoutée :
  - `void_reason` (utilisation d'IA / vol / manipulation, etc.)
  - `revoked_at` (temps de révocation)
- La source de la décision de révocation est clairement visible dans le registre :
  - vote communautaire / comité autorisé / note d'enquête forensique (selon le cas)

> **Cette section est la contrepartie dans le registre du concept VOID dans la section "Protocole de Drapeau Rouge".**

---

### 6.5 Exemple d'Enregistrement de Registre (Lisible par Machine)
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
> *Note : `asset.fingerprints.sha512` et autres valeurs de hash sont abrégées à des fins d'affichage ; dans l'implémentation réelle, des chaînes de caractères hexadécimales de pleine longueur sont utilisées.*

---

## 7) 🔐 SCEAU TECHNIQUE (NOTARY SEAL)

L'algorithme de sceau inébranlable généré par **PoArt Forensic Engine (PFE) v1.0** :

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Protocole de Notaire Numérique et Preuve Forensique (Beta v1.0)

> **"La culture est plus grande que le capital. Protégez vos œuvres aujourd'hui, portez-les à demain."**

---

## Pourquoi Public ?

La vraie sécurité vient de la transparence. Grâce à notre système de **Registre Public**, n'importe qui n'importe où dans le monde peut vérifier si un fichier est original en quelques secondes, sans avoir besoin d'aucune autorité.

---

## 🧩 Pourquoi Plusieurs "Modules de Visibilité" ?

C'est la partie la plus critique du code (menu de sélection de visibilité). Ces options permettent aux utilisateurs d'équilibrer **"Vie Privée vs. Transparence"** :

### 🔒 Privé

- **Scénario :** L'artiste ne veut pas encore publier l'œuvre mais veut l'horodater pour prouver "j'ai fait ceci à cette date".
- **Ce que Fait le Code :** Écrit les données dans la base de données mais estampille `visibility: "private"`. Plus tard lors de l'écriture de la politique "Public Read", vous pouvez cacher ces enregistrements du public avec `WHERE visibility = 'public'`.

### 🕶️ Masqué

- **Scénario :** L'artiste veut la transparence mais craint que son adresse personnelle (localisation IP) soit trouvée.
- **Ce que Fait le Code :** Les fonctions `maskIP` et `maskLoc` fonctionnent côté JavaScript. Convertit l'adresse IP au format `88.241.***.***`, la localisation au format `***/TR`, et envoie la version censurée à la base de données.
- **Note de Confidentialité :** Le masquage est fait dans le navigateur, Supabase ne voit pas la vraie localisation. **Cependant :** Si des API tierces comme ipapi.co sont utilisées pour les données de localisation, ces fournisseurs voient l'adresse IP au moment de la demande.
- **Scellement en Mode Masqué :** Le calcul d'EvidenceRoot et NotarySeal est fait avec des données forensiques masquées ; ainsi la vérification reste déterministe.

### 🌍 Public

- **Scénario :** Transparence totale. Selon les normes [PoArt], où, quand, depuis quel réseau l'œuvre a été produite est clairement déclaré.

---

## 💡 Innovation Technologique

PoArt n'est pas seulement un système de téléchargement de fichiers. C'est un moteur de **"Chaîne de Custodie Forensique"** qui apporte une nouvelle norme en fondant trois couches technologiques différentes dans un seul pot.

**La couche décrite comme "moteur" dans cette section correspond au cœur PoArt Forensic Engine (PFE) dans la terminologie précédente.**

### 1) Hachage Côté Client (Confidentialité Maximale)

Vos fichiers d'œuvres d'art ne sont jamais téléchargés sur le serveur. Notre moteur basé sur navigateur (côté client) calcule le hash (résumé numérique) du fichier sur votre propre ordinateur. Seule cette empreinte digitale et les métadonnées sont envoyées au serveur.

> **Note de Confidentialité :** Le fichier de l'œuvre n'est pas téléchargé sur le serveur et est protégé de cette manière. Cependant, les données forensiques (IP/localisation) sont partagées selon le mode de visibilité sélectionné (privé/masqué/public).

### 2) Fusion de Données Forensiques (Puissance Forensique)

Bien plus qu'un simple horodatage ordinaire. Le système combine ces données dans un seul "Sceau Genèse" :

- **Résumé Numérique (SHA-512) :** Empreinte digitale utilisant la norme de résumé cryptographique (SHA-512) qui se cassera si même un pixel de l'œuvre change.
- **Localisation et Temps :** Date avec précision à la milliseconde, pays, ville et données de district de la transaction.
- **Identité de l'Appareil :** Système d'exploitation, navigateur et type d'appareil (analyse User-Agent).

---

## 🛡️ Cas d'Utilisation et Avantages

Si vous êtes artiste, écrivain ou designer, dire "J'ai fait ceci plus tôt" ne suffit pas ; vous devez le prouver.

**Une œuvre que vous scellez avec PoArt :**

- **Preuve Mathématique :** Si même un pixel de votre fichier change, le système le sait. La manipulation est impossible.
- **Base Juridique :** À quelle date, quelle ville, depuis quel appareil l'œuvre a été scellée est enregistré.
- **Certificat Instantané :** Génère un **"Certificat d'Identité d'Actif"** spécial pour vous en quelques secondes, avec code QR et scellé.

---

## ⚙️ Architecture du Système et Caractéristiques Techniques

Le système est conçu sur une architecture "Sans Serveur", se concentrant sur la haute performance et l'évolutivité.

| Couche | Technologie | Description |
|--------|-----------|-------------|
| **Cryptographie** | SHA-256 & SHA-512 | Résumé cryptographique double couche |
| **Base de Données** | Supabase (PostgreSQL) | Structure de données JSONB, politiques RLS |
| **Données Forensiques** | ipapi.co API | Trinité IP/Localisation/Temps |
| **Rendu** | html2canvas + jsPDF | Génération PNG/PDF côté client |
| **Frontend** | Vanilla JavaScript | Dépendance framework zéro |
| **Sécurité** | Hachage côté client | Le fichier ne va jamais au serveur |

### Caractéristiques Mises en Avant

| Fonctionnalité | Détail | Chez les Concurrents ? |
|---------|-------|-----------------|
| **UI Glisser-Déposer** | Glisser-déposer fichier, aperçu instantané | ❌ Absent chez la plupart |
| **Export Multi-Format** | PNG, JSON, PDF - un clic | ⚠️ Limité |
| **Aperçu en Temps Réel** | Aperçu de certificat en direct | ❌ Aucun |
| **Contrôles de Confidentialité** | Options Privé/Masqué/Public | ❌ Aucun |
| **Hachage Côté Client** | Le fichier ne va jamais au serveur | ✅ Seulement dans quelques-uns |
| **Métadonnées Forensiques** | IP, localisation, appareil, temps - tout ensemble | ❌ Fragmenté |
| **Vérification QR** | Code QR de vérification instantanée | ⚠️ Limité |
| **Limitation de Débit** | Protection contre le spam (RLS + Client) | ❌ Absent chez la plupart |

---

## 🗺️ Feuille de Route : Avenir "Sans Confiance"

La version actuelle **(Beta v1.0)** est optimisée pour fournir aux utilisateurs finaux une vitesse maximale, une interface facile et un accès gratuit. Cependant, notre vision ultime est de passer à une structure où même l'administrateur de base de données (nous) ne peut pas interférer.

### Phase 1 : Beta (Actuellement en Direct)

- **Infrastructure :** Base de Données Cloud (Supabase).
- **Objectif :** Vitesse, suppression des barrières UX (Expérience Utilisateur) et adaptation. Fournir une sécurité "sans friction".

### 🚀 Phase 2 : (Exigences Backend / Fonction Edge)

Cette phase couvre la transition de la structure de travail entièrement "côté client" vers une structure "Autorité Côté Serveur" plus sécurisée et gérable.

| Élément | Qu'apporte-t-il ? | Pile Technologique | Priorité |
|-------|---------------|------------|---------|
| **`INSERT` → Fonction Edge** | Prévention spam + sécurité clé API | Supabase Edge (Deno) | 🔴 Haute |
| **Signature de Portefeuille** | Authentification cryptographique | Solana Wallet Adapter | 🟡 Moyenne |
| **Sauvegarde IPFS/Arweave** | Immuabilité décentralisée | IPFS SDK + Pinata | 🟢 Basse |
| **Mécanisme de Révocation** | Annulation de certificat faux | Mise à jour Schéma BD | 🔴 Haute |
| **Journal d'Audit** | Enregistrement de requête forensique | Table de journaux personnalisée | 🟡 Moyenne |
| **OpenTimestamps** | Ancrage Bitcoin | OTS JavaScript | 🟢 Basse |
| **Intégration DID** | Identité Décentralisée | ION/Ceramic | 🟢 Basse |

### Phase 3 : Décentralisation Complète (Long Terme)

| Fonctionnalité | Objectif | ETA |
|---------|------|-----|
| **Registre Blockchain** | Enregistrement sur chaîne Ethereum/Solana | Q4 2026 |
| **Gouvernance DAO** | Gestion communautaire | Q1 2027 |
| **Support Multi-Chaîne** | Polygon, Arbitrum, Base | Q2 2027 |
| **Reconnaissance Légale** | Validité dans les tribunaux turcs | 2027-2028 |
| **API pour Développeurs** | Point de terminaison API publique | Q3 2026 |

---

## 📊 Analyse Concurrentielle (Mise à Jour)

PoArt est positionné sur le "Point Optimal" qui complète les lacunes des solutions existantes.

| Fonctionnalité | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Coût** | 🆓 Gratuit | 🆓 | 💰 Payant | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI Glisser-Déposer** | ✅ Très Facile | ❌ CLI | ⚠️ Moyen | ⚠️ Moyen | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Export Multi-Format** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Aperçu Temps Réel** | ✅ En Direct | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Contrôles Confidentialité** | ✅ 3 Modes | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Hachage Côté Client** | ✅ Confidentialité | ✅ | ❌ Téléchargement | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Métadonnées Forensiques** | ✅ Complet | ❌ | ❌ | ⚠️ Limité | ❌ | ⚠️ | ❌ | ⚠️ |
| **Vérification QR** | ✅ Instantanée | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Limitation Débit** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Ancrage Blockchain** | 🔄 Feuille de Route | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Support Turc** | ✅ Natif | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Légende :**
- ✅ : Support complet / disponible
- ⚠️ : Limité / dans les plans payants
- ❌ : Aucun / non supporté
- 🔄 : Dans la feuille de route (en développement)
- 🆓 : Complètement gratuit
- 💰 : Payant / abonnement requis

### Lacunes des Concurrents, Forces de PoArt

| Moins | Concurrents | PoArt |
|-------|-------------|-------|
| **Difficulté d'Utilisation** | CLI, connaissance API, portefeuille requis | Glisser-déposer, terminé en 3 clics |
| **Barrière de Coût** | Abonnement $50-500/mois | 100% gratuit |
| **Confidentialité** | Le fichier est téléchargé sur le serveur | Côté client, le fichier ne part jamais |
| **Données Forensiques** | Seulement horodatage | IP, localisation, appareil, temps - tout |
| **Support Turc** | Aucun ou très limité | Support linguistique natif |
| **Open Source** | Boîte fermée | Tout le code ouvert sur GitHub |

---

## 🧬 Structure de Données du Protocole (JSON Schema)

**Chaque certificat [PoArt] a une carte d'identité JSON portable et vérifiable produite dans la norme suivante.**

> **Note :** Ce format JSON d'identité est le format de certificat présenté aux utilisateurs. Dans les enregistrements de registre, `registry.asset` est utilisé au lieu de `identity.asset_data` (mappage : `identity.asset_data` == `registry.asset`).
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

## 🔬 Profondeur Technique : Algorithme de Sceau

### Fonctions de Hachage Déterministes
```javascript
// Fonctions Auxiliaires : Convertir le résumé en chaîne hexadécimale
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Convertir la chaîne en tableau d'octets
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Génération de chaîne forensique canonique (v1.0 : ordre de champ fixe + UTF-8 + délimiteur \n)
// Note Phase 2 : Transition vers JSON canonique avec RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Processus de Production de NotarySeal (Entièrement Déterministe)
```javascript
// 1. Calcul de FileHash (côté client)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Collecte de données forensiques (utilisation d'horodatage unique)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Génération d'horodatage unique
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Même horodatage
  };
  
  return { forensics, timestamp };
}

// 3. Création d'EvidenceRoot (avec encodage canonique)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Génération de NotarySeal (utilisation du même horodatage)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Fonctions auxiliaires de masquage (support IPv4 et IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Vérification IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 ou format inconnu
  return "***";
}
```

### Flux de Vérification (Deux Niveaux)

#### Quick Verify (Vérification Rapide)
```javascript
// Vérifie uniquement le hash du fichier (drapeau rouge rapide)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Récupérer du registre
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Comparaison de hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Original - Le hash du fichier correspond"
    };
  } else {
    return {
      valid: false,
      message: "❌ Faux - Le fichier a été manipulé"
    };
  }
}
```

#### Full Verify (Vérification Complète)
```javascript
// Régénère et vérifie EvidenceRoot et NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Récupérer du registre
  const cert = await fetchFromRegistry(certificateId);

  // 1) Vérification de FileHash (drapeau rouge rapide)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Faux - Le hash du fichier ne correspond pas" };
  }

  // 2) Régénérer EvidenceRoot (avec données forensiques stockées dans le registre)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Ne correspond pas - EvidenceRoot ne tient pas" };
  }

  // 3) Régénérer NotarySeal (avec le même horodatage + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Ne correspond pas - NotarySeal ne tient pas" };
  }

  // Optionnel : En Phase 2, vérifier également signer_sig avec attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Signature invalide" };

  return { valid: true, message: "✅ Original - Vérification complète réussie" };
}
```

> **Notes Importantes :**
> - **Quick Verify :** Vérifie uniquement le hash du fichier pour une utilisation rapide.
> - **Full Verify :** Vérifie toutes les couches du protocole (EvidenceRoot + NotarySeal).
> - Toutes les opérations de hachage sont effectuées de manière déterministe avec encodage et délimiteurs fixes.
> - **Norme de canonicalisation v1.0 :** Ordre de champ fixe + encodage UTF-8 + délimiteur `\n`.
> - **Plan Phase 2 :** Transition vers JSON canonique avec RFC 8785 (JCS - JSON Canonicalization Scheme).
> - En mode masqué, le calcul d'EvidenceRoot et NotarySeal est effectué avec des données forensiques masquées ; ainsi la vérification reste déterministe.
> - Un seul horodatage est utilisé dans tout le processus (forensique + NotarySeal) ; le déterminisme est garanti.
> - **Noms de champs forensiques :** `ip_masked`, `location`, `device`, `timestamp` (code et registre entièrement compatibles).
> - **Chemin de registre :** `certificate.asset.fingerprints` (entièrement compatible avec le code de vérification).
> - **signer_sig dans le registre :** Le champ `proof.signer_sig` est nécessaire pour Full Verify.
> - Le mécanisme SignerSignature sera activé en Phase 2 avec Solana Wallet Adapter ; en v1.0, la vérification peut être faite avec `attestation_pubkey`.

---

## 📈 Statistiques d'Utilisation (Objectifs Q1 2026)

| Métrique | Objectif | Statut |
|--------|--------|--------|
| **Certificats Totaux** | 1,000 | 🔄 Progrès |
| **Utilisateurs Actifs** | 500 | 🔄 Progrès |
| **Nombre de Vérifications** | 5,000 | 🔄 Progrès |
| **Temps de Disponibilité** | 99.9% | ✅ Actif |
| **Temps de Réponse Moyen** | <200ms | ✅ Optimal |

---

## 🌍 Communauté et Support

- **Twitter :** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web :** [ilhanart.org](https://ilhanart.org)
- **Email :** galeri@ilhanart.org

---

## 🙏 Contributeurs

Le protocole PoArt continue de se développer avec les contributions de la communauté open source.

**Pour contribuer :**
1. Forkez le dépôt
2. Créez une branche de fonctionnalité (`git checkout -b feature/amazing-feature`)
3. Committez (`git commit -m 'Add amazing feature'`)
4. Poussez (`git push origin feature/amazing-feature`)
5. Ouvrez une Pull Request

### 🛠️ De Quoi Avons-Nous Besoin Maintenant ? (Appel à l'Aide)

Le Protocole PoArt recherche des développeurs expérimentés dans les domaines suivants pour les développements de **Phase 2** :

* **Supabase Edge Functions :** Déplacer la protection contre le spam côté serveur.
* **Solana Web3.js :** Intégration de signature de portefeuille.
* **IPFS / Arweave :** Intégration de services d'archivage et d'épinglage.

> Veuillez lancer une discussion dans l'onglet "Issues" avant d'ajouter une fonctionnalité.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital"*

## 🧾 Licence

Licence MIT © 2026 İlhan Art Gallery Initiative

Voir [![Licence](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) pour les conditions complètes.

---

## 💬 Crédits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Sécurité](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Plateforme](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![Licence](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Ce projet est développé par l'initiative [İlhan Art Gallery], et ses codes sources sont accessibles publiquement pour la transparence.**

**PROTOCOLE V1.0 // SCELLÉ AVEC SHA-512**

*© 2026 İLHAN ART | TOUS LES DROITS RÉSERVÉS POUR LES ŒUVRES D'ART, LES VISUELS ET LES IDÉES.*

---
