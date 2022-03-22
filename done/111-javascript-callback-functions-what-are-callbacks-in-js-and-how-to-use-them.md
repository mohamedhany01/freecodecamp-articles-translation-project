

# الدوال المتوالية "Callback Functions" فى جافاسكريبت - ماهى وكيف تستخدمها

اذا كنت على علم بأساسيات البرمجة، فأنت بالفعل على علم مسبق بماهية الدوال "functions" وكيف تستخدمهم. لكن ماهى الـ"Callback Functions"؟ الـ"Callback Functions" مبدأ مهم من لغة جافاسكريبت بمجرد فهم كيفية عملها، سوف يتحسن مستواك بالتأكيد فى جافاسكريبت

فى هذا المقال، سوف اساعدك على فهم الـ"Callback Functions" وكيفية استخدمها فى جافاسكريبت من خلال امثلة توضيحة.

## ماهى الـ"Callback Functions"؟
فى جافا سكريبت، الـfunctions هى كائنات "objects". ومن خواص الـobjects انه يمكن تمرريها للـfunctions كـparameters

وسبب هذه الخاصية يمكن تمرر الـfunctions كـparameters لـfunctions اخرى وعمل تنفيذ للـfunctions المررة داخل الـfunction الحاوية لهم. هل يبدو الامر معقد قليلا؟ لنشاهد مثال للتوضيح:

```javascript
function print(callback) {
    callback();
}
```
دالة الـ()print هنا تأخذ function كـparameter وتقوم بتنفيذها داخلها. هذه الطريقة صحيحة فى عالم جافاسكريبت وهذا ما يسمى بالـcallback. اذا الـfunction التى تم تمررها لـfunction اخرى كـparameter تدعى بالـcallback function. لكن ليس هذا كل شئ.

**يمكنك أيضًا مشاهدة الفيديو الخاص ب بالـcallback function بالاسفل:**

### لما الحاجة للـCallback Functions؟
تقوم جافاسكريبت بتشغيل الاكواد البرمجية بالتتابع اى بترتيب من أعلى إلى أسفل. ومع ذلك ، هناك بعض الحالات التي يتم فيها تشغيل الكود (أو يجب تشغيله) بعد حدوث شيء آخر وليس بشكل تسلسلي. وهذا ما يسمى بالبرمجة غير المتزامنة "asynchronous programming".

تحرص الـCallbacks من أن الـfunctions لن تعمل قبل اكتمال المهمة ولكنها ستعمل مباشرة بعد اكتمال المهمة. وبالتالى تساعد هذه الخاصية فى كتابة اكواد جافاسكريبت غير متزامن "asynchronous" وتبقينا في مأمن من المشاكل والأخطاء.

في جافاسكريبت ، يمكن إنشاء callback function بتمريرها كـparameters لـfunctions أخرى، ثم إعادة استدعائها بعد حدوث شيء ما أو اكتمال بعض المهام. دعونا نرى كيف...

## طريقة إنشاء الـCallback
لفهم ما شرحته أعلاه ، اسمحوا لي أن أبدأ بمثال بسيط. نريد طباعة رسالة فى وحدة التحكم الخاصة بالمتصفح "console" ولكن يجب أن يكون هناك فارق قدره 3 ثوانٍ لتظهر هذه الرسالة.

```javascript
const message = function() {
    console.log("This message is shown after 3 seconds");
}

setTimeout(message, 3000);
```

هناك method جاهزة يمكنها فعل ذلك في جافاسكريبت تدعى "setTimeout" ، والتي تستدعي/تنفذ function ما بعد فترة زمنية محددة (بالمللي ثانية). وفى مثالنا السابق ، سوف يتم استدعاء الـfunction التى تحمل الرسالة بعد مرور 3 ثوانٍ. (ثانية واحدة = 1000 مللي ثانية).

بمعنى آخر، سوف يتم استدعاء الـfunction التى تحمل الرسالة بعد حدوث شيء ما (فى حالتنا هذه، بعد مرور 3 ثوانٍ) ، ولكن ليس قبل ذلك. لذا فإن الـfunction التى تحمل الرسالة "المثال السابق" هي مثال صريح على الـcallback function.

### ما هى الدالة المجهولة "Anonymous Function"؟
بطريقة اخرى، يمكننا كتابة دالة بدون اسم "anonymous function" مباشرا داخل "setTimeout" كالاتي:
```javascript
setTimeout(function() {
    console.log("This message is shown after 3 seconds");
}, 3000);
```

كما نرى، لا يوجد اسم للـcallback function هنا ، ويُطلق على كتابة الـfunction بهذه الطريقة "بدون اسم" في جافاسكريبت لفظ “anonymous function”. وهذا ما فعلناه في المثال السابق.

### الـCallback بطريقة الـArrow Function
اذا اردت، يمكنك أيضًا كتابة نفس الـcallback function بطريقة الدلة ذات السهم "arrow function" فى اصدار جافاسكريبت الحديث ES6 كالاتى:

```javascript
setTimeout(() => {
    console.log("This message is shown after 3 seconds");
}, 3000);
```
## ماذا عن الاحداث "Events"؟
جافاسكريبت لغة برمجة تعتمد على الأحداث بشكل كبير "event-driven programming language". يمكن استخدام الـcallback function أيضًا للتعامل مع الـevents. على سبيل المثال ، لنفترض أننا نريد أن ينقر المستخدمون على الزر فى المثال الاتى:
```html
<button id="callback-btn">Click here</button>
```
سوف تظهر هذه الرسالة على الـconsole فقط عندما يتفاعل المستخدم على الزر بالنقر "click":

```javascript
document.queryselector("#callback-btn")
    .addEventListener("click", function() {
      console.log("User has clicked on the button!");
});
```
هنا نقتنص الزر بأستخدام معرفه "id"، ثم نضيف مستمع للحدث باستخدام الـaddEventListener. نريد هنا تمرر شيئان. الأول نوع الحدث، وفى حالتنا هنا نريد حدث الـ"click" ، والثاني هو الـcallback function المراد تنفيذها عند حدوث الحدث.

وكما نري، الـcallback functions ذات اهمية كبيرة عند التعامل مع الـevents فى جافاسكريبت

## خاتمة
راينا اهمية الـCallbacks فى جافاسكريبت، اتنمى ان يكون هذا المقال اوضح ماهية الـCallbacks وكيفية عملهم بطريقة سهلة. التالى، يمكن ان تلقى نظرة على [JavaScript Promises](https://www.freecodecamp.org/news/javascript-es6-promises-for-beginners-resolve-reject-and-chaining-explained/) اذا اردت ذلك.

**اذا ارت المزيد من المواضيع عن تطوير الويب، يمكن متابعة [**قناتى على يوتيوب**](https://www.youtube.com/channel/UC1EgYPCvKCXFn8HlpoJwY3Q)**

شكرا للقراءة!
