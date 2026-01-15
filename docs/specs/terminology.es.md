# 📚 GLOSARIO DE TERMINOLOGÍA Y CONCEPTOS
> **"Comprender el lenguaje de este protocolo es comprender su visión."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Infraestructura Central

**PoArt Forensic Engine (PFE)** es la capa principal que representa la lógica central y el funcionamiento técnico detrás del protocolo [PoArt]. Este es el "motor forense" que toma los datos de producción brutos de la obra de arte y los transforma en **evidencia digital** verificable e inmutable.

### 🧩 ¿Por qué "PoArt Forensic"?

- **PoArt (Proof of Art - Prueba de Arte):** El enfoque del motor es vincular el valor de un activo digital no a la especulación, sino al **proceso de producción demostrable**.
- **Forensic (Verificación Forense):**
  - **Definición Técnica:** Enfoque algorítmico y de cadena de registros orientado a verificar que los datos del proceso de producción (trazos de pincel, timelapse, registros) no han sido manipulados.
  - **Capa Filosófica:** La afirmación de transformar en una realidad medible la producción humana que contiene **tiempo, esfuerzo y costo de decisión**, frente a la producción de "salida instantánea" de la Inteligencia Artificial.

> Nota: La integración blockchain (ej. Solana) no es el núcleo de PFE; se trata como una **Chain Anchor Layer** (Capa de Anclaje en Cadena) que se definirá por separado para verificación/registro.

### 🛠️ Alcance Técnico v1.0

**PoArt Forensic Engine (PFE) v1.0** está construido sobre estos **3 pilares principales** en lugar de modelos financieros complejos:

1. **Hashing & Sealing (Hash y Sellado):**  
   PFE procesa de manera determinista todos los elementos dentro del Evidence Pack (archivo de obra, video, JSON/logs, firma, etc.) y genera el valor único **NotarySeal**.

   **Conceptos centrales (v1.0):**
   - **FileHash (huella digital de la obra):** Hash generado a partir de los bytes del archivo de la obra.
   - **EvidenceRoot (raíz del paquete de evidencia):** Resumen raíz que representa la integridad del Evidence Pack (Merkle root o hash de manifiesto canónico).
   - **NotarySeal (sello final / Salida PFE):** Sello final generado a partir de la combinación de EvidenceRoot + tiempo + firma.

   **Fórmulas (visibles claramente para el inversor):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Definiciones de Payload Canónico (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Nota: El valor previsto como salida PFE es **NotarySeal**. El mecanismo **SignerSignature** se activará en la Fase 2 (con Solana Wallet Adapter); en la v1.0 actual se utiliza la firma de attestation del propio sistema. La clave pública de attestation se publica en el campo `issuer.attestation_pubkey` del registro.

2. **Indexing (Archivo):**  
   Procesa en una capa de registro transparente y consultable qué billetera, en qué fecha, presentó **Labor Proof (Prueba de Trabajo)** para qué obra.  
   *(Esta capa puede ser una base de datos; la integración en cadena se define por separado como "Chain Anchor Layer".)*

3. **Verification (Verificación):**  
   Cuando se cuestiona la autenticidad de una obra, PFE reprocesa las evidencias brutas; prueba con certeza matemática si los valores calculados **EvidenceRoot / NotarySeal** coinciden con el registro en el archivo.

---

### 🧮 Teorema del Valor PoArt (The Value Theorem)

El protocolo [PoArt] relaciona el valor ($V$) de un activo digital no con la percepción subjetiva del mercado, sino con **la realidad física del proceso de producción**.

La Inteligencia Artificial (IA) destruye el proceso al dar el resultado instantáneamente ($t \to 0$). [PoArt], en cambio, trata el valor como la acumulación de los componentes de **tiempo, trabajo y voluntad**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definición de Variables

- **$\int dt$ (Acumulación de Proceso):**  
  El valor no es una "salida" (output) instantánea; es un **proceso** que se acumula entre $t_{\text{start}}$ y $t_{\text{end}}$. A medida que disminuye la duración (producción IA), el resultado de la integral se aproxima a 0.

- **$P_{\text{labor}}(t)$ (Fuerza de Trabajo Instantánea):**  
  Representa la intensidad del esfuerzo mental y físico gastado en el momento de producción. A medida que aumenta el esfuerzo demostrable, crece el integrando.  
  > Nota: Este término puede normalizarse en la práctica a través de "señales de trabajo medibles/demostrables".

- **$I_{\text{agency}}(t)$ (Coeficiente de Voluntad):**  
  Es la capacidad del productor para asumir riesgos y tomar decisiones. Toma un valor entre $0$ y $1$.
  - **IA ($I \approx 0$):** Ejecuta comandos, no asume riesgos, no paga un precio.
  - **Humano ($I \to 1$):** Cambia decisiones, duda, asume riesgos.

- **$U_{\text{irreversible}}$ (Singularidad Irreversible):**  
  Mientras que en la producción digital es posible deshacer (`Ctrl+Z`); en la producción física (pintura aplicada al lienzo, mármol tallado, gesto en transmisión en vivo) no hay vuelta atrás. Esta **irreversibilidad** es un término adicional que crea "singularidad" (carácter no fungible) en la obra.

### 🔎 Análisis de Caso: IA "Salida Instantánea" vs. Humano "Proceso Probado"

El siguiente escenario muestra cómo funciona el **Teorema del Valor PoArt** en la práctica y por qué las producciones de IA obtienen puntuaciones bajas en el estándar [PoArt].

#### Escenario A: Producción Visual con IA en 10 Segundos

- **Duración ($\Delta t$):** $10$ segundos (proceso casi inexistente)
- **Fuerza de Trabajo ($P_{\text{labor}}$):** $1$ unidad (solo escribir comando)
- **Coeficiente de Voluntad ($I_{\text{agency}}$):** $0.01$ (sin riesgo, sin costo)
- **Irreversibilidad ($U_{\text{irreversible}}$):** $0$ (reversible / copiable)

**Resultado:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Comentario:** Aunque la salida sea perfecta; dado que no se experimenta el proceso y no contiene voluntad/riesgo, el valor [PoArt] se aproxima a $0$.

#### Escenario B: Producción Física de 6 Horas en Transmisión en Vivo

- **Duración ($\Delta t$):** $6$ horas ($21{,}600$ segundos)
- **Fuerza de Trabajo ($P_{\text{labor}}$):** $0.5$ unidades (continuidad del esfuerzo físico y mental)
- **Coeficiente de Voluntad ($I_{\text{agency}}$):** $0.9$ (cambio de decisiones, asunción de riesgos, elecciones irreversibles)
- **Irreversibilidad ($U_{\text{irreversible}}$):** $>0$ (huellas físicas irreversibles)

**Resultado:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Comentario:** A medida que se alarga el proceso y aumenta la voluntad (riesgo), el valor aumenta acumulativamente. El término $U_{\text{irreversible}}$ es una contribución adicional que crea "singularidad" (carácter no fungible) en la obra.

---

### ✅ Conclusión: Valor Vinculado a la Prueba (Proof-Bound Value)

Este teorema saca la afirmación de valor de [PoArt] de ser un "gusto" o "narrativa de mercado" y la vincula a una **realidad de producción demostrable**.

1. **Sin Proceso No Hay Valor:**  
   La IA destruye el proceso con salida instantánea ($t \to 0$). A medida que se estrecha la ventana del proceso, el resultado de la integral disminuye por necesidad matemática:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **La Voluntad y el Riesgo son Multiplicadores:**  
   [PoArt] mide no solo el "tiempo gastado", sino también la capa real de decisión, riesgo y costo en ese tiempo. El valor de una producción sin riesgo (IA) es bajo:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **La Singularidad es una Prueba Física, No Marketing:**  
   Las huellas irreversibles en la producción física (trazo en lienzo, fractura de mármol) están fuera de la lógica del `Ctrl+Z` digital. Esta irreversibilidad ($U_{\text{irreversible}}$) singulariza ontológicamente la obra.

> **🔐 RESUMEN:** Aunque el teorema del valor pueda parecer incierto como medición (aunque no pueda medirse 100% en la vida real), el propósito de esta fórmula es mostrar la construcción y dirección de las variables. En la era de la IA, lo escaso no es la "imagen"; son el **trabajo demostrable, el tiempo y la voluntad**. [PoArt] mide esta escasez y la registra con el **Evidence Pack**.

### 🏛️ Importancia del Concepto "Engine" (Motor)

Los tokens que salen de Pump.fun o plataformas similares son a menudo solo **"boletos de acceso"**. **PoArt Forensic Engine (PFE)**, en cambio, es la **capa de lógica constitucional** que determina qué derechos protege ese boleto, cómo se registrará el trabajo y cómo se perpetuará el arte/ciencia/tecnología.

> **Nota:** La razón por la que iniciamos este proyecto en Pump.fun es porque no contábamos con suficiente liquidez y número de seguidores. Usar los datos existentes fue estratégicamente el movimiento más correcto, aunque no fuera de la más alta calidad. Independientemente del presupuesto y las posibilidades, definir la lógica de este motor en GitHub demuestra que el proyecto no es solo una especulación financiera, sino una **infraestructura de software** a largo plazo y una visión de **biblioteca nacional digital**.

---

## 🎨 [PoArt] PROTOCOLO DE PRUEBA DE TRABAJO (Proof of Art Protocol v1.0)

> **"Artista Real, Producción Real, Valor Real."**

Este protocolo es un **mecanismo de defensa biológico e intelectual** desarrollado contra los estafadores anónimos que rodean el ecosistema cripto, las imágenes de inteligencia artificial producidas en 5 minutos y la cultura "Pump & Dump" (Bombeo y Descarga).

---

## a) ¿Qué es [PoArt]? (Definición Filosófica y Técnica)

**Proof of Art [PoArt];** es un estándar de verificación institucional que garantiza que el valor detrás de un activo en blockchain se basa no en la especulación, sino en el **trabajo humano** verificable, el **tiempo** y la **energía física**.

Así como Bitcoin genera valor con *"Electricidad y Potencia de Procesador"* **(Proof of Work)**, los proyectos compatibles con [PoArt] generan valor con *"Talento Artístico y Tiempo Humano"*.

Elimina el riesgo de *"El desarrollador (Dev) vendió, proyecto terminado"* en Pump.fun y plataformas DEX; porque aquí el valor no está en el código, sino en la **continuidad de la producción**.

> **[PoArt] no dice a su participante "Confía en nosotros"; dice "Aquí están las pruebas, mira con tus ojos, verifica con tu matemática".**

---

## b) Estándar de 5 Pilares [PoArt] (The 5 Pillars of Truth)

Estos 5 elementos son filtros no manipulables que un proyecto debe pasar para obtener el sello [PoArt].

### 1) Prueba de Identidad en Vivo (Live Identity Proof)

- **Problema:** El mundo cripto está lleno de fundadores anónimos (Devs) de identidad incierta que recaudan dinero y abandonan el proyecto.
- **Solución [PoArt]:** El productor demuestra no solo su documento de identidad, sino **su presencia durante la producción**. Esto incluye sesiones de transmisión en vivo donde se interactúa con la comunidad y se cumplen solicitudes específicas instantáneas, no videos pregrabados.  
  (Ej: *"Escribe la fecha de hoy y el número de bloque actual en la esquina derecha del lienzo"*)
- **Lema:** *"Los bots pueden hacer imágenes, pero los bots no sudan ni improvisan."*

### 2) Prueba de Trabajo y Proceso (Labor & Process Proof)

- **Problema:** Que las imágenes de IA (Inteligencia Artificial) producidas en 2 segundos y la pintura al óleo hecha en 2 meses reciban el mismo trato de "jpeg" en el mundo digital.
- **Solución [PoArt]:** Se registra el proceso de "gestación y nacimiento" de la obra. Se documentan las etapas de boceto, capas de pintura, horas acumuladas gastadas y el proceso físico que vivió el artista al crear esa obra. Esto añade **"Costo de Tiempo" (Time Cost)** al token. Cuanto más difícil es la producción de un activo, más sólido es su valor.

### 3) Prueba de Valor Estético (Aesthetic Value Proof)

- **Problema:** Que la cultura "Meme" ignore la estética y la profundidad artística enfocándose solo en la comedia instantánea y resultando en proyectos de "Hype" de corta duración.
- **Solución [PoArt]:** El proyecto debe tener estándares de arte académico, teoría del color, reglas de composición y conocimiento de materiales (Impasto, Textura, etc.). El contenido no debe solo hacer reír; debe inspirar admiración en el espectador y tener **valor de colección**.

### 4) Innovación Conceptual (Conceptual Novelty)

- **Problema:** Miles de monedas de perros/gatos que son copias entre sí, alejadas de la creatividad.
- **Solución [PoArt]:** El proyecto debe construir un nuevo puente que combine arte, ciencia, filosofía o tecnología en una estructura significativa.  
  (Ej: Combinar la clásica estatua de David con datos del mercado cripto; procesar la idea de que la percepción humana se "petrifica" a través de esto y poder fundamentarlo con fuentes científicas.)  
  La obra no debe ser solo un festín visual; también debe ser un desafío intelectual que haga pensar sobre **Ciencia, Filosofía o Tecnología**.

> [!IMPORTANT]
> **Ejemplo de Referencia (Efecto Las Palmitas):**  
> En el barrio Las Palmitas de México que luchaba contra el crimen, más de 200 casas se transformaron en un enorme festín de arcoíris. Como resultado de esta intervención estética, las tasas de criminalidad en el barrio disminuyeron en cierta medida, los jóvenes comenzaron a interesarse en el arte en lugar de las pandillas. El cambio estético recodificó el respeto de las personas hacia su entorno y entre ellos (Cohesión Social).
>
> **Expectativa:** Un proyecto que entre en la lista [PoArt]; al igual que el ejemplo anterior, debe contener una relación causa-efecto sociológica, científica o filosófica más allá de la pura estética visual. Dado que el único activo que no puede comprarse con dinero es el "Tiempo", en este protocolo el tiempo debe apostarse como garantía y demostrarse. La base conceptual del proyecto debe ser tan fuerte y universal que; incluso en un posible escenario de CTO (Community Take Over) años después, la comunidad pueda heredar este legado y continuar autónomamente el potencial innovador del proyecto.

### 5) Voluntad No Algorítmica (Non-Algorithmic Agency)

- **Problema:** Producciones digitales perfectas pero sin alma, que se repiten entre sí.
- **Solución [PoArt]:** La voluntad genuina del ser humano que puede cometer errores, asumir riesgos y experimentar fluctuaciones emocionales debe sentirse en la obra. La incertidumbre en los trazos del pincel, las reacciones inesperadas del material y las decisiones instantáneas del artista son la **Firma Biológica** que distingue la obra de la "Producción de Máquina".

---

## c) Mecanismo de Verificación y Anti-Falsificación

Este sistema garantiza que el proyecto permanezca confiable y vivo no solo "al principio", sino "para siempre".

### 📦 Paquete de Evidencia (Evidence Pack - The Digital Twin)

Detrás de cada obra certificada [PoArt] hay un paquete de datos cifrado y con marca de tiempo que los inversores pueden descargar:

- **Grabaciones de Video RAW:** Imágenes brutas ininterrumpidas del momento de producción.
- **Análisis de Metadatos:** Fecha de creación del archivo, información del dispositivo utilizado y datos de ubicación.
- **Referencias Físicas:** Evidencia de que la obra existe en el mundo físico  
  (Ej: Periódico actual junto a la obra o datos de blockchain de ese momento).

> *Nota de coherencia:* La expresión "paquete de evidencia" se conecta a la línea **Evidence Pack → EvidenceRoot → NotarySeal** de secciones anteriores; es decir, la integridad del paquete está representada por un sello verificable.

### 🔄 Renovación de 365 Días (The Sustainability Protocol)

- **Característica Revolucionaria:** En proyectos cripto, el "Dev" (Desarrollador) lanza el token al mercado y generalmente desaparece después de 1-2 meses (Soft Rug). [PoArt] hace esto imposible.
- **Regla:** El estatus de "Verified Artist" (Artista Verificado) no es de por vida. Solo es válido por **1 año**.
- **Funcionamiento:** El artista/desarrollador debe presentar a la comunidad cada 365 días una **obra nueva, importante y demostrable**.
- **Escenario de Ejemplo:** Iniciaste el proyecto en 2026. En enero de 2027, el sistema da la advertencia "Tiempo de Prueba Expirado". Si el artista no presenta una nueva exposición, una nueva obra física o una nueva integración tecnológica, la "Insignia de Confianza" del proyecto cae.
- **Resultado:** Este sistema garantiza que **el contenido nunca pierda actualidad** y que el inversor no experimente el miedo de *"¿Sigue aquí el desarrollador?"*. El proyecto se convierte en un estudio vivo.

### 🚩 Bandera Roja (Red Flag Protocol)

**En caso de cualquier falsificación detectada por la comunidad o algoritmos (uso de IA, obra robada, video manipulado):**

1. El certificado se marca inmediatamente como **"ANULADO" (VOID)**.
2. Los paquetes de evidencia se etiquetan públicamente como **"Falso"**.
3. El proyecto se añade a la lista negra [PoArt]. Esto refuerza el hecho de que en un mundo descentralizado, **la reputación es la única moneda**.

---

## d) Conclusión: No un Casino, Sino un Museo

**Pump.fun y los Intercambios Descentralizados (DEX) son actualmente, lamentablemente, casinos; las luces parpadean, todos persiguen ganancias rápidas y la casa (estafadores) siempre gana. Iniciamos el proyecto aquí porque no teníamos presupuesto suficiente y teníamos un entorno para llegar a la audiencia existente con transmisiones en vivo.**

**[PoArt] es una fortaleza construida en el medio de este casino.**

- 🎰 El casino se basa en juegos de cartas; nosotros nos basamos en la **realidad física**.
- 🃏 El casino está abierto al engaño; nosotros estamos abiertos a **pruebas transparentes**.
- ⏳ El casino es temporal; nosotros nos enfocamos en **la eternidad del arte y la ciencia**.

**El token que usa este protocolo no es solo una "moneda"; es una acción digital que contiene sudor, pintura, código y filosofía detrás.**

---

## 🗳️ 6) GOBERNANZA Y REGISTRO PÚBLICO (Governance & Public Registry)

**El propósito de esta sección es el siguiente: Sacar el estándar [PoArt] del plano de "confianza en las personas" y transformarlo en una infraestructura pública sostenible con registro + verificación + supervisión comunitaria.**

### 6.1 Registro Público (Public Registry)

- **Registro Público:** Todos los datos aprobados se registran en la dirección `ilhanart.org/registry` (o GitHub Registry).

**Lógica de registro (estándar recomendado - formato de ruta JSON):**

Cada registro que entra en el registro tiene mínimamente estos campos centrales verificables:

- **Identidad y Estado:**
  - `certificate_id` (referencia legible)
  - `status` (active / void)
  - `void_reason` (si existe)
  - `visibility` (private / masked / public)
  - `created_at` (marca de tiempo)

- **Institución Emisora:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Información de la Obra:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (si es posible; para identificación del titular del token)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Datos Forenses:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Pruebas Criptográficas:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Gobernanza:**
  - `governance.decision`
  - `governance.review_notes`

El registro puede tener dos capas:
- **1)** Índice legible para humanos (listado web / búsqueda / filtro)
- **2)** Manifiesto legible para máquinas (registros JSON; para verificación PFE)

**El "registro" aquí se vuelve verificable a través de la cadena Evidence Pack → EvidenceRoot → NotarySeal de PFE. El registro ofrece un objetivo de verificación, no una "afirmación".**

---

### 6.2 Proceso de Solicitud PoArt Verified

**Las solicitudes PoArt Verified son evaluadas por la Galería İlhanArt según los 5 estándares PoArt. Se considera la retroalimentación de la comunidad, pero la decisión final corresponde al equipo curatorial. Las decisiones se explican de forma transparente y se registran en ilhanart.org/registry.**

#### Proceso de Solicitud

**Solicitud:**
- El artista/proyecto realiza una solicitud PoArt Verified
- Se prepara el Evidence Pack (grabaciones de video, metadatos, enlaces de transmisión en vivo)
- La solicitud se envía a la Galería İlhanArt

**Revisión (30 Días):**
- El equipo de la galería examina detalladamente el Evidence Pack
- Se verifican todos los 5 estándares PoArt:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Entrevista con el artista (opcional)

**Consulta Comunitaria:**
- El Evidence Pack se comparte públicamente durante el proceso de solicitud
- Los titulares de tokens (mínimo 10,000 $CULTURE) pueden hacer sugerencias especialmente
- **Toda la retroalimentación se considera en el proceso de revisión**
- **Sin embargo, la decisión final depende de la evaluación curatorial**

**Decisión:**
- La galería aprueba o rechaza la solicitud
- La justificación de la decisión se explica de forma transparente
- Si se aprueba → insignia PoArt Verified
- Si se rechaza → se puede volver a solicitar después de 6 meses

**Transparencia:**
- Todas las solicitudes y decisiones se registran en ilhanart.org/registry
- El registro de decisión se publica públicamente:
  - Fecha de solicitud
  - Resumen del proceso de revisión
  - Decisión (Aprobada / Rechazada)
  - Justificación de la decisión (explicación breve)
  - Resumen de retroalimentación comunitaria (anónimo)

#### ¿Por qué Decisión Curatorial?

**Control de Calidad:**  
El estado PoArt Verified es una insignia con altos estándares. La evaluación curatorial garantiza el mantenimiento de estos estándares.

**Prevención de Manipulación Especulativa:**  
Con tokens de Pump.fun, la gobernanza completa on-chain (ej: Realms, votación DAO) no es técnicamente posible. Los sistemas de votación off-chain son vulnerables a la manipulación de ballenas y ataques coordinados. La decisión curatorial elimina este riesgo.

**Eficiencia Operativa:**  
En lugar de mecanismos de votación complejos, proceso de decisión rápido y claro. Los artistas obtienen resultados en 30 días.

**Participación Comunitaria:**  
La retroalimentación de la comunidad se considera completamente y afecta el proceso de decisión. Sin embargo, la decisión final corresponde al equipo curatorial protegido de manipulación.

**Futuro:**  
Cuando el proyecto madure (2027+), el mecanismo de consulta comunitaria puede fortalecerse. Sin embargo, la protección del estándar curatorial es permanente.

---

### 6.3 Utilidad del Token (Token Utility)

**Beneficios proporcionados a los titulares de tokens $CULTURE:**

**1. Acceso Prioritario a Eventos de Galería:**
- Inauguraciones de exposiciones físicas de la Galería İlhanArt
- Reuniones con artistas y visitas a talleres
- Visualizaciones de colecciones especiales

**2. Acceso Completo al Registro PoArt:**
- Registros detallados de todas las obras autenticadas
- Versiones completas de Evidence Packs
- Herramientas de verificación forense

**3. Votación Consultiva:**
- Derecho de consulta en solicitudes PoArt Verified
- Acceso a canales de retroalimentación comunitaria
- Participación en discusiones de gobernanza

**4. Contenido Exclusivo:**
- Contenido detrás de escenas del estudio
- Entrevistas con artistas y videos de procesos
- Acceso a documentación técnica

**Nota:**  
Los titulares de tokens emiten voto consultivo (advisory vote). La decisión final pertenece al equipo curatorial. Esta estructura se prefiere para prevenir la manipulación de ballenas y ataques especulativos. No hay recompensas de staking porque buscamos participantes culturales a largo plazo, no capital mercenario a corto plazo.

---

### 6.4 Sincronización de Metadatos (Metadata Sync)

- **Sincronización de Metadatos:** Los datos técnicos en el registro deben coincidir 100% con la entidad física.

**Definir técnicamente la "coincidencia del 100%" (claridad recomendada):**

- **Coincidencia mínima (obligatoria):**
  - El `asset.fingerprints.sha256/sha512` en el registro debe ser **exactamente el mismo** que el hash del archivo en mano.
  - Cuando se reproduce el `proof.notary_seal` en el registro (si hay Evidence Pack) debe ser **exactamente el mismo**.

- **Coincidencia de referencia física (tipo de prueba):**
  - Las evidencias como obra física + referencia de fecha/bloque mostradas en transmisión en vivo deben ser consistentes con el Evidence Pack.

- **Cumplimiento de privacidad:**
  - En visibilidad `masked`, campos como IP/ubicación se publican **de acuerdo con el estándar de enmascaramiento**.

---

### 6.5 Disputa, Revisión y Revocación (Dispute & Revocation)

El registro no es solo un mecanismo de "aprobación"; es un **mecanismo de supervisión vivo contra la falsificación**.

- Cuando se inicia una disputa, el registro puede llevarse al modo **"review"** (revisión).
- Si se detecta falsificación, se marca como `status: void` y se añade justificación:
  - `void_reason` (uso de IA / plagio / manipulación, etc.)
  - `revoked_at` (tiempo de cancelación)
- La fuente de la decisión de cancelación es claramente visible en el registro:
  - revisión curatorial / disputa comunitaria / nota de análisis forense (lo que sea aplicable)

> **Esta parte es la contraparte en el registro del concepto VOID en la sección "Red Flag Protocol".**

---

### 6.6 Ejemplo de Registro en el Registro (Legible por Máquina)
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

> *Nota: `asset.fingerprints.sha512` y otros valores hash están abreviados con fines ilustrativos; en la aplicación real se utiliza una cadena de caracteres hexadecimales de longitud completa.*

---

## 7) 🔐 SELLO TÉCNICO (NOTARY SEAL)

**Algoritmo de sello inquebrantable producido por PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Protocolo de Notario Digital y Evidencia Forense (Beta v1.0)

> **"La cultura es más grande que el capital. Proteja sus obras desde hoy, llévelas al mañana."**

---

## ¿Por Qué Público?

La seguridad real proviene de la transparencia. Gracias a nuestro sistema de **Registro Público (Public Registry)**, una persona en cualquier parte del mundo puede verificar en segundos si el archivo que tiene es original, sin necesidad de ninguna autoridad.

---

## 🧩 ¿Por Qué Hay Varios "Módulos de Visibilidad"?

Esta es la parte más crítica del código (menú de selección de visibilidad). Estas opciones permiten a los usuarios establecer el equilibrio **"Privacidad vs. Transparencia"**:

### 🔒 Privado (Private)

- **Escenario:** El artista aún no quiere publicar la obra pero quiere poner una marca de tiempo y demostrar "yo hice esto en esta fecha".
- **Lo que Hace el Código:** Escribe los datos en la base de datos pero pone la etiqueta `visibility: "private"`. Al escribir la política "Public Read" más adelante, puedes ocultar estos registros del público diciendo `WHERE visibility = 'public'`.

### 🕶️ Enmascarado (Masked)

- **Escenario:** El artista quiere transparencia pero teme que se encuentre su dirección de casa (ubicación IP).
- **Lo que Hace el Código:** Las funciones `maskIP` y `maskLoc` funcionan en el lado de JavaScript. Convierte la dirección IP a la forma `88.241.***.***`, la ubicación a la forma `***/TR` y envía la versión censurada a la base de datos.
- **Nota de Privacidad:** El enmascaramiento se realiza en el navegador, Supabase no ve la ubicación real. **Sin embargo:** Si se utilizan API de terceros como ipapi.co para datos de ubicación, estos proveedores ven la dirección IP en el momento de la solicitud.
- **Sellado en Modo Enmascarado:** El cálculo de EvidenceRoot y NotarySeal se realiza con datos forenses enmascarados; así la verificación permanece determinista.

### 🌍 Público (Public)

- **Escenario:** Transparencia total. Según el estándar [PoArt], se declara claramente dónde, cuándo, desde qué red se produjo la obra.

---

## 💡 Innovación Tecnológica

PoArt no es solo un sistema de carga de archivos. Es un motor de **"Cadena de Custodia Forense" (Forensic Chain of Custody)** que fusiona tres capas tecnológicas diferentes en una sola olla y trae un nuevo estándar.

**La capa explicada como "motor" en esta sección corresponde al núcleo del PoArt Forensic Engine (PFE) en la terminología anterior.**

### 1) Hashing del Lado del Cliente (Máxima Privacidad)

Sus archivos de obras nunca se cargan al servidor. Nuestro motor que funciona basado en navegador (del lado del cliente) calcula el hash (resumen digital) del archivo en su propia computadora. Solo esta huella digital y metadatos se envían al servidor.

> **Nota de Privacidad:** El archivo de obra no se carga al servidor y se protege de esta manera. Sin embargo, los datos forenses (IP/ubicación) se comparten según el modo de visibilidad seleccionado (private/masked/public).

### 2) Fusión de Datos Forenses (Poder Forense)

Es mucho más que una simple marca de tiempo (Timestamp). El sistema combina estos datos en un solo "Sello Génesis":

- **Resumen Digital (SHA-512):** Huella digital que se corromperá incluso si cambia un solo píxel de la obra usando el estándar de resumen criptográfico (SHA-512).
- **Ubicación y Tiempo:** Fecha, país, ciudad y datos de distrito con precisión de milisegundos de cuando se realizó la operación.
- **Identidad del Dispositivo:** Sistema operativo, navegador y tipo de dispositivo (análisis de User-Agent).

---

## 🛡️ Áreas de Uso y Beneficio

Si eres artista, escritor o diseñador, no basta con decir "Yo hice esto antes", necesitas demostrarlo.

**Una obra que sellas con PoArt:**

- **Prueba Matemática:** Incluso si cambia un solo píxel de tu archivo, el sistema lo entiende. La manipulación es imposible.
- **Base Legal:** Está registrado en qué fecha, en qué ciudad, desde qué dispositivo se selló la obra.
- **Certificado Instantáneo:** Genera en segundos un **"Certificado de Identidad de Activo"** personalizado, con código QR y sellado.

---

## ⚙️ Arquitectura del Sistema y Características Técnicas

El sistema está diseñado en una arquitectura "Sin Servidor" (Serverless), enfocado en alto rendimiento y escalabilidad.

| Capa | Tecnología | Descripción |
|------|------------|-------------|
| **Criptografía** | SHA-256 & SHA-512 | Resumen criptográfico de doble capa |
| **Base de Datos** | Supabase (PostgreSQL) | Estructura de datos JSONB, políticas RLS |
| **Datos Forenses** | API ipapi.co | Trío IP/Ubicación/Tiempo |
| **Renderizado** | html2canvas + jsPDF | Generación PNG/PDF del lado del cliente |
| **Frontend** | Vanilla JavaScript | Cero dependencia de framework |
| **Seguridad** | Hashing del lado del cliente | El archivo nunca se carga al servidor |

### Características Destacadas

| Característica | Detalle | ¿En Competidores? |
|----------------|---------|-------------------|
| **UI Arrastrar y Soltar** | Arrastrar archivo, vista previa instantánea | ❌ No en la mayoría |
| **Exportación Multi-Formato** | PNG, JSON, PDF - un clic | ⚠️ Limitado |
| **Vista Previa en Tiempo Real** | Vista previa en vivo del certificado | ❌ No |
| **Controles de Privacidad** | Opciones Private/Masked/Public | ❌ No |
| **Hashing del Lado del Cliente** | El archivo nunca va al servidor | ✅ Solo en algunos |
| **Metadatos Forenses** | IP, ubicación, dispositivo, tiempo - todo junto | ❌ Fragmentado |
| **Verificación QR** | Código QR de verificación instantánea | ⚠️ Restringido |
| **Limitación de Tasa** | Protección contra spam (RLS + Client) | ❌ No en la mayoría |

---

## 🗺️ Hoja de Ruta: Futuro "Sin Confianza"

La versión actual **(Beta v1.0)** está optimizada para proporcionar al usuario final máxima velocidad, interfaz fácil y acceso gratuito. Sin embargo, nuestra visión final es pasar a una estructura donde incluso el administrador de la base de datos (nosotros) no pueda intervenir.

### Fase 1: Beta v1.0 (Actualmente en Línea)

**Infraestructura:**
- Base de Datos en la Nube (Supabase)
- Registro off-chain (PostgreSQL + respaldo IPFS)
- Auto-atestación de galería (centralizada pero transparente)

**Token:**
- Plataforma: Pump.fun
- Liquidez: Raydium (automática)
- Gobernanza: Solo consultiva (consulta comunitaria)

**Propósito:**
- Velocidad, eliminar barreras UX
- Proporcionar seguridad "sin fricción"
- Construcción de comunidad

**Utilidad del Token (v1.0):**
- Acceso prioritario a eventos de galería
- Visualización del Registro PoArt
- Derecho de votación consultiva

---

### 🚀 Fase 2: Autoridad Descentralizada (2026 Q2-Q4)

Esta fase cubre la transición del sistema desde una estructura completamente operativa "del lado del cliente" a una estructura más segura y descentralizada.

| Característica | ¿Qué Aporta? | Stack Tecnológico | ETA |
|----------------|--------------|-------------------|-----|
| **Edge Function INSERT** | Bloqueo de spam + seguridad de API Key | Supabase Edge (Deno) | Q2 2026 |
| **Firma de Billetera** | Identidad descentralizada | Solana Wallet Adapter | Q2 2026 |
| **Respaldo IPFS/Arweave** | Archivo descentralizado | IPFS SDK + Pinata | Q3 2026 |
| **Mecanismo de Revocación** | Cancelación de certificado falso | Actualización de Esquema DB | Q2 2026 |
| **Registro de Auditoría** | Registro de consulta forense | Tabla de logs personalizada | Q3 2026 |
| **OpenTimestamps** | Anclaje en Bitcoin | OTS JavaScript | Q4 2026 |

**Gobernanza del Token (v2.0):**
- Votación off-chain (x/web) + firma de billetera
- Selección de representantes comunitarios (primeros 90 días)
- Control de billetera de operaciones multi-firma
- Votación consultiva ponderada (con límite de ballenas)

**Inmutabilidad:**
- Respaldo del registro con hashes IPFS
- Anclaje de marca de tiempo en Bitcoin
- Preparación de verificación entre cadenas

---

### Fase 3: Descentralización Total (2027+)

| Característica | Objetivo | ETA |
|----------------|----------|-----|
| **Registro On-Chain** | Registro on-chain en Solana | Q1 2027 |
| **Soporte Multi-Cadena** | Ethereum, Polygon, Base | Q2 2027 |
| **Integración DID** | Identidad Descentralizada | Q3 2027 |
| **Gobernanza Comunitaria** | Sistema consultivo fortalecido | Q4 2027 |
| **Reconocimiento Legal** | Validez en tribunales turcos | 2027-2028 |
| **API para Desarrolladores** | Endpoint de API pública | Q3 2027 |

**Evolución de Gobernanza:**
- v3.0: Modelo híbrido (curatorial + ponderado comunitario)
- 2028+: Gobernanza comunitaria completa (opcional)
- Control de calidad curatorial siempre preservado

---

## 🧬 Estructura de Datos del Protocolo (JSON Schema)

**Cada certificado [PoArt] tiene una tarjeta de identidad JSON portátil y verificable producida en el siguiente estándar.**

> **Nota:** Este formato Identity JSON es el formato de certificado presentado al usuario. En los registros del Registro, se usa `registry.asset` en lugar de `identity.asset_data` (mapeo: `identity.asset_data` == `registry.asset`).
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

## 🔬 Profundidad Técnica: Algoritmo de Sellado

### Funciones Hash Deterministas
```javascript
// Funciones Auxiliares: Convertir digest a cadena hex
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Convertir cadena a array de bytes
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Generación de cadena forense canónica (v1.0: orden de campo fijo + UTF-8 + delimitador \n)
// Nota Fase 2: Transición a JSON canónico con RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Proceso de Generación de NotarySeal (Completamente Determinista)
```javascript
// 1. Cálculo de FileHash (del lado del cliente)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Recopilación de datos forenses (uso de marca de tiempo única)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Generación de marca de tiempo única
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Misma marca de tiempo
  };
  
  return { forensics, timestamp };
}

// 3. Creación de EvidenceRoot (con codificación canónica)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Generación de NotarySeal (usando misma marca de tiempo)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Funciones auxiliares de enmascaramiento (soporte IPv4 e IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Verificación IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 o formato desconocido
  return "***";
}
```

### Flujo de Verificación (Dos Niveles)

#### Verificación Rápida (Quick Verify)
```javascript
// Solo verifica el hash del archivo (bandera roja rápida)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Obtener del registro
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Comparación de hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Original - Hash del archivo coincide"
    };
  } else {
    return {
      valid: false,
      message: "❌ Falso - Archivo manipulado"
    };
  }
}
```

#### Verificación Completa (Full Verify)
```javascript
// Regenera y verifica EvidenceRoot y NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Obtener del registro
  const cert = await fetchFromRegistry(certificateId);

  // 1) Verificación de FileHash (bandera roja rápida)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Falso - Hash del archivo no coincide" };
  }

  // 2) Regenerar EvidenceRoot (con forense almacenado en registro)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ No coincide - EvidenceRoot no pasa" };
  }

  // 3) Regenerar NotarySeal (con misma marca de tiempo + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ No coincide - NotarySeal no pasa" };
  }

  // Opcional: En Fase 2 también verificar signer_sig con attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Firma inválida" };

  return { valid: true, message: "✅ Original - Full Verify aprobado" };
}
```

> **Notas Importantes:**
> - **Quick Verify:** Solo verifica el hash del archivo para uso rápido.
> - **Full Verify:** Verifica todas las capas del protocolo (EvidenceRoot + NotarySeal).
> - Todas las operaciones hash se realizan determinísticamente, con codificación y delimitadores fijos.
> - **Estándar de canonicalización v1.0:** Orden de campo fijo + codificación UTF-8 + delimitador `\n`.
> - **Plan Fase 2:** Transición a JSON canónico con RFC 8785 (JCS - JSON Canonicalization Scheme).
> - En modo enmascarado, el cálculo de EvidenceRoot y NotarySeal se realiza con datos forenses enmascarados.
> - Se utiliza una única marca de tiempo en todo el proceso (forensics + NotarySeal); se garantiza el determinismo.
> - **Nombres de campos forenses:** `ip_masked`, `location`, `device`, `timestamp` (código y registro completamente compatibles).
> - **Ruta del registro:** `certificate.asset.fingerprints` (completamente compatible con código de verificación).
> - **signer_sig en el registro:** El campo `proof.signer_sig` es necesario para Full Verify.
> - El mecanismo SignerSignature se activará en Fase 2 con Solana Wallet Adapter; en v1.0 se puede verificar con `attestation_pubkey`.

---

## 📊 Análisis Competitivo (Actualizado)

PoArt está posicionado en el "Punto Óptimo" (Sweet Spot) que completa las deficiencias de las soluciones existentes.

| Característica | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|----------------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Costo** | 🆓 Gratis | 🆓 | 💰 De pago | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI Arrastrar y Soltar** | ✅ Muy fácil | ❌ CLI | ⚠️ Medio | ⚠️ Medio | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Exportación Multi-Formato** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Vista Previa en Tiempo Real** | ✅ En vivo | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Controles de Privacidad** | ✅ 3 Modos | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Hash del Lado Cliente** | ✅ Privacidad | ✅ | ❌ Carga | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Metadatos Forenses** | ✅ Completo | ❌ | ❌ | ⚠️ Restringido | ❌ | ⚠️ | ❌ | ⚠️ |
| **Verificación QR** | ✅ Instantánea | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Limitación de Tasa** | ✅ RLS+Cliente | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Anclaje Blockchain** | 🔄 Hoja de ruta | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Código Abierto** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Soporte Español** | ✅ Nativo | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Explicación:**
- ✅ : Soporte completo / disponible
- ⚠️ : Restringido / en planes de pago
- ❌ : No existe / no soportado
- 🔄 : En hoja de ruta (en desarrollo)
- 🆓 : Completamente gratis
- 💰 : De pago / requiere suscripción

### Deficiencias de Competidores, Fortalezas de PoArt

| Deficiencia | Competidores | PoArt |
|-------------|--------------|-------|
| **Dificultad de Uso** | CLI, conocimiento de API, billetera requerida | Arrastrar y soltar, termina en 3 clics |
| **Barrera de Costo** | Suscripción $50-500/mes | 100% gratis |
| **Privacidad** | Archivo se carga al servidor | Del lado del cliente, archivo nunca va |
| **Datos Forenses** | Solo marca de tiempo | IP, ubicación, dispositivo, tiempo - todo |
| **Soporte Español** | No existe o muy restringido | Soporte de idioma nativo |
| **Código Abierto** | Caja cerrada | Todo el código abierto en GitHub |

---

## 📈 Estadísticas de Uso (Objetivos Q1 2026)

| Métrica | Objetivo | Estado |
|---------|----------|--------|
| **Certificados Totales** | 1,000 | 🔄 En progreso |
| **Usuarios Activos** | 500 | 🔄 En progreso |
| **Número de Verificaciones** | 5,000 | 🔄 En progreso |
| **Tiempo de Actividad** | 99.9% | ✅ Activo |
| **Tiempo Promedio de Respuesta** | <200ms | ✅ Óptimo |

---

## 🌍 Comunidad y Soporte

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Colaboradores

El protocolo PoArt continúa desarrollándose con las contribuciones de la comunidad de código abierto.

**Para contribuir:**
1. Haga un Fork
2. Cree una rama de característica (`git checkout -b feature/amazing-feature`)
3. Haga Commit (`git commit -m 'Add amazing feature'`)
4. Haga Push (`git push origin feature/amazing-feature`)
5. Abra un Pull Request

### 🛠️ ¿Qué Necesitamos Ahora? (Llamado de Ayuda)

Esperamos las contribuciones de desarrolladores experimentados en los siguientes temas para los desarrollos de **Fase 2** del Protocolo PoArt:

* **Supabase Edge Functions:** Mover la protección contra spam al lado del servidor.
* **Solana Web3.js:** Integración de firma de billetera (Wallet Signing).
* **IPFS / Arweave:** Integración de servicios de archivo y pinning<

> Por favor, inicie una discusión en la pestaña "Issues" antes de agregar una característica.

---

## 💬 Notas Finales

### Pump.fun y Realidad

Este proyecto se inició en Pump.fun porque:
- ✅ Acceso a liquidez (migración automática Raydium)
- ✅ Acceso a comunidad existente
- ✅ Bajo costo inicial

Sin embargo, aclaremos esto:
- **El precio del token** no es un indicador de éxito artístico
- El valor del token es importante para el **presupuesto operativo** (galería, exposiciones, infraestructura)
- **Métricas de éxito:** Obras autenticadas + compromiso comunitario + visitantes físicos

### Gobernanza y Descentralización

**Realidad v1.0 (2026):**
- Registro: Off-chain (PostgreSQL + respaldo IPFS)
- Attestation: Auto-firmado por galería (centralizado pero transparente)
- Gobernanza: Solo consultiva (decisión final curatorial)

**Visión v2.0+ (2027+):**
- Registro: On-chain (Solana)
- Firmas: Basadas en billetera (descentralizadas)
- Gobernanza: Híbrida (consultiva comunitaria + calidad curatorial)
- Utilidad del token: Características mejoradas + acceso avanzado

Esta estructura proporciona **eficiencia operativa** y **control de calidad** en la etapa temprana, mientras mantiene abierto el camino para aumentar la **participación comunitaria** en el futuro.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // La Cultura es Más Grande Que el Capital*

## 🧾 Licencia

MIT License © 2026 İlhan Art Gallery Initiative

Vea [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) para términos completos.

---

## 💬 Créditos

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Este proyecto ha sido desarrollado con la iniciativa [İlhan Art Gallery] y los códigos fuente están abiertos al público en nombre de la transparencia.**

**PROTOCOLO V1.0 // SELLADO CON SHA-512**

*© 2026 İLHAN ART | TODOS LOS DERECHOS DE LAS OBRAS, IMÁGENES E IDEAS ESTÁN RESERVADOS.*

---

## 📝 Notas sobre Adaptación Cultural para el Mercado Hispanohablante

### Consideraciones Especiales para la Versión en Español

**Registro Lingüístico y Terminología:**
- Se mantiene un tono formal y técnico apropiado para documentación profesional
- Los términos criptográficos se mantienen en inglés (ej: PoArt, NotarySeal, EvidenceRoot)
- Se utilizan equivalentes técnicos establecidos en español (ej: "hash" → "hash", "blockchain" → "blockchain/cadena de bloques")
- Se preserva la terminología técnica internacional para mantener compatibilidad

**Expresiones Matemáticas:**
- Todas las fórmulas LaTeX se mantienen intactas
- Las explicaciones matemáticas siguen convenciones académicas hispanas
- Variables y símbolos permanecen sin cambios por universalidad

**Adaptación Cultural:**
- La metáfora "Casino vs. Museo" resuena fuertemente en el contexto hispanohablante
- Conceptos como "confianza", "transparencia" y "control de calidad" tienen gran peso cultural
- La distinción IA vs. creatividad humana es altamente relevante en mercados artísticos latinos

**Precisión Técnica:**
- Todos los ejemplos de código permanecen sin modificar (comentarios en inglés preservados)
- Estructuras JSON y nombres de campos mantienen formato original
- Endpoints de API y estructuras URL sin cambios

**Recomendaciones de Localización:**
- Para mercados hispanohablantes, mantener "İlhanArt Gallery" como nombre propio
- Información de contacto permanece original (orientación internacional)
- Considerar eventualmente soporte específico en español para consultas

---

## 🌎 Perspectivas para el Mercado Hispanohablante

**Asociaciones Potenciales:**
- Colaboración con galerías de arte contemporáneo en España y Latinoamérica
- Conexión con comunidades blockchain de habla hispana

**Cumplimiento Regulatorio:**
- Adaptación a regulaciones de activos cripto en países hispanohablantes
- Posible cooperación con ministerios de cultura
- Alineación con leyes de propiedad intelectual locales

**Propuesta de Valor Cultural:**
- Resonancia con tradiciones artísticas de "artesanía" y "oficio"
- Conexión con valores de autenticidad y origen
- Apreciación por la fusión de tradición y tecnología

**Oportunidades de Mercado:**
- Mercados de arte emergentes en México, Argentina, Colombia
- Comunidades artísticas digitales en España

---
