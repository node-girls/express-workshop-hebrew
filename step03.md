# &#x202b; שלב שלישי: בניית השרת

&#x202b;
הדבר הראשון שעלינו לעשות זה לבנות את השרת שלנו. את תמיד תצטרכי לבנות שרת בעת כתיבת קוד backend. שרת יכול להיבנות ב-Node.js, אך Express מפשט לנו דברים והופך את זה לקל יותר.

## &#x202b; מה זה שרת?

&#x202b;
שרתים הם תוכנות מחשב שמקבלות בקשות מתוכנות אחרות, "הלקוח", ושולחות בחזרה את התגובה. כלומר, את המידע המבוקש או כל מקור חומרה / תוכנה אחר.

### &#x202b; … ומה זה שרת בעברית?

&#x202b;
שרת הוא תוכנת מחשב. התפקיד שלו הוא לשלוח ולקבל מידע.

&#x202b;
בואי ניקח לדוגמה אתר אינטרנט. אתר אינטרנט הוא רק אוסף של קבצי HTML ו-CSS, ואולי קצת קבצי JavaScript. כאשר את מקלידה את כתובת האתר בשורת הכתובת בדפדפן שלך, הדפדפן (הלקוח) שולח בקשה לשרת שחי בכתובת הזו. הדפדפן מבקש מהשרת שיביא לו את הקבצים שהוא צריך להציג בשביל להראות את האתר.

![Server flow](https://files.gitter.im/heron2014/FiiK/server.png)

## &#x202b; 1. יצירת קובץ `server.js`

&#x202b;
בואי ניצור את השרת שלנו! לפני שאנו מתחילות לעשות משהו, עלינו ליצור קובץ חדש שנקרא `server.js`. זה המקום בו כל הקוד שלנו הולך להיות.

## &#x202b; 2. `require` לתיקיית Express

&#x202b;
התקנו כבר את Express בשלב 2, אך עלינו לוודא שהוא כלול בקובץ שלנו באופן ספציפי, כדי שנוכל לבצע שימוש במתודות שלו. ב-Node.js, כאשר את רוצה לגשת לפונקציונליות של ספריות או מודולים בקבצים אחרים, עליך לעשות להם `require` לקובץ שלך.

&#x202b;
על מנת לייבא את Express, כתבי את שורת הקוד הבאה בקובץ `server.js` בהתחלה:

```js
var express = require('express');
```

## &#x202b; 3. אתחול השרת 

&#x202b;
על מנת לאתחל את השרת, אנו רק צריכים לקרוא לפונקציה `()express`. פקודה זו תיצור לנו אפליקציית Express לעבוד איתה.

&#x202b;
בשורה השנייה של הקוד שלך בקובץ `server.js` כתבי:

```js
var express = require('express');
var app = express();
```

## &#x202b; 4. "האזנה" לבקשות פוטנציאליות
&#x202b;
שלב אחד נוסף נותר, עלינו להגדיר את ה-**port** שבו השרת שלנו יאזין.
תחשבי שה-port הוא כמו מספר דירה בבניין - כל בקשה שתגיע אל השרת שלך, תעבור דרך הדלת שעליה כתוב מספר הדירה.
הגדרת ה-port תאפשר לנו למצוא בקלות איפה השרת שלנו רץ.

&#x202b;
אנו נשתמש במתודה **`app.listen`** לעשות את זה.
המתודה הזו מקבלת שני ארגומנטים: מספר **port** ופונקצית **callback**, אשר אומרת מה לעשות ברגע שהשרת רץ.

&#x202b;
צריכה הסבר נוסף? קראי עוד על המתודה `app.listen` באתר של [Express](http://expressjs.com/en/4x/api.html#app.listen).

&#x202b;
אנו הולכות להריץ את השרת שלנו ב-port מספר `3000`, לקרוא ב-callback ל-`console.log`. עדכני את קובץ ה-`server.js` שיקרא למתודה `app.listen`:

```js
var express = require('express');
var app = express();

app.listen(3000, function () {
  console.log('Server is listening on port 3000. Ready to accept requests!');
});
```

## &#x202b;  5. הפעלת השרת!

&#x202b;
בנית את השרת שלך, אך הוא עדיין לא רץ. עליך להריץ פקודה בטרמינל על מנת להריץ אותו. אנו עומדות להשתמש במילת המפתח `node` בשביל להריץ את קובץ השרת.

&#x202b;
הקלידי את הפקודה הבאה בטרמינל שלך:

```
$ node server.js
```

&#x202b;
אם את רואה את השורה הבאה, מזל טוב! בנית לעצמך שרת!

![success](https://raw.githubusercontent.com/node-girls/workshop-cms/master/readme-images/step2-server02.png)


### &#x202b; [לשלב 4 >>>>](https://github.com/node-girls/express-workshop-hebrew/blob/master/step04.md)