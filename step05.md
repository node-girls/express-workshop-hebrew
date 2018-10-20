# &#x202b; שלב חמישי: ניתוב

&#x202b;
כרגע, השרת שלנו עושה רק דבר אחד. כאשר הוא מקבל request מה-endpoint `/`,
הוא שולח בחזרה את ה-response שכתבת `Yay Node Girls` לדפדפן.

&#x202b;
רוצה לבדוק? נסי להקליד http://localhost:3000/nodegirls ולראות מה קורה.

&#x202b;
אולם, ע"י שימוש ב-endpoints, אנו יכולות לגרום לשרת שלנו לשלוח תגובות שונות לבקשות שונות. הקונספט הזה נקרא **routing** - ניתוב.

### &#x202b; מה זה endpoint

&#x202b;
Endpoint הוא החלק ב-URL (כתובת אתר) אשר מגיע אחרי הלוכסן `/` . לדוגמה: לדוגמה: `/chocolate` היא נקודת הקצה עבור chocolate. זו הכתובת אליה את שולחת את הבקשה.

## &#x202b; 1. צרי endpoints משלך ושלחי אליהן בקשות שונות

&#x202b;
אנו הולכות לנסות לשלוח responses שונים ל-endpoints שונות. זוכרת את המתודה `app.get()`? כדי להגדיר ניתובים שונים בשרת שלך, עלינו לחזור על המתודה הזו עם endpoints שונות.

&#x202b;
לדוגמה:

```js
app.get("/", function (req, res) {
    res.send("Hello World!");
});

app.get("/chocolate", function (req, res) {
    res.send("Mm chocolate :O");
});
```

#### &#x202b; אתגר

&#x202b;
הוסיפי קוד כך שהשרת שלך ישלח הודעה אחת כשה-endpoint היא

`/node`

&#x202b;
ותגובה אחרת כאשר היא:

`/girls`

### &#x202b; [לשלב 6 >>>>](https://github.com/node-girls/express-workshop-hebrew/blob/master/step06.md)