# &#x202b; פוסטים יחידים
&#x202b;
זהו שלב אופציונלי, בשביל הכיף. הוא מתבסס על כך שסיימת את כל השלבים שלפניו.

&#x202b;
אנחנו הולכות להפוך את האתר שלך להרבה יותר טוב, ע"י הוספת האפשרות לקבל ולראות פוסטים יחידים. בואי נראה כיצד אנחנו יכולות לעשות את זה.

## &#x202b; שלב 1 - פרמטרים ב-URL

&#x202b;
אנחנו לא רוצים לכתוב handler לכל כתובת URL באפליקציה שלנו.
[הפרמטרים](https://expressjs.com/en/guide/routing.html#route-parameters) ב-URL של Express נותנים לנו להגדיר חלקים דינמיים בתוך ה-URL - מקום בשביל פוסט לפי ID מסוים או שם משתמש, לדוגמה.
אפשר להסתכל עליהם כמו על ארגומנטים המועברים לפונקציות בשרת שלך.

&#x202b;
הפרמטרים ב-URL של Express משתמשים ב `:` כדי להגדיר שזהו חלק דינמי בכתובת:

- &#x202b; `/users/:userId` - מתאים לכתובות כגון:
 
    * `/users/123`
    * `/users/node-girls`
- &#x202b; `/users/:userId/posts/:postId` - מתאים לכתובות כגון:
    * `/users/node-girls/posts/node-is-best`

&#x202b;
בואי נוסיף handler לפוסטים יחידים:
```js
app.get('/posts/:postId', function (req, res) {
    res.send('post id: ' + req.params.postId);
});
```

&#x202b;
מה את חושבת שתראי כאשר תבקרי בכתובת: `http://localhost:3000/posts/abc123` בדפדפן שלך?

## &#x202b; שלב 2 - קריאה מהקובץ ושליחת הפוסט הספציפי

&#x202b;
בדיוק כמו `create-post/`, עליך לקרוא את קובץ ה-JSON שלך. נסי לשלוח את תוכן הפוסט בחזרה לדפדפן שלך:
```
res.send(postContentHere)
```

## &#x202b; שלב 3 - עיבוד תבנית
&#x202b;
כרגע, אנחנו רק שולחות את התוכן של הבלוג שלך, אך את בטח תרצי לייפות את ההודעה שלך עם קצת HTML ו-CSS. לשם כך, ניתן להשתמש במערכת תבניות המובנית של Express.
תוכלי להשתמש באיזה שפה לתבנית שתרצי (כמו [pug/jade](https://pugjs.org/), [ejs](http://www.embeddedjs.com/) או [handlebars](http://handlebarsjs.com/)),
אבל אנחנו נשתמש ב- [mustache](https://mustache.github.io/) בדוגמה הזו.

&#x202b;
הריצי את הפקודה
```
npm install --save mustache-express.
```
&#x202b;
לאחר מכן, הסתכלי במידע על [mustache-express](https://www.npmjs.com/package/mustache-express) וה-[Express's templating](http://expressjs.com/en/guide/using-template-engines.html).
עליך ליצור קובץ template בנתיב: `views/post.mustache`

&#x202b;
ככה זה נראה:

```mustache
<!DOCTYPE html>
<html>
  <head>
    <title>Blog Post</title>
  </head>
  <body>
    <h1>yay blog post!</h1>
    <article>
      {{ post }}
    </article>
  </body>
</html>
```

אם את נתקעת, תוכלי להיעזר [בפתרון לדוגמה](https://github.com/node-girls/express-workshop-complete/tree/templating) שלנו. :)

## &#x202b; הנה משימות נוספות שתוכלי לעשות:
- &#x202b; הוסיפי לפוסטים שלך כותרות
- &#x202b; הוסיפי דף תוכן עניינים לפוסטים שלך
- &#x202b; הוסיפי לפוסטים תיעוד בשפת [Markdown](https://www.markdownguide.org/cheat-sheet/)
- &#x202b; יאיי!
