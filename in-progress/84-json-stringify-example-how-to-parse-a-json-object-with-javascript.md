# كيف تحول "Parse" كائن "Object" بصيغة الـJSON بأستخدام جافا سكريبت

ملفات الـJSON، او ما يطلق عليها ترميز الكائنات باستعمال جافا سكريبت "JavaScript Object Notation"، تحيط بنا فى كل مكان. اذا استخدمت تطبيق ويب، فهناك احتمال كبير انه يستخدم هذه التقنية بالفعل لهيكلة، تخزين و التخاطب بين الخوادم و حاسوبك الشخصي.

فى هذا المقال، سوف نتحدث بشكل مختصر عن الاختلافات بين ملفات الـJSON  وجافا سكريبت، وبعدها سوف ننتقل الى طرق التحويل "parse" ملفات  الـJSON   باستعمال جافا سكريبت و بيئة تشغيل الجافا سكريبت الـNode.js.

## الاختلافات بين JSON و جافاسكريبت

بينما يبدو شكل JSON فى الكتابة مشابه لجافاسكريبت ،لكن الأفضل التفكير في صيغة JSON  على انها نظام تنسيق منظم للبيانات ، مشابه لنظام تنسيق الملفات النصية العادية. يتصادف الامر ان كتابة JSON مستوحاة من طريقة كتابة "syntax" الـJavaScript ، وهذا هو ما يوضح أنها تبدو متشابهة جدًا.

دعنا الان نلقى نظرة على طريقة كتابة كل من الكائنات "objects" والمصفوفات "arrays" فى الـJSON  ونقارنها بنظريه الـجافاسكريبت

### طريقة كتابة الكائنات "objects" فى الـجافاسكريبت مقابل الـJSON

اولا: طريقة الـJSON

```json
{
  "name": "Jane Doe",
  "favorite-game": "Stardew Valley",
  "subscriber": false
}

```

ملف jane-profile.json

الاختلاف الرئيسي بين JSON و جافاسكريبت فى طريقة الكتابة - أيضًا تسمى بالطريقة الحرفية لكتابة الكائن "object literal" - تتلخص فى علامات الاقتباس "quotation marks". يجب احاطة جميع المفاتيح "keys" السلاسل النصية "string" في طريقة كتابة كائن الـJSON بعلامات اقتباس مزدوجة (`"`).

بينما الطريقة الحرفية لكتابة الكائن "object literal" فى جافاسكريبت اكثر مرونة. حيث لا يجب ان تحيط جميع المفاتيح "keys" السلاسل النصية "string" في طريقة كتابة بعلامات اقتباس مزدوجة (`"`). بدلا من ذلك يمكن احاطتها علامات اقتباس عادية (`'`)، او لا تحيتها بشئ اطلاقا فى حالة المفاتيح "keys".

هنا مثال يوضح طريقة الكتابة الحرفية "object literal" للكائن فى جافاسكريبت المذكورة سابقا:

```js
const profile = {
  name: 'Jane Doe',
  'favorite-game': 'Stardew Valley',
  subscriber: false
}

```

لاحظ ان المفتاح `'favorite-game'` محاط بعلامة اقتباس عادية "single quotes"، حيث يجب عليك احاطة المفاتيح "keys" المفصولة بشرطات "dashes" بعلامات اقتباس.

اذا اردت تجنب استخدام  علامات الاقتباس، يمكن كتابة المفتاح (`favoriteGame`) بطربقة سنام الجمل "camel case" او فصل اجزاء المفتاح (`favorite_game`)  بشرطة سفلية "underscore" (`_`).

### طريقة كتابة المصفوفات "arrays" فى الـجافاسكريبت مقابل الـJSON

طريقة كتابة المصفوفات "arrays" فى الـJSON مثلها مثل جافاسكريبت، ويمكن ان تحمل قيم سلاسل نصية "strings"، القيم المنطقية "booleans"، ارقام وحتى كائنات من نوع الـJSON.

على سبيل المثال
```json
[
  {
    "name": "Jane Doe",
    "favorite-game": "Stardew Valley",
    "subscriber": false
  },
  {
    "name": "John Doe",
    "favorite-game": "Dragon Quest XI",
    "subscriber": true
  }
]

```

ملف profiles.json

وهذا ما يقابلها فى جافاسكريبت

```js
const profiles = [
  {
    name: 'Jane Doe',
    'favorite-game': 'Stardew Valley',
    subscriber: false
  },
  {
    name: 'John Doe',
    'favorite-game': 'Dragon Quest XI',
    subscriber: true
  }
];

```

## الـJSON هى نص عادى!

يمكن ان تتسائل الان، اذا كان هناك كائنات "objects" ومصفوفات "arrays" من نوع الـJSON، اذا لماذا لا يمكن استخدمها مثل الكائنات "objects" والمصفوفات "arrays" فى جافاسكريبت؟

الاجابة، هى ان الـJSON فى الحقيقة عبارة عن نص عادى!

للتوضيح، عند كتابة الـJSON فى ملف  منفصل مثل `jane-profile.json` او`profiles.json`، فى الحقيقة هذه الملفات هى ملفات نصية عادية من نوع الـJSON، حيث تحتوى كائنات "objects" ومصفوفات "arrays" من نوع JSON والتى بشكلها فقط تشبه جافاسكربت.

واذا قمت بإرسال طلب "request" لخادم بيانات "server" من نوع الـAPI، فسوف يرسل لك شئ مثل هذا:

```
{"name":"Jane Doe","favorite-game":"Stardew Valley","subscriber":false}
```

وبالتالى، اذا اردت استخدام JSON، فعليك تحويله "parse" او تغيره الى شئ مفهوم للغات البرمجة. على سبيل المثال، عملية تحويل "parsing" كائن من نوع JSON فى لغة مثل Python سوف ينتج عنها فهرس "dictionary".

مع استيعاب المعلومات السابقة، لنشاهد الان طرق التحويل المختلفة لملفات الـJSON فى جافاسكريبت.

## كيفية تحويل الـJSON فى متصفح الانترنت

اذا كنت تتعامل مع JSON من خلال متصفح الانترنت، فأنت على الارجح تستقبل وترسل بيانات من خادم من نوع API.

لنشاهد الان عدة امثلة.

### كيفية تحويل الـJSON فى بأستخدام `fetch`

ايسر طريقة لجلب بيانات من خادم هى بأستخدام `fetch`، حيث تحتوى على دالة "method" تدعى `()json.` لتحويل JSON الى كائن او مصفوفة جافاسكريبت عادية.

دعنا الان نستخدم `fetch` ونقوم بعمل طلب من نوع `GET` لخادم من خلال الرابط التالى
[Chuck Norris Jokes API](https://api.chucknorris.io):
```js
fetch('https://api.chucknorris.io/jokes/random?category=dev')
  .then(res => res.json()) // the .json() method parses the JSON response into a JS object literal
  .then(data => console.log(data));

```

اذا قمت بتشغيل الكود السابق فى متصفح الانترنت، سوف تظهر هذه البيانات فى لوحة تحكم "console" متصفحك:

```js
{
    "categories": ["dev"],
    "created_at": "2020-01-05 13:42:19.324003",
    "icon_url": "https://assets.chucknorris.host/img/avatar/chuck-norris.png",
    "id": "elgv2wkvt8ioag6xywykbq",
    "updated_at": "2020-01-05 13:42:19.324003",
    "url": "https://api.chucknorris.io/jokes/elgv2wkvt8ioag6xywykbq",
    "value": "Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris."
}

```

فى الوهلة الاولى يشبه هذا الشكل، شكل كائن "object" من نوع JSON، لكن فى الحقيقة هذا كائن "object" من نوع جافاسكريبت، تستطيع الان استخدامه بدون مشاكل.

### تحويل JSON الى نص بأستخدام `()JSON.stringify`

لكن ماذا عن إرسال بيانات الى API؟

على سبيل المثال، انت تريد ان ترسل بيانات ما الى خادم Chuck Norris joke API ليستطيع المزيد من الاشخاص استخدام هذه البيانات لاحقا.

دعنا اولا، نقوم بكتابة كائن "object" من نوع جافاسكريبت، كالاتى:

```js
const newJoke = {
  categories: ['dev'],
  value: "Chuck Norris's keyboard is made up entirely of Cmd keys because Chuck Norris is always in command."
};

```

الان، انت تريد إرسال بيانات API، اذا يجب عليك تحويل الكائن `newJoke` الى JSON اولا.

لحسن الحظ، جافا سكريبت تحتوى على دالة "method" مهمة سوف تساعدنا فى ذلك، تدعى `()JSON.stringify`:

```js
const newJoke = {
  categories: ['dev'],
  value: "Chuck Norris's keyboard is made up entirely of Cmd keys because Chuck Norris is always in command."
};

console.log(JSON.stringify(newJoke)); // {"categories":["dev"],"value":"Chuck Norris's keyboard is made up entirely of Cmd keys because Chuck Norris is always in command."}

console.log(typeof JSON.stringify(newJoke)); // string

```

بينما يمكن تحويل كائن من نوع جافاسكريبت الى نص من نوع JSON فى هذا المثال، `()JSON.stringify` يمكنها ايضا تحويل المصفوفات.

الان، يمكن إرسال JSON الذى تم تحويله الى نص الى API بأستخدام `POST`.

Note that the Chuck Norris Jokes API doesn't actually have this feature. But if it did, here's what the code might look like:
لاحظ، Chuck Norris Jokes API لا يملك خاصة التحويل السابقة. لكن فى حالة امتلاكها يمكن ان يصبح الكود كالاتى:

```js
const newJoke = {
  categories: ['dev'],
  value: "Chuck Norris's keyboard is made up entirely of Cmd keys because Chuck Norris is always in command."
};

fetch('https://api.chucknorris.io/jokes/submit', { // fake API endpoint
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify(newJoke), // turn the JS object literal into a JSON string
})
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => {
    console.error(err);
  });
```

سابقا، قمنا بتحويل البيانات القادمة من API بأستخدام `fetch`، وقمنا بعكس العملية بأستخدام `()JSON.stringify`، حيث قمنا بتحويل كائن جافاسكريبت الى نص بصيغة JSON.

### How to work with local JSON files in the browser

Unfortunately, it's not possible (or advisable) to load a local JSON file in the browser.

`fetch`  will throw an error if you try to load a local file. For example, say you have a JSON file with some jokes:

```json
[
  {
    "categories": ["dev"],
    "created_at": "2020-01-05 13:42:19.324003",
    "icon_url": "https://assets.chucknorris.host/img/avatar/chuck-norris.png",
    "id": "elgv2wkvt8ioag6xywykbq",
    "updated_at": "2020-01-05 13:42:19.324003",
    "url": "https://api.chucknorris.io/jokes/elgv2wkvt8ioag6xywykbq",
    "value": "Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris."
  },
  {
    "categories": ["dev"],
    "created_at": "2020-01-05 13:42:19.324003",
    "icon_url": "https://assets.chucknorris.host/img/avatar/chuck-norris.png",
    "id": "ae-78cogr-cb6x9hluwqtw",
    "updated_at": "2020-01-05 13:42:19.324003",
    "url": "https://api.chucknorris.io/jokes/ae-78cogr-cb6x9hluwqtw",
    "value": "There is no Esc key on Chuck Norris' keyboard, because no one escapes Chuck Norris."
  }
]

```

jokes.json

And you want to parse it and create a list of jokes on a simple HTML page.

If you create a page with the following and open it in your browser:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <meta name="viewport" content="width=device-width" />
    <title>Fetch Local JSON</title>
  </head>
  <script>
    fetch("./jokes.json", { mode: "no-cors" }) // disable CORS because path does not contain http(s)
      .then((res) => res.json())
      .then((data) => console.log(data));
  </script>
</html>

```

index.html

You'll see this in the console:

```
Fetch API cannot load file://<path>/jokes.json. URL scheme "file" is not supported

```

By default, browsers don't allow access to local files for security reasons. This is a good thing, and you shouldn't try to work around this behavior.

Instead, the best thing to do is to convert the local JSON file into JavaScript. Fortunately, this is pretty easy since JSON syntax is so similar to JavaScript.

All you need to do is create a new file and declare your JSON as a variable:

```js
const jokes = [
  {
    "categories": ["dev"],
    "created_at": "2020-01-05 13:42:19.324003",
    "icon_url": "https://assets.chucknorris.host/img/avatar/chuck-norris.png",
    "id": "elgv2wkvt8ioag6xywykbq",
    "updated_at": "2020-01-05 13:42:19.324003",
    "url": "https://api.chucknorris.io/jokes/elgv2wkvt8ioag6xywykbq",
    "value": "Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris."
  },
  {
    "categories": ["dev"],
    "created_at": "2020-01-05 13:42:19.324003",
    "icon_url": "https://assets.chucknorris.host/img/avatar/chuck-norris.png",
    "id": "ae-78cogr-cb6x9hluwqtw",
    "updated_at": "2020-01-05 13:42:19.324003",
    "url": "https://api.chucknorris.io/jokes/ae-78cogr-cb6x9hluwqtw",
    "value": "There is no Esc key on Chuck Norris' keyboard, because no one escapes Chuck Norris."
  }
]

```

jokes.js

And add it to your page as a separate script:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <meta name="viewport" content="width=device-width" />
    <title>Fetch Local JSON</title>
  </head>
  <script src="jokes.js"></script>
  <script>
    console.log(jokes);
  </script>
</html>

```

You'll be able to use the  `jokes`  array freely in your code.

You could also use JavaScript  `[modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)`  to do the same thing, but that's a bit outside the scope of this article.

But what if you want to work with local JSON files and have Node.js installed? Let's take a look at how to do that now.

## How to parse JSON in Node.js

Node.js is a JavaScript runtime that allows you to run JavaScript outside of the browser. You can read all about  [Node.js here](https://www.freecodecamp.org/news/the-definitive-node-js-handbook-6912378afc6e/).

Whether you use Node.js to run code locally on your computer, or to run entire web applications on a server, it's good to know how to work with JSON.

For the following examples, we'll use the same  `jokes.json`  file:

```json
[
  {
    "categories": ["dev"],
    "created_at": "2020-01-05 13:42:19.324003",
    "icon_url": "https://assets.chucknorris.host/img/avatar/chuck-norris.png",
    "id": "elgv2wkvt8ioag6xywykbq",
    "updated_at": "2020-01-05 13:42:19.324003",
    "url": "https://api.chucknorris.io/jokes/elgv2wkvt8ioag6xywykbq",
    "value": "Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris."
  },
  {
    "categories": ["dev"],
    "created_at": "2020-01-05 13:42:19.324003",
    "icon_url": "https://assets.chucknorris.host/img/avatar/chuck-norris.png",
    "id": "ae-78cogr-cb6x9hluwqtw",
    "updated_at": "2020-01-05 13:42:19.324003",
    "url": "https://api.chucknorris.io/jokes/ae-78cogr-cb6x9hluwqtw",
    "value": "There is no Esc key on Chuck Norris' keyboard, because no one escapes Chuck Norris."
  }
]

```

jokes.json

### How to parse a JSON file with  `require()`

Let's start with the easiest method.

If you have a local JSON file, all you need to do is use  `require()`  to load it like any other Node.js module:

```js
const jokes = require('./jokes.json');

```

The JSON file will be parsed for you automatically and you can start using it in your project:

```js
const jokes = require('./jokes.json');

console.log(jokes[0].value); // "Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris."

```

Note that this is synchronous, meaning that your program will stop until it parses the entire file before continuing. Really large JSON files can cause your program to slow down, so just be careful with that.

Also, because parsing JSON this way loads the entire thing into memory, it's better to use this method for static JSON files. If the JSON file changes while your program is running, you won't have access to those changes until you restart your program and parse the updated JSON file.

### How to parse a JSON file with  `fs.readFileSync(`) and  `JSON.parse()`

This is the more traditional way (for lack of a better term) to parse JSON files in Node.js projects – read the file with  `fs`  (file system) module, then parse with  `JSON.parse()`.

Let's see how to do this with the  `fs.readFileSync()`  method. First, add the  `fs`  module to your project:

```js
const fs = require('fs');

```

Then, create a new variable to store the output of the  `jokes.json`  file and set it equal to  `fs.readFileSync()`:

```js
const fs = require('fs');
const jokesFile = fs.readFileSync();

```

`fs.readFileSync()`  takes a couple of arguments. The first is the path to the file you want to read:

```js
const fs = require('fs');
const jokesFile = fs.readFileSync('./jokes.json');

```

But if you log  `jokesFile`  to the console now, you'd see something like this:

```
<Buffer 5b 0a 20 20 7b 0a 20 20 20 20 22 63 61 74 65 67 6f 72 69 65 73 22 3a 20 5b 22 64 65 76 22 5d 2c 0a 20 20 20 20 22 63 72 65 61 74 65 64 5f 61 74 22 3a ... 788 more bytes>
```

That just means that the  `fs`  module is reading the file, but it doesn't know the encoding or format the file is in.  `fs`  can be used to load pretty much any file, and not just text-based ones like JSON, so we need to tell it how the file is encoded.

For text-based files, the encoding is usually  `utf8`:

```js
const fs = require('fs');
const jokesFile = fs.readFileSync('./jokes.json', 'utf8');

```

Now if you log  `jokesFile`  to the console, you'll see the contents of the file.

But so far we're just reading the file, and it's still a string. We'll need to use another method to parse  `jokesFile`  into a usable JavaScript object or array.

To do that, we'll use  `JSON.parse()`:

```js
const fs = require('fs');
const jokesFile = fs.readFileSync('./jokes.json', 'utf8');
const jokes = JSON.parse(jokesFile);

console.log(jokes[0].value); // "Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris."

```

As the name suggests,  `JSON.parse()`  takes a JSON string and parses it into a JavaScript object literal or array.

Like with the  `require`  method above,  `fs.readFileSync()`  is a synchronous method, meaning it could cause your program to slow down if it's reading a large file, JSON or otherwise.

Also, it only reads the file once and loads it into memory. If the file changes, you'll need to read the file again at some point. To make things easier, you might want to create a simple function to read files.

Here's what that might look like:

```js
const fs = require('fs');
const readFile = path => fs.readFileSync(path, 'utf8');

const jokesFile1 = readFile('./jokes.json');
const jokes1 = JSON.parse(jokesFile1);

console.log(jokes1[0].value); // "Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris."

// the jokes.json file changes at some point

const jokesFile2 = readFile('./jokes.json');
const jokes2 = JSON.parse(jokesFile2);

console.log(jokes2[0].value); // "Chuck Norris's keyboard is made up entirely of Cmd keys because Chuck Norris is always in command."
```

### How to parse JSON with  `fs.readFile(`) and  `JSON.parse()`

The  `fs.readFile()`  method is very similar to  `fs.readFileSync()`, except that it works asynchronously. This is great if you have a large file to read and you don't want it to hold up the rest of your code.

Here's a basic example:

```js
const fs = require('fs');

fs.readFile('./jokes.json', 'utf8');
```

So far this looks similar to what we did with  `fs.readFileSync()`, except we're not assigning it to a variable like  `jokesFile`. Because it's asynchronous, any code after  `fs.readFile()`  it will run before it's finished reading the file.

Instead, we'll use a callback function and parse the JSON inside it:

```js
const fs = require('fs');

fs.readFile('./jokes.json', 'utf8', (err, data) => {
  if (err) console.error(err);
  const jokes = JSON.parse(data);

  console.log(jokes[0].value);
});

console.log("This will run first!");
```

Which prints the following to the console:

```
This will run first
Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris.

```

Like with  `fs.readFileSync()`,  `fs.readFile()`  loads the file into memory, meaning you'll need to read the file again if it changes.

Also, even though  `fs.readFile()`  is asynchronous, it eventually loads the entire file it's reading into memory. If you have a massive file, it may be better to look into  [Node.js streams](https://www.freecodecamp.org/news/node-js-streams-everything-you-need-to-know-c9141306be93/)  instead.

### How to stringify JSON with  `JSON.stringify()`  in Node.js

Finally, if you're parsing JSON with Node.js, there's a good chance that you'll need to return JSON at some point, maybe as an API response.

Luckily, this works the same way as in the browser – just use  `JSON.stringify()`  to convert JavaScript object literals or arrays into a JSON string:

```js
const newJoke = {
  categories: ['dev'],
  value: "Chuck Norris's keyboard is made up entirely of Cmd keys because Chuck Norris is always in command."
};

console.log(JSON.stringify(newJoke)); // {"categories":["dev"],"value":"Chuck Norris's keyboard is made up entirely of Cmd keys because Chuck Norris is always in command."}

```

And that's it! We've covered just about everything you need to know about working with JSON in the browser and in Node.js projects.

Now get out there and parse or stringify JSON to your heart's content.

Did I miss something? How do you parse JSON in your projects? Let me know over on  [Twitter](https://twitter.com/kriskoishigawa).
