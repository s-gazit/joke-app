# תוכנית Milestone 1: Walking Skeleton

## מטרה
הדף והפונקציה באוויר ב-Vercel, באותה כתובת, ומדברים זה עם זה. עוד בלי AI. המפתח נשמר ב-Vercel, והפונקציה רק מדווחת "נמצא" או "חסר".

## בדיקת מצב קיים (בוצעה)
- קיימים ומתועדים בגיט: `.gitignore` (עם `.env`, `.env.*`, `!.env.example`, `.vercel`, `node_modules`), `.env.example`, `.claude/settings.json` (חוסם קריאת `.env` ו-`.env.*`).
- קיימים ב-`assets/`: logo, ארבעת הציורים של הדמות, bg-dots, bg-doodles, האייקונים.
- חסרים: `index.html`, `api/joke.js`, `package.json`.

## קבצים לבנייה
1. `package.json`: `{ "type": "module" }`, בלי dependencies.
2. `api/joke.js`:
   - `export default { async fetch(request) { ... } }`.
   - לא POST: 405 עם `{ "error": "..." }` בעברית.
   - POST: קורא `topic` מהגוף (גוף שבור או ריק = ריק), חותך ל-100 תווים.
   - מחזיר 200 עם `{ "joke": "בדיחה זמנית מהשרת: [הנושא]. המפתח: נמצא" }`, או "המפתח: חסר" כש-`process.env.OPENAI_API_KEY` ריק. אף פעם לא את המפתח עצמו.
   - `console.log` קצר לכל לחיצה (הנושא), כדי שיופיע ב-Logs של Vercel.
   - בלי כותרות CORS ובלי טיפול ב-OPTIONS.
3. `index.html` (CSS ו-JS בתוכו, `lang="he"`, `dir="rtl"`):
   - מבנה לפי DESIGN.md: לוגו (300), שורת הסבר, תווית "על מה הבדיחה?", תיבה (maxlength 100, "למשל: חתולים"), כפתור "תנו לי בדיחה!", בועה עם הדמות, שורה תחתונה "מיישם AI ואוטומציה · 53500".
   - סגנון: צבעים, גופנים (Fredoka ו-Playpen Sans Hebrew מ-Google Fonts, גיבוי system-ui), גלולה אדומה עם צל קשה, תיבה ובועה מסובבות, רקע bg-dots וקישוט bg-doodles, מרווחים ורוחב מקסימלי 440.
   - הבועה עם `data-state`: idle, think, joke, error, כל אחד עם הציור שלו. ב-Milestone 1 פעילים idle, think ו-joke (מצב שגיאה בסיסי אם הבקשה נכשלת). ההשלמה המלאה של ארבעת המצבים והאנימציות היא ב-Milestone 2, אבל נכין כבר את הבסיס.
   - שליחה: POST ל-`/api/joke` עם `{ "topic": ... }`, והצגת `joke` ב-`textContent`. אזור הבדיחה עם `aria-live`.
   - אנימציות לפי DESIGN.md, עם `prefers-reduced-motion`.

## הערה על היקף
DESIGN.md מגדיר ארבעה מצבים. MILESTONES.md מציב אותם ב-Milestone 2. ב-Milestone 1 ממומש המסך המלא בעיצוב, ומצבי idle, think ו-joke. שגיאה מציגה הודעה פשוטה. אם תרצי את כל ארבעת המצבים כבר עכשיו, אפשר, זה קטן.

## תהליך
1. תכנון (המסמך הזה) ואישור.
2. בנייה.
3. הרצה לבדיקה: בכתובת Vercel, או מקומית עם `vercel dev` (http://localhost:3000), לפי הבחירה שלך.
4. commit ו-push ל-`main` (`s-gazit/joke-app`), ייבוא ל-Vercel (Framework Preset: Other), ולינק חי.

## צעדים ידניים שלך (אחרי הפריסה הראשונה)
- OpenAI, API keys: מפתח production בשם `joke-in-a-click`.
- Vercel, Environment Variables: `OPENAI_API_KEY`, סוג Secret, Production ו-Preview. אחר כך Redeploy.
- רשות, הרצה מקומית: מפתח dev בשם `joke-in-a-click-dev`, מועתק ל-`.env.local` ביד (העתקת `.env.example`), ו-`npm i -g vercel`, `vercel login`, `vercel link`, `vercel dev`.
- Claude אף פעם לא מבקש, קורא או כותב מפתח.

## תנאי השלמה
1. הכתובת נפתחת בטלפון, בעברית, מימין לשמאל, בעיצוב של DESIGN.md.
2. לחיצה מציגה "בדיחה זמנית מהשרת" עם הנושא ו"המפתח: נמצא".
3. ב-Network: בקשת POST אחת ל-`/api/joke`, באותה כתובת.
4. ב-Logs של Vercel שורה לכל לחיצה.
5. אין כותרות CORS ואין טיפול ב-OPTIONS.
6. בריפו אין `.env` ו-`.env.local`. יש `.env.example` עם `OPENAI_API_KEY=` בלבד, ויש `.claude/settings.json`.
7. מקומית: אותה תוצאה ב-http://localhost:3000.
