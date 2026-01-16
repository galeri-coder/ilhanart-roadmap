# 📚 מילון מונחים ומושגים
> **"להבין את שפת הפרוטוקול הזה פירושו להבין את החזון שלו."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: תשתית ליבה

**PoArt Forensic Engine (PFE)** מייצג את שכבת הליבה של הלוגיקה והפעולה הטכנית מאחורי פרוטוקול [PoArt]. זהו "המנוע הפורנזי" שלוקח את נתוני הייצור הגולמיים של יצירת האמנות והופך אותם ל**ראיה דיגיטלית** ניתנת לאימות ובלתי ניתנת לשינוי.

### 🧩 למה "PoArt Forensic"?

- **PoArt (Proof of Art):** המוקד של המנוע הוא לקשר את ערך הנכס הדיגיטלי לא לספקולציה אלא ל**תהליך ייצור שניתן להוכיח**.
- **Forensic (אימות פורנזי):**
  - **הגדרה טכנית:** גישת אלגוריתם ושרשרת רישום לאימות שנתונים הקשורים לתהליך הייצור (משיכות מכחול, timelapse, לוגים) לא עברו מניפולציה.
  - **שכבה פילוסופית:** הטענה להפוך את הייצור האנושי המכיל **זמן, מאמץ ועלות החלטה** למציאות מדידה, בניגוד ל"פלט מיידי" של בינה מלאכותית.

> הערה: אינטגרציית בלוקצ'יין (למשל Solana) אינה הליבה של PFE; היא מטופלת בנפרד כ**Chain Anchor Layer** לאימות/רישום.

### 🛠️ היקף טכני v1.0

**PoArt Forensic Engine (PFE) v1.0** נבנה על **3 עמודים עיקריים** במקום מודלים פיננסיים מורכבים:

1. **Hashing & Sealing (חתימה והטבעה):**  
   PFE מעבד את כל האלמנטים ב-Evidence Pack (קובץ יצירה, וידאו, JSON/לוג, חתימה וכו') באופן דטרמיניסטי ומייצר ערך **NotarySeal** ייחודי.

   **מושגי ליבה (v1.0):**
   - **FileHash (טביעת אצבע של יצירה):** Hash שנוצר מהבייטים של קובץ היצירה.
   - **EvidenceRoot (שורש חבילת הראיות):** סיכום שורש המייצג את שלמות ה-Evidence Pack (Merkle root או canonical manifest hash).
   - **NotarySeal (חותמת סופית / פלט PFE):** החותמת הסופית שנוצרת משילוב EvidenceRoot + זמן + חתימה.

   **נוסחאות (מוצגות בבהירות למשקיע):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **הגדרות Canonical Payload (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > הערה: הערך המכוון כפלט PFE הוא **NotarySeal**. מנגנון **SignerSignature** יופעל בשלב 2 (עם Solana Wallet Adapter); v1.0 הנוכחי משתמש בחתימת attestation של המערכת עצמה. מפתח ציבורי של Attestation מתפרסם בשדה `issuer.attestation_pubkey` ברישום.

2. **Indexing (אינדקסציה):**  
   רושם איזה ארנק הגיש **Labor Proof (הוכחת עבודה)** לאיזו יצירה באיזה תאריך לשכבת רישום שקופה וניתנת לשאילתות.  
   *(שכבה זו יכולה להיות מסד נתונים; אינטגרציית שרשרת מוגדרת בנפרד כ"Chain Anchor Layer".)*

3. **Verification (אימות):**  
   כאשר אותנטיות של יצירה נשאלת, PFE מעבד מחדש את הראיות הגולמיות; בודק בוודאות מתמטית האם ערכי **EvidenceRoot / NotarySeal** המחושבים תואמים לרשומה בארכיון.

---

### 🧮 משפט הערך של PoArt (The Value Theorem)

פרוטוקול [PoArt] מקשר את ערך ($V$) הנכס הדיגיטלי לא לתפיסת שוק סובייקטיבית אלא ל**מציאות הפיזית של תהליך הייצור**.

בינה מלאכותית (AI) הורסת את התהליך על ידי מתן תוצאה מיידית ($t \to 0$). [PoArt] רואה את הערך כהצטברות של רכיבי **זמן, עבודה ורצון**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### הגדרות משתנים

- **$\int dt$ (הצטברות תהליך):**  
  ערך אינו "פלט" מיידי; הוא **תהליך** המצטבר בין $t_{\text{start}}$ ו-$t_{\text{end}}$. ככל שהזמן מתקצר (ייצור AI), תוצאת האינטגרל מתקרבת ל-0.

- **$P_{\text{labor}}(t)$ (עוצמת עבודה רגעית):**  
  מייצג את עוצמת המאמץ המנטלי והפיזי המושקע ברגע הייצור. ככל שהמאמץ הניתן להוכחה גדל, האינטגרנד גדל.  
  > הערה: מונח זה יכול להיות מנורמל בפועל דרך "אותות עבודה מדידים/ניתנים להוכחה".

- **$I_{\text{agency}}(t)$ (מקדם רצון):**  
  יכולת לקיחת סיכונים וקבלת החלטות של היוצר. לוקח ערך בין $0$ ל-$1$.
  - **AI ($I \approx 0$):** מבצע פקודות, לא לוקח סיכונים, לא משלם מחיר.
  - **אדם ($I \to 1$):** משנה החלטות, מהסס, לוקח סיכונים.

- **$U_{\text{irreversible}}$ (ייחודיות בלתי הפיכה):**  
  בייצור דיגיטלי, ביטול (`Ctrl+Z`) אפשרי; אבל בייצור פיזי (צבע על קנבס, שיש מגולף, מחווה בשידור חי), אין חזרה. **בלתי הפיכות** זו היא מונח נוסף שיוצר "ייחודיות" (אופי non-fungible) ביצירה.

### 🔎 ניתוח מקרה: AI "פלט מיידי" לעומת "תהליך מוכח" אנושי

התרחיש הבא מראה איך **משפט הערך של PoArt** עובד בפועל ולמה יצירות AI מקבלות ציון נמוך בתקן [PoArt].

#### תרחיש A: יצירת תמונה עם AI ב-10 שניות

- **זמן ($\Delta t$):** $10$ שניות (כמעט ללא תהליך)
- **עוצמת עבודה ($P_{\text{labor}}$):** $1$ יחידה (רק כתיבת פקודה)
- **מקדם רצון ($I_{\text{agency}}$):** $0.01$ (ללא סיכון, ללא מחיר)
- **בלתי הפיכות ($U_{\text{irreversible}}$):** $0$ (ניתן לביטול / להעתקה)

**תוצאה:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **פרשנות:** גם אם הפלט מושלם; מכיוון שהתהליך לא חוויה ואינו מכיל רצון/סיכון, ערך [PoArt] מתקרב ל-$0$.

#### תרחיש B: ייצור פיזי של 6 שעות בשידור חי

- **זמן ($\Delta t$):** $6$ שעות ($21{,}600$ שניות)
- **עוצמת עבודה ($P_{\text{labor}}$):** $0.5$ יחידה (רציפות מאמץ פיזי ומנטלי)
- **מקדם רצון ($I_{\text{agency}}$):** $0.9$ (שינוי החלטות, לקיחת סיכונים, בחירות בלתי הפיכות)
- **בלתי הפיכות ($U_{\text{irreversible}}$):** $>0$ (עקבות פיזיים לא ניתנים לביטול)

**תוצאה:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **פרשנות:** ככל שהתהליך מתארך והרצון (סיכון) גדל, הערך גדל באופן מצטבר. מונח $U_{\text{irreversible}}$ הוא תרומה נוספת שיוצרת "ייחודיות" (אופי non-fungible) ביצירה.

---

### ✅ מסקנה: נעילת ערך עם הוכחה (Proof-Bound Value)

משפט זה ממיר את טענת הערך של [PoArt] מ"לייק" או "נרטיב שוק" ל**עובדת ייצור שניתנת להוכחה**.

1. **ללא תהליך אין ערך:**  
   AI הורס את התהליך בפלט מיידי ($t \to 0$). ככל שחלון התהליך מצטמצם, תוצאת האינטגרל קטנה כהכרח מתמטי:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **רצון וסיכון הם מכפילים:**  
   [PoArt] מודד לא רק "זמן שהושקע" אלא גם את שכבת ההחלטה, הסיכון והמחיר האמיתיים באותו זמן. ערך ייצור שלא לוקח סיכון (AI) נמוך:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **ייחודיות היא ראיה פיזית, לא שיווק:**  
   בייצור פיזי, עקבות בלתי הפיכים (מגע קנבס, סדק בשיש) נמצאים מחוץ ללוגיקת ה-`Ctrl+Z` הדיגיטלית. בלתי הפיכות זו ($U_{\text{irreversible}}$) הופכת את היצירה לייחודית באופן אונטולוגי.

> **🔐 סיכום:** גם אם משפט הערך נראה לא ודאי כמדידה (גם אם לא ניתן למדוד 100% התאמה בחיים האמיתיים), מטרת הנוסחה היא להראות את המבנה והכיוון של המשתנים. מה שנדיר בעידן ה-AI אינו "תמונה" אלא **עבודה, זמן ורצון שניתנים להוכחה**. [PoArt] מודד מחסור זה ורושם אותו עם **Evidence Pack**.

### 🏛️ חשיבות מושג "Engine" (מנוע)

טוקנים שיוצאים מ-Pump.fun או פלטפורמות דומות הם לעתים קרובות רק **"כרטיס כניסה"**. **PoArt Forensic Engine (PFE)** היא **שכבת הלוגיקה החוקתית** שקובעת אילו זכויות הכרטיס מגן, איך העבודה תירשם, ואיך אמנות/מדע/טכנולוגיה יונצחו.

> **הערה:** הסיבה שהתחלנו את הפרויקט הזה ב-Pump.fun היא שלא היו לנו מספיק נזילות ומספר עוקבים. שימוש בנתונים קיימים אולי לא היה האסטרטגיה האיכותית ביותר אבל היה הצעד הנכון ביותר. ללא קשר לתקציב ומשאבים, הגדרת הלוגיקה של מנוע זה ב-GitHub מוכיחה שהפרויקט אינו רק ספקולציה פיננסית אלא **תשתית תוכנה** לטווח ארוך וחזון של **ספרייה דיגיטלית לאומית**.

---

## 🎨 פרוטוקול [PoArt] הוכחת עבודה אמנותית (Proof of Art Protocol v1.0)

> **"אמן אמיתי, ייצור אמיתי, ערך אמיתי."**

פרוטוקול זה הוא **מנגנון הגנה ביולוגי ואינטלקטואלי** שפותח נגד הנוכלים האנונימיים שמציפים את אקוסיסטם הקריפטו, תמונות AI שנוצרות ב-5 דקות, ותרבות "Pump & Dump".

---

## א) מה זה [PoArt]? (הגדרה פילוסופית וטכנית)

**Proof of Art [PoArt];** הוא תקן אימות מוסדי שמבטיח שהערך מאחורי נכס בלוקצ'יין מובטח לא על ידי ספקולציה אלא על ידי **עבודה אנושית** ניתנת לאימות, **זמן** ו**אנרגיה פיזית**.

כמו שביטקוין יוצר ערך דרך *"חשמל וכוח עיבוד"* **(Proof of Work)**; פרויקטים תואמי [PoArt] יוצרים ערך דרך *"כישרון וזמן אנושי מושקע"*. זה "Stake" של זמן.

זה מסיר את הסיכון של *"המפתח (Dev) מכר, הפרויקט נגמר"* ב-Pump.fun ופלטפורמות DEX; כי כאן הערך אינו בקוד אלא ב**רציפות הייצור**.

> **[PoArt] לא אומר למשתתף "תסמכו עלינו"; הוא אומר "הנה הראיות, ראו בעיניכם, אמתו עם המתמטיקה שלכם."**

---

## ב) תקן 5 העמודים של [PoArt] (The 5 Pillars of Truth)

5 פריטים אלה הם מסננים בלתי ניתנים למניפולציה שפרויקט חייב לעבור כדי לקבל חותמת [PoArt].

### 1) הוכחת זהות חיה (Live Identity Proof)

- **בעיה:** עולם הקריפטו מלא במייסדים אנונימיים (Dev) שאוספים כסף ונוטשים את הפרויקט.
- **פתרון [PoArt]:** היוצר מוכיח לא רק תעודת זהות אלא גם **נוכחות ברגע הייצור**. זה כולל מפגשי שידור חי שבהם הם מתקשרים עם הקהילה וממלאים בקשות ספציפיות מיידיות, לא סרטונים שהוקלטו מראש.  
  (לדוגמה: *"כתוב את התאריך של היום ומספר הבלוק הנוכחי בפינה הימנית של הקנבס"*)
- **מוטו:** *"בוטים יכולים לצייר אבל בוטים לא מזיעים ולא מאלתרים."*

### 2) הוכחת עבודה ותהליך (Labor & Process Proof)

- **בעיה:** תמונות AI שנוצרות ב-2 שניות וציור שמן שנעשה ב-2 חודשים מקבלים יחס "jpeg" זהה בעולם הדיגיטלי.
- **פתרון [PoArt]:** תהליך "ההריון והלידה" של היצירה מתועד. שלבי סקיצה, שכבות צבע, שעות מצטברות, והתהליך הפיזי שהאמן חווה בעת יצירת העבודה מתועדים. זה מוסיף **"עלות זמן" (Time Cost)** לטוקן. ככל שקשה יותר לייצר נכס, כך ערכו יציב יותר.

### 3) הוכחת ערך אסתטי (Aesthetic Value Proof)

- **בעיה:** תרבות ה"מימ" מתעלמת מאסתטיקה ועומק אמנותי, מתמקדת רק בקומדיה מיידית, ויוצרת פרויקטי "הייפ" קצרי טווח.
- **פתרון [PoArt]:** הפרויקט חייב להיות בעל תקני אמנות אקדמיים, תורת צבע, חוקי קומפוזיציה, וידע בחומרים (Impasto, טקסטורה וכו'). התוכן לא צריך רק להצחיק; הוא צריך לעורר התפעלות אצל הצופה ולהיות בעל **ערך אספנות**.

### 4) חדשנות רעיונית (Conceptual Novelty)

- **בעיה:** אלפי מטבעות כלב/חתול שהם העתקים זה של זה, ללא יצירתיות.
- **פתרון [PoArt]:** הפרויקט חייב לבנות גשר חדש שמשלב אמנות, מדע, פילוסופיה או טכנולוגיה במבנה משמעותי.  
  (לדוגמה: שילוב פסל דוד הקלאסי עם נתוני שוק הקריפטו; עיבוד הרעיון של התפיסה האנושית "הופכת לאבן" והיכולת להוכיח זאת עם מקורות מדעיים.)  
  היצירה לא צריכה להיות רק חגיגה חזותית; היא צריכה להיות גם אתגר אינטלקטואלי שגורם לאנשים לחשוב על **מדע, פילוסופיה או טכנולוגיה**.

> [!IMPORTANT]
> **דוגמה לייחוס (אפקט Las Palmitas):**  
> בשכונת Las Palmitas במקסיקו שנאבקה בפשיעה, יותר מ-200 בתים הפכו לחגיגת קשת ענקית. לאחר התערבות אסתטית זו, שיעורי הפשיעה בשכונה ירדו במידה מסוימת, צעירים החלו להתעניין באמנות במקום בכנופיות. השינוי האסתטי תכנת מחדש את הכבוד של אנשים לסביבה שלהם ולזה לזה (לכידות חברתית).
>
> **ציפייה:** פרויקט שרוצה להיכנס לרשימת [PoArt] חייב להכיל קשר סיבה-תוצאה סוציולוגי, מדעי או פילוסופי מעבר לאסתטיקה חזותית טהורה, כמו בדוגמה לעיל. מכיוון ש"זמן" הוא הנכס היחיד שלא ניתן לקנות בכסף, בפרוטוקול זה זמן חייב להיות מושקע כבטוחה ומוכח. הבסיס הרעיוני של הפרויקט חייב להיות כל כך חזק ואוניברסלי שאפילו בתרחיש CTO (Community Take Over) אפשרי שנים לאחר מכן, הקהילה יכולה לירש מורשת זו ולהמשיך את הפוטנציאל החדשני של הפרויקט באופן אוטונומי.

### 5) רצון לא-אלגוריתמי (Non-Algorithmic Agency)

- **בעיה:** יצירות דיגיטליות מושלמות אבל חסרות נשמה, חוזרות על עצמן.
- **פתרון [PoArt]:** הרצון הייחודי של האדם שיכול לטעות, לקחת סיכונים ולחוות תנודות רגשיות חייב להיות מורגש ביצירה. אי-הוודאות במשיכות מכחול, תגובות בלתי צפויות של החומר, והחלטות מיידיות של האמן הם **חתימה ביולוגית** שמבדילה את היצירה מ"ייצור מכונה".

---

## ג) מנגנון אימות ואנטי-זיוף

מערכת זו מבטיחה שהפרויקט יישאר אמין וחי לא רק "בהתחלה" אלא "לנצח".

### 📦 חבילת ראיות (Evidence Pack - The Digital Twin)

מאחורי כל יצירה מאושרת [PoArt] יש חבילת נתונים מוצפנת וחתומת זמן שמשקיעים יכולים להוריד:

- **הקלטות וידאו RAW:** צילומי גלם ללא הפסקה של רגע הייצור.
- **ניתוח מטאדאטה:** תאריך יצירת הקובץ, מידע מכשיר ששימש, ונתוני מיקום (עיר-מדינה).
- **התייחסויות פיזיות:** ראיות שהיצירה קיימת בעולם הפיזי  
  (לדוגמה: עיתון נוכחי שמונח ליד היצירה או נתוני בלוקצ'יין מאותו רגע).

> *הערת עקביות:* המונח "חבילת ראיות" מתחבר לשרשרת **Evidence Pack → EvidenceRoot → NotarySeal** בסעיפים הקודמים; כלומר, שלמות החבילה מיוצגת על ידי חותמת ניתנת לאימות.

### 🔄 חידוש 365 ימים (The Sustainability Protocol)

- **תכונה מהפכנית:** בפרויקטי קריפטו, "Dev" (מפתח) משחרר את הטוקן לשוק ובדרך כלל נעלם אחרי 1-2 חודשים (Soft Rug). [PoArt] הופך את זה לבלתי אפשרי.
- **כלל:** סטטוס "Verified Artist" (אמן מאומת) אינו קבוע. הוא תקף רק **שנה אחת**.
- **תפעול:** האמן/מפתח חייב להציג לקהילה **יצירה חדשה, גדולה וניתנת להוכחה** כל 365 ימים.
- **תרחיש לדוגמה:** התחלתם פרויקט ב-2026. בינואר 2027, המערכת נותנת אזהרת "תקופת ההוכחה פגה". אם האמן לא מציג תערוכה חדשה, יצירה פיזית חדשה או אינטגרציה טכנולוגית חדשה, "תג האמון" של הפרויקט יורד.
- **תוצאה:** מערכת זו מבטיחה ש**תוכן לעולם לא יהפוך מיושן** ומשקיעים לא יחוו את הפחד *"האם המפתח עדיין כאן?"*. הפרויקט הופך לסטודיו חי.

### 🚩 פרוטוקול דגל אדום (Red Flag Protocol)

**אם זיוף כלשהו (שימוש ב-AI, יצירה גנובה, וידאו ממופלל) מזוהה על ידי הקהילה או אלגוריתמים:**

1. התעודה מסומנת מיד כ**"בטל" (VOID)**.
2. חבילות הראיות מתוייגות בפומבי כ**"מזויף"**.
3. הפרויקט נכנס לרשימה השחורה של [PoArt]. זה מחזק את העובדה שבעולם מבוזר, **מוניטין הוא המטבע היחיד**.
4. אין לכלול ביטויי [PoArt] בשום פרסום; המקור התקף היחיד הוא https://www.ilhanart.org/public-registry

---

## ד) מסקנה: לא קזינו, אלא מוזיאון

**Pump.fun ובורסות מבוזרות (DEX) כרגע לצערנו הם קזינו; אורות מהבהבים, כולם רודפים אחרי רווח מהיר, והקזינו (הנוכלים) תמיד מנצח. הסיבה שהתחלנו את הפרויקט כאן היא גם כדי לנסות לשפר את המקום הזה, וכי יש לנו נתונים קיימים וסביבה להגיע לקהל קיים דרך שידורים חיים.**

**[PoArt] היא מבצר שנבנה באמצע הקזינו הזה.**

- 🎰 קזינו מסתמך על משחקי קלפים; אנחנו מסתמכים על **מציאות פיזית**.
- 🃏 קזינו פתוח לרמאות; אנחנו פתוחים ל**ראיות שקופות**.
- ⏳ קזינו הוא זמני; אנחנו מתמקדים ב**נצחיות של אמנות ומדע**.

**טוקן שמשתמש בפרוטוקול זה אינו רק "מטבע"; הוא מניה דיגיטלית שמכילה זיעה, צבע, קוד ופילוסופיה מאחוריה.**

---

## 🗳️ 6) ממשל ורישום ציבורי (Governance & Public Registry)

**מטרת סעיף זה: להמיר את תקן [PoArt] ממישור של "אמון באנשים" לתשתית ציבורית בת-קיימא עם רישום + אימות + פיקוח קהילתי.**

### 6.1 Public Registry (רישום ציבורי)

- **Public Registry:** כל הנתונים המאושרים נרשמים ב-`ilhanart.org/registry` (או GitHub Registry).

**לוגיקת רישום (תקן מומלץ - בפורמט נתיב JSON):**

כל רשומה שנכנסת לרישום נושאת לפחות את שדות הליבה הניתנים לאימות הבאים:

- **זהות וסטטוס:**
  - `certificate_id` (הפניה קריאה)
  - `status` (active / void)
  - `void_reason` (אם קיים)
  - `visibility` (private / masked / public)
  - `created_at` (חותמת זמן)

- **מוסד מנפיק:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **מידע על היצירה:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (אם אפשר; לזיהוי מחזיק טוקן)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **נתונים פורנזיים:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **הוכחות קריפטוגרפיות:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **ממשל:**
  - `governance.decision`
  - `governance.review_notes`

הרישום יכול להכיל שתי שכבות:
- **1)** אינדקס קריא לאדם (רשימת ווב / חיפוש / סינון)
- **2)** מניפסט קריא למכונה (רשומות JSON; לאימות PFE)

**ה"רשומה" כאן ניתנת לאימות עם שרשרת Evidence Pack → EvidenceRoot → NotarySeal של PFE. הרישום מספק יעד אימות, לא "טענה".**

---

### 6.2 תהליך בקשת PoArt Verified

**בקשות PoArt Verified מוערכות על ידי גלריית İlhanArt לפי 5 תקני PoArt. משוב קהילתי נלקח בחשבון, אבל ההחלטה הסופית תלויה בצוות האוצרות. החלטות מוכרזות בשקיפות ונרשמות ב-ilhanart.org/registry.**

#### תהליך הבקשה

**בקשה:**
- אמן/פרויקט מגיש בקשת PoArt Verified
- Evidence Pack מוכן (הקלטות וידאו, מטאדאטה, קישורי שידור חי)
- הבקשה נשלחת לגלריית İlhanArt

**בדיקה (30 ימים):**
- צוות הגלריה בודק את ה-Evidence Pack לפרטים
- כל 5 תקני PoArt נבדקים:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- ראיון עם האמן (אופציונלי)

**ייעוץ קהילתי:**
- Evidence Pack משותף בפומבי במהלך תהליך הבקשה
- הקהילה יכולה לספק משוב דרך ilhanart.org
- מחזיקי טוקן (מינימום 10,000 $CULTURE) יכולים במיוחד להציע הצעות
- **כל המשוב נלקח בחשבון בתהליך הבדיקה**
- **עם זאת, ההחלטה הסופית תלויה בהערכה אוצרותית**

**החלטה:**
- הגלריה מאשרת או דוחה את הבקשה
- סיבת ההחלטה מוכרזת בשקיפות
- אם מאושר → תג PoArt Verified
- אם נדחה → ניתן להגיש מחדש אחרי 6 חודשים

**שקיפות:**
- כל הבקשות וההחלטות נרשמות ב-ilhanart.org/registry
- רשומת החלטה מתפרסמת בפומבי:
  - תאריך בקשה
  - סיכום תהליך הבדיקה
  - החלטה (Approved / Rejected)
  - סיבת ההחלטה (הסבר קצר)
  - סיכום משוב קהילתי (אנונימי)

#### למה החלטה אוצרותית?

**בקרת איכות:**  
סטטוס PoArt Verified הוא תג עם תקנים גבוהים. הערכה אוצרותית מבטיחה שתקנים אלה יישמרו.

**מניעת מניפולציה ספקולטיבית:**  
ממשל on-chain מלא (למשל: Realms, הצבעת DAO) אינו אפשרי טכנית עם טוקני Pump.fun. מערכות הצבעה off-chain פגיעות למניפולציית לוויתנים והתקפות מתואמות. החלטה אוצרותית מבטלת סיכון זה.

**יעילות תפעולית:**  
תהליך החלטה מהיר וברור במקום מנגנוני הצבעה מורכבים. אמנים מקבלים תוצאות תוך 30 יום.

**השתתפות קהילתית:**  
משוב קהילתי נלקח בחשבון לחלוטין ומשפיע על תהליך ההחלטה. עם זאת, ההחלטה הסופית תלויה בצוות האוצרות המוגן ממניפולציה.

**עתיד:**  
כאשר הפרויקט מתבגר (2027+), מנגנון הייעוץ הקהילתי יכול להתחזק. עם זאת, הגנת התקן האוצרותי היא קבועה.

---

### 6.3 תועלת טוקן (Token Utility)

**יתרונות שניתנים למחזיקי טוקן $CULTURE:**

**1. גישה מועדפת לאירועי גלריה:**
- זכות לקיים תערוכה של שבוע בשנה בגלריית İlhanArt (הזכות ניתנת להעברה)
- הנחות Drop painting
- זכות הנחה של 10% עד 30% על ציורים בגלריה

**2. גישה מלאה לרישום PoArt:**
- רשומות מפורטות של כל היצירות המאומתות
- גרסאות מלאות של Evidence Pack
- כלי אימות פורנזי


**3. הצבעה ייעוצית:**
- זכות ייעוץ בבקשות PoArt Verified
- גישה לערוצי משוב קהילתיים
- השתתפות בדיוני ממשל

**4. תוכן בלעדי:**
- תוכן מאחורי הקלעים מהסטודיו
- ראיונות אמנים וסרטוני תהליך
- גישה לתיעוד טכני

**הערה:**  
מחזיקי טוקן נותנים advisory vote (הצבעה ייעוצית). ההחלטה הסופית שייכת לצוות האוצרות. מבנה זה נבחר כדי למנוע מניפולציית לוויתנים והתקפות ספקולטיביות. אין תגמול staking כי אנחנו מחפשים משתתפים תרבותיים לטווח ארוך, לא הון שכיר לטווח קצר.

---

### 6.4 סנכרון מטאדאטה (Metadata Sync)

- **Metadata Sync:** הנתונים הטכניים ברישום חייבים להתאים 100% לנכס הפיזי.

**הגדרה טכנית של "התאמה של 100%" (בהירות מומלצת):**

- **התאמה מינימלית (חובה):**
  - `asset.fingerprints.sha256/sha512` ברישום חייב להיות **זהה לחלוטין** ל-hash של הקובץ שביד.
  - `proof.notary_seal` ברישום כשנוצר מחדש (אם Evidence Pack קיים) חייב להיות **זהה לחלוטין**.

- **התאמת הפניה פיזית (סוג ראיה):**
  - ראיות כמו יצירה פיזית שהוצגה בשידור חי + הפניית תאריך/בלוק חייבות להיות עקביות עם Evidence Pack.

- **תאימות פרטיות:**
  - שדות כמו IP/מיקום בנראות `masked` מתפרסמים **בהתאם לתקן המיסוך**.

---

### 6.5 ערעור, בדיקה וביטול (Dispute & Revocation)

הרישום אינו רק מנגנון "אישור"; הוא **מנגנון פיקוח חי נגד זיוף**.

- כאשר ערעור מתחיל, הרשומה יכולה להיכנס למצב **"review"**.
- אם זיוף מזוהה, הוא מסומן כ-`status: void` והסיבה מתווספת:
  - `void_reason` (שימוש ב-AI / גנוב / מניפולציה וכו')
  - `revoked_at` (זמן ביטול)
- מקור החלטת הביטול נראה בבירור ברישום:
  - בדיקה אוצרותית / ערעור קהילתי / הערת ניתוח פורנזי (מה שרלוונטי)

> **חלק זה הוא המקבילה ברישום של מושג VOID בסעיף "Red Flag Protocol".**

---

### 6.6 דוגמה לרשומת רישום (קריאה למכונה)
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

> *הערה: `asset.fingerprints.sha512` וערכי hash אחרים קוצרו למטרות הצגה; ביישום אמיתי משתמשים במחרוזת תווים הקסדצימלית באורך מלא.*

---

## 7) 🔐 חותמת טכנית (NOTARY SEAL)

**אלגוריתם החותמת הבלתי ניתנת לערעור שנוצר על ידי PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# פרוטוקול [PoArt] נוטריון דיגיטלי וראיות פורנזיות (Beta v1.0)

> **"תרבות גדולה מהון. הגנו על יצירותיכם מהיום, קחו אותן למחר."**

---

## למה פתוח לציבור?

אבטחה אמיתית מגיעה משקיפות. בזכות מערכת **Public Registry (רישום ציבורי)** שלנו, כל אחד בכל מקום בעולם יכול לאמת תוך שניות האם הקובץ שבידיו הוא מקורי או לא, ללא צורך בשום סמכות.

---

## 🧩 למה יש מספר "מודולי נראות"?

זהו החלק הקריטי ביותר של הקוד (תפריט בחירת visibility). אפשרויות אלה מאפשרות למשתמשים לאזן **"פרטיות מול שקיפות"**:

### 🔒 פרטי (Private)

- **תרחיש:** האמן עדיין לא רוצה לפרסם את היצירה אבל רוצה לחתום תאריך כדי להוכיח "עשיתי את זה בתאריך הזה".
- **מה הקוד עושה:** כותב את הנתונים למסד הנתונים אבל מדביק תווית `visibility: "private"`. מאוחר יותר כשכותבים מדיניות "Public Read", אפשר להסתיר רשומות אלה מהציבור עם `WHERE visibility = 'public'`.

### 🕶️ מוסווה (Masked)

- **תרחיש:** האמן רוצה שקיפות אבל מפחד שימצאו את כתובת הבית שלו (מיקום IP).
- **מה הקוד עושה:** בצד JavaScript פועלות פונקציות `maskIP` ו-`maskLoc`. ממירות את כתובת ה-IP לפורמט `88.241.***.***`, מיקום לפורמט `***/TR` ושולחות את הגרסה המצונזרת למסד הנתונים.
- **הערת פרטיות:** ההסוואה נעשית בדפדפן, Supabase לא רואה את המיקום האמיתי. **עם זאת:** אם נעשה שימוש ב-API של צד שלישי כמו ipapi.co לנתוני מיקום, ספקים אלה רואים את כתובת ה-IP ברגע הבקשה.
- **חתימה במצב Masked:** חישוב EvidenceRoot ו-NotarySeal נעשה עם נתוני forensics מוסווים; כך האימות נשאר דטרמיניסטי.

### 🌍 ציבורי (Public)

- **תרחיש:** שקיפות מלאה. לפי תקן [PoArt], איפה, מתי, ומאיזו רשת היצירה נוצרה מוצהר בגלוי.

---

## 💡 חדשנות טכנולוגית

PoArt אינו רק מערכת העלאת קבצים. הוא מנוע **"שרשרת משמורת ראיות פורנזיות" (Forensic Chain of Custody)** שמביא תקן חדש על ידי מיזוג שלוש שכבות טכנולוגיה שונות בכור היתוך אחד.

**השכבה שמתוארת כ"מנוע" בסעיף זה מתאימה לליבת PoArt Forensic Engine (PFE) מהמונחים הקודמים.**

### 1) Client-Side Hashing (פרטיות מקסימלית)

קבצי היצירה שלכם לעולם לא מועלים לשרת. המנוע מבוסס הדפדפן (Client-side) שלנו מחשב את ה-hash (סיכום דיגיטלי) של הקובץ במחשב שלכם. רק טביעת אצבע זו ומטאדאטה נשלחים לשרת.

> **הערת פרטיות:** קובץ היצירה לא מועלה לשרת ומוגן בדרך זו. עם זאת, נתוני forensics (IP/מיקום) משותפים בהתאם למצב הנראות שנבחר (private/masked/public).

### 2) Forensic Data Fusion (כוח פורנזי)

זה הרבה יותר מחותמת זמן (Timestamp) רגילה. המערכת משלבת את הנתונים הבאים ב"חותמת Genesis" אחת:

- **סיכום דיגיטלי (SHA-512):** טביעת אצבע דיגיטלית שתישבר אם אפילו פיקסל אחד של היצירה משתנה, באמצעות תקן סיכום קריפטוגרפי (SHA-512).
- **מיקום וזמן:** תאריך בדיוק של מילישניות כאשר העסקה בוצעה, נתוני מדינה, עיר ואזור.
- **זהות מכשיר:** מערכת הפעלה, דפדפן וסוג מכשיר (ניתוח User-Agent).

---

## 🛡️ מקרי שימוש ויתרון

אם אתם אמן, כותב או מעצב, לומר "עשיתי את זה קודם" לא מספיק, אתם צריכים להוכיח.

**יצירה שנחתמה עם PoArt:**

- **הוכחה מתמטית:** המערכת מזהה אם אפילו פיקסל אחד של הקובץ שלכם משתנה. מניפולציה בלתי אפשרית.
- **בסיס משפטי:** באיזה תאריך, באיזו עיר, מאיזה מכשיר היצירה נחתמה - הכל נרשם.
- **תעודה מיידית:** מייצר **"תעודת זהות נכס"** ייחודית לכם עם קוד QR וחותמת תוך שניות.

---

## ⚙️ ארכיטקטורת מערכת ומפרט טכני

המערכת מעוצבת על ארכיטקטורה "Serverless", ממוקדת בביצועים גבוהים ויכולת הרחבה.

| שכבה | טכנולוגיה | תיאור |
|------|-----------|-------|
| **קריפטוגרפיה** | SHA-256 & SHA-512 | סיכום קריפטוגרפי דו-שכבתי |
| **מסד נתונים** | Supabase (PostgreSQL) | מבנה נתוני JSONB, מדיניות RLS |
| **נתונים פורנזיים** | ipapi.co API | משולש IP/מיקום/זמן |
| **עיבוד** | html2canvas + jsPDF | ייצור PNG/PDF בצד לקוח |
| **Frontend** | Vanilla JavaScript | ללא תלות ב-framework |
| **אבטחה** | Client-side hashing | הקובץ לעולם לא מועלה לשרת |

### תכונות בולטות

| תכונה | פרט | אצל מתחרים? |
|--------|------|-------------|
| **Drag & Drop UI** | גרור ושחרר קובץ, תצוגה מקדימה מיידית | ❌ רוב אין |
| **Multi-Format Export** | PNG, JSON, PDF - בלחיצה אחת | ⚠️ מוגבל |
| **Real-Time Preview** | תצוגה מקדימה חיה של תעודה | ❌ אין |
| **Privacy Controls** | אפשרויות Private/Masked/Public | ❌ אין |
| **Client-Side Hashing** | הקובץ לעולם לא הולך לשרת | ✅ רק בכמה |
| **Forensic Metadata** | IP, מיקום, מכשיר, זמן - הכל ביחד | ❌ חלקי |
| **QR Verification** | קוד QR לאימות מיידי | ⚠️ מוגבל |
| **Rate Limiting** | הגנה מספאם (RLS + Client) | ❌ רוב אין |

---

## 🗺️ מפת דרכים: עתיד "Trustless"

הגרסה הנוכחית **(Beta v1.0)** מותאמת לספק למשתמש הקצה מהירות מקסימלית, ממשק קל וגישה חינמית. עם זאת, החזון הסופי שלנו הוא לעבור למבנה שבו אפילו מנהל מסד הנתונים (אנחנו) לא יכול להתערב.

### שלב 1: Beta v1.0 (כעת פעיל)

**תשתית:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + IPFS backup)
- Gallery self-attestation (מרכזי אבל שקוף)

**טוקן:**
- Platform: Pump.fun
- Liquidity: Raydium (automatic)
- Governance: Advisory only (ייעוץ קהילתי)

**מטרה:**
- מהירות, הסרת מחסומי UX
- לספק אבטחה "ללא חיכוך"
- בניית קהילה

**Token Utility (v1.0):**
- גישה מועדפת לאירועי גלריה
- צפייה ברישום PoArt
- זכות הצבעה ייעוצית

---

### 🚀 שלב 2: Decentralized Authority (2026 Q2-Q4)

שלב זה מכסה את המעבר מהמבנה שעובד לגמרי "Client-Side" למבנה מאובטח ומבוזר יותר.

| תכונה | מה מרוויחים? | Tech Stack | ETA |
|--------|-------------|------------|-----|
| **Edge Function INSERT** | חסימת ספאם + אבטחת API Key | Supabase Edge (Deno) | Q2 2026 |
| **Wallet Signature** | זהות מבוזרת | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | ארכיון מבוזר | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | ביטול תעודות מזויפות | DB Schema Update | Q2 2026 |
| **Audit Log** | רישום שאילתות פורנזיות | טבלת logs מותאמת | Q3 2026 |
| **OpenTimestamps** | עיגון ביטקוין | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain voting (x/web) + wallet signature
- בחירת נציגי קהילה (90 יום ראשונים)
- שליטה על ארנק פעולות Multi-sig
- הצבעה ייעוצית משוקללת (עם whale cap)

**Immutability:**
- גיבוי רישום עם hash-ים של IPFS
- עיגון חותמת זמן ביטקוין
- הכנה לאימות cross-chain

---

### שלב 3: ביזור מלא (2027+)

| תכונה | יעד | ETA |
|--------|-----|-----|
| **On-Chain Registry** | רישום on-chain של Solana | Q1 2027 |
| **Enhanced Token Utility** | NFT mint, תכונות מתקדמות | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **DID Integration** | זהות מבוזרת | Q3 2027 |
| **Community Governance** | מערכת ייעוץ מחוזקת | Q4 2027 |
| **Legal Recognition** | תוקף בבתי משפט טורקיים | 2027-2028 |
| **API for Developers** | Public API endpoint | Q3 2027 |

**Governance Evolution:**
- v3.0: מודל היברידי (אוצרותי + community weighted)
- 2028+: Full community governance (אופציונלי)
- בקרת איכות אוצרותית תמיד נשמרת

---

## 🧬 מבנה נתוני פרוטוקול (JSON Schema)

**לכל תעודת [PoArt] יש כרטיס זהות JSON נייד וניתן לאימות שנוצר לפי התקן הבא.**

> **הערה:** פורמט Identity JSON זה הוא פורמט התעודה שמוצג למשתמש. ברשומות רישום, `registry.asset` משמש במקום `identity.asset_data` (מיפוי: `identity.asset_data` == `registry.asset`).
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

## 🔬 עומק טכני: אלגוריתם חתימה

### פונקציות Hash דטרמיניסטיות
```javascript
// פונקציות עזר: המרת Digest למחרוזת hex
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// המרת String למערך בייטים
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// ייצור מחרוזת forensics קנונית (v1.0: סדר שדות קבוע + UTF-8 + מפריד \n)
// הערת שלב 2: מעבר ל-canonical JSON עם RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### תהליך ייצור NotarySeal (דטרמיניסטי לחלוטין)
```javascript
// 1. חישוב FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. איסוף נתוני Forensic (שימוש ב-timestamp יחיד)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // ייצור timestamp יחיד
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // אותו timestamp
  };
  
  return { forensics, timestamp };
}

// 3. יצירת EvidenceRoot (עם canonical encoding)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. ייצור NotarySeal (שימוש באותו timestamp)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// פונקציות עזר להסוואה (תמיכה ב-IPv4 ו-IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // בדיקת IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 או פורמט לא ידוע
  return "***";
}
```

### זרימת אימות (שני רמות)

#### Quick Verify (אימות מהיר)
```javascript
// בודק רק hash של קובץ (דגל אדום מהיר)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // משיכה מהרישום
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // השוואת Hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ מקורי - Hash הקובץ תואם"
    };
  } else {
    return {
      valid: false,
      message: "❌ מזויף - הקובץ עבר מניפולציה"
    };
  }
}
```

#### Full Verify (אימות מלא)
```javascript
// יוצר מחדש EvidenceRoot ו-NotarySeal ומאמת
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // משיכה מהרישום
  const cert = await fetchFromRegistry(certificateId);

  // 1) בדיקת FileHash (דגל אדום מהיר)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ מזויף - Hash הקובץ לא תואם" };
  }

  // 2) יצירה מחדש של EvidenceRoot (עם forensics שנשמר ברישום)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ לא תואם - EvidenceRoot לא מתאים" };
  }

  // 3) יצירה מחדש של NotarySeal (עם אותו timestamp + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ לא תואם - NotarySeal לא מתאים" };
  }

  // אופציונלי: בשלב 2 לאמת גם signer_sig עם attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ חתימה לא תקפה" };

  return { valid: true, message: "✅ מקורי - Full Verify עבר" };
}
```

> **הערות חשובות:**
> - **Quick Verify:** בודק רק hash של קובץ לשימוש מהיר.
> - **Full Verify:** מאמת את כל שכבות הפרוטוקול (EvidenceRoot + NotarySeal).
> - כל פעולות ה-hash מבוצעות באופן דטרמיניסטי עם encoding ומפרידים קבועים.
> - **תקן canonicalization v1.0:** סדר שדות קבוע + encoding UTF-8 + מפריד `\n`.
> - **תוכנית שלב 2:** מעבר ל-canonical JSON עם RFC 8785 (JCS - JSON Canonicalization Scheme).
> - במצב Masked, חישוב EvidenceRoot ו-NotarySeal נעשה עם forensics מוסווה.
> - timestamp יחיד משמש בכל התהליך (forensics + NotarySeal); דטרמיניזם מובטח.
> - **שמות שדות Forensics:** `ip_masked`, `location`, `device`, `timestamp` (קוד ורישום תואמים לחלוטין).
> - **נתיב רישום:** `certificate.asset.fingerprints` (תואם לחלוטין לקוד verify).
> - **signer_sig ברישום:** שדה `proof.signer_sig` נדרש ל-Full Verify.
> - מנגנון SignerSignature יופעל בשלב 2 עם Solana Wallet Adapter; ב-v1.0 ניתן לאמת עם `attestation_pubkey`.

---

## 📊 ניתוח מתחרים (מעודכן)

PoArt ממוקם ב"Sweet Spot" שמשלים את החסרונות של פתרונות קיימים.

| תכונה | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|-------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **עלות** | 🆓 חינם | 🆓 | 💰 בתשלום | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ קל מאוד | ❌ CLI | ⚠️ בינוני | ⚠️ בינוני | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ חי | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 מצבים | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ פרטיות | ✅ | ❌ העלאה | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ מלא | ❌ | ❌ | ⚠️ מוגבל | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ מיידי | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **תמיכה בטורקית** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**הסבר:**
- ✅ : תמיכה מלאה / קיים
- ⚠️ : מוגבל / בתוכניות בתשלום
- ❌ : אין / לא נתמך
- 🔄 : ב-Roadmap (בפיתוח)
- 🆓 : חינם לחלוטין
- 💰 : בתשלום / נדרש מנוי

### חסרונות מתחרים, חוזקות PoArt

| חיסרון | מתחרים | PoArt |
|--------|--------|-------|
| **קושי בשימוש** | CLI, נדרש ידע API, ארנק | גרור ושחרר, מסתיים ב-3 לחיצות |
| **מחסום עלות** | מנוי $50-500/חודש | 100% חינם |
| **פרטיות** | קובץ מועלה לשרת | Client-side, קובץ אף פעם לא הולך |
| **נתונים פורנזיים** | רק timestamp | IP, מיקום, מכשיר, זמן - הכל |
| **תמיכה בטורקית** | אין או מוגבל מאוד | תמיכת שפה Native |
| **קוד פתוח** | קופסה שחורה | כל הקוד פתוח ב-GitHub |

---

## 📈 סטטיסטיקות שימוש (יעדי Q1 2026)

| מדד | יעד | סטטוס |
|------|-----|-------|
| **סה"כ תעודות** | 1,000 | 🔄 בתהליך |
| **משתמשים פעילים** | 500 | 🔄 בתהליך |
| **מספר אימותים** | 5,000 | 🔄 בתהליך |
| **Uptime** | %99.9 | ✅ פעיל |
| **Avg Response Time** | <200ms | ✅ אופטימלי |

---

## 🌍 קהילה ותמיכה

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 תורמים

פרוטוקול PoArt ממשיך להתפתח עם תרומות קהילת הקוד הפתוח.

**כדי לתרום:**
1. עשו Fork
2. צרו feature branch (`git checkout -b feature/amazing-feature`)
3. עשו Commit (`git commit -m 'Add amazing feature'`)
4. עשו Push (`git push origin feature/amazing-feature`)
5. פתחו Pull Request

### 🛠️ מה אנחנו צריכים עכשיו? (קריאה לעזרה)

פרוטוקול PoArt מחכה לתרומות של מפתחים מנוסים בתחומים הבאים לפיתוחי **שלב 2**:

* **Supabase Edge Functions:** העברת הגנת ספאם לצד השרת.
* **Solana Web3.js:** אינטגרציית Wallet Signing.
* **IPFS / Arweave:** אינטגרציית שירותי ארכיון ו-pinning.
* **Community Tools:** הצבעת X, מערכות voting, לוח analytics.

> אנא התחילו דיון בכרטיסיית "Issues" לפני הוספת תכונה.

---

## 💬 הערות אחרונות

### Pump.fun והמציאות

הפרויקט הזה הושק ב-Pump.fun כי:
- ✅ גישה לנזילות (Raydium automatic migration)
- ✅ גישה לקהילה קיימת
- ✅ עלות התחלה נמוכה

עם זאת, בואו נבהיר:
- **מחיר הטוקן** אינו מדד להצלחה אמנותית
- **תקציב תפעולי** דורש ערך טוקן (גלריה, תערוכות, תשתית)
- **מדדי הצלחה:** Authenticated artworks + community engagement + מבקרים פיזיים

### ממשל וביזור

**מציאות v1.0 (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (מרכזי אבל שקוף)
- Governance: Advisory only (החלטה סופית אוצרותית)
- Token utility: Gallery access + registry + NFT priority

**חזון v2.0+ (2027+):**
- Registry: On-chain (Solana)
- Signatures: Wallet-based (מבוזר)
- Governance: Hybrid (community advisory + curatorial quality)
- Token utility: Enhanced features + advanced access

מבנה זה מספק **יעילות תפעולית** ו**בקרת איכות** בשלב מוקדם, תוך שמירה על הנתיב הפתוח להגברת **השתתפות קהילתית** בעתיד.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // תרבות גדולה מהון*

## 🧾 רישיון

MIT License © 2026 İlhan Art Gallery Initiative

ראו [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) לתנאים מלאים.

---

## 💬 קרדיטים

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**פרויקט זה פותח עם יוזמת [İlhan Art Gallery], קוד המקור פתוח לציבור למען שקיפות.**

**PROTOCOL V1.0 // חתום עם SHA-512.**

*© 2026 İLHAN ART | כל הזכויות ליצירות, לתמונות ולרעיונות שמורות.*

---
