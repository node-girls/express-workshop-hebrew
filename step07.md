# &#x202b; שלב שביעי: שליחת פוסט הבלוג שלך לשרת

&#x202b;
עד כה ביקשנו מידע מהשרת שלנו, אבל אנחנו יכולים גם לשלוח מידע אל השרת שלנו, כדי שיאוחסן איפה שהוא.

### &#x202b; מתודות HTTP request
&#x202b;
כל הבקשות משתמשות באחת ממתודות HTTP. המתודות העיקריות הן:

* `GET`
* `PUT`
* `POST`
* `DELETE`

&#x202b;
הפונקציה `app.get` מתעסקת רק בבקשות המשתמשות במתודת `GET`

### &#x202b; מתודת בקשת `POST` ב-HTTP
&#x202b;
כאשר שולחים מידע לשרת, אנחנו משתמשים במתודה `POST` על מנת לבצע בקשת HTTP לשרת, במקום ב-`GET`.
על מנת להבין את ההבדל בין `GET` לבין `POST`, תוכלי לקרוא עוד בקישור הנמצא בחלק "מילות מפתח" שבהמשך.

&#x202b;
בואי ננסה לשלוח (`POST`) טקסט כלשהו לשרת.

&#x202b;
אנו הולכים להוסיף טופס לדף ה-`index.html`, כך שתוכלי לכתוב את הפוסטים לבלוג שלך משם.

&#x202b;
פתחי את קובץ `index.html` בעורך הטקסט שלך. כאשר תסתכלי היטב, תראי את הקוד הבא:

```html
<div class="entry-container">
    <!--PASTE YOUR CODE HERE!! -->
</div>
```
&#x202b;
**החליפי את ההערה המסומנת באפור עם קטע הקוד הבא:**

```html
<h3>Create a blog post</h3>
<form action="/create-post" method="POST">
    <textarea name="blogpost" rows="10" cols="14"></textarea>
    <button type="submit">Send</button>
</form>
```

&#x202b;
בואי נביט על הטופס מקרוב:
* &#x202b; לטופס יש אזור טקסט וכפתור "שליחה".
* &#x202b; המאפיין `action` הוא ה-endpoint אליו ישלח המידע.
* &#x202b; במאפיין `name` נשתמש בשלב מאוחר יותר לשם אזכור של המידע.

&#x202b;
כאשר תלחצי על Send, הטופס ישלח בקשת `POST` אל השרת, אל ה-endpoint שכתובתו מצוינת במאפיין `action`.
במקרה שלנו אל `create-post/`.

&#x202b;
בהמשך, נצטרך להוסיף מעט קוד בשרת שלנו אשר יתמודד עם בקשות `POST /create-post` המגיעות ל-endpoint הזה.

When you hit Send, the form will send a `POST` request to the server, using whatever is in the `action` attribute as the endpoint.  In our case it's `/create-post`.

### &#x202b; קבלת הפוסט החדש לבלוג בשרת

* &#x202b; המידע אינו מגיע אל השרת שלנו בבת אחת, הוא זורם אליו כמו ב-**stream**. תחשבי על stream כמו על מים הזורמים מהברז אל דלי.

* &#x202b; אם היינו כותבות שרת Node טהור, היינו חייבות לחשוב כיצד אנחנו אוספות את כל המידע שמגיע אל השרת כראוי. אבל למזלנו, Express מטפל בכל הדברים הלו בשבילנו.

* &#x202b; כל מה שעלינו לעשות הוא להגדיר route (נתיב) חדש אשר מתמודד עם כל הבקשות המגיעות דרך ה-endpoint החדש: `/create-post`

* &#x202b; בואי ניזכר כיצד נראה ה-route בשביל בקשת `GET` ב-Express

```js
app.get('/my-lovely-endpoint', function (req, res) {
    res.send('Hello there!');
});
```

&#x202b;
אבל הפעם אנחנו רוצות להגדיר route בשביל בקשות `POST`. מה את חושבת שעלינו לעשות שונה? נסי בעצמך לראות אם את יכולה להגדיר route חדש בשביל ה-endpoint שלנו `create-post/`

&#x202b;
בינתיים, תגרמי למתודה `create-post/` שלך לעשות כך:
```
console.log('/create-post')
```

&#x202b; **רמז!**

&#x202b;
אם את צריכה רמז, שאלי את המדריכה שלך או את אחת מחברותייך לקבוצה ותראי אם אתן יכולות לפתח זאת יחדיו.

&#x202b;
אם הצלחת בעצמך להתמודד עם בקשות המגיעות אל ה-endpoint החדש שלנו עם בקשות `POST`, את מוכנה לעבור לשלב הבא!


---

### &#x202b; Extracting the blog post

Now the contents of your blogpost is hidden in your `req` object somewhere.  Normally you would extract it using `req.body`.  Try to console.log `req.body` now.

Getting `undefined`?  Not to worry, that's normal.  When data has been `POST`ed to the server as `FormData`, we need to do things slightly differently to access the data that's come through in the request.

We need another middleware function.  Something that can get extract the contents out of the special `FormData` object.  For this we will use `express-formidable`.  `express-formidable` is another Express middleware. It will extract the form data from the request and make it available to you when you do `req.fields`.

This time though, `express-formidable` is not built-in, we need to explicitly install it.

**In your terminal, install express-formidable**
```bash
npm install express-formidable --save
```

`require` `express-formidable` so you can use it in your code.  You can't use dashes in JavaScript variable names, so just call it `var formidable`.
```js
var formidable = require('express-formidable');
```

Now add this towards the top of your server, after your `require`s and `app.use(express.static('public'))`, but before your `/create-post` endpoint:
```js
app.use(formidable());

```
Now inside your `/create-post` function, add:
```js
console.log(req.fields);
```
Refresh your server and have another go at writing a blogpost.

You should now see an object in the console.  The key should be `blogpost`, just like the name attribute in the form on the HTML page.  The value of `blogpost` will be your message!

### &#x202b; [לשלב 8 >>>>](https://github.com/node-girls/express-workshop-hebrew/blob/master/step08.md)