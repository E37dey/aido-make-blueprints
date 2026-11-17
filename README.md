# Make Blueprints - שיעור 5

תרחישי Make שבניתי, מיוצאים כ-Blueprint (JSON) שאפשר לייבא לכל חשבון Make.

## ai-lead-qualifier.blueprint.json (המשימה הראשית)
סוכן שמסנן ומדרג פניות לקוחות שמגיעות מטופס באתר.

1. Webhook: מקבל את הפנייה מהטופס (name, email, company, phone, source, message).
2. Data store: בודק אם השולח כבר פנה בעבר (מפתח: המייל).
3. Claude (Haiku 5.5): מנתח את הפנייה ומחזיר JSON: ספאם או לא, איזה שירות, ציון ליד 0-100, רמה (hot / warm / cold), דחיפות, שפה, תקציר בעברית, הפעולה הבאה, וטיוטת תשובה אישית בשפת הלקוח.
4. Parse JSON: הופך את התשובה לשדות.
5. Router עם 3 מסלולים:
   - כל פנייה שאינה ספאם: שורה בגיליון Leads CRM, ושמירת השולח ב-Data store.
   - ליד עם ציון 40 ומעלה: טיוטת תשובה ב-Gmail. לא נשלחת אוטומטית, רק טיוטה לאישור.
   - תשובה לטופס: JSON עם הרמה של הליד.

נבדק בריצה אמיתית ב-17.11.2026: 8 מודולים, בלי שגיאות, כ-7 שניות, כ-8.5 credits לפנייה.
דוגמת פנייה לבדיקה: `samples/lead-example.json`.

## job-replies-tracker.blueprint.json (3 רכיבים)
1. Gmail - Watch emails: מיילים מתוויות חיפוש העבודה, סינון ראשוני לפי מילות מפתח.
2. Claude: מסווג כל מייל: דחייה, צעד הבא, אישור קבלה, אחר.
3. Google Sheets: כותב תאריך, שולח, נושא, תקציר, קישור למייל והסיווג. Filter מדלג על "אישור קבלה".

## invoices-log.blueprint.json
Gmail (מיילים עם חשבונית / קבלה / invoice) ל-Google Sheets. יומן חשבוניות פשוט.

## ייבוא
Make > Create a new scenario > תפריט שלוש הנקודות > Import Blueprint > לבחור את הקובץ.
אחרי הייבוא:
- לחבר Connection של Gmail ושל Google.
- לבחור Spreadsheet משלכם (במקום `<YOUR_SPREADSHEET_ID>`).
- ב-AI Lead Qualifier: ליצור Webhook חדש במודול הראשון, ליצור Data store עם השדות name, lead_score, tier, last_seen, ולבחור Data structure במודול Parse JSON (או להריץ פעם אחת כדי ש-Make ילמד את המבנה).

מודול Claude לא צריך Connection נפרד בחשבון Make.
מזהי Connection, Webhook, Data store וגיליונות אישיים הוסרו מהקבצים.
