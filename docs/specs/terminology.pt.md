# 📚 GLOSSÁRIO DE TERMINOLOGIA E CONCEITOS
> **"Compreender a linguagem deste protocolo é compreender a sua visão."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Infraestrutura Central

**PoArt Forensic Engine (PFE)** representa a camada central que incorpora a lógica nuclear e o funcionamento técnico por trás do protocolo [PoArt]. Este é o "motor forense" que transforma os dados brutos de produção de uma obra de arte em **prova digital** verificável e imutável.

### 🧩 Por que "PoArt Forensic"?

- **PoArt (Proof of Art):** O foco do motor é vincular o valor de um ativo digital não à especulação, mas ao **processo de produção comprovável**.
- **Forensic (Verificação Forense):**
  - **Definição Técnica:** Abordagem de algoritmo e cadeia de registos para verificar que os dados do processo de produção (pinceladas, timelapse, logs) não foram manipulados.
  - **Camada Filosófica:** A afirmação de transformar a produção humana que contém **tempo, esforço e custo de decisão** numa realidade mensurável, em contraste com a "produção instantânea" da inteligência artificial.

> Nota: A integração blockchain (ex.: Solana) é tratada como uma **Chain Anchor Layer** a ser definida separadamente para verificação/registo, não como o núcleo do PFE.

### 🛠️ Âmbito Técnico v1.0

**PoArt Forensic Engine (PFE) v1.0** é construído sobre **3 pilares principais** em vez de modelos financeiros complexos:

1. **Hashing & Sealing (Selagem):**  
   O PFE processa deterministicamente todos os elementos dentro do Evidence Pack (ficheiro da obra, vídeo, JSON/log, assinatura, etc.) e produz o valor único **NotarySeal**.

   **Conceitos centrais (v1.0):**
   - **FileHash (impressão digital da obra):** Hash gerado a partir dos bytes do ficheiro da obra.
   - **EvidenceRoot (raiz do pacote de evidências):** Resumo raiz que representa a integridade do Evidence Pack (raiz Merkle ou hash canónico do manifesto).
   - **NotarySeal (selo final / Saída do PFE):** O selo final gerado a partir da combinação de EvidenceRoot + tempo + assinatura.

   **Fórmulas (claramente visíveis para investidores):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Definições de Payload Canónico (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Nota: O valor referido como saída do PFE é **NotarySeal**. O mecanismo **SignerSignature** será ativado na Fase 2 (com Solana Wallet Adapter); na v1.0 atual, é utilizada a própria assinatura de atestação do sistema. A chave pública de atestação é publicada no registo no campo `issuer.attestation_pubkey`.

2. **Indexing (Arquivamento):**  
   Regista qual carteira, em que data, submeteu **Labor Proof (Prova de Trabalho)** para qual obra, numa camada de registo transparente e consultável.  
   *(Esta camada pode ser uma base de dados; a integração blockchain é tratada separadamente como "Chain Anchor Layer".)*

3. **Verification (Verificação):**  
   Quando a originalidade de uma obra é questionada, o PFE reprocessa as evidências brutas; testa matematicamente com certeza absoluta se os valores calculados de **EvidenceRoot / NotarySeal** correspondem ao registo no arquivo.

---

### 🧮 O Teorema do Valor PoArt (The Value Theorem)

O protocolo [PoArt] relaciona o valor ($V$) de um ativo digital não com a perceção subjetiva do mercado, mas com a **realidade física do processo de produção**.

A Inteligência Artificial (IA) elimina o processo ao dar o resultado instantaneamente ($t \to 0$). [PoArt], por outro lado, trata o valor como a acumulação de componentes de **tempo, trabalho e vontade**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definição das Variáveis

- **$\int dt$ (Acumulação do Processo):**  
  O valor não é um "output" instantâneo; é um **processo** que se acumula entre $t_{\text{start}}$ e $t_{\text{end}}$. À medida que a duração diminui (produção por IA), o resultado do integral aproxima-se de 0.

- **$P_{\text{labor}}(t)$ (Poder de Trabalho Instantâneo):**  
  Representa a intensidade do esforço mental e físico despendido no momento da produção. À medida que o esforço comprovável aumenta, o integrando cresce.  
  > Nota: Este termo pode ser normalizado na prática através de "sinais de trabalho mensuráveis/comprováveis".

- **$I_{\text{agency}}(t)$ (Coeficiente de Vontade):**  
  É a capacidade do produtor de assumir riscos e tomar decisões. Assume um valor entre $0$ e $1$.
  - **IA ($I \approx 0$):** Executa comandos, não assume riscos, não paga custos.
  - **Humano ($I \to 1$):** Muda decisões, hesita, assume riscos.

- **$U_{\text{irreversible}}$ (Singularidade Irreversível):**  
  Enquanto na produção digital é possível desfazer (`Ctrl+Z`); na produção física (tinta aplicada na tela, mármore esculpido, gestos em transmissão ao vivo) não há retorno. Esta **irreversibilidade** é um termo adicional que cria "singularidade" (caráter não fungível) na obra.

### 🔎 Análise de Caso: IA "Produção Instantânea" vs. Humano "Processo Comprovado"

O cenário seguinte demonstra como o **Teorema do Valor PoArt** funciona na prática e porque as produções de IA obtêm pontuações baixas no padrão [PoArt].

#### Cenário A: Produção Visual com IA em 10 Segundos

- **Duração ($\Delta t$):** $10$ segundos (praticamente sem processo)
- **Poder de Trabalho ($P_{\text{labor}}$):** $1$ unidade (apenas escrever o comando)
- **Coeficiente de Vontade ($I_{\text{agency}}$):** $0.01$ (sem risco, sem custo)
- **Irreversibilidade ($U_{\text{irreversible}}$):** $0$ (pode ser desfeito / copiado)

**Resultado:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Interpretação:** Mesmo que a produção seja perfeita; como não houve processo vivido e não contém vontade/risco, o valor [PoArt] aproxima-se de $0$.

#### Cenário B: Produção Física de 6 Horas em Transmissão ao Vivo

- **Duração ($\Delta t$):** $6$ horas ($21{,}600$ segundos)
- **Poder de Trabalho ($P_{\text{labor}}$):** $0.5$ unidades (continuidade de esforço físico e mental)
- **Coeficiente de Vontade ($I_{\text{agency}}$):** $0.9$ (mudança de decisões, assunção de riscos, escolhas irreversíveis)
- **Irreversibilidade ($U_{\text{irreversible}}$):** $>0$ (marcas físicas não podem ser desfeitas)

**Resultado:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Interpretação:** À medida que o processo se prolonga e a vontade (risco) aumenta, o valor acumula-se cumulativamente. O termo $U_{\text{irreversible}}$ é uma contribuição adicional que cria "singularidade" (caráter não fungível) na obra.

---

### ✅ Conclusão: Bloqueio do Valor com Prova (Proof-Bound Value)

Este teorema retira a afirmação de valor do [PoArt] de ser um "gosto" ou "narrativa de mercado" e vincula-a a uma **realidade de produção comprovável**.

1. **Sem Processo Não Há Valor:**  
   A IA elimina o processo na produção instantânea ($t \to 0$). À medida que a janela do processo se estreita, o resultado do integral diminui por necessidade matemática:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Vontade e Risco São Multiplicadores:**  
   [PoArt] mede não apenas o "tempo gasto", mas também a camada real de decisão, risco e custo durante esse tempo. O valor de uma produção sem risco (IA) é baixo:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Singularidade é Prova Física, Não Marketing:**  
   Marcas irreversíveis na produção física (golpe de pincel na tela, fragmento de mármore) estão fora da lógica de `Ctrl+Z` do digital. Esta irreversibilidade ($U_{\text{irreversible}}$) singulariza ontologicamente a obra.

> **🔐 RESUMO:** Embora o teorema do valor possa parecer incerto como medição (mesmo que não possa ser medido 100% na vida real), o objetivo desta fórmula é mostrar a construção e direção das variáveis. O que é raro na era da IA não é a "imagem"; é o **trabalho, tempo e vontade comprováveis.** [PoArt] mede esta escassez e regista-a com o **Evidence Pack**.

### 🏛️ Importância do Conceito "Engine" (Motor)

Os tokens lançados em Pump.fun ou plataformas similares são frequentemente apenas **"bilhetes de acesso"**. **PoArt Forensic Engine (PFE)**, por outro lado, é a **camada de lógica constitucional** que determina quais direitos esse bilhete protege, como o trabalho será registado e como a arte/ciência/tecnologia será preservada.

> **Nota:** A razão pela qual iniciámos este projeto no Pump.fun é porque não tínhamos liquidez suficiente e número suficiente de seguidores. Embora usar os dados existentes não seja estrategicamente ideal, podemos dizer que foi a decisão mais correta. Independentemente do orçamento e recursos, definir a lógica deste motor no GitHub prova que o projeto não é apenas uma especulação financeira, mas uma visão de **infraestrutura de software** de longo prazo e **biblioteca nacional digital**.

---

## 🎨 PROTOCOLO [PoArt] DE PROVA DE TRABALHO (Proof of Art Protocol v1.0)

> **"Artista Real, Produção Real, Valor Real."**

Este protocolo é um **mecanismo de defesa biológico e intelectual** desenvolvido contra fraudadores anónimos que infestam o ecossistema cripto, imagens de inteligência artificial produzidas em 5 minutos e a cultura "Pump & Dump" (Inflacionar e Despejar).

---

## a) O que é [PoArt]? (Definição Filosófica e Técnica)

**Proof of Art [PoArt];** é um padrão de verificação institucional que garante que o valor por trás de um ativo na blockchain é baseado não na especulação, mas em **trabalho humano**, **tempo** e **energia física** verificáveis.

Assim como o Bitcoin cria valor com *"Eletricidade e Poder de Processamento"* **(Proof of Work)**; projetos compatíveis com [PoArt] criam valor com *"Talento Gasto e Tempo Humano"*. Faz "Stake" do Tempo.

Elimina o risco de *"O desenvolvedor (Dev) vendeu, o projeto acabou"* em Pump.fun e plataformas DEX; porque aqui o valor está escondido não no código, mas na **continuidade da produção**.

> **[PoArt] não diz ao seu participante "Confie em nós"; diz "Aqui estão as provas, veja com os seus olhos, verifique com a sua matemática".**

---

## b) O Padrão de 5 Pilares [PoArt] (The 5 Pillars of Truth)

Estes 5 itens são filtros não manipuláveis que um projeto deve passar para receber o selo [PoArt].

### 1) Prova de Identidade ao Vivo (Live Identity Proof)

- **Problema:** O mundo cripto está cheio de fundadores anónimos (Devs) que recolhem o dinheiro e abandonam o projeto.
- **Solução [PoArt]:** O produtor prova não apenas o seu cartão de identidade, mas a sua **presença no momento da produção**. Isto inclui sessões de transmissão ao vivo onde há interação com a comunidade e pedidos específicos instantâneos são atendidos, não vídeos pré-gravados.  
  (Ex.: *"Escreva a data de hoje e o número do bloco atual no canto direito da tela"*)
- **Lema:** *"Bots podem pintar, mas bots não suam e não improvisam."*

### 2) Prova de Trabalho e Processo (Labor & Process Proof)

- **Problema:** Imagens de IA (Inteligência Artificial) produzidas em 2 segundos e pinturas a óleo feitas em 2 meses receberem o mesmo tratamento de "jpeg" no mundo digital.
- **Solução [PoArt]:** O processo de "gravidez e nascimento" da obra é registado. Fases de esboço, camadas de tinta, horas cumulativas gastas e o processo físico que o artista viveu ao criar essa obra são documentados. Isto adiciona **"Custo de Tempo" (Time Cost)** ao token. Quanto mais difícil for produzir um ativo, mais sólido é o seu valor.

### 3) Prova de Valor Estético (Aesthetic Value Proof)

- **Problema:** A cultura "Meme" ignorar a estética e profundidade artística, focando apenas na comédia instantânea, resultando em projetos "Hype" de curta duração.
- **Solução [PoArt]:** O projeto deve ter padrões artísticos académicos, teoria da cor, regras de composição e conhecimento de materiais (Impasto, Textura, etc.). O conteúdo não deve apenas fazer rir; deve despertar admiração no espectador e ter **valor de coleção**.

### 4) Inovação Conceptual (Conceptual Novelty)

- **Problema:** Milhares de coins de cães/gatos que são cópias uns dos outros, longe da criatividade.
- **Solução [PoArt]:** O projeto deve construir uma nova ponte que combine arte, ciência, filosofia ou tecnologia de forma significativa.  
  (Ex.: Combinar a clássica estátua de David com dados do mercado cripto; trabalhar a ideia de "petrificação" da perceção humana através disso e ser capaz de fundamentar com fontes científicas.)  
  A obra não deve ser apenas um festim visual; deve também ser um desafio intelectual que faça pensar sobre **Ciência, Filosofia ou Tecnologia**.

> [!IMPORTANT]
> **Exemplo de Referência (Efeito Las Palmitas):**  
> No bairro de Las Palmitas, no México, que lutava contra o crime, mais de 200 casas foram transformadas num enorme festim de arco-íris. Como resultado desta intervenção estética, as taxas de criminalidade no bairro diminuíram até certo ponto, e os jovens começaram a interessar-se pela arte em vez de gangues. A mudança estética recodificou o respeito das pessoas pelo seu ambiente e uns pelos outros (Coesão Social).
>
> **Expectativa:** Um projeto para entrar na lista [PoArt] deve conter, como no exemplo acima, uma relação causa-efeito sociológica, científica ou filosófica além da pura estética visual. Como o único ativo que não pode ser comprado com dinheiro é o "Tempo", neste protocolo o tempo deve ser comprovado fazendo stake como garantia. A base conceptual do projeto deve ser tão forte e universal que, mesmo num cenário de CTO (Community Take Over) anos depois, a comunidade possa herdar este legado e continuar autonomamente o potencial inovador do projeto.

### 5) Vontade Não Algorítmica (Non-Algorithmic Agency)

- **Problema:** Produções digitais perfeitas mas sem alma, que se repetem.
- **Solução [PoArt]:** A vontade original do ser humano que pode errar, assumir riscos e experimentar flutuações emocionais deve ser sentida na obra. A incerteza nas pinceladas, as reações inesperadas do material e as decisões instantâneas do artista são a **Assinatura Biológica** que distingue a obra de "Produção Mecânica".

---

## c) Mecanismo de Verificação & Anti-Fraude

Este sistema garante que o projeto permaneça fiável e vivo não apenas "no início", mas "para sempre".

### 📦 Pacote de Evidências (Evidence Pack - The Digital Twin)

Por trás de cada obra certificada [PoArt], há um pacote de dados encriptado e com carimbo temporal que os investidores podem descarregar:

- **Gravações de Vídeo RAW:** Imagens brutas ininterruptas do momento de produção.
- **Análise de Metadados:** Data de criação do ficheiro, informações do dispositivo utilizado e dados de localização (Cidade-País).
- **Referências Físicas:** Provas de que a obra existe no mundo físico  
  (Ex.: Jornal atual ao lado da obra ou dados da blockchain naquele momento).

> *Nota de consistência:* A expressão "pacote de evidências" liga-se à linha **Evidence Pack → EvidenceRoot → NotarySeal** nas secções anteriores; ou seja, a integridade do pacote é representada por um selo verificável.

### 🔄 Renovação de 365 Dias (The Sustainability Protocol)

- **Característica Revolucionária:** Em projetos cripto, o "Dev" (Desenvolvedor) lança o token e geralmente desaparece 1-2 meses depois (Soft Rug). [PoArt] torna isto impossível.
- **Regra:** O estatuto "Verified Artist" (Artista Verificado) não é vitalício. É válido apenas por **1 ano**.
- **Funcionamento:** O artista/desenvolvedor é obrigado a apresentar à comunidade uma **nova obra grande e comprovável** a cada 365 dias.
- **Cenário Exemplo:** Lançou o projeto em 2026. Em janeiro de 2027, o sistema dá o aviso "Prazo de Prova Expirado". Se o artista não apresentar uma nova exposição, uma nova obra física ou uma nova integração tecnológica, o "Emblema de Confiança" do projeto cai.
- **Resultado:** Este sistema garante que **o conteúdo nunca fique desatualizado** e que o investidor não viva o medo de *"O desenvolvedor ainda está aqui?"*. O projeto transforma-se num estúdio vivo.

### 🚩 Bandeira Vermelha (Red Flag Protocol)

**Em caso de qualquer fraude detetada pela comunidade ou algoritmos (uso de IA, obra roubada, vídeo manipulado):**

1. O certificado é imediatamente marcado como **"ANULADO" (VOID)**.
2. Os pacotes de evidências são publicamente etiquetados como **"Falso"**.
3. O projeto é colocado na lista negra [PoArt]. Isto reforça o facto de que a **reputação é a única moeda** num mundo descentralizado.
4. Não pode ser feita referência a declarações [PoArt] em qualquer publicação, a única fonte válida é https://www.ilhanart.org/public-registry

---

## d) Conclusão: Não é Casino, é Museu

**Pump.fun e as Exchanges Descentralizadas (DEX) são infelizmente casinos atualmente; as luzes piscam, todos perseguem ganhos rápidos e a casa (fraudadores) sempre ganha. A razão pela qual iniciámos o projeto aqui é também porque estamos a tentar melhorar este lugar, e temos o ambiente que alcançará o público existente através das nossas transmissões ao vivo e dos nossos dados existentes.**

**[PoArt] é uma fortaleza construída no meio deste casino.**

- 🎰 O casino baseia-se em jogos de cartas; nós baseamo-nos na **realidade física**.
- 🃏 O casino está aberto à fraude; nós estamos abertos a **provas transparentes**.
- ⏳ O casino é temporário; nós focamo-nos na **eternidade da arte e da ciência**.

**Um token que usa este protocolo não é apenas uma "coin"; é uma ação digital que contém suor, tinta, código e filosofia por trás.**

---

## 🗳️ 6) GOVERNANÇA E REGISTO PÚBLICO (Governance & Public Registry)

**O objetivo desta secção é: retirar o padrão [PoArt] do plano de "confiança em pessoas" e transformá-lo numa infraestrutura pública sustentável com registo + verificação + supervisão da comunidade.**

### 6.1 Public Registry (Registo Público)

- **Public Registry:** Todos os dados aprovados são registados em `ilhanart.org/registry` (ou GitHub Registry).

**Lógica de registo (padrão sugerido - em formato JSON path):**

Cada registo que entra no cadastro carrega no mínimo os seguintes campos centrais verificáveis:

- **Identidade & Estado:**
  - `certificate_id` (referência legível)
  - `status` (active / void)
  - `void_reason` (se aplicável)
  - `visibility` (private / masked / public)
  - `created_at` (carimbo temporal)

- **Instituição Emissora:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informação da Obra:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (se possível; para identidade do detentor do token)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Dados Forenses:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Provas Criptográficas:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Governança:**
  - `governance.decision`
  - `governance.review_notes`

O registo pode ter duas camadas:
- **1)** Índice legível por humanos (listagem web / pesquisa / filtro)
- **2)** Manifesto legível por máquina (registos JSON; para verificação PFE)

**O "registo" aqui torna-se verificável com a cadeia Evidence Pack → EvidenceRoot → NotarySeal do PFE. O registo oferece não "alegação", mas alvo de verificação.**

---

### 6.2 Processo de Candidatura PoArt Verified

**As candidaturas PoArt Verified são avaliadas pela İlhanArt Gallery de acordo com os 5 padrões PoArt. O feedback da comunidade é considerado, mas a decisão final depende da equipa curatorial. As decisões são explicadas de forma transparente e registadas em ilhanart.org/registry.**

#### Processo de Candidatura

**Candidatura:**
- O artista/projeto faz candidatura PoArt Verified
- O Evidence Pack é preparado (gravações de vídeo, metadados, links de transmissão ao vivo)
- A candidatura é enviada à İlhanArt Gallery

**Análise (30 Dias):**
- A equipa da galeria analisa detalhadamente o Evidence Pack
- Todos os 5 padrões PoArt são verificados:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Entrevista com o artista (opcional)

**Consulta à Comunidade:**
- O Evidence Pack é partilhado publicamente durante o processo de candidatura
- A comunidade pode fornecer feedback através de ilhanart.org
- Detentores de tokens (mínimo 10.000 $CULTURE) podem particularmente fazer sugestões
- **Todo o feedback é considerado durante o processo de análise**
- **No entanto, a decisão final depende da avaliação curatorial**

**Decisão:**
- A galeria aprova ou rejeita a candidatura
- A justificação da decisão é explicada de forma transparente
- Se aprovado → emblema PoArt Verified
- Se rejeitado → nova candidatura pode ser feita após 6 meses

**Transparência:**
- Todas as candidaturas e decisões são registadas em ilhanart.org/registry
- O registo de decisão é publicado publicamente:
  - Data da candidatura
  - Resumo do processo de análise
  - Decisão (Approved / Rejected)
  - Justificação da decisão (explicação breve)
  - Resumo do feedback da comunidade (anónimo)

#### Por que Decisão Curatorial?

**Controlo de Qualidade:**  
O estatuto PoArt Verified é um emblema com padrões elevados. A avaliação curatorial garante a manutenção destes padrões.

**Prevenção de Manipulação Especulativa:**  
A governança on-chain completa (ex.: Realms, votação DAO) não é tecnicamente possível com tokens Pump.fun. Sistemas de votação off-chain são vulneráveis a manipulação de baleias e ataques coordenados. A decisão curatorial elimina este risco.

**Eficiência Operacional:**  
Em vez de mecanismos de votação complexos, processo de decisão rápido e claro. Os artistas obtêm resultado dentro de 30 dias.

**Participação da Comunidade:**  
O feedback da comunidade é totalmente considerado e afeta o processo de decisão. No entanto, a decisão final depende da equipa curatorial protegida contra manipulação.

**Futuro:**  
Quando o projeto amadurecer (2027+), o mecanismo de consulta à comunidade pode ser fortalecido. No entanto, a proteção do padrão curatorial é permanente.

---

### 6.3 Token Utility (Áreas de Utilização do Token)

**Benefícios fornecidos aos detentores de tokens $CULTURE:**

**1. Acesso Prioritário a Eventos da Galeria:**
- Direito de fazer exposição de 1 semana por ano na İlhanArt Gallery (direito transferível)
- Descontos em drop painting
- Direito a desconto entre 10% e 30% em pinturas na galeria

**2. Acesso Completo ao PoArt Registry:**
- Registos detalhados de todas as obras autenticadas
- Versões completas dos Evidence Packs
- Ferramentas de verificação forense

**3. Advisory Voting:**
- Direito de consulta em candidaturas PoArt Verified
- Acesso a canais de feedback da comunidade
- Participação em discussões de governança

**4. Conteúdo Exclusivo:**
- Conteúdos de bastidores do estúdio
- Entrevistas com artistas e vídeos de processo
- Acesso a documentação técnica

**Nota:**  
Os detentores de tokens dão advisory vote (voto consultivo). A decisão final pertence à equipa curatorial. Esta estrutura foi escolhida para prevenir manipulação de baleias e ataques especulativos. Não há staking reward porque procuramos participantes culturais de longo prazo, não capital mercenário de curto prazo.

---

### 6.4 Metadata Sync (Correspondência com o Mundo Físico)

- **Metadata Sync:** Os dados técnicos no registo devem corresponder 100% ao ativo físico.

**Definir tecnicamente "correspondência 100%" (clareza sugerida):**

- **Correspondência mínima (obrigatória):**
  - O hash do ficheiro em mãos deve ser **exatamente igual** a `asset.fingerprints.sha256/sha512` no registo.
  - Quando `proof.notary_seal` no registo é regenerado (se o Evidence Pack existir), deve ser **exatamente igual**.

- **Correspondência de referência física (tipo de prova):**
  - Provas como obra física mostrada em transmissão ao vivo + referência de data/bloco devem ser consistentes com o Evidence Pack.

- **Conformidade de privacidade:**
  - Campos como IP/localização em visibilidade `masked` são publicados **em conformidade com o padrão de mascaramento**.

---

### 6.5 Contestação, Análise e Anulação (Dispute & Revocation)

O registo não é apenas um mecanismo de "aprovação"; é um mecanismo de **supervisão viva contra fraude**.

- Quando uma contestação é iniciada, o registo pode ser colocado em modo **"review"**.
- Se fraude for detetada, é marcado como `status: void` e a justificação é adicionada:
  - `void_reason` (uso de IA / roubo / manipulação, etc.)
  - `revoked_at` (hora da anulação)
- A fonte da decisão de anulação é claramente visível no registo:
  - análise curatorial / contestação da comunidade / nota de análise forense (o que for aplicável)

> **Esta parte é a correspondência no registo do conceito VOID na secção "Red Flag Protocol".**

---

### 6.6 Exemplo de Registo no Cadastro (Legível por Máquina)
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

> *Nota: `asset.fingerprints.sha512` e outros valores de hash foram abreviados para fins de demonstração; na aplicação real, usa-se uma sequência de caracteres hexadecimais de comprimento total.*

---

## 7) 🔐 SELO TÉCNICO (NOTARY SEAL)

**Algoritmo de selo inquebrável produzido pelo PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Protocolo [PoArt] de Notário Digital & Prova Forense (Beta v1.0)

> **"Cultura é maior que capital. Proteja as suas obras hoje, leve-as para amanhã."**

---

## Por que é Público?

A verdadeira segurança vem da transparência. Graças ao nosso sistema **Public Registry (Registo Público)**, qualquer pessoa em qualquer parte do mundo pode verificar em segundos se o ficheiro que tem em mãos é original, sem precisar de qualquer autoridade.

---

## 🧩 Por que Existem Múltiplos "Módulos de Visibilidade"?

A parte mais crítica do código é esta (menu de seleção de visibilidade). Estas opções permitem aos utilizadores estabelecer o equilíbrio **"Privacidade vs. Transparência"**:

### 🔒 Privado (Private)

- **Cenário:** O artista ainda não quer publicar a obra mas quer carimbar a data e provar "eu fiz isto nesta data".
- **O que o Código Faz:** Escreve os dados na base de dados mas aplica a etiqueta `visibility: "private"`. Mais tarde, ao escrever a política "Public Read", podes ocultar estes registos do público dizendo `WHERE visibility = 'public'`.

### 🕶️ Mascarado (Masked)

- **Cenário:** O artista quer transparência mas tem medo de que o seu endereço residencial (localização IP) seja encontrado.
- **O que o Código Faz:** As funções `maskIP` e `maskLoc` funcionam no lado do JavaScript. Converte o endereço IP para o formato `88.241.***.***`, a localização para o formato `***/TR` e envia a versão censurada para a base de dados.
- **Nota de Privacidade:** O mascaramento é feito no navegador, o Supabase não vê a localização real. **No entanto:** Se APIs de terceiros como ipapi.co são usadas para dados de localização, estes fornecedores veem o endereço IP no momento do pedido.
- **Selagem em Modo Masked:** O cálculo de EvidenceRoot e NotarySeal é feito com dados forenses mascarados; assim a verificação permanece determinística.

### 🌍 Público para Todos (Public)

- **Cenário:** Transparência total. De acordo com o padrão [PoArt], é declarado abertamente onde, quando e de que rede a obra foi produzida.

---

## 💡 Inovação Tecnológica

PoArt não é apenas um sistema de upload de ficheiros. É um motor de **"Cadeia de Custódia Forense" (Forensic Chain of Custody)** que traz um novo padrão ao fundir três camadas tecnológicas diferentes num único recipiente.

**A camada descrita como "motor" nesta secção corresponde ao núcleo do PoArt Forensic Engine (PFE) na terminologia anterior.**

### 1) Client-Side Hashing (Privacidade Máxima)

Os seus ficheiros de obras nunca são carregados para o servidor. O nosso motor baseado em navegador (Client-side) calcula o hash (resumo digital) do ficheiro no seu próprio computador. Apenas esta impressão digital e metadados são enviados para o servidor.

> **Nota de Privacidade:** O ficheiro da obra não é carregado para o servidor e é assim protegido. No entanto, os dados forenses (IP/localização) são partilhados de acordo com o modo de visibilidade selecionado (private/masked/public).

### 2) Forensic Data Fusion (Poder Forense)

É muito mais do que um simples carimbo temporal (Timestamp). O sistema combina os seguintes dados num único "Genesis Seal":

- **Resumo Digital (SHA-512):** Impressão digital que se quebrará se um único pixel da obra mudar, usando o padrão de resumo criptográfico (SHA-512).
- **Localização & Tempo:** Data com precisão de milissegundos, país, cidade e dados de distrito onde a transação foi feita.
- **Identidade do Dispositivo:** Sistema operativo, navegador e tipo de dispositivo (análise User-Agent).

---

## 🛡️ Áreas de Utilização e Benefícios

Se és um artista, escritor ou designer, dizer "Eu fiz isto antes" não é suficiente, precisas de provar.

**Uma obra selada com PoArt:**

- **Prova Matemática:** Se um único pixel do teu ficheiro mudar, o sistema deteta. A manipulação é impossível.
- **Base Jurídica:** Está registado em que data, em que cidade e de que dispositivo a obra foi selada.
- **Certificado Instantâneo:** Produz em segundos um **"Certificado de Identidade do Ativo"** único, com código QR e selado.

---

## ⚙️ Arquitetura do Sistema e Especificações Técnicas

O sistema é desenhado numa arquitetura "Serverless" (Sem Servidor), focada em alto desempenho e escalabilidade.

| Camada | Tecnologia | Descrição |
|--------|-----------|----------|
| **Criptografia** | SHA-256 & SHA-512 | Resumo criptográfico de dupla camada |
| **Base de Dados** | Supabase (PostgreSQL) | Estrutura de dados JSONB, políticas RLS |
| **Dados Forenses** | ipapi.co API | Tripleto IP/Localização/Tempo |
| **Renderização** | html2canvas + jsPDF | Produção PNG/PDF do lado do cliente |
| **Frontend** | Vanilla JavaScript | Zero dependência de framework |
| **Segurança** | Client-side hashing | O ficheiro nunca é carregado para o servidor |

### Características em Destaque

| Característica | Detalhe | Nos Concorrentes? |
|---------|-------|-------------|
| **UI Drag & Drop** | Arrastar e soltar ficheiro, pré-visualização instantânea | ❌ A maioria não tem |
| **Exportação Multi-Formato** | PNG, JSON, PDF - um clique | ⚠️ Limitado |
| **Pré-visualização em Tempo Real** | Pré-visualização ao vivo do certificado | ❌ Não existe |
| **Controlos de Privacidade** | Opções Private/Masked/Public | ❌ Não existe |
| **Client-Side Hashing** | O ficheiro nunca vai para o servidor | ✅ Apenas em alguns |
| **Metadados Forenses** | IP, localização, dispositivo, tempo - tudo junto | ❌ Fragmentado |
| **Verificação QR** | Código QR de verificação instantânea | ⚠️ Restrito |
| **Rate Limiting** | Proteção contra spam (RLS + Client) | ❌ A maioria não tem |

---

## 🗺️ Roteiro: Futuro "Trustless"

A versão atual **(Beta v1.0)** está otimizada para fornecer velocidade máxima, interface fácil e acesso gratuito ao utilizador final. No entanto, a nossa visão final é migrar para uma estrutura onde nem mesmo o administrador da base de dados (nós) possa intervir.

### Fase 1: Beta v1.0 (Atualmente Online)

**Infraestrutura:**
- Cloud Database (Supabase)
- Registo off-chain (PostgreSQL + backup IPFS)
- Auto-atestação da galeria (centralizado mas transparente)

**Token:**
- Plataforma: Pump.fun
- Liquidez: Raydium (automático)
- Governança: Apenas consultivo (consulta à comunidade)

**Objetivo:**
- Velocidade, remover barreiras de UX
- Fornecer segurança "sem atrito"
- Construção de comunidade

**Token Utility (v1.0):**
- Acesso prioritário a eventos da galeria
- Visualização do PoArt Registry
- Direito de advisory voting

---

### 🚀 Fase 2: Autoridade Descentralizada (2026 Q2-Q4)

Esta fase cobre a transição do sistema de uma estrutura totalmente "Client-Side" para uma estrutura mais segura e descentralizada.

| Característica | O que Traz? | Tech Stack | ETA |
|---------|---------------|------------|-----|
| **Edge Function INSERT** | Bloqueio de spam + segurança da API Key | Supabase Edge (Deno) | Q2 2026 |
| **Assinatura de Carteira** | Identidade descentralizada | Solana Wallet Adapter | Q2 2026 |
| **Backup IPFS/Arweave** | Arquivo descentralizado | IPFS SDK + Pinata | Q3 2026 |
| **Mecanismo de Revogação** | Anulação de certificado falso | DB Schema Update | Q2 2026 |
| **Audit Log** | Registo de consulta forense | Tabela de logs personalizada | Q3 2026 |
| **OpenTimestamps** | Ancoragem Bitcoin | OTS JavaScript | Q4 2026 |

**Governança de Token (v2.0):**
- Votação off-chain (x/web) + assinatura de carteira
- Eleição de representantes da comunidade (primeiros 90 dias)
- Controlo de carteira de operações multi-sig
- Votação consultiva ponderada (com limite de baleias)

**Imutabilidade:**
- Backup do registo com hashes IPFS
- Ancoragem de timestamp Bitcoin
- Preparação para verificação cross-chain

---

### Fase 3: Descentralização Total (2027+)

| Característica | Objetivo | ETA |
|---------|-------|-----|
| **Registo On-Chain** | Registo on-chain Solana | Q1 2027 |
| **Token Utility Melhorado** | Mint NFT, funcionalidades avançadas | Q1 2027 |
| **Suporte Multi-Chain** | Ethereum, Polygon, Base | Q2 2027 |
| **Integração DID** | Identidade Descentralizada | Q3 2027 |
| **Governança Comunitária** | Sistema consultivo fortalecido | Q4 2027 |
| **Reconhecimento Legal** | Validade nos tribunais turcos | 2027-2028 |
| **API para Developers** | Endpoint API público | Q3 2027 |

**Evolução da Governança:**
- v3.0: Modelo híbrido (curatorial + comunidade ponderada)
- 2028+: Governança comunitária total (opcional)
- Controlo de qualidade curatorial sempre preservado

---

## 🧬 Estrutura de Dados do Protocolo (JSON Schema)

**Cada certificado [PoArt] tem um cartão de identidade JSON portátil e verificável produzido no padrão seguinte.**

> **Nota:** Este formato JSON de Identidade é o formato do certificado apresentado ao utilizador. Nos registos do Registry, usa-se `registry.asset` em vez de `identity.asset_data` (mapeamento: `identity.asset_data` == `registry.asset`).
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

## 🔬 Profundidade Técnica: Algoritmo de Selagem

### Funções Hash Determinísticas
```javascript
// Funções Auxiliares: Converter Digest para string hex
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Converter String para byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Produção de string forensics canónica (v1.0: ordem de campos fixa + UTF-8 + delimitador \n)
// Nota Fase 2: Transição para JSON canónico com RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Processo de Produção NotarySeal (Totalmente Determinístico)
```javascript
// 1. Cálculo FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Recolha de dados forenses (uso de timestamp único)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Produção de timestamp único
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Mesmo timestamp
  };
  
  return { forensics, timestamp };
}

// 3. Criação EvidenceRoot (com codificação canónica)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Produção NotarySeal (uso do mesmo timestamp)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Funções auxiliares de mascaramento (suporte IPv4 e IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Verificação IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 ou formato desconhecido
  return "***";
}
```

### Fluxo de Verificação (Dois Níveis)

#### Quick Verify (Verificação Rápida)
```javascript
// Verifica apenas o hash do ficheiro (bandeira vermelha rápida)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Obter do Registry
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Comparação de hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Original - Hash do ficheiro corresponde"
    };
  } else {
    return {
      valid: false,
      message: "❌ Falso - Ficheiro foi manipulado"
    };
  }
}
```

#### Full Verify (Verificação Completa)
```javascript
// Regenera EvidenceRoot e NotarySeal e verifica
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Obter do Registry
  const cert = await fetchFromRegistry(certificateId);

  // 1) Verificação FileHash (bandeira vermelha rápida)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Falso - Hash do ficheiro não corresponde" };
  }

  // 2) Regenerar EvidenceRoot (com forensics armazenado no registry)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Não Corresponde - EvidenceRoot não bate" };
  }

  // 3) Regenerar NotarySeal (com mesmo timestamp + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Não Corresponde - NotarySeal não bate" };
  }

  // Opcional: Na Fase 2, verificar signer_sig com attestation_pubkey também
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Assinatura inválida" };

  return { valid: true, message: "✅ Original - Full Verify passou" };
}
```

> **Notas Importantes:**
> - **Quick Verify:** Verifica apenas o hash do ficheiro para uso rápido.
> - **Full Verify:** Verifica todas as camadas do protocolo (EvidenceRoot + NotarySeal).
> - Todas as operações de hash são feitas deterministicamente, com codificação e delimitadores fixos.
> - **Padrão de canonicalização v1.0:** Ordem de campos fixa + codificação UTF-8 + delimitador `\n`.
> - **Plano Fase 2:** Transição para JSON canónico com RFC 8785 (JCS - JSON Canonicalization Scheme).
> - No modo Masked, o cálculo de EvidenceRoot e NotarySeal é feito com forensics mascarado.
> - Um único timestamp é usado em todo o processo (forensics + NotarySeal); determinismo garantido.
> - **Nomes dos campos forensics:** `ip_masked`, `location`, `device`, `timestamp` (código e registry totalmente compatíveis).
> - **Caminho do registry:** `certificate.asset.fingerprints` (totalmente compatível com o código de verificação).
> - **signer_sig no Registry:** O campo `proof.signer_sig` é necessário para Full Verify.
> - O mecanismo SignerSignature será ativado na Fase 2 com Solana Wallet Adapter; na v1.0, a verificação pode ser feita com `attestation_pubkey`.

---

## 📊 Análise de Concorrentes (Atualizada)

PoArt está posicionado no "Sweet Spot" (Ponto ideal) que completa as lacunas das soluções existentes.

| Característica | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Custo** | 🆓 Grátis | 🆓 | 💰 Pago | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI Drag & Drop** | ✅ Muito Fácil | ❌ CLI | ⚠️ Médio | ⚠️ Médio | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Exportação Multi-Formato** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Pré-visualização em Tempo Real** | ✅ Ao Vivo | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Controlos de Privacidade** | ✅ 3 Modos | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Hash Client-Side** | ✅ Privacidade | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Metadados Forenses** | ✅ Completo | ❌ | ❌ | ⚠️ Restrito | ❌ | ⚠️ | ❌ | ⚠️ |
| **Verificação QR** | ✅ Instantânea | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Âncora Blockchain** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Suporte Turco** | ✅ Nativo | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Explicação:**
- ✅ : Suporte total / disponível
- ⚠️ : Restrito / em planos pagos
- ❌ : Não existe / não suportado
- 🔄 : No Roadmap (em desenvolvimento)
- 🆓 : Totalmente grátis
- 💰 : Pago / subscrição necessária

### Lacunas dos Concorrentes, Pontos Fortes do PoArt

| Lacuna | Concorrentes | PoArt |
|------|----------|-------|
| **Dificuldade de Uso** | CLI, conhecimento de API, carteira necessária | Arrastar-soltar, termina em 3 cliques |
| **Barreira de Custo** | Subscrição $50-500/mês | 100% grátis |
| **Privacidade** | Ficheiro carregado para servidor | Client-side, ficheiro nunca sai |
| **Dados Forenses** | Apenas timestamp | IP, localização, dispositivo, tempo - tudo |
| **Suporte Turco** | Não existe ou muito limitado | Suporte de língua nativa |
| **Open Source** | Caixa fechada | Todo o código aberto no GitHub |

---

## 📈 Estatísticas de Utilização (Objetivos Q1 2026)

| Métrica | Objetivo | Estado |
|--------|-------|-------|
| **Certificados Totais** | 1.000 | 🔄 Em Progresso |
| **Utilizadores Ativos** | 500 | 🔄 Em Progresso |
| **Número de Verificações** | 5.000 | 🔄 Em Progresso |
| **Uptime** | 99,9% | ✅ Ativo |
| **Tempo de Resposta Médio** | <200ms | ✅ Ótimo |

---

## 🌍 Comunidade & Suporte

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Contribuidores

O protocolo PoArt continua a evoluir com as contribuições da comunidade open source.

**Para contribuir:**
1. Faça Fork
2. Crie uma branch de feature (`git checkout -b feature/amazing-feature`)
3. Faça Commit (`git commit -m 'Add amazing feature'`)
4. Faça Push (`git push origin feature/amazing-feature`)
5. Abra um Pull Request

### 🛠️ De que Precisamos Agora? (Chamada de Ajuda)

O Protocolo PoArt espera contribuições de desenvolvedores experientes nas seguintes áreas para desenvolvimentos da **Fase 2**:

* **Supabase Edge Functions:** Mover proteção contra spam para o lado do servidor.
* **Solana Web3.js:** Integração de Wallet Signing (Assinatura de Carteira).
* **IPFS / Arweave:** Integração de serviços de arquivamento e pinning.
* **Ferramentas de Comunidade:** Votação X, sistemas de votação, dashboard de analytics.

> Por favor, inicie uma discussão na aba "Issues" antes de adicionar uma funcionalidade.

---

## 💬 Notas Finais

### Pump.fun e Realidade

Este projeto foi lançado no Pump.fun porque:
- ✅ Acesso a liquidez (migração automática Raydium)
- ✅ Acesso a comunidade existente
- ✅ Baixo custo inicial

No entanto, vamos esclarecer:
- **O preço do token** não é indicador de sucesso artístico
- **O valor do token** é importante para **orçamento operacional** (galeria, exposições, infraestrutura)
- **Métricas de sucesso:** Obras autenticadas + envolvimento da comunidade + visitantes físicos

### Governança e Descentralização

**Realidade v1.0 (2026):**
- Registry: Off-chain (PostgreSQL + backup IPFS)
- Atestação: Auto-assinado pela galeria (centralizado mas transparente)
- Governança: Apenas consultivo (decisão final curatorial)
- Token utility: Acesso à galeria + registry + prioridade NFT

**Visão v2.0+ (2027+):**
- Registry: On-chain (Solana)
- Assinaturas: Baseadas em carteira (descentralizado)
- Governança: Híbrido (consultivo comunitário + qualidade curatorial)
- Token utility: Funcionalidades melhoradas + acesso avançado

Esta estrutura fornece **eficiência operacional** e **controlo de qualidade** na fase inicial, enquanto mantém aberto o caminho para **aumentar a participação da comunidade** no futuro.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Cultura é Maior que Capital*

## 🧾 Licença

MIT License © 2026 İlhan Art Gallery Initiative

Ver [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) para termos completos.

---

## 💬 Créditos

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Este projeto foi desenvolvido com a iniciativa [İlhan Art Gallery] e os códigos-fonte são públicos por transparência.**

**PROTOCOLO V1.0 // SELADO COM SHA-512.**

*© 2026 İLHAN ART | TODOS OS DIREITOS DAS OBRAS, IMAGENS E IDEIAS RESERVADOS.*

---
