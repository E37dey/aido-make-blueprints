# Make Blueprints - שיעור 5

תרחישי Make שבניתי, מיוצאים כ-Blueprint (JSON) שאפשר לייבא לכל חשבון Make.

## job-replies-tracker.blueprint.json (המשימה הראשית, 3 רכיבים)
1. Gmail - Watch emails: אוסף מיילים מתיוויות חיפוש העבודה, מסנן מראש לפי מילות מפתח של דחייה / המשך תהליך.
2. Anthropic Claude - Simple text prompt: מסווג כל מייל לאחת מארבע תוויות: דחייה, צעד הבא, אישור קבלה, אחר.
3. Google Sheets - Add a row: כותב תאריך, שולח, נושא, תקציר, קישור למייל והסיווג. Filter בדרך מדלג על "אישור קבלה".

רץ כל שעתיים (Free plan).

## invoices-log.blueprint.json
Gmail (מיילים עם חשבונית / קבלה / invoice) ל-Google Sheets. 2 רכיבים, יומן חשבוניות פשוט.

## ייבוא
Make > Create a new scenario > תפריט שלוש הנקודות > Import Blueprint > לבחור את הקובץ.
אחרי הייבוא: לחבר Connection של Gmail ושל Google, ולבחור Spreadsheet משלכם (במקום `<YOUR_SPREADSHEET_ID>`).
מודול Claude לא צריך Connection נפרד בחשבון Make.

מזהי Connection ומזהי הגיליונות האישיים הוסרו מהקבצים.
