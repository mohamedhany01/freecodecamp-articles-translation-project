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

### كيفية التعامل مع ملفات الـJSON المخزنة على جهازك "local" على المتصفح "browser"
لسوء الحظ، لا يمكن تحميل ملفات الـJSON المحفوظة على جهازك الى المتصفح.

حيث سوف تقوم `fetch`  بأظهارة رسالة خطأ فى حالة قمت بأستخدمها لتحميل اى ملفات على جهازك "local". على سبيل المثال، انت تملك الملف المحمل بالبيانات التالية بصيغة الـJSON على جهازك:

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

ملف jokes.json

وتريد تحويله "parse" وعمل قائمة لعرضها فى صفحة HTML بسيطة.

وبالفعل قمت بعمل الصفحة التالية وقمت بفتحها فى متصفحك:

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

ملف index.html

سوف تفاجئ برسالة الخطأ التالية فى لوحة التحكم "console" فى المتصفح:

```
Fetch API cannot load file://<path>/jokes.json. URL scheme "file" is not supported

```

بشكل عام، لا تسمح المتصفحات "browsers" بالوصول للملفات المخزنة على جهازك "local" بسهولة وذلك للأسباب امنية. هذا امر جيد، وبتالى لا تحاول استخدام هذه الطريقة.

بدلا من ذلك، الافضل أن تحول ملفات الـJSON على جهازك "local" الى جافا سكريبت. لحسن الحظ، هذا الطريقة مضمونة وسهلة وذلك لان طريقة الكتابة الخاص بالـJSON مشابهة تماما لجافا سكريبت.

كل ما نريده ان نقوم بعمل ملف جديد كالاتى مع عمل متغير من نوع مصفوفه "Array" يحمل الـJSON الذى نريد كقيمة افتراضية:

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

ملف jokes.js

وإرفاقه فى صفحة الـHTML:
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

وبالتالى سوف تكون قادر على استخدام المتغير `jokes` بسهولة.

يمكن استخدام وحدات "modules" جافا سكريبت [modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules) لعمل نفس الشئ، لكن هذا خارج نطاق شرحنا الان.

لكن ماذا عن التعامل مع ملفات الـJSON محليا "local" مع وجود بيئة عمل الـNode.js؟ لنلقى نظرة على هذه الطريقة الجديدة.

## كيفية تحويل JSON مع وجود بيئة عمل الـNode.js
الـNode.js هى بيئة تشغيل "runtime" للجافا سكريبت، تسمح لك بأستخدام جافا سكريبت خارج المتصفح. لقراءة المزيد [Node.js](https://www.freecodecamp.org/news/the-definitive-node-js-handbook-6912378afc6e/).

سواء قمت بأستخدام Node.js لتشغيل جافا سكريبت محليا "locally" على جهازك، او تشغيل تطبيق ويب "web applications" كامل على خادم "server" ما، لمن الجيد أن تعرف كيفية التعامل مع JSON.

فى المثال التالى، سوف نستخدم نفس الملف `jokes.json`:

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

ملف jokes.json

## كيفية تحويل "parse" الـJSON بأستخدام `()require`

لنبدأ بالطريقة السهلة.

اذا كانت تمتلك ملف JSON على جهازك، فكل ما عليك فعله استخدام `()require` لاستخدام ملف JSON كأحد ملفات "module" الـNode.js:

```js
const jokes = require('./jokes.json');

```

ملف الـJSON سوف يتم تحويله "parsed" تلقائيا ويمكن البدأ بأستخدامه بشكل طبيعى فى مشروعك:

```js
const jokes = require('./jokes.json');

console.log(jokes[0].value); // "Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris."

```

ملاحظة عملية التحويل والتحميل بأستخدام `()require` هى عملية متزامنة "synchronous"، اى انه البرنامج سوف يتوقف عن العمل لحين تحويل "parses" الملف بشكل كامل، وبالتالى فى ملفات الـJSON كبيرة الحجم سوف تؤثر هذه العملية على سرعة البرنامج بشكل ملحوظ، لذلك وجب التحذير مع هذه الطريقة.

بالاضافة لذلك، عملية التحويل "parsing" تقوم بتحميل الملف بالكامل للذكرة العشوائية "memory" للمعالجة، لذلك من المستحسن استخدام هذه الطريقة مع الملفات الـJSON التى لا يوجد تغير فى محتواها "static". اذا كان هناك تغير دائما فى ملفات الـJSON  اثناء فترة تشغيل البرنامج، فلن تستطيع الوصول لهذه التغيرات حتى تعيد تشغيل البرنامج و تعيد تحميل ملفات الـJSON بالتغيرات الجديدة.

### طريقة تحويل "parse" ملف من نوع JSON بأستخدام `()fs.readFileSync` و `()JSON.parse`

هذه طريقة تقليدية الى حد ما، لتحول ملفات الـJSON فى مشاريع تستخدم Node.js - استخدم `fs` لقراءة الملفات، وبعدها حول الملفات بأستخدام `()JSON.parse`.

لنر كيف يتم ذلك بأستخدام `()fs.readFileSync`. أولا، قم بإضافة `fs` للمشروع كألاتى:


```js
const fs = require('fs');

```

وبعد ذلك، قم بإنشاء متغير "variable" جديد لتخزين ناتج "output" ملف `jokes.json` بأستخدام `()fs.readFileSync`:

```js
const fs = require('fs');
const jokesFile = fs.readFileSync();

```

`()fs.readFileSync` يمكنة تمرير له العديد من الخيارات "arguments". اول خيار هو مسار الملف المراد قراءته:

```js
const fs = require('fs');
const jokesFile = fs.readFileSync('./jokes.json');

```
والان اذا قمت بعرض محتويات `jokesFile` فى لوحة التحكم "console"، سوف يظهر الاتى:

```
<Buffer 5b 0a 20 20 7b 0a 20 20 20 20 22 63 61 74 65 67 6f 72 69 65 73 22 3a 20 5b 22 64 65 76 22 5d 2c 0a 20 20 20 20 22 63 72 65 61 74 65 64 5f 61 74 22 3a ... 788 more bytes>
```

هذه يعنى انه تم قراءة الملف بنجاح من طرف `fs`، لكن لم يتم تحديد نوع ترميز "encoding" محدد لذلك يظهر بهذه الطريقة. `fs`  يمكنه قراءة اى نوع من الملفات, وليس فقط الــJSON، لذلك لعرض محتوى الملف بشكل صحيح يجب تحدد نوع الترميز.

فى حالة الملفات النصية "text-based"، يكون الترميز "encoding" عادة من نوع `utf8`.


```js
const fs = require('fs');
const jokesFile = fs.readFileSync('./jokes.json', 'utf8');

```

دعنا الان نعرض ناتج `jokesFile`.

لهذ الحد نحن نقوم بقراء الملف، و بالطبع لا يزال عبارة عن نص عادى "string". سوف تحتاج طريقة لتحويل `jokesFile` الى كائن "object" جافا سكريبت او مصفوفة "array".

لعمل ذلك نحن فى حاجة ﻷستخدام `()JSON.parse`:

```js
const fs = require('fs');
const jokesFile = fs.readFileSync('./jokes.json', 'utf8');
const jokes = JSON.parse(jokesFile);

console.log(jokes[0].value); // "Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris."

```

كما يظهر اسم الدالة "method"، يمكن تمرير JSON نصى لـ`()JSON.parse` وسوف تقوم بتحويله الى كائن "object" جافا سكريبت او مصفوفة "array".

ذكرنا سابقا أن `require` متزامنة "synchronous"، ايضا `()fs.readFileSync` كذلك،  اى انه البرنامج سوف يتوقف عن العمل لحين تحويل "parses" الملف بشكل كامل ومن الممكن ان يحدث بطئ البرنامج اذا كان الملف كبير الحجم.

ايضا، `()fs.readFileSync` تقوم بقراء الملف مرة واحدة فقط وتحمله الى الذكرة "memory". لذلك اى تعديل فى الملف سوف تحتاج الى قراءة الملف مرة اخرى. لجعل الامور اكثر سهولة، لما لا نقوم بأنشاء دالة "function" بسيطة لقراءة الملفات.

انظر الى المثال الاتى:

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
### ### طريقة تحويل "parse" ملف من نوع JSON بأستخدام `()fs.readFile` و `()JSON.parse`

`()fs.readFile` مشابهة تمام لـ`()fs.readFileSync`، الاختلاف الوحيد انها تعمل بشكل غير متزامن "asynchronously"، سوف يكون هذا ذو نفع فى الملفات كبيرة الحجم.

انظر الى المثال الاتى:
```js
const fs = require('fs');

fs.readFile('./jokes.json', 'utf8');
```

يبدو هذا مشابه الى حد ما مع الذى قمنا به فى `()fs.readFileSync`، الاختلاف اننا لا نحفظ الناتج فى متغير مثل  `jokesFile`.
ولانها عملية غير متزامنه "asynchronous"، اى كود برمجى يأتى بعد `()fs.readFile` سوف ينفذ قبل انتهاء عملية قراءة الملف.

بدلا من ذلك، يمكن عمل دالة "function" من نوع callback و عمل تحويل "parse" لـJSON بداخل الدالة:
```js
const fs = require('fs');

fs.readFile('./jokes.json', 'utf8', (err, data) => {
  if (err) console.error(err);
  const jokes = JSON.parse(data);

  console.log(jokes[0].value);
});

console.log("This will run first!");
```
وسوف يكون الناتج كالاتى:

```
This will run first
Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris.

```

تقوم كل من `()fs.readFileSync()`,  `fs.readFile` بتحميل البيانات الى الذكرة "memory"، وبالتالى اى تغير يلزم عنده إعادة قراءة للملف مرة اخرى.

بالفعل `()fs.readFile` تعمل بشكل غير متزامن "asynchronous"، وفى النهاية سوف يتم تحميل الملف بالكامل وتتم عملية القراءة فى الذكرة "memory". لكن اذا كنت تتعامل مع ملفات كبيرة الحجم، فمن الافضل الاطلاع على [Node.js streams](https://www.freecodecamp.org/news/node-js-streams-everything-you-need-to-know-c9141306be93/)

### كيف تحول ملفات الـJSON الى ملفات نصية "stringify" بأستخدام `()JSON.stringify` فى Node.js

فى الخاتمة، اذا كنت تقوم بتحويل JSON بأستخدام Node.js، سوف يكون هناك حاجة لتبادل JSON مع API معين.

لحسن الحظ، هذه العملية يمكن القيام بها بأستخدام المتصفح - وذلك بأستخدام `()JSON.stringify` لتحويل كائن "object" جافا سكريبت او مصفوفة "array" لملف JSON نصى "string":
```js
const newJoke = {
  categories: ['dev'],
  value: "Chuck Norris's keyboard is made up entirely of Cmd keys because Chuck Norris is always in command."
};

console.log(JSON.stringify(newJoke)); // {"categories":["dev"],"value":"Chuck Norris's keyboard is made up entirely of Cmd keys because Chuck Norris is always in command."}

```
هنا نحن الان فى نهاية المقال! لقد قمنا بالتعرف على كل شئ يختص بالتعامل مع JSON سواء فى المتصفح "browser" او بيئة عمل Node.js.

الان متسلاحا بهذه المعرفة، انطلاق وطبق مع تعلمته فى التعامل مع JSON.

هل نسيت شئ ما؟ كيف تتعامل مع JSON فى مشاريع البرمجية؟ اخبرنى على حسابى [Twitter](https://twitter.com/kriskoishigawa)
