
# كيف تنتظر انتهاء وظيفة دالة "Function" ما بأستخدام Async و Await فى جافا سكريبت

متى تنتهى دالة غير متزامنة "asynchronous function" من وظيفتها؟ ولماذا هذا سؤال صعب الاجابة عليه؟

حسنا اتضح انه لكى تفهم الدوال الغير متزامنة "asynchronous functions" يتطلب فهم جيد لطريقة عمل لغة الجافا سكريبت.

دعنا نكتشف هذا المبدأ معا، وبالطبع سوف نفهم الكثير عن الجافا سكريبت فى هذه الرحلة.

هل انت جاهز للرحلة؟ حسنا، دعنا نبدأ.

## ما هو الكود الغير متزامن "Asynchronous"؟

تم تصميم جافا سكريبت على انها لغة برمجة متزامنة "synchronous"، اى ان الكود عند تشغيله، تبدأ جافا سكريبت بقراءة الكود من الاعلى سطرا سطرا الى نهاية الكود.

وكنتيجة لهذا التصميم، تستطيع جافا سكريبت ان تقوم بعمل شئ واحد كل مرة.

يمكنك التفكير في هذا كما لو كنت تتلاعب بست كرات صغيرة. أثناء قيامك باللعب ، تكون يداك مشغولة ولا تستطيع التعامل مع أي شيء آخر.

بالمثل فى جافاسكريبت: بمجرد تشغيل الكود، تكون جافاسكريبت مشغولة بتنفيذ الكود البرمجي. يسمى هذا التأثير/المبدئ بالكود المتزامن او المقيد "synchronous/blocking code". لانه يقوم بتقيد تنفيذ بقية الاكود لحين الانتهاء من الكود الحالى.

لنرجع الى مثال التلاعب بالكرات الصغيرة. ماذا سوف يحدث اذا ارت إضافة كرة اخري؟ بدلا من ستة كرات تريد ان يكونوا سبعة. هذه سوف تكون معضلة.

فأنت لا تريد ان توقف عملية التلاعب، لانها ممتعة كثيرا بالنسبة لك. وبالطبع لا يمكنك ان تأتى بكرة اخرى، لانه سوف يوقف عملية التلاعب حتما وهذا ما لا تريده.

اذا ما الحل؟ ببساطة يمكن الاستعانة بصديق او احد افراد العائلة متفرغ. لكى يحضر لك الكرة الاضافية، وفى اثناء عملية التلاعب بالكرات وفى منتصف العملية يمكن قذف الكرة الاضافية لكى تستطيع الامساك بها واضافتها لبقية الكرات.

يمكن وصف العملية السابقة فة عالم جافا سكريبت بالعملية الغير متزامنة "asynchronous". حيث تعمل جافاسكريبت على تفويض العمل الاضافى الى شئ اخر، وتقوم هى بتنفذ عملها فى تشغيل الكود. وبمجرد انتهاء العمل الاضافى، تستقبل جافاسكريبت الناتج النهائى.


## من المسئول عن العمل الاضافى؟
حسنا، نعرف الان ان جافاسكريبت متزامنة "synchronous" وكسولة. فى لا تريد ان تقوم بكل العمل لوحدها، لذلك تقوم بإلقاء العمل الاضافة على عاتق شخص اخر.

لكن من هو هذا الشخص الغامض الذى يعمل لحساب جافاسكريبت؟ وكيف تم تعينه للعمل لحساب جافاسكريبت؟

لننظر الى المثال التالى وهو عبارة عن كود غير متزامن "asynchronous code"

```javascript
const logName = () => {
   console.log("Han")
}

setTimeout(logName, 0)

console.log("Hi there")
```
عند تنفيذ هذا الكود يكون الناتج كالاتى:

```javascript
// in console
Hi there
Han
```

ما الذى يحدث هنا؟

من المثال السابق يتضح ان المسئول عن القيام بالعمل الاضافى لحساب جافاسكريبت هى بعض الدوال المخصوصة ببيئة تشغيل جافا سكريبت "environment-specific functions" و بعض الـAPIs. وبتالى هذا هو مصدر الارباك وعدم الفهم لمفهوم الكود غير متزامن "asynchronous code" فى جافاسكريبت.

## جافاسكريبت تعمل دائما فى بيئة عمل محددة!

غالبًا ما تكون هذه البيئة هي متصفح الانترنت "browser". ولكن يمكن أن يكون أيضًا على الخادم "server" مع NodeJS. لكن ما هو الفرق؟

الاختلاف - وهذا مهم جدا - هو ان المتصفح "browser" والخادم "server" فى حالة NodeJS من حيث الوظائف "functionality-wise"، ليسوا متساوين. غالبًا ما تكون متشابهة ، لكنها ليست كذلك.

دعنا نوضح هذا بمثال. لنفترض ان جافاسكريبت هو بطل رواية خيالية ملحمية. مجرد طفل عادى يعيش فى مزرعة.

بالصدفة يجد بطلنا الصغير بذلتين من نوع خاص تعطى مرتديها قوة تفوق الخيال.

عندما يرتدى بطلنا الصغير بذلة المتصفح "browser" للتسلح، يكتسب مباشرة القدرة على الوصول الى قدرات خاصة.

وعندما يرتدى بطلنا بذلة الخادم "server" للتسلح، يكتسب مباشرة قدرات اخرى خاصة.

تمتلك هذا البذلات سمات متشابهة، لان صناع هذه البذلات لديهم نفس الاحتياجات في أماكن معينة ، واحتياجات خاصة في أماكن أخرى.

هذا هو المقصود ببيئة تشغيل "environment"، مكان يمكن للكود فيه ان يعمل بشكل صحيح، بالاضافة لوجود ادوات إضافية لمساعدة جافاسكريبت فى عملها. ليست من صميم جافاسكريبت، لكن غالبا لا نلاحظ هذه الفروقات لانشغالنا بكتابة الاكواد كل يوم.

الـAPIs مثل [setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/setTimeout)، [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) و [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model) امثلة على الـWeb APIs. (يمكن أن [ترى لائحة كاملة عن الـWeb APIs](https://developer.mozilla.org/en-US/docs/Web/API)) كلها ادوات تم دمجها داخل المتصفح "browser"، وتم جعلها متاحة لنا عند كتابة الاكواد بجافاسكريبت فى بيئة المتصفح.

ولاننا نقوم دائما بالعمل داخل بيئة عمل "environment" معينة، يخيل لنا انها جزء من اللغة. لكن هذا غير صحيح بالمرة.

لذلك اذا تسألت لماذا يمكن استخدام `fetch` فى جافاسكريبت عند العمل داخل المتصفح (لكن تحتاج تنزيل حزمة "package" معينة عند العمل ببيئة الـNodeJS)، فهذا هو السبب. شخص ما خيل له ان `fetch` فكرة جيدة، فبتالى قرر ان يبنى نظير لها فى بيئة  الـNodeJS.

لازلت لم تفهم! اجل؟

الان، فهمنا من هو المساعد المجهول لجافاسكريب، وكيف تم توظيفه للقيام بهذا العمل الاضافى عن جافا سكريبت.

اتضح أن البيئة هي التي تتولى هذا العمل الاضافى، وكيفية قيام البيئة بهذا العمل، هي استخدام الوظائف المدمجة بها. على سبيل المثال `fetch` أو `setTimeout` في بيئة المتصفح.

## ماذا حدث للعمل الاضافى؟

حسنا، عظيم الان علمنا ان العمل الاضافى يكون على عاتق بيئة التشغيل "environment". اذا ماذا بعد ذلك؟

في مرحلة ما تحتاج إلى الحصول على النتائج. لكن دعنا نفكر في كيفية عمل ذلك.

دعنا نرجع الى مثال التلاعب بالكرات. تخيل أنك طلبت جلب كرة جديدة ، وبدأ صديقك فى هذا اللحظة في رمي الكرة نحوك عندما لم تكن مستعدًا للالتقاطها.

قد يتحول ذلك لكارثة. ربما يمكنك أن تكون محظوظًا وتلتقطها بشكل سليم. ولكن هناك فرصة كبيرة فى التسبب في إسقاط كل الكرات وفشل عملة التلاعب بالكامل. ألن يكون من الأفضل إذا أعطيت صديقك تعليمات محددة بشأن موعد رمى الكرة؟

حسنا، فى عالم جافاسكريبت، هناك قواعد صارمة توضع على عملية إسناد العمل الاضافى.

يتم التحكم بهذه القواعد من قبل حلقة الحدث "event loop" وتتضمن هذه الحلقة قائمة انتظار "queue" للمهام الصغيرة او ذات الاولوية الاقل "microtask" والمهام الكبيرة او ذات الاولوية الاهم "macrotask". يبدوا انها معلومات كثيرة بالنسبة لك. لكن تحمل معي.

![](https://www.freecodecamp.org/news/content/images/2020/08/autodraw-31_08_2020.png)

عندما يتم اسناد كود برمجي غير متزامن "asynchronous" للمتصفح "browser" يأخذ المتصفح الكود البرمجي ويديره ويتحمل عبء تشغيله بشكل كامل. ولكن قد تكون هناك مهام اكثر يتم اسنادها للمتصفح ، فى هذه الحالة نحتاج إلى طريقة يمكننا بها تحديد أولويات لهذه المهام.

وهنا يأتى دور قائمة انتظار المهام الكبيرة او ذات الاولوية القصوى "microtask queue" وقائمة انتظار المهام الصغيرة او ذات الاولوية الاقل "macrotask queue". سيأخذ المتصفح الكود البرمجى ويقوم بتنفيذه ، ثم يضع نتيجة هذا الكود في واحدة من قائمتين الانتظار بناءً على درجة اولوية الكود.

على سبيل المثال، الوعود "Promises" يتم وضع نتائجها فى قائمة المهام الكبيرة او ذات الاولوية القصوى "microtask queue".

الـEvents وsetTimeout امثلة على اكود برمجية او مهام صغيرة وذات درجة اولوية اقل ويتم وضع نتائجها فى قائمة المهام الصغيرة او ذات الاولوية الاقل "macrotask queue".

بمجرد الانتهاء من العمل ما ووصل النتائج، يتم وضعه في إحدى قائمتَي الانتظار، وفى هذه اللحظة يتم تشغيل حلقة الحدث "event loop" ذهابًا وإيابًا والتحقق مما إذا كانت جافاسكريبت جاهزه لتلقي النتائج أم لا.

عندما تنتهى جافاسكريبت من كل مهامها المتزامنة "synchronous" بالكامل ، وتكون متفرغة وجاهزة، ستبدأ حلقة الحدث "event loop" تلقائيا في الانتقاء من قوائم الانتظار وتسليم نتائج المهام الاضافية إلى جافاسكريبت لعرضها.

لتوضيح، شاهد المثال الاتى:

```
setTimeout(() => console.log("hello"), 0)

fetch("https://someapi/data").then(response => response.json())
                             .then(data => console.log(data))

console.log("What soup?")
```
ما هو ترتيب نتائج هذا الكود فى رأيك؟

1. فى المقام الاول، يتم إسناد setTimeout الى المتصفح، والذى بدوره يقوم بتنفيذ الكود ووضع نتائجه فى قائمة المهام الصغيرة او ذات الاولوية الاقل "macrotask queue".
2. ثانيا، يتم إسناد fetch الى المتصفح ايضا، والذى بدوره يقوم بتنفيذ الكود. وايضا بأستقبال البيانات من الـendpoint ووضعها فى قائمة المهام الكبيرة او ذات الاولوية الاقصى "microtask queue".
3. وبعدها يتم إظهار رسالة "?What soup".
4. فى هذه اللحظة ستبدأ حلقة الحدث "event loop" تلقائيا بتحقق ما اذا كانت جافاسكريبت جاهزة بتلاقى النتائج الاضافية من قائمة المهام.
5. بمجرد انتهاء مهمة console.log، تكون جافاسكريبت جاهزة. تبدأ حلقة الحدث "event loop" فى الانتقاء النتائج من قائمة المهام الكبيرة او ذات الاولوية الاقصى "macrotask queue"، وتعطى النتائج لجافا سكريبت لتعرضها.
6. بعد تفريغ قائمة المهام الكبيرة او ذات الاولوية الاقصى "microtask queue"، تنتقل حلقة الحدث "event loop" الى قائمة انتظار المهام الصغيرة او ذات الاولوية الاقل "macrotask queue"، وفى هذا الحالة تكون نتائج setTimeout جاهزة لتستلمها جافا سكريبت لتنفذها.
```
In console:
// What soup?
// the data from the api
// hello
```
## الوعود "Promises" فى جافاسكريبت

اخذنا فكرة جيدة عن ما هية الكود الغير متزامن "asynchronous code" وكيف يتم التعامل معه بواسطة جافاسكريبت وبيئة التشغيل "المتصفح". لان لنتطرق لموضوع جديد وهو الوعود "Promises"

الوعد "Promise" فى جافا سكريبت يمثل قيمة مجهولة سوف يتم الحصول عليها فى المستقبل "مدة زمنية". فى الاساس الوعد "Promise" هو ميثاق بينك وبين جافاسكريبت على ارجاع قيمة ما. من الممكن ان يكون طلب بيانات من API محدد، او قد يكون خطأ ناتج عن فشل فى طلب بيانات من الانترنت. فى كلا الحالتين انت بتأكيد سوف تحصل على قيمة ما.

انظر الى المثال التالى:

```
const promise = new Promise((resolve, reject) => {
	// Make a network request
   if (response.status === 200) {
      resolve(response.body)
   } else {
      const error = { ... }
      reject(error)
   }
})

promise.then(res => {
	console.log(res)
}).catch(err => {
	console.log(err)
})
```
يمكن ترجمة الوعد "promise" الى الحالات الاتية

-  وعد تم الوفاء به "fulfilled" - عمل تم تنفيذ بشكل ناجح.
-   وعد تم كسره "rejected" - عمل لم يتم تنفيذ بشكل ناجح.
-   وعد فى الانتظار "pending" - لم يتم اتخذ اى إجراء.
-   وعد مبهم "settled" - اما تم الوفاء به او تم كسره.

عند تنفيذ "promise" وعد ما يجب اما يتم الوفاء به "resolve" او يتم كسره "reject"

افتراضيا, توفر الوعود "promises" دوال "functions" ليتم تطبيق الوعد، اما يتم الوفاء به "resolve" فى حالة النجاح او يتم كسره "reject" فى حالة الفشل.

 احد مميزات الوعود "promises" هو انه يمكن عمل سلسة "chain" من الدوال "functions" للاستجابة لكل من حالة النجاج "resolve" او حالة الفشل "reject":

-  لتفعيل دالة "function" فى حالة النجاح والحصول على النتائج نستخدم then.
-  لتفعيل دالة "function" فى حالة النجاح والحصول على النتائج نستخدم catch.

شاهد المثال التالى:

```javascript
// Fetch returns a promise
fetch("https://swapi.dev/api/people/1")
	.then((res) => console.log("This function is run when the request succeeds", res)
    .catch(err => console.log("This function is run when the request fails", err)

// Chaining multiple functions
 fetch("https://swapi.dev/api/people/1")
	.then((res) => doSomethingWithResult(res))
    .then((finalResult) => console.log(finalResult))
    .catch((err => doSomethingWithErr(err))
```

ممتاز, والان لنأخذ نظرة اقرب لما يحدث خلف الكواليس، وسوف نستخدم دالة fetch فى المثال:

```javascript
const fetch = (url, options) => {
  // simplified
  return new Promise((resolve, reject) => {

  const xhr = new XMLHttpRequest()
  // ... make request
  xhr.onload = () => {
    const options = {
        status: xhr.status,
        statusText: xhr.statusText
        ...
    }

    resolve(new Response(xhr.response, options))
  }

  xhr.onerror = () => {
    reject(new TypeError("Request failed"))
  }
}

 fetch("https://swapi.dev/api/people/1")
   // Register handleResponse to run when promise resolves
	.then(handleResponse)
  .catch(handleError)

 // conceptually, the promise looks like this now:
 // { status: "pending", onsuccess: [handleResponse], onfailure: [handleError] }

 const handleResponse = (response) => {
  // handleResponse will automatically receive the response, ¨
  // because the promise resolves with a value and automatically injects into the function
   console.log(response)
 }

  const handleError = (response) => {
  // handleError will automatically receive the error, ¨
  // because the promise resolves with a value and automatically injects into the function
   console.log(response)
 }

// the promise will either resolve or reject causing it to run all of the registered functions in the respective arrays
// injecting the value. Let's inspect the happy path:

// 1. XHR event listener fires
// 2. If the request was successfull, the onload event listener triggers
// 3. The onload fires the resolve(VALUE) function with given value
// 4. Resolve triggers and schedules the functions registered with .then


```

كما شاهدنا يمكن استخدام الوعود "promises" لخلق كود غير متزامن "asynchronous"، وكيف التعامل مع نتائج الوعود. اذا اردت الاطلاع اكثر عن الوعود اقرأ عنها [هنا](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) و[هنا](https://web.dev/promises/)

عند استخدام الوعود "promises"، يمكن عمل سلسة "chain" من الدوال "functions" لتعامل مع ردود مختلفة للوعود.

هذا جيد، لكن نحتاج طريقة لتعامل مع الكود داخل نتائج الوعود "callbacks" بمجرد الحصول على النتائج. ماذا لو استطعنا استخدام الوعود ولكن فى نفس الوقت كتابة كود متزامن "synchronous" المظهر؟ اتضح أننا نستطيع ذلك.

## Async/Await

بأستخدام كل من Async/Await يمكن كتابة الـpromises بطريقة مختلفة نسبيا، حيث يمكن كتابة الـAsynchronous code بطريقة او اسلوب مشابه لـSynchronous code. دعنا نلقى نظرة.

```
const getData = async () => {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos/1")
    const data = await response.json()

    console.log(data)
}

getData()
```

لم يختلف اى شئ فى هذا المثال عن سابقه. لازالنا نستخدم الـpromises لجلب البيانات، لكن طريقة الكتابة اصبحت شبية بالـsynchronous الى حد ما، ولم نعد فى حاجة لأستخدام `then.` و `catch.`

اسلوب Async / Await هو طريقة مبسطة لكتابة كود يسهل التفكير فيه، دون تغيير الديناميكية الأساسية لمبدء الـpromises.

لنلقى نظرية كيف يعمل.

خلف الكواليس، تمكنا طريقة Async/Await من استخدام الـ[generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator) لوقف تنفيذ function ما مؤقتا. عند استخدام Async/Await لن يتوقف الكود عن العمل لان الـfunction ترجع التحكم الكامل بالكود الى البرنامح الرئيسي المسؤول عن التنفيذ.

وبعدها، عندما يتم تنفيذ الـpromise نستخدم الـgenerator مرة اخرى لاعادة التحكم مرة اخري لـasynchronous function بالاضافة الى البيانات العادة من تنفيذ الـpromise.

لمعرفة تفاصيل اكثر عن هذه المفاهيم اقرأ [هنا](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/async%20%26%20performance/ch4.md).

في الواقع ، يمكننا الآن كتابة كود asynchronous يشبه الكود synchronous. مما يسهل كتابة والتفكير فى الكود، ويمكننا استخدام try / catch لمعالجة الاخطاء المتوقعة:

```javascript
const getData = async () => {
    try {
    	const response = await fetch("https://jsonplaceholder.typicode.com/todos/1")
    	const data = await response.json()
        console.log(data)
    } catch (err) {
       console.log(err)
    }

}

getData()
```

والان. فكيف نستخدمها؟ من أجل استخدام async / await، نحتاج إضافة كلمة async الى الـfunction المراد استخدمها. هذا لا يجعل الـfunction غير متزامنة "asynchronous"، لكن يسمح لنا باستخدام كلمة await داخلها.

بدون استخدام كلمة async مع الـfunction سوف ينتج رسالة خطأ عند استخدام كلمة await داخل الـfunction.
```javascript
const getData = async () => {
	console.log("We can use await in this function")
}
```

ولهذا السبب، لا يمكن استخدام async / await مع الكود العادى. لكن async / await هى مجرد طريقة مبسطة عن استخدام الـpromises. لكن يمكن استخدام التسلسل "promise chaining" مع ناتج العائد من async / await.

```
async function getData() {
  let response = await fetch('http://apiurl.com');
}

// getData is a promise
getData().then(res => console.log(res)).catch(err => console.log(err);
```

الحقيقة المثير عن async / await. ان الـfunction المستخدم بها async / await سوف ترجع دائما promise كنتيجة.

تعمل طريقة async / await كالسحر عند استخدامك لها فى الوهلة الاولى. لكن مثل اى السحر، يزول اثره بإنكشاف اسراره. تنقنية async / await  مجرد تقنية متقدمة تقدمها جافاسكريبت، تطورت على مر السنين. نأمل الآن أن يكون لديك فهم قوي لكيفة استخدمها  واساس عملها.

# الخاتمة

اذا نجت فى الوصول الى هذه النقطة، تهاني الحارة. انت الان تملك معرفة إضافية عن جافاسكريبت وكيفية عملها فى بيئة التشغيل الخاصة بها.

هذه المواضيع مربكة للبعض احيانا، والمعلومات المتوفرة ليست واضحة دائمًا. ولكن الآن نأمل أن يكون لديك فهم حول كيفية عمل جافاسكريبت مع الـasynchronous code في المتصفح ، وفهم أقوى لكل من الـpromises و طريقة async / await.

اذا اسمتعت بهذا المقال، يمكن ان تحب [قناتى](https://www.youtube.com/channel/UCZTeUahnA2GMoo_YpTBFo9A?view_as=subscriber) على يوتيوب. حاليا لدى سلسة عن[ اساسيات الويب](https://www.youtube.com/watch?v=kmvg9C8hVa0&list=PL_kr51suci7XVVw4SJLZ0QQBAsL2K8Opy)، حيث اتحدث عن [HTTP](https://www.youtube.com/watch?v=0ykAOzJb-U8&t=19s) و[بناء خوادم الويب من البداية](https://www.youtube.com/watch?v=R5uwuG1wPR8) والكثير ايضا.

ايضا لدى سلسلة عن [بناء تطبيق ويب بأستخدام ReactJS](https://www.youtube.com/playlist?list=PL_kr51suci7WkVde-b09G4XHEWQrmzcpJ). وأخطط لإضافة المزيد من المحتوى في المستقبل بالتعمق في موضوعات جافاسكريبت

ولا تنسى متابعتى على تويتر @foseberg.

شكرا للقراء
