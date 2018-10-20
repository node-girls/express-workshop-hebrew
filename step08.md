# &#x202b; שלב שמיני: חילוץ פוסט הבלוג שלך

&#x202b;
אז עכשיו יש לך handler ל-endpoint חדש ששמו `create-post/`. השלב הבא הוא למצוא את הפוסט לבלוג שלנו.

&#x202b;
התוכן של הפוסט בבלוג שלך מוסתר בתוך האובייקט `req` איפה שהוא.
לרוב, היית מחלצת אותו מתוך `req.body`.
נסי להדפיס לקונסול את `req.body` עכשיו.

&#x202b;
קיבלת `undefined` ? אל תדאגי, זה בסדר.
כאשר מידע נשלח אל השרת במתודת `POST` כאובייקט `FormData`, עלינו לעשות דברים קצת אחרת כדי לגשת אל הנתונים בתוך הבקשה.

&#x202b;
אנחנו צריכות עוד פונקצית middleware, משהו שיוכל לחלץ את המידע מתוך אובייקט ה-`FormData`.
בשביל זה אנחנו נשתמש ב-`express-formidable`, זוהי עוד שכבת middleware ב-Express.
מתודה זו תחלץ את המידע מהבקשה ותהפוך אותה לזמינה בשבילך ב-`req.fields`.

&#x202b;
הפעם, `express-formidable` לא קיימת עדיין, ונצטרך להתקין אותה במיוחד.


#### &#x202b; התקנת express-formidable

&#x202b;
לכי לטרמינל שלך והתקיני את express-formidable
```bash
npm install express-formidable --save
```

&#x202b;
הדבר הבא שעליך לעשות הוא להוסיף `require` לספריית `express-formidable`, על מנת שתוכלי להשתמש בה בקוד שלך.
ב-JavaScript אי אפשר להשתמש במקפים בשמות משתנים, לכן נקרא למשתנה `var formidable`.
הוסיפי זאת בראש הקובץ `server.js`, ליד ה-`require` הנוספים בקוד
```js
var formidable = require('express-formidable');
```

&#x202b;
כעת, במקום כלשהו בין ה-`require`-ים ובין ה-endpoint של `create-post/` הוסיפי את הקוד הבא:

```js
app.use(formidable());

```

&#x202b;
לבסוף, בתוך הפונקציה של `create-post/` הוסיפי את הקוד הבא:

```js
console.log(req.fields);
```

&#x202b;
התחילי מחדש את השרת שלך, ונסי שוב לכתוב פוסט חדש לבלוג שלך.

&#x202b;
כעת, תוכלי לראות את האובייקט בקונסול שלך. ה-key אמור להיות `blogpost`, בדיוק כמו השם במאפיין בטופס ה-HTML. הערך ב-`blogpost` יהיה ההודעה שלך.

### &#x202b; [לשלב 9 >>>>](https://github.com/node-girls/express-workshop-hebrew/blob/master/step09.md)