# 📚 GLOSARIO DE TERMINOLOGÍA Y CONCEPTOS
> **"Comprender el lenguaje de este protocolo es comprender su visión."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Infraestructura Central

**PoArt Forensic Engine (PFE)** es la capa principal que representa la lógica central y el funcionamiento técnico detrás del protocolo [PoArt]. Este es el "motor forense" que toma los datos brutos de producción de una obra de arte y los transforma en **evidencia digital** verificable e inmutable.

### 🧩 ¿Por qué "PoArt Forensic"?

- **PoArt (Proof of Art):** El enfoque del motor es vincular el valor de un activo digital no a la especulación, sino al **proceso de producción demostrable**.
- **Forensic (Verificación Forense):**
  - **Definición Técnica:** Un enfoque de algoritmo y cadena de registros para verificar que los datos del proceso de producción (pinceladas, timelapse, registros) no han sido manipulados.
  - **Capa Filosófica:** La afirmación de transformar **el tiempo humano, el esfuerzo y el costo de decisión** en una realidad medible, frente a la producción de "salida instantánea" de la IA.

> Nota: La integración de blockchain (p. ej., Solana) no es el núcleo de PFE; se definirá por separado como una **Chain Anchor Layer** para fines de verificación/registro.

### 🛠️ Alcance Técnico v1.0

**PoArt Forensic Engine (PFE) v1.0** está construido sobre los siguientes **3 pilares principales** en lugar de modelos financieros complejos:

1. **Hashing & Sealing (Sellado):**  
   PFE procesa de manera determinista todos los elementos en el Evidence Pack (archivo de obra, video, JSON/log, firma, etc.) y genera un valor único de **NotarySeal**.

   **Conceptos centrales (v1.0):**
   - **FileHash (huella digital de la obra):** Hash generado a partir de los bytes del archivo de la obra.
   - **EvidenceRoot (raíz del paquete de evidencia):** Resumen raíz que representa la integridad del Evidence Pack (raíz Merkle o hash de manifiesto canónico).
   - **NotarySeal (sello final / salida PFE):** Sello final generado a partir de la combinación de EvidenceRoot + tiempo + firma.

   **Fórmulas (claramente visibles para los inversores):**
   
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
   
   > Nota: El valor al que se hace referencia como salida PFE es **NotarySeal**. El mecanismo **SignerSignature** se activará en la Fase 2 (con Solana Wallet Adapter); en la v1.0 actual se utiliza la firma de certificación propia del sistema. La clave pública de certificación se publica en el registro bajo el campo `issuer.attestation_pubkey`.

2. **Indexing (Archivo):**  
   Registra qué billetera, en qué fecha, envió **Proof of Labor (Prueba de Trabajo)** para qué obra a una capa de registro transparente y consultable.  
   *(Esta capa puede ser una base de datos; la integración de cadena se define por separado como "Chain Anchor Layer".)*

3. **Verification (Verificación):**  
   Cuando se cuestiona la autenticidad de una obra, PFE reprocesa la evidencia bruta; prueba matemáticamente si los valores calculados de **EvidenceRoot / NotarySeal** coinciden con los registros de archivo.

---

### 🧮 Teorema de Valor PoArt (The Value Theorem)

El protocolo [PoArt] relaciona el valor ($V$) de un activo digital no con la percepción subjetiva del mercado, sino con **la realidad física del proceso de producción**.

La Inteligencia Artificial (IA) destruye el proceso al entregar el resultado instantáneamente ($t \to 0$). [PoArt], sin embargo, trata el valor como la acumulación de componentes de **tiempo, trabajo y voluntad**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definiciones de Variables

- **$\int dt$ (Acumulación de Proceso):**  
  El valor no es una "salida" instantánea; es un **proceso** acumulado entre $t_{\text{start}}$ y $t_{\text{end}}$. A medida que disminuye la duración (producción IA), el resultado de la integral se acerca a 0.

- **$P_{\text{labor}}(t)$ (Poder de Trabajo Instantáneo):**  
  Representa la intensidad del esfuerzo mental y físico gastado en el momento de producción. A medida que aumenta el esfuerzo demostrable, el integrando crece.  
  > Nota: Este término puede normalizarse en la práctica a través de "señales de trabajo medibles/demostrables".

- **$I_{\text{agency}}(t)$ (Coeficiente de Voluntad):**  
  La capacidad del productor para asumir riesgos y tomar decisiones. Toma un valor entre $0$ y $1$.
  - **IA ($I \approx 0$):** Ejecuta comandos, no asume riesgos, no paga costos.
  - **Humano ($I \to 1$):** Cambia decisiones, duda, asume riesgos.

- **$U_{\text{irreversible}}$ (Singularidad Irreversible):**  
  Mientras que deshacer (`Ctrl+Z`) es posible en la producción digital, en la producción física (pintura aplicada al lienzo, mármol tallado, gesto en transmisión en vivo) no hay vuelta atrás. Esta **irreversibilidad** es un término adicional que crea "singularidad" (carácter no fungible) en la obra.

### 🔎 Análisis de Caso: IA "Salida Instantánea" vs. Humano "Proceso Probado"

El siguiente escenario demuestra cómo funciona el **Teorema de Valor PoArt** en la práctica y por qué las producciones de IA obtienen puntuaciones bajas en el estándar [PoArt].

#### Escenario A: Producción Visual en 10 Segundos con IA

- **Duración ($\Delta t$):** $10$ segundos (proceso insignificante)
- **Poder de Trabajo ($P_{\text{labor}}$):** $1$ unidad (solo escribir comandos)
- **Coeficiente de Voluntad ($I_{\text{agency}}$):** $0.01$ (sin riesgo, sin costo)
- **Irreversibilidad ($U_{\text{irreversible}}$):** $0$ (reversible / copiable)

**Resultado:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Comentario:** Aunque la salida sea perfecta; el valor [PoArt] se acerca a $0$ porque no se vivió ningún proceso y no involucró voluntad/riesgo.

#### Escenario B: Producción Física de 6 Horas en Transmisión en Vivo

- **Duración ($\Delta t$):** $6$ horas ($21{,}600$ segundos)
- **Poder de Trabajo ($P_{\text{labor}}$):** $0.5$ unidades (continuidad del esfuerzo físico y mental)
- **Coeficiente de Voluntad ($I_{\text{agency}}$):** $0.9$ (cambiar decisiones, asumir riesgos, elecciones irreversibles)
- **Irreversibilidad ($U_{\text{irreversible}}$):** $>0$ (las huellas físicas no pueden deshacerse)

**Resultado:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Comentario:** A medida que el proceso se alarga y aumenta la voluntad (riesgo), el valor se acumula. El término $U_{\text{irreversible}}$ es una contribución adicional que crea "singularidad" (carácter no fungible) en la obra.

---

### ✅ Conclusión: Valor Vinculado a la Prueba (Proof-Bound Value)

Este teorema extrae la afirmación de valor de [PoArt] de ser un "me gusta" o una "narrativa de mercado" y lo vincula a **una realidad de producción demostrable**.

1. **Sin Proceso, Sin Valor:**  
   La IA destruye el proceso con salida instantánea ($t \to 0$). A medida que se estrecha la ventana del proceso, el resultado de la integral necesariamente se reduce:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **La Voluntad y el Riesgo son Multiplicadores:**  
   [PoArt] no solo mide el "tiempo invertido" sino también la capa real de decisión, riesgo y costo en ese tiempo. Una producción sin asumir riesgos (IA) tiene bajo valor:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **La Singularidad es Prueba Física, No Marketing:**  
   Las huellas irreversibles en la producción física (trazo de lienzo, astilla de mármol) están fuera de la lógica `Ctrl+Z` de lo digital. Esta irreversibilidad ($U_{\text{irreversible}}$) singulariza ontológicamente la obra.

> **🔐 RESUMEN:** Aunque el teorema del valor puede parecer incierto como medición (incluso si su contraparte en el mundo real no puede medirse completamente), el propósito de esta fórmula es mostrar la configuración y dirección de las variables. En la era de la IA, lo escaso no es la "imagen" sino **el trabajo demostrable, el tiempo y la voluntad.** [PoArt] mide esta escasez y la registra con **Evidence Pack**.

### 🏛️ La Importancia del Concepto de "Motor"

Los tokens que emergen de Pump.fun o plataformas similares suelen ser meramente **"boletos de acceso"**. **PoArt Forensic Engine (PFE)**, sin embargo, es la **capa lógica constitucional** que determina qué derechos protege ese boleto, cómo se registrará el trabajo y cómo se perpetuará el arte/ciencia/tecnología.

> **Nota:** La razón por la que lanzamos este proyecto en Pumpfun es porque no teníamos suficiente liquidez ni suficientes seguidores. Usar los datos existentes fue estratégicamente el movimiento correcto, aunque no fuera de la más alta calidad. Independientemente del presupuesto y los recursos, definir la lógica de este motor en GitHub demuestra que el proyecto no es solo especulación financiera, sino una visión de **infraestructura de software** y **biblioteca nacional digital** a largo plazo.

---

## 🎨 [PoArt] PROTOCOLO DE PRUEBA DE TRABAJO (Proof of Art Protocol v1.0)

> **"Artista Real, Producción Real, Valor Real."**

Este protocolo es un **mecanismo de defensa biológica e intelectual** desarrollado contra estafadores anónimos que rodean el ecosistema cripto, visuales de IA producidos en 5 minutos y la cultura "Pump & Dump".

---

## a) ¿Qué es [PoArt]? (Definición Filosófica y Técnica)

**Proof of Art [PoArt];** es un estándar de verificación institucional que garantiza que el valor detrás de un activo en la blockchain se basa no en la especulación, sino en **trabajo humano**, **tiempo** y **energía física** verificables.

Así como Bitcoin genera valor con *"Electricidad y Potencia de Procesador"* **(Proof of Work)**, los proyectos compatibles con [PoArt] generan valor con *"Habilidad Artística y Tiempo Humano"*.

Elimina el riesgo de *"El desarrollador vendió, el proyecto terminó"* en las plataformas Pump.fun y DEX; porque aquí el valor no está en el código, sino en la **continuidad de la producción**.

> **[PoArt] no dice a los participantes "Confía en nosotros"; dice "Aquí está la evidencia, ve con tus ojos, verifica con tus matemáticas."**

---

## b) Estándar de 5 Pilares [PoArt] (Los 5 Pilares de la Verdad)

Estos 5 elementos son filtros no manipulables que un proyecto debe pasar para recibir el sello [PoArt].

### 1) Prueba de Identidad en Vivo

- **Problema:** El mundo cripto está lleno de fundadores anónimos (Devs) con identidades poco claras que recaudan dinero y abandonan proyectos.
- **Solución [PoArt]:** El productor prueba no solo un documento de identidad, sino **presencia en el momento de producción**. Esto incluye sesiones de transmisión en vivo donde ocurre interacción con la comunidad y se cumplen solicitudes instantáneas específicas, no videos pregrabados.  
  (P. ej., *"Escribe la fecha de hoy y el número de bloque actual en la esquina derecha del lienzo"*)
- **Lema:** *"Los bots pueden pintar pero los bots no sudan y no pueden improvisar."*

### 2) Prueba de Trabajo y Proceso

- **Problema:** Visuales de IA (Inteligencia Artificial) producidos en 2 segundos recibiendo el mismo trato de "jpeg" que pinturas al óleo hechas en 2 meses en el mundo digital.
- **Solución [PoArt]:** Se registra el proceso de "embarazo y nacimiento" de la obra. Se documentan las etapas de boceto, capas de pintura, horas acumuladas gastadas y el proceso físico que experimentó el artista al crear la obra. Esto agrega **"Costo de Tiempo"** al token. Cuanto más difícil sea la producción de un activo, más sólido es su valor.

### 3) Prueba de Valor Estético

- **Problema:** Cultura "Meme" que se enfoca solo en la comedia instantánea mientras ignora la estética y la profundidad artística, resultando en proyectos "Hype" de corta duración.
- **Solución [PoArt]:** El proyecto debe tener estándares de arte académico, teoría del color, reglas de composición y conocimiento de materiales (Impasto, Textura, etc.). El contenido no solo debe hacer reír; debe inspirar admiración en los espectadores y tener **valor coleccionable**.

### 4) Novedad Conceptual

- **Problema:** Miles de monedas de perro/gato copias sin creatividad.
- **Solución [PoArt]:** El proyecto debe construir un nuevo puente que combine arte, ciencia, filosofía o tecnología en una estructura significativa.  
  (P. ej., Combinar la escultura clásica de David con datos del mercado cripto; procesar la idea de que la percepción humana "se convierte en piedra" a través de esto y fundamentarlo con fuentes científicas.)  
  La obra no solo debe ser una fiesta visual sino también un desafío intelectual que provoque pensamiento sobre **Ciencia, Filosofía o Tecnología**.

> [!IMPORTANT]
> **Ejemplo de Referencia (Efecto Las Palmitas):** En el barrio de Las Palmitas en México, plagado de crimen, más de 200 casas se transformaron en un espectáculo arcoíris masivo. Como resultado de esta intervención estética, las tasas de criminalidad en el barrio disminuyeron en cierta medida, y los jóvenes comenzaron a involucrarse con el arte en lugar de las pandillas. El cambio estético recodificó el respeto de las personas por su entorno y entre sí (Cohesión Social).
>
> **Expectativa:** Un proyecto que entre en la lista [PoArt] debe, como en el ejemplo anterior, contener una relación de causa-efecto sociológica, científica o filosófica más allá de la estética visual pura. Dado que el tiempo es el único activo que no se puede comprar con dinero, en este protocolo el tiempo debe probarse siendo apostado como garantía. La base conceptual del proyecto debe ser tan fuerte y universal que incluso en un posible escenario CTO (Community Take Over) años después, la comunidad pueda continuar autónomamente el potencial innovador del proyecto heredando este legado.

### 5) Voluntad No Algorítmica

- **Problema:** Producciones digitales perfectas pero sin alma que se repiten entre sí.
- **Solución [PoArt]:** La voluntad única del humano que puede cometer errores, asumir riesgos y experimentar fluctuaciones emocionales debe sentirse en la obra. La incertidumbre en las pinceladas, las reacciones inesperadas de los materiales y las decisiones instantáneas del artista son la **Firma Biológica** que separa la obra de la "Producción de Máquina".

---

## c) Mecanismo de Verificación y Anti-Fraude

Este sistema garantiza que el proyecto permanezca confiable y vivo no solo "al principio" sino "para siempre".

### 📦 Paquete de Evidencia - El Gemelo Digital

Detrás de cada obra certificada [PoArt] hay un paquete de datos cifrado y con marca de tiempo que los inversores pueden descargar:

- **Grabaciones de Video RAW:** Metraje en bruto ininterrumpido del momento de producción.
- **Análisis de Metadatos:** Fecha de creación del archivo, información del dispositivo utilizado y datos de ubicación.
- **Referencias Físicas:** Evidencia de que la obra existe en el mundo físico  
  (P. ej., Periódico actual o datos de blockchain de ese momento al lado de la obra).

> *Nota de consistencia:* El término "paquete de evidencia" se conecta a la cadena **Evidence Pack → EvidenceRoot → NotarySeal** en secciones anteriores; es decir, la integridad del paquete está representada por un sello verificable.

### 🔄 Renovación de 365 Días (El Protocolo de Sostenibilidad)

- **Característica Revolucionaria:** En los proyectos cripto, el "Dev" (Desarrollador) lanza el token y generalmente desaparece después de 1-2 meses (Soft Rug). [PoArt] hace esto imposible.
- **Regla:** El estado de "Artista Verificado" no es de por vida. Solo **1 año** es válido.
- **Operación:** El artista/desarrollador debe presentar a la comunidad **una nueva obra importante y demostrable** cada 365 días.
- **Escenario de Ejemplo:** Lanzaste el proyecto en 2026. En enero de 2027, el sistema da una advertencia de "Período de Prueba Expirado". Si el artista no presenta una nueva exposición, nueva obra física o nueva integración tecnológica, la "Insignia de Confianza" del proyecto cae.
- **Resultado:** Este sistema garantiza que **el contenido nunca pierda relevancia** y que el inversor nunca experimente el miedo de *"¿Sigue aquí el desarrollador?"*. El proyecto se convierte en un estudio vivo.

### 🚩 Protocolo de Bandera Roja

**En caso de cualquier fraude detectado por la comunidad o algoritmos (uso de IA, obra robada, video manipulado):**

1. El certificado se marca inmediatamente como **"VOID" (NULO)**.
2. Los paquetes de evidencia se etiquetan públicamente como **"Falsos"**.
3. El proyecto se coloca en la lista negra de [PoArt]. Esto refuerza que en un mundo descentralizado, **la reputación es la única moneda**.

---

## d) Conclusión: No un Casino, Sino un Museo

**Pump.fun y los Intercambios Descentralizados (DEX) desafortunadamente son casinos ahora mismo; las luces parpadean, todos persiguen ganancias rápidas, y la casa (estafadores) siempre gana. La razón por la que comenzamos el proyecto aquí es la falta de presupuesto suficiente y tener un entorno para llegar a la audiencia existente a través de transmisiones en vivo.**

**[PoArt] es una fortaleza construida en medio de este casino.**

- 🎰 El casino se basa en juegos de cartas; nosotros nos basamos en la **realidad física**.
- 🃏 El casino está abierto al engaño; nosotros estamos abiertos a la **evidencia transparente**.
- ⏳ El casino es temporal; nos enfocamos en **la eternidad del arte y la ciencia**.

**Un token que usa este protocolo no es solo una "moneda"; es una equidad digital que contiene sudor, pintura, código y filosofía.**

---

## 🗳️ 6) GOBERNANZA Y REGISTRO PÚBLICO

**El propósito de esta sección es: transformar el estándar [PoArt] del plano de "confianza en individuos" a una infraestructura pública sostenible con registro + verificación + supervisión de la comunidad.**

### 6.1 Registro Público

- **Registro Público:** Todos los datos aprobados se registran en `ilhanart.org/registry` (o GitHub Registry).

**Lógica de registro (estándar recomendado - en formato de ruta JSON):**

Cada registro que ingresa al registro lleva estos campos centrales verificables mínimos:

- **Identidad y Estado:**
  - `certificate_id` (referencia legible)
  - `status` (active / void)
  - `void_reason` (si aplica)
  - `visibility` (private / masked / public)
  - `created_at` (marca de tiempo)

- **Institución Emisora:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Información de la Obra:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (si es posible; para identidad con puerta de token)
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
  - `governance.veto_threshold`

El registro puede tener dos capas:
- **1)** Índice legible por humanos (listado web / búsqueda / filtro)
- **2)** Manifiesto legible por máquina (registros JSON; para verificación PFE)

**Este "registro" se vuelve verificable a través de la cadena Evidence Pack → EvidenceRoot → NotarySeal de PFE. El registro ofrece objetivos de verificación, no "afirmaciones".**

---

### 6.2 Veto Comunitario del 40% (Gobernanza con Puerta de Token)

- **Veto Comunitario del 40%:** La votación comienza un mes antes de que se otorgue el estado; el 40% de objeción de la comunidad **con Puerta de Token (verificada por Solana)** invalida la solicitud.

**Flujo de votación (proceso claro recomendado):**
- **Ventana de solicitud:** El proyecto candidato abre "registro de candidato PoArt" (los registros de candidatos aparecen en estado "pendiente").
- **Período de revisión:** La comunidad examina la evidencia durante 30 días (Evidence Pack + grabaciones de transmisión en vivo + metadatos).
- **Verificación con puerta de token:** La votación se realiza con billeteras verificadas en Solana (p. ej., propiedad de token/NFT específico + firma de billetera).
- **Regla de veto:** Si el 40% de los votos son **objeción (NO / VETO)**, la solicitud es rechazada.
- **Transparencia:** El resultado de la votación se almacena en el registro como "registro de decisión" (fecha, proporción, ID de instantánea).

---

### 6.3 Sincronización de Metadatos (Alineación con el Mundo Físico)

- **Sincronización de Metadatos:** Los datos técnicos en el registro deben coincidir 100% con la entidad física.

**Definir técnicamente la "coincidencia del 100%" (claridad recomendada):**
- **Coincidencia mínima (obligatoria):**
  - El `asset.fingerprints.sha256/sha512` en el registro debe ser **idéntico** al hash del archivo en cuestión.
  - Cuando se reproduce el `proof.notary_seal` en el registro (si existe Evidence Pack), debe ser **idéntico**.
- **Coincidencia de referencia física (tipo de prueba):**
  - La obra física + referencia de fecha/bloque mostrada en la transmisión en vivo y pruebas similares deben ser consistentes con el Evidence Pack.
- **Cumplimiento de privacidad:**
  - Los campos como IP/ubicación en visibilidad `masked` se publican **según estándares de enmascaramiento**.

---

### 6.4 Disputa y Revocación

El registro no es solo un mecanismo de "aprobación"; es un **mecanismo de auditoría vivo contra el fraude**.

- Cuando se inicia una disputa, el registro puede colocarse en modo **"review" (revisión)**.
- Si se detecta fraude, se marca como `status: void` con razón agregada:
  - `void_reason` (uso de IA / robo / manipulación, etc.)
  - `revoked_at` (tiempo de revocación)
- La fuente de la decisión de revocación es claramente visible en el registro:
  - votación comunitaria / comité autorizado / nota de investigación forense (lo que aplique)

> **Esta sección es la contraparte en el registro del concepto VOID en la sección "Protocolo de Bandera Roja".**

---

### 6.5 Ejemplo de Registro (Legible por Máquina)
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
> *Nota: `asset.fingerprints.sha512` y otros valores hash están abreviados para fines de visualización; en la implementación real se utilizan cadenas de caracteres hexadecimales de longitud completa.*

---

## 7) 🔐 SELLO TÉCNICO (NOTARY SEAL)

El algoritmo de sello inquebrantable generado por **PoArt Forensic Engine (PFE) v1.0**:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Protocolo de Notario Digital y Evidencia Forense (Beta v1.0)

> **"La cultura es mayor que el capital. Protege tus obras hoy, llévalas al mañana."**

---

## ¿Por Qué Público?

La verdadera seguridad proviene de la transparencia. Gracias a nuestro sistema de **Registro Público**, cualquier persona en cualquier parte del mundo puede verificar si un archivo es original en segundos, sin necesidad de ninguna autoridad.

---

## 🧩 ¿Por Qué Múltiples "Módulos de Visibilidad"?

Esta es la parte más crítica del código (menú de selección de visibilidad). Estas opciones permiten a los usuarios equilibrar **"Privacidad vs. Transparencia"**:

### 🔒 Privado

- **Escenario:** El artista aún no quiere publicar la obra pero quiere marcarla con tiempo para probar "hice esto en esta fecha".
- **Lo que Hace el Código:** Escribe datos en la base de datos pero estampa `visibility: "private"`. Más tarde, al escribir la política "Public Read", puedes ocultar estos registros del público con `WHERE visibility = 'public'`.

### 🕶️ Enmascarado

- **Escenario:** El artista quiere transparencia pero teme que se encuentre su dirección de casa (ubicación IP).
- **Lo que Hace el Código:** Las funciones `maskIP` y `maskLoc` funcionan en el lado de JavaScript. Convierte la dirección IP al formato `88.241.***.***`, la ubicación al formato `***/TR`, y envía la versión censurada a la base de datos.
- **Nota de Privacidad:** El enmascaramiento se realiza en el navegador, Supabase no ve la ubicación real. **Sin embargo:** Si se utilizan APIs de terceros como ipapi.co para datos de ubicación, estos proveedores ven la dirección IP en el momento de la solicitud.
- **Sellado en Modo Enmascarado:** El cálculo de EvidenceRoot y NotarySeal se realiza con datos forenses enmascarados; por lo tanto, la verificación permanece determinista.

### 🌍 Público

- **Escenario:** Transparencia total. Según los estándares [PoArt], dónde, cuándo, desde qué red se produjo la obra se declara claramente.

---

## 💡 Innovación Tecnológica

PoArt no es solo un sistema de carga de archivos. Es un motor de **"Cadena de Custodia Forense"** que trae un nuevo estándar fundiendo tres capas de tecnología diferentes en una sola olla.

**La capa descrita como "motor" en esta sección corresponde al núcleo PoArt Forensic Engine (PFE) en la terminología anterior.**

### 1) Hashing del Lado del Cliente (Máxima Privacidad)

Tus archivos de obra de arte nunca se cargan en el servidor. Nuestro motor basado en navegador (lado del cliente) calcula el hash (resumen digital) del archivo en tu propia computadora. Solo esta huella digital y los metadatos se envían al servidor.

> **Nota de Privacidad:** El archivo de la obra no se carga en el servidor y está protegido de esta manera. Sin embargo, los datos forenses (IP/ubicación) se comparten según el modo de visibilidad seleccionado (privado/enmascarado/público).

### 2) Fusión de Datos Forenses (Poder Forense)

Mucho más que una marca de tiempo ordinaria. El sistema combina estos datos en un solo "Sello Génesis":

- **Resumen Digital (SHA-512):** Huella digital usando el estándar de resumen criptográfico (SHA-512) que se romperá si incluso un píxel de la obra cambia.
- **Ubicación y Tiempo:** Fecha con precisión de milisegundos, país, ciudad y datos de distrito de la transacción.
- **Identidad del Dispositivo:** Sistema operativo, navegador y tipo de dispositivo (análisis de User-Agent).

---

## 🛡️ Casos de Uso y Beneficios

Si eres artista, escritor o diseñador, decir "Hice esto antes" no es suficiente; necesitas probarlo.

**Una obra que sellas con PoArt:**

- **Prueba Matemática:** Si incluso un píxel de tu archivo cambia, el sistema lo sabe. La manipulación es imposible.
- **Base Legal:** Está registrado en qué fecha, qué ciudad, desde qué dispositivo se selló la obra.
- **Certificado Instantáneo:** Genera un **"Certificado de Identidad de Activo"** especial para ti en segundos, con código QR y sellado.

---

## ⚙️ Arquitectura del Sistema y Características Técnicas

El sistema está diseñado en una arquitectura "Sin Servidor", enfocándose en alto rendimiento y escalabilidad.

| Capa | Tecnología | Descripción |
|--------|-----------|-------------|
| **Criptografía** | SHA-256 & SHA-512 | Resumen criptográfico de doble capa |
| **Base de Datos** | Supabase (PostgreSQL) | Estructura de datos JSONB, políticas RLS |
| **Datos Forenses** | ipapi.co API | Trinidad de IP/Ubicación/Tiempo |
| **Renderizado** | html2canvas + jsPDF | Generación de PNG/PDF del lado del cliente |
| **Frontend** | Vanilla JavaScript | Dependencia de framework cero |
| **Seguridad** | Hashing del lado del cliente | El archivo nunca va al servidor |

### Características Destacadas

| Característica | Detalle | ¿En Competidores? |
|---------|-------|-----------------|
| **UI de Arrastrar y Soltar** | Arrastrar y soltar archivo, vista previa instantánea | ❌ Ausente en la mayoría |
| **Exportación Multi-Formato** | PNG, JSON, PDF - un clic | ⚠️ Limitado |
| **Vista Previa en Tiempo Real** | Vista previa de certificado en vivo | ❌ Ninguno |
| **Controles de Privacidad** | Opciones Privado/Enmascarado/Público | ❌ Ninguno |
| **Hashing del Lado del Cliente** | Archivo nunca va al servidor | ✅ Solo en algunos |
| **Metadatos Forenses** | IP, ubicación, dispositivo, tiempo - todo junto | ❌ Fragmentado |
| **Verificación QR** | Código QR de verificación instantánea | ⚠️ Limitado |
| **Limitación de Velocidad** | Protección contra spam (RLS + Cliente) | ❌ Ausente en la mayoría |

---

## 🗺️ Hoja de Ruta: Futuro "Sin Confianza"

La versión actual **(Beta v1.0)** está optimizada para proporcionar a los usuarios finales máxima velocidad, interfaz fácil y acceso gratuito. Sin embargo, nuestra visión final es hacer la transición a una estructura donde incluso el administrador de la base de datos (nosotros) no pueda interferir.

### Fase 1: Beta (Actualmente en Vivo)

- **Infraestructura:** Base de Datos en la Nube (Supabase).
- **Propósito:** Velocidad, eliminación de barreras UX (Experiencia de Usuario) y adaptación. Proporcionar seguridad "sin fricción".

### 🚀 Fase 2: (Requisitos de Backend / Función Edge)

Esta fase cubre la transición de la estructura de trabajo completamente "del lado del cliente" a una estructura de "Autoridad del Lado del Servidor" más segura y manejable.

| Elemento | ¿Qué Aporta? | Pila Tecnológica | Prioridad |
|-------|---------------|------------|---------|
| **`INSERT` → Función Edge** | Prevención de spam + seguridad de clave API | Supabase Edge (Deno) | 🔴 Alta |
| **Firma de Billetera** | Autenticación criptográfica | Solana Wallet Adapter | 🟡 Media |
| **Respaldo IPFS/Arweave** | Inmutabilidad descentralizada | IPFS SDK + Pinata | 🟢 Baja |
| **Mecanismo de Revocación** | Cancelación de certificado falso | Actualización de esquema de BD | 🔴 Alta |
| **Registro de Auditoría** | Registro de consulta forense | Tabla de registros personalizada | 🟡 Media |
| **OpenTimestamps** | Anclaje de Bitcoin | OTS JavaScript | 🟢 Baja |
| **Integración DID** | Identidad Descentralizada | ION/Ceramic | 🟢 Baja |

### Fase 3: Descentralización Completa (Largo Plazo)

| Característica | Objetivo | ETA |
|---------|------|-----|
| **Registro Blockchain** | Registro en cadena Ethereum/Solana | Q4 2026 |
| **Gobernanza DAO** | Gestión comunitaria | Q1 2027 |
| **Soporte Multi-Cadena** | Polygon, Arbitrum, Base | Q2 2027 |
| **Reconocimiento Legal** | Validez en tribunales turcos | 2027-2028 |
| **API para Desarrolladores** | Punto final de API pública | Q3 2026 |

---

## 📊 Análisis Competitivo (Actualizado)

PoArt está posicionado en el "Punto Óptimo" que completa las deficiencias de las soluciones existentes.

| Característica | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Costo** | 🆓 Gratis | 🆓 | 💰 Pago | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI de Arrastrar y Soltar** | ✅ Muy Fácil | ❌ CLI | ⚠️ Medio | ⚠️ Medio | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Exportación Multi-Formato** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Vista Previa en Tiempo Real** | ✅ En Vivo | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Controles de Privacidad** | ✅ 3 Modos | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Hash del Lado del Cliente** | ✅ Privacidad | ✅ | ❌ Carga | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Metadatos Forenses** | ✅ Completo | ❌ | ❌ | ⚠️ Limitado | ❌ | ⚠️ | ❌ | ⚠️ |
| **Verificación QR** | ✅ Instantánea | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Limitación de Velocidad** | ✅ RLS+Cliente | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Anclaje Blockchain** | 🔄 Hoja de Ruta | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Código Abierto** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Soporte Turco** | ✅ Nativo | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Leyenda:**
- ✅ : Soporte completo / disponible
- ⚠️ : Limitado / en planes pagos
- ❌ : Ninguno / no soportado
- 🔄 : En hoja de ruta (desarrollando)
- 🆓 : Completamente gratis
- 💰 : Pago / requiere suscripción

### Deficiencias de Competidores, Fortalezas de PoArt

| Menos | Competidores | PoArt |
|-------|-------------|-------|
| **Dificultad de Uso** | CLI, conocimiento de API, se requiere billetera | Arrastrar y soltar, listo en 3 clics |
| **Barrera de Costo** | Suscripción de $50-500/mes | 100% gratis |
| **Privacidad** | El archivo se carga en el servidor | Del lado del cliente, el archivo nunca va |
| **Datos Forenses** | Solo marca de tiempo | IP, ubicación, dispositivo, tiempo - todo |
| **Soporte Turco** | Ninguno o muy limitado | Soporte de idioma nativo |
| **Código Abierto** | Caja cerrada | Todo el código abierto en GitHub |

---

## 🧬 Estructura de Datos del Protocolo (JSON Schema)

**Cada certificado [PoArt] tiene una tarjeta de identidad JSON portátil y verificable producida en el siguiente estándar.**

> **Nota:** Este formato de JSON de identidad es el formato de certificado presentado a los usuarios. En los registros del registro, se usa `registry.asset` en lugar de `identity.asset_data` (mapeo: `identity.asset_data` == `registry.asset`).
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

## 🔬 Profundidad Técnica: Algoritmo de Sello

### Funciones Hash Deterministas
```javascript
// Funciones Auxiliares: Convertir resumen a cadena hexadecimal
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Convertir cadena a matriz de bytes
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Generación de cadena forense canónica (v1.0: orden de campo fijo + UTF-8 + delimitador \n)
// Nota Fase 2: Se hará transición a JSON canónico con RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Proceso de Producción de NotarySeal (Completamente Determinista)
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

// 4. Generación de NotarySeal (uso de la misma marca de tiempo)
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

#### Quick Verify (Verificación Rápida)
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
      message: "✅ Original - El hash del archivo coincide"
    };
  } else {
    return {
      valid: false,
      message: "❌ Falso - El archivo ha sido manipulado"
    };
  }
}
```

#### Full Verify (Verificación Completa)
```javascript
// Regenera y verifica EvidenceRoot y NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Obtener del registro
  const cert = await fetchFromRegistry(certificateId);

  // 1) Verificación de FileHash (bandera roja rápida)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Falso - El hash del archivo no coincide" };
  }

  // 2) Regenerar EvidenceRoot (con datos forenses almacenados en el registro)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ No coincide - EvidenceRoot no se sostiene" };
  }

  // 3) Regenerar NotarySeal (con la misma marca de tiempo + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ No coincide - NotarySeal no se sostiene" };
  }

  // Opcional: En Fase 2, también verificar signer_sig con attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Firma inválida" };

  return { valid: true, message: "✅ Original - Verificación completa aprobada" };
}
```

> **Notas Importantes:**
> - **Quick Verify:** Solo verifica el hash del archivo para uso rápido.
> - **Full Verify:** Verifica todas las capas del protocolo (EvidenceRoot + NotarySeal).
> - Todas las operaciones hash se realizan de manera determinista con codificación y delimitadores fijos.
> - **Estándar de canonicalización v1.0:** Orden de campo fijo + codificación UTF-8 + delimitador `\n`.
> - **Plan Fase 2:** Transición a JSON canónico con RFC 8785 (JCS - JSON Canonicalization Scheme).
> - En modo enmascarado, el cálculo de EvidenceRoot y NotarySeal se realiza con datos forenses enmascarados; por lo tanto, la verificación permanece determinista.
> - Se usa una única marca de tiempo en todo el proceso (forense + NotarySeal); se garantiza el determinismo.
> - **Nombres de campo forenses:** `ip_masked`, `location`, `device`, `timestamp` (código y registro completamente compatibles).
> - **Ruta de registro:** `certificate.asset.fingerprints` (completamente compatible con el código de verificación).
> - **signer_sig en el registro:** El campo `proof.signer_sig` es necesario para Full Verify.
> - El mecanismo SignerSignature se activará en Fase 2 con Solana Wallet Adapter; en v1.0, la verificación se puede hacer con `attestation_pubkey`.

---

## 📈 Estadísticas de Uso (Objetivos Q1 2026)

| Métrica | Objetivo | Estado |
|--------|--------|--------|
| **Certificados Totales** | 1,000 | 🔄 Progreso |
| **Usuarios Activos** | 500 | 🔄 Progreso |
| **Conteo de Verificación** | 5,000 | 🔄 Progreso |
| **Uptime** | 99.9% | ✅ Activo |
| **Tiempo de Respuesta Promedio** | <200ms | ✅ Óptimo |

---

## 🌍 Comunidad y Soporte

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 Contribuidores

El protocolo PoArt continúa desarrollándose con contribuciones de la comunidad de código abierto.

**Para contribuir:**
1. Haz Fork del repositorio
2. Crea una rama de característica (`git checkout -b feature/amazing-feature`)
3. Haz Commit (`git commit -m 'Add amazing feature'`)
4. Haz Push (`git push origin feature/amazing-feature`)
5. Abre un Pull Request

### 🛠️ ¿Qué Necesitamos Ahora? (Llamado de Ayuda)

El Protocolo PoArt busca desarrolladores experimentados en las siguientes áreas para desarrollos de **Fase 2**:

* **Supabase Edge Functions:** Mover la protección contra spam al lado del servidor.
* **Solana Web3.js:** Integración de firma de billetera.
* **IPFS / Arweave:** Integración de servicios de archivo y fijación.

> Por favor, inicia una discusión en la pestaña "Issues" antes de agregar una característica.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Cultura > Capital"*

## 🧾 Licencia

Licencia MIT © 2026 Iniciativa Galería de Arte İlhan

Ver [![Licencia](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) para términos completos.

---

## 💬 Créditos

![Versión](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Seguridad](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Plataforma](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![Licencia](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Este proyecto es desarrollado por la iniciativa [Galería de Arte İlhan], y sus códigos fuente están disponibles públicamente para transparencia.**

**PROTOCOLO V1.0 // SELLADO CON SHA-512**

*© 2026 İLHAN ART | TODOS LOS DERECHOS RESERVADOS PARA OBRAS DE ARTE, VISUALES E IDEAS.*

---
