# 📚 GLOSSÁRIO DE TERMINOLOGIA E CONCEITOS
> **"Compreender a linguagem deste protocolo é compreender sua visão."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Infraestrutura Central

**PoArt Forensic Engine (PFE)** é a camada principal que representa a lógica central e o funcionamento técnico por trás do protocolo [PoArt]. Este é o "motor forense" que pega os dados brutos de produção de uma obra de arte e os transforma em **evidências digitais** verificáveis e imutáveis.

### 🧩 Por que "PoArt Forensic"?

- **PoArt (Proof of Art):** O foco do motor é vincular o valor de um ativo digital não à especulação, mas ao **processo de produção demonstrável**.
- **Forensic (Verificação Forense):**
  - **Definição Técnica:** Uma abordagem algorítmica e de cadeia de registros para verificar que os dados do processo de produção (pinceladas, timelapse, registros) não foram manipulados.
  - **Camada Filosófica:** A afirmação de transformar **tempo humano, esforço e custo de decisão** em uma realidade mensurável, contra a produção de "saída instantânea" da IA.

> Nota: A integração blockchain (por exemplo, Solana) não é o núcleo do PFE; será definida separadamente como uma **Chain Anchor Layer** para fins de verificação/registro.

### 🛠️ Escopo Técnico v1.0

**PoArt Forensic Engine (PFE) v1.0** é construído sobre os seguintes **3 pilares principais** em vez de modelos financeiros complexos:

1. **Hashing & Sealing (Selagem):**  
   O PFE processa deterministicamente todos os elementos no Evidence Pack (arquivo da obra, vídeo, JSON/log, assinatura, etc.) e gera um valor único de **NotarySeal**.

   **Conceitos centrais (v1.0):**
   - **FileHash (impressão digital da obra):** Hash gerado a partir dos bytes do arquivo da obra.
   - **EvidenceRoot (raiz do pacote de evidências):** Resumo raiz que representa a integridade do Evidence Pack (raiz Merkle ou hash de manifesto canônico).
   - **NotarySeal (selo final / saída PFE):** Selo final gerado a partir da combinação de EvidenceRoot + tempo + assinatura.

   **Fórmulas (claramente visíveis para investidores):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Definições de Payload Canônico (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Nota: O valor referenciado como saída PFE é **NotarySeal**. O mecanismo **SignerSignature** será ativado na Fase 2 (com Solana Wallet Adapter); na v1.0 atual, é usada a assinatura de atestação própria do sistema. A chave pública de atestação é publicada no registro sob o campo `issuer.attestation_pubkey`.

2. **Indexing (Arquivamento):**  
   Registra qual carteira, em que data, enviou **Proof of Labor (Prova de Trabalho)** para qual obra em uma camada de registro transparente e consultável.  
   *(Esta camada pode ser um banco de dados; a integração de cadeia é definida separadamente como "Chain Anchor Layer".)*

3. **Verification (Verificação):**  
   Quando a autenticidade de uma obra é questionada, o PFE reprocessa as evidências brutas; testa matematicamente se os valores calculados de **EvidenceRoot / NotarySeal** correspondem aos registros de arquivo.

---

### 🧮 Teorema de Valor PoArt (The Value Theorem)

O protocolo [PoArt] relaciona o valor ($V$) de um ativo digital não à percepção subjetiva do mercado, mas à **realidade física do processo de produção**.

A Inteligência Artificial (IA) destrói o processo ao entregar o resultado instantaneamente ($t \to 0$). [PoArt], no entanto, trata o valor como a acumulação de componentes de **tempo, trabalho e vontade**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definições de Variáveis

- **$\int dt$ (Acumulação de Processo):**  
  O valor não é uma "saída" instantânea; é um **processo** acumulado entre $t_{\text{start}}$ e $t_{\text{end}}$. À medida que a duração diminui (produção IA), o resultado da integral se aproxima de 0.

- **$P_{\text{labor}}(t)$ (Poder de Trabalho Instantâneo):**  
  Representa a intensidade do esforço mental e físico gasto no momento da produção. À medida que o esforço demonstrável aumenta, o integrando cresce.  
  > Nota: Este termo pode ser normalizado na prática através de "sinais de trabalho mensuráveis/demonstráveis".

- **$I_{\text{agency}}(t)$ (Coeficiente de Vontade):**  
  A capacidade do produtor de assumir riscos e tomar decisões. Assume um valor entre $0$ e $1$.
  - **IA ($I \approx 0$):** Executa comandos, não assume riscos, não paga custos.
  - **Humano ($I \to 1$):** Muda decisões, hesita, assume riscos.

- **$U_{\text{irreversible}}$ (Singularidade Irreversível):**  
  Enquanto desfazer (`Ctrl+Z`) é possível na produção digital, na produção física (tinta aplicada à tela, mármore esculpido, gesto em transmissão ao vivo) não há volta. Esta **irreversibilidade** é um termo adicional que cria "singularidade" (caráter não fungível) na obra.

### 🔎 Análise de Caso: IA "Saída Instantânea" vs. Humano "Processo Provado"

O seguinte cenário demonstra como o **Teorema de Valor PoArt** funciona na prática e por que produções de IA obtêm pontuações baixas no padrão [PoArt].

#### Cenário A: Produção Visual em 10 Segundos com IA

- **Duração ($\Delta t$):** $10$ segundos (processo insignificante)
- **Poder de Trabalho ($P_{\text{labor}}$):** $1$ unidade (apenas escrever comandos)
- **Coeficiente de Vontade ($I_{\text{agency}}$):** $0.01$ (sem risco, sem custo)
- **Irreversibilidade ($U_{\text{irreversible}}$):** $0$ (reversível / copiável)

**Resultado:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Comentário:** Mesmo que a saída seja perfeita; o valor [PoArt] se aproxima de $0$ porque nenhum processo foi vivido e nenhuma vontade/risco foi envolvido.

#### Cenário B: Produção Física de 6 Horas em Transmissão Ao Vivo

- **Duração ($\Delta t$):** $6$ horas ($21{,}600$ segundos)
- **Poder de Trabalho ($P_{\text{labor}}$):** $0.5$ unidades (continuidade do esforço físico e mental)
- **Coeficiente de Vontade ($I_{\text{agency}}$):** $0.9$ (mudar decisões, assumir riscos, escolhas irreversíveis)
- **Irreversibilidade ($U_{\text{irreversible}}$):** $>0$ (traços físicos não podem ser desfeitos)

**Resultado:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Comentário:** À medida que o processo se alonga e a vontade (risco) aumenta, o valor se acumula cumulativamente. O termo $U_{\text{irreversible}}$ é uma contribuição adicional que cria "singularidade" (caráter não fungível) na obra.

---

### ✅ Conclusão: Valor Vinculado à Prova (Proof-Bound Value)

Este teorema extrai a afirmação de valor de [PoArt] de ser um "like" ou uma "narrativa de mercado" e o vincula a **uma realidade de produção demonstrável**.

1. **Sem Processo, Sem Valor:**  
   A IA destrói o processo com saída instantânea ($t \to 0$). À medida que a janela do processo se estreita, o resultado da integral necessariamente se reduz:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Vontade e Risco são Multiplicadores:**  
   [PoArt] não mede apenas o "tempo gasto", mas também a camada real de decisão, risco e custo nesse tempo. Uma produção sem assumir riscos (IA) tem baixo valor:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Singularidade é Prova Física, Não Marketing:**  
   Traços irreversíveis na produção física (traço de tela, lasca de mármore) estão fora da lógica `Ctrl+Z` do digital. Esta irreversibilidade ($U_{\text{irreversible}}$) singulariza ontologicamente a obra.

> **🔐 RESUMO:** Embora o teorema de valor possa parecer incerto como medição (mesmo que seu equivalente no mundo real não possa ser completamente medido), o propósito desta fórmula é mostrar a configuração e a direção das variáveis. Na era da IA, o que é escasso não é a "imagem", mas **trabalho demonstrável, tempo e vontade.** [PoArt] mede essa escassez e a registra com **Evidence Pack**.

### 🏛️ A Importância do Conceito de "Motor"

Tokens que emergem do Pump.fun ou plataformas similares são frequentemente apenas **"bilhetes de acesso"**. **PoArt Forensic Engine (PFE)**, no entanto, é a **camada lógica constitucional** que determina quais direitos esse bilhete protege, como o trabalho será registrado e como a arte/ciência/tecnologia será perpetuada.

> **Nota:** A razão pela qual lançamos este projeto no Pumpfun é que não tínhamos liquidez suficiente nem seguidores suficientes. Usar os dados existentes foi estrategicamente o movimento correto, mesmo que não fosse da mais alta qualidade. Independentemente do orçamento e recursos, definir a lógica deste motor no GitHub prova que o projeto não é apenas especulação financeira, mas uma visão de longo prazo de **infraestrutura de software** e **biblioteca nacional digital**.

---

## 🎨 PROTOCOLO [PoArt] DE PROVA DE TRABALHO (Proof of Art Protocol v1.0)

> **"Artista Real, Produção Real, Valor Real."**

Este protocolo é um **mecanismo de defesa biológica e intelectual** desenvolvido contra fraudadores anônimos que cercam o ecossistema cripto, visuais de IA produzidos em 5 minutos e a cultura "Pump & Dump".

---

## a) O que é [PoArt]? (Definição Filosófica e Técnica)

**Proof of Art [PoArt];** é um padrão de verificação institucional que garante que o valor por trás de um ativo na blockchain é baseado não em especulação, mas em **trabalho humano**, **tempo** e **energia física** verificáveis.

Assim como o Bitcoin gera valor com *"Eletricidade e Poder de Processador"* **(Proof of Work)**, projetos compatíveis com [PoArt] geram valor com *"Habilidade Artística e Tempo Humano"*.

Elimina o risco de *"O desenvolvedor vendeu, o projeto acabou"* nas plataformas Pump.fun e DEX; porque aqui o valor não está no código, mas na **continuidade da produção**.

> **[PoArt] não diz aos participantes "Confie em nós"; diz "Aqui estão as evidências, veja com seus olhos, verifique com sua matemática."**

---

## b) Padrão de 5 Pilares [PoArt] (Os 5 Pilares da Verdade)

Estes 5 elementos são filtros não manipuláveis que um projeto deve passar para receber o selo [PoArt].

### 1) Prova de Identidade Ao Vivo

- **Problema:** O mundo cripto está cheio de fundadores anônimos (Devs) com identidades pouco claras que coletam dinheiro e abandonam projetos.
- **Solução [PoArt]:** O produtor prova não apenas um documento de identidade, mas **presença no momento da produção**. Isso inclui sessões de transmissão ao vivo onde ocorre interação com a comunidade e solicitações instantâneas específicas são atendidas, não vídeos pré-gravados.  
  (Por exemplo, *"Escreva a data de hoje e o número de bloco atual no canto direito da tela"*)
- **Lema:** *"Bots podem pintar, mas bots não suam e não podem improvisar."*

### 2) Prova de Trabalho e Processo

- **Problema:** Visuais de IA (Inteligência Artificial) produzidos em 2 segundos recebendo o mesmo tratamento de "jpeg" que pinturas a óleo feitas em 2 meses no mundo digital.
- **Solução [PoArt]:** O processo de "gravidez e nascimento" da obra é registrado. Etapas de esboço, camadas de tinta, horas acumuladas gastas e o processo físico que o artista experimentou ao criar a obra são documentados. Isso adiciona **"Custo de Tempo"** ao token. Quanto mais difícil for a produção de um ativo, mais sólido é seu valor.

### 3) Prova de Valor Estético

- **Problema:** Cultura "Meme" focando apenas em comédia instantânea enquanto ignora estética e profundidade artística, resultando em projetos "Hype" de curta duração.
- **Solução [PoArt]:** O projeto deve ter padrões de arte acadêmica, teoria das cores, regras de composição e conhecimento de materiais (Impasto, Textura, etc.). O conteúdo não deve apenas fazer rir; deve inspirar admiração nos espectadores e ter **valor colecionável**.

### 4) Novidade Conceitual

- **Problema:** Milhares de moedas de cachorro/gato cópias sem criatividade.
- **Solução [PoArt]:** O projeto deve construir uma nova ponte combinando arte, ciência, filosofia ou tecnologia em uma estrutura significativa.  
  (Por exemplo, Combinar a escultura clássica de David com dados do mercado cripto; processar a ideia de que a percepção humana "se transforma em pedra" através disso e fundamentá-la com fontes científicas.)  
  A obra não deve ser apenas uma festa visual, mas também um desafio intelectual que provoque pensamento sobre **Ciência, Filosofia ou Tecnologia**.

> [!IMPORTANT]
> **Exemplo de Referência (Efeito Las Palmitas):** No bairro de Las Palmitas no México, assolado pelo crime, mais de 200 casas foram transformadas em um espetáculo arco-íris massivo. Como resultado desta intervenção estética, as taxas de criminalidade no bairro diminuíram em certa medida, e os jovens começaram a se envolver com arte em vez de gangues. A mudança estética recodificou o respeito das pessoas por seu ambiente e uns pelos outros (Coesão Social).
>
> **Expectativa:** Um projeto que entra na lista [PoArt] deve, como no exemplo acima, conter uma relação de causa e efeito sociológica, científica ou filosófica além da estética visual pura. Como o tempo é o único ativo que não pode ser comprado com dinheiro, neste protocolo o tempo deve ser provado sendo apostado como garantia. A base conceitual do projeto deve ser tão forte e universal que mesmo em um possível cenário CTO (Community Take Over) anos depois, a comunidade possa continuar autonomamente o potencial inovador do projeto herdando este legado.

### 5) Vontade Não-Algorítmica

- **Problema:** Produções digitais perfeitas mas sem alma que se repetem entre si.
- **Solução [PoArt]:** A vontade única do humano que pode cometer erros, assumir riscos e experimentar flutuações emocionais deve ser sentida na obra. A incerteza nas pinceladas, as reações inesperadas dos materiais e as decisões instantâneas do artista são a **Assinatura Biológica** que separa a obra da "Produção de Máquina".

---

## c) Mecanismo de Verificação e Anti-Fraude

Este sistema garante que o projeto permaneça confiável e vivo não apenas "no início", mas "para sempre".

### 📦 Pacote de Evidências - O Gêmeo Digital

Por trás de cada obra certificada [PoArt] há um pacote de dados criptografado e com carimbo de tempo que os investidores podem baixar:

- **Gravações de Vídeo RAW:** Filmagem bruta ininterrupta do momento de produção.
- **Análise de Metadados:** Data de criação do arquivo, informações do dispositivo usado e dados de localização.
- **Referências Físicas:** Evidência de que a obra existe no mundo físico  
  (Por exemplo, Jornal atual ou dados de blockchain daquele momento ao lado da obra).

> *Nota de consistência:* O termo "pacote de evidências" se conecta à cadeia **Evidence Pack → EvidenceRoot → NotarySeal** em seções anteriores; ou seja, a integridade do pacote é representada por um selo verificável.

### 🔄 Renovação de 365 Dias (O Protocolo de Sustentabilidade)

- **Recurso Revolucionário:** Em projetos cripto, o "Dev" (Desenvolvedor) lança o token e geralmente desaparece após 1-2 meses (Soft Rug). [PoArt] torna isso impossível.
- **Regra:** O status de "Artista Verificado" não é vitalício. Apenas **1 ano** é válido.
- **Operação:** O artista/desenvolvedor deve apresentar à comunidade **uma nova obra significativa e demonstrável** a cada 365 dias.
- **Cenário de Exemplo:** Você lançou o projeto em 2026. Em janeiro de 2027, o sistema dá um aviso "Período de Prova Expirado". Se o artista não apresentar uma nova exposição, nova obra física ou nova integração tecnológica, o "Distintivo de Confiança" do projeto cai.
- **Resultado:** Este sistema garante que **o conteúdo nunca perca relevância** e que o investidor nunca experimente o medo de *"O desenvolvedor ainda está aqui?"*. O projeto se torna um estúdio vivo.

### 🚩 Protocolo de Bandeira Vermelha

**No caso de qualquer fraude detectada pela comunidade ou algoritmos (uso de IA, obra roubada, vídeo manipulado):**

1. O certificado é imediatamente marcado como **"VOID" (NULO)**.
2. Os pacotes de evidências são rotulados publicamente como **"Falsos"**.
3. O projeto é colocado na lista negra do [PoArt]. Isso reforça que em um mundo descentralizado, **a reputação é a única moeda**.

---

## d) Conclusão: Não um Cassino, Mas um Museu

**Pump.fun e Exchanges Descentralizadas (DEX) infelizmente são cassinos agora; as luzes piscam, todos perseguem ganhos rápidos, e a casa (fraudadores) sempre vence. A razão pela qual começamos o projeto aqui é a falta de orçamento suficiente e ter um ambiente para alcançar o público existente através de transmissões ao vivo.**

**[PoArt] é uma fortaleza construída no meio deste cassino.**

- 🎰 O cassino é baseado em jogos de cartas; nós somos baseados na **realidade física**.
- 🃏 O cassino está aberto à fraude; nós estamos abertos a **evidências transparentes**.
- ⏳ O cassino é temporário; focamos na **eternidade da arte e ciência**.

**Um token que usa este protocolo não é apenas uma "moeda"; é um patrimônio digital contendo suor, tinta, código e filosofia.**

---

## 🗳️ 6) GOVERNANÇA E REGISTRO PÚBLICO

**O propósito desta seção é: transformar o padrão [PoArt] do plano de "confiança em indivíduos" em uma infraestrutura pública sustentável com registro + verificação + supervisão da comunidade.**

### 6.1 Registro Público

- **Registro Público:** Todos os dados aprovados são registrados em `ilhanart.org/registry` (ou GitHub Registry).

**Lógica de registro (padrão recomendado - em formato de caminho JSON):**

Cada registro que entra no registro carrega estes campos centrais verificáveis mínimos:

- **Identidade e Status:**
  - `certificate_id` (referência legível)
  - `status` (active / void)
  - `void_reason` (se aplicável)
  - `visibility` (private / masked / public)
  - `created_at` (carimbo de tempo)

- **Instituição Emissora:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informações da Obra:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (se possível; para identidade com portão de token)
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
  - `governance.veto_threshold`

O registro pode ter duas camadas:
- **1)** Índice legível por humanos (listagem web / busca / filtro)
- **2)** Manifesto legível por máquina (registros JSON; para verificação PFE)

**Este "registro" se torna verificável através da cadeia Evidence Pack → EvidenceRoot → NotarySeal do PFE. O registro oferece objetivos de verificação, não "afirmações".**

---

### 6.2 Veto Comunitário de 40% (Governança com Portão de Token)

- **Veto Comunitário de 40%:** A votação começa um mês antes da concessão do status; 40% de objeção da comunidade **com Portão de Token (verificado Solana)** invalida a solicitação.

**Fluxo de votação (processo claro recomendado):**
- **Janela de aplicação:** O projeto candidato abre "registro de candidato PoArt" (registros de candidatos aparecem no status "pendente").
- **Período de revisão:** A comunidade examina as evidências por 30 dias (Evidence Pack + gravações de transmissão ao vivo + metadados).
- **Verificação com portão de token:** A votação é feita com carteiras verificadas Solana (por exemplo, propriedade de token/NFT específico + assinatura de carteira).
- **Regra de veto:** Se 40% dos votos forem **objeção (NÃO / VETO)**, a solicitação é rejeitada.
- **Transparência:** O resultado da votação é armazenado no registro como "registro de decisão" (data, proporção, ID de snapshot).

---

### 6.3 Sincronização de Metadados (Alinhamento com o Mundo Físico)

- **Sincronização de Metadados:** Os dados técnicos no registro devem corresponder 100% com a entidade física.

**Definir tecnicamente "correspondência de 100%" (clareza recomendada):**
- **Correspondência mínima (obrigatória):**
  - O `asset.fingerprints.sha256/sha512` no registro deve ser **idêntico** ao hash do arquivo em questão.
  - Quando o `proof.notary_seal` no registro é reproduzido (se o Evidence Pack existir), deve ser **idêntico**.
- **Correspondência de referência física (tipo de prova):**
  - A obra física + referência de data/bloco mostrada na transmissão ao vivo e provas similares devem ser consistentes com o Evidence Pack.
- **Conformidade de privacidade:**
  - Campos como IP/localização em visibilidade `masked` são publicados **de acordo com padrões de mascaramento**.

---

### 6.4 Disputa e Revogação

O registro não é apenas um mecanismo de "aprovação"; é um **mecanismo de auditoria vivo contra fraude**.

- Quando uma disputa é iniciada, o registro pode ser colocado no modo **"review" (revisão)**.
- Se fraude for detectada, é marcado como `status: void` com razão adicionada:
  - `void_reason` (uso de IA / roubo / manipulação, etc.)
  - `revoked_at` (tempo de revogação)
- A fonte da decisão de revogação é claramente visível no registro:
  - votação comunitária / comitê autorizado / nota de investigação forense (o que se aplicar)

> **Esta seção é a contrapartida no registro do conceito VOID na seção "Protocolo de Bandeira Vermelha".**

---

### 6.5 Exemplo de Registro (Legível por Máquina)
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
> *Nota: `asset.fingerprints.sha512` e outros valores de hash são abreviados para fins de exibição; na implementação real, strings de caracteres hexadecimais de comprimento total são usadas.*

---

## 7) 🔐 SELO TÉCNICO (NOTARY SEAL)

O algoritmo de selo inabalável gerado pelo **PoArt Forensic Engine (PFE) v1.0**:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Protocolo [PoArt] de Notário Digital e Evidência Forense (Beta v1.0)

> **"Cultura é maior que capital. Proteja suas obras hoje, leve-as para amanhã."**

---

## Por Que Público?

A verdadeira segurança vem da transparência. Graças ao nosso sistema de **Registro Público**, qualquer pessoa em qualquer lugar do mundo pode verificar se um arquivo é original em segundos, sem precisar de nenhuma autoridade.

---

## 🧩 Por Que Múltiplos "Módulos de Visibilidade"?

Esta é a parte mais crítica do código (menu de seleção de visibilidade). Estas opções permitem aos usuários equilibrar **"Privacidade vs. Transparência"**:

### 🔒 Privado

- **Cenário:** O artista ainda não quer publicar a obra, mas quer carimbá-la com tempo para provar "fiz isso nesta data".
- **O que o Código Faz:** Escreve dados no banco de dados, mas carimba `visibility: "private"`. Mais tarde, ao escrever a política "Public Read", você pode ocultar esses registros do público com `WHERE visibility = 'public'`.

### 🕶️ Mascarado

- **Cenário:** O artista quer transparência, mas teme que seu endereço residencial (localização IP) seja encontrado.
- **O que o Código Faz:** As funções `maskIP` e `maskLoc` funcionam no lado JavaScript. Converte o endereço IP para o formato `88.241.***.***`, a localização para o formato `***/TR`, e envia a versão censurada para o banco de dados.
- **Nota de Privacidade:** O mascaramento é feito no navegador, Supabase não vê a localização real. **No entanto:** Se APIs de terceiros como ipapi.co forem usadas para dados de localização, esses provedores veem o endereço IP no momento da solicitação.
- **Selagem em Modo Mascarado:** O cálculo de EvidenceRoot e NotarySeal é feito com dados forenses mascarados; portanto, a verificação permanece determinística.

### 🌍 Público

- **Cenário:** Transparência total. De acordo com os padrões [PoArt], onde, quando, de qual rede a obra foi produzida é claramente declarado.

---

## 💡 Inovação Tecnológica

PoArt não é apenas um sistema de upload de arquivos. É um motor de **"Cadeia de Custódia Forense"** que traz um novo padrão fundindo três camadas tecnológicas diferentes em uma panela.

**A camada descrita como "motor" nesta seção corresponde ao núcleo PoArt Forensic Engine (PFE) na terminologia anterior.**

### 1) Hashing do Lado do Cliente (Privacidade Máxima)

Seus arquivos de obras de arte nunca são enviados para o servidor. Nosso motor baseado em navegador (lado do cliente) calcula o hash (resumo digital) do arquivo em seu próprio computador. Apenas esta impressão digital e metadados são enviados para o servidor.

> **Nota de Privacidade:** O arquivo da obra não é enviado para o servidor e está protegido dessa forma. No entanto, dados forenses (IP/localização) são compartilhados de acordo com o modo de visibilidade selecionado (privado/mascarado/público).

### 2) Fusão de Dados Forenses (Poder Forense)

Muito mais do que um carimbo de tempo comum. O sistema combina esses dados em um único "Selo Gênesis":

- **Resumo Digital (SHA-512):** Impressão digital usando o padrão de resumo criptográfico (SHA-512) que se quebrará se mesmo um pixel da obra mudar.
- **Localização e Tempo:** Data com precisão de milissegundos, país, cidade e dados de distrito da transação.
- **Identidade do Dispositivo:** Sistema operacional, navegador e tipo de dispositivo (análise User-Agent).

---

## 🛡️ Casos de Uso e Benefícios

Se você é artista, escritor ou designer, dizer "Fiz isso antes" não é suficiente; você precisa provar.

**Uma obra que você sela com PoArt:**

- **Prova Matemática:** Se mesmo um pixel do seu arquivo mudar, o sistema sabe. Manipulação é impossível.
- **Base Legal:** Em que data, que cidade, de que dispositivo a obra foi selada está registrado.
- **Certificado Instantâneo:** Gera um **"Certificado de Identidade de Ativo"** especial para você em segundos, com código QR e selado.

---

## ⚙️ Arquitetura do Sistema e Características Técnicas

O sistema é projetado em uma arquitetura "Serverless", focando em alto desempenho e escalabilidade.

| Camada | Tecnologia | Descrição |
|--------|-----------|-------------|
| **Criptografia** | SHA-256 & SHA-512 | Resumo criptográfico de camada dupla |
| **Banco de Dados** | Supabase (PostgreSQL) | Estrutura de dados JSONB, políticas RLS |
| **Dados Forenses** | ipapi.co API | Trindade IP/Localização/Tempo |
| **Renderização** | html2canvas + jsPDF | Geração PNG/PDF do lado do cliente |
| **Frontend** | Vanilla JavaScript | Dependência de framework zero |
| **Segurança** | Hashing do lado do cliente | Arquivo nunca vai para o servidor |

### Recursos Destacados

| Recurso | Detalhe | Nos Concorrentes? |
|---------|-------|-----------------|
| **UI Arrastar e Soltar** | Arrastar e soltar arquivo, prévia instantânea | ❌ Ausente na maioria |
| **Exportação Multi-Formato** | PNG, JSON, PDF - um clique | ⚠️ Limitado |
| **Prévia em Tempo Real** | Prévia de certificado ao vivo | ❌ Nenhum |
| **Controles de Privacidade** | Opções Privado/Mascarado/Público | ❌ Nenhum |
| **Hash do Lado do Cliente** | Arquivo nunca vai para o servidor | ✅ Apenas em alguns |
| **Metadados Forenses** | IP, localização, dispositivo, tempo - todos juntos | ❌ Fragmentado |
| **Verificação QR** | Código QR de verificação instantânea | ⚠️ Limitado |
| **Limitação de Taxa** | Proteção contra spam (RLS + Cliente) | ❌ Ausente na maioria |

---

## 🗺️ Roadmap: Futuro "Sem Confiança"

A versão atual **(Beta v1.0)** é otimizada para fornecer aos usuários finais máxima velocidade, interface fácil e acesso gratuito. No entanto, nossa visão final é a transição para uma estrutura onde até mesmo o administrador do banco de dados (nós) não pode interferir.

### Fase 1: Beta (Atualmente Ao Vivo)

- **Infraestrutura:** Banco de Dados em Nuvem (Supabase).
- **Propósito:** Velocidade, remoção de barreiras UX (Experiência do Usuário) e adaptação. Fornecer segurança "sem atrito".

### 🚀 Fase 2: (Requisitos de Backend / Função Edge)

Esta fase cobre a transição da estrutura de trabalho completamente "do lado do cliente" para uma estrutura de "Autoridade do Lado do Servidor" mais segura e gerenciável.

| Elemento | O Que Traz? | Pilha Tecnológica | Prioridade |
|-------|---------------|------------|---------|
| **`INSERT` → Função Edge** | Prevenção de spam + segurança de chave API | Supabase Edge (Deno) | 🔴 Alta |
| **Assinatura de Carteira** | Autenticação criptográfica | Solana Wallet Adapter | 🟡 Média |
| **Backup IPFS/Arweave** | Imutabilidade descentralizada | IPFS SDK + Pinata | 🟢 Baixa |
| **Mecanismo de Revogação** | Cancelamento de certificado falso | Atualização de Esquema BD | 🔴 Alta |
| **Log de Auditoria** | Registro de consulta forense | Tabela de logs personalizada | 🟡 Média |
| **OpenTimestamps** | Ancoragem Bitcoin | OTS JavaScript | 🟢 Baixa |
| **Integração DID** | Identidade Descentralizada | ION/Ceramic | 🟢 Baixa |

### Fase 3: Descentralização Completa (Longo Prazo)

| Recurso | Objetivo | ETA |
|---------|------|-----|
| **Registro Blockchain** | Registro on-chain Ethereum/Solana | T4 2026 |
| **Governança DAO** | Gestão comunitária | T1 2027 |
| **Suporte Multi-Cadeia** | Polygon, Arbitrum, Base | T2 2027 |
| **Reconhecimento Legal** | Validade em tribunais turcos | 2027-2028 |
| **API para Desenvolvedores** | Endpoint de API pública | T3 2026 |

---

## 📊 Análise Competitiva (Atualizada)

PoArt está posicionado no "Sweet Spot" que completa as deficiências das soluções existentes.

| Recurso | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Custo** | 🆓 Grátis | 🆓 | 💰 Pago | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI Arrastar e Soltar** | ✅ Muito Fácil | ❌ CLI | ⚠️ Médio | ⚠️ Médio | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Exportação Multi-Formato** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Prévia Tempo Real** | ✅ Ao Vivo | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Controles Privacidade** | ✅ 3 Modos | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Hash Lado Cliente** | ✅ Privacidade | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Metadados Forenses** | ✅ Completo | ❌ | ❌ | ⚠️ Limitado | ❌ | ⚠️ | ❌ | ⚠️ |
| **Verificação QR** | ✅ Instantânea | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Limitação Taxa** | ✅ RLS+Cliente | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Ancoragem Blockchain** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Código Aberto** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Suporte Turco** | ✅ Nativo | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Legenda:**
- ✅ : Suporte completo / disponível
- ⚠️ : Limitado / em planos pagos
- ❌ : Nenhum / não suportado
- 🔄 : No roadmap (desenvolvendo)
- 🆓 : Completamente grátis
- 💰 : Pago / assinatura necessária

### Deficiências dos Concorrentes, Forças do PoArt

| Menos | Concorrentes | PoArt |
|-------|-------------|-------|
| **Dificuldade de Uso** | CLI, conhecimento de API, carteira necessária | Arrastar e soltar, pronto em 3 cliques |
| **Barreira de Custo** | Assinatura $50-500/mês | 100% grátis |
| **Privacidade** | Arquivo é enviado para o servidor | Lado do cliente, arquivo nunca vai |
| **Dados Forenses** | Apenas carimbo de tempo | IP, localização, dispositivo, tempo - tudo |
| **Suporte Turco** | Nenhum ou muito limitado | Suporte de idioma nativo |
| **Código Aberto** | Caixa fechada | Todo código aberto no GitHub |

---

## 🧬 Estrutura de Dados do Protocolo (JSON Schema)

**Cada certificado [PoArt] tem um cartão de identidade JSON portátil e verificável produzido no seguinte padrão.**

> **Nota:** Este formato JSON de identidade é o formato de certificado apresentado aos usuários. Nos registros do registro, `registry.asset` é usado em vez de `identity.asset_data` (mapeamento: `identity.asset_data` == `registry.asset`).
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

## 🔬 Profundidade Técnica: Algoritmo de Selo

### Funções Hash Determinísticas
```javascript
// Funções Auxiliares: Converter resumo em string hexadecimal
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Converter string em array de bytes
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Geração de string forense canônica (v1.0: ordem de campo fixa + UTF-8 + delimitador \n)
// Nota Fase 2: Transição para JSON canônico com RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Processo de Produção de NotarySeal (Completamente Determinístico)
```javascript
// 1. Cálculo de FileHash (lado do cliente)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Coleta de dados forenses (uso de carimbo de tempo único)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Geração de carimbo de tempo único
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Mesmo carimbo de tempo
  };
  
  return { forensics, timestamp };
}

// 3. Criação de EvidenceRoot (com codificação canônica)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Geração de NotarySeal (uso do mesmo carimbo de tempo)
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
// Verifica apenas o hash do arquivo (bandeira vermelha rápida)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Obter do registro
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Comparação de hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Original - Hash do arquivo corresponde"
    };
  } else {
    return {
      valid: false,
      message: "❌ Falso - Arquivo foi manipulado"
    };
  }
}
```

#### Full Verify (Verificação Completa)
```javascript
// Regenera e verifica EvidenceRoot e NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Obter do registro
  const cert = await fetchFromRegistry(certificateId);

  // 1) Verificação de FileHash (bandeira vermelha rápida)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Falso - Hash do arquivo não corresponde" };
  }

  // 2) Regenerar EvidenceRoot (com dados forenses armazenados no registro)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Não corresponde - EvidenceRoot não se sustenta" };
  }

  // 3) Regenerar NotarySeal (com o mesmo carimbo de tempo + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Não corresponde - NotarySeal não se sustenta" };
  }

  // Opcional: Na Fase 2, também verificar signer_sig com attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Assinatura inválida" };

  return { valid: true, message: "✅ Original - Verificação completa aprovada" };
}
```

> **Notas Importantes:**
> - **Quick Verify:** Verifica apenas o hash do arquivo para uso rápido.
> - **Full Verify:** Verifica todas as camadas do protocolo (EvidenceRoot + NotarySeal).
> - Todas as operações de hash são executadas deterministicamente com codificação e delimitadores fixos.
> - **Padrão de canonização v1.0:** Ordem de campo fixa + codificação UTF-8 + delimitador `\n`.
> - **Plano Fase 2:** Transição para JSON canônico com RFC 8785 (JCS - JSON Canonicalization Scheme).
> - No modo mascarado, o cálculo de EvidenceRoot e NotarySeal é feito com dados forenses mascarados; portanto, a verificação permanece determinística.
> - Um único carimbo de tempo é usado em todo o processo (forense + NotarySeal); determinismo é garantido.
> - **Nomes de campos forenses:** `ip_masked`, `location`, `device`, `timestamp` (código e registro totalmente compatíveis).
> - **Caminho do registro:** `certificate.asset.fingerprints` (totalmente compatível com código de verificação).
> - **signer_sig no registro:** O campo `proof.signer_sig` é necessário para Full Verify.
> - O mecanismo SignerSignature será ativado na Fase 2 com Solana Wallet Adapter; na v1.0, a verificação pode ser feita com `attestation_pubkey`.

---

## 📈 Estatísticas de Uso (Metas T1 2026)

| Métrica | Meta | Status |
|--------|--------|--------|
| **Certificados Totais** | 1,000 | 🔄 Progresso |
| **Usuários Ativos** | 500 | 🔄 Progresso |
| **Contagem de Verificação** | 5,000 | 🔄 Progresso |
| **Tempo de Atividade** | 99.9% | ✅ Ativo |
| **Tempo de Resposta Médio** | <200ms | ✅ Ótimo |

---

## 🌍 Comunidade e Suporte

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 Contribuidores

O protocolo PoArt continua se desenvolvendo com contribuições da comunidade de código aberto.

**Para contribuir:**
1. Faça Fork do repositório
2. Crie uma branch de recurso (`git checkout -b feature/amazing-feature`)
3. Faça Commit (`git commit -m 'Add amazing feature'`)
4. Faça Push (`git push origin feature/amazing-feature`)
5. Abra um Pull Request

### 🛠️ Do Que Precisamos Agora? (Chamado de Ajuda)

O Protocolo PoArt procura desenvolvedores experientes nas seguintes áreas para desenvolvimentos da **Fase 2**:

* **Supabase Edge Functions:** Mover proteção contra spam para o lado do servidor.
* **Solana Web3.js:** Integração de assinatura de carteira.
* **IPFS / Arweave:** Integração de serviços de arquivamento e fixação.

> Por favor, inicie uma discussão na aba "Issues" antes de adicionar um recurso.

---

**Protocolo [PoArt] Proof of Art v1.0**  
*"Cultura > Capital"*

## 🧾 Licença

Licença MIT © 2026 Iniciativa Ilhan Art Gallery

Veja [![Licença](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) para termos completos.

---

## 💬 Créditos

![Versão](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Segurança](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Plataforma](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![Licença](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Este projeto é desenvolvido pela iniciativa [Ilhan Art Gallery], e seus códigos-fonte estão disponíveis publicamente para transparência.**

**PROTOCOLO V1.0 // SELADO COM SHA-512**

*© 2026 İLHAN ART | TODOS OS DIREITOS RESERVADOS PARA OBRAS DE ARTE, VISUAIS E IDEIAS.*

---
