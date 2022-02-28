
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

[setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/setTimeout)، [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) و [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model) كلها امثلة على الـWeb APIs. (يمكن أن [ترى لائحة كاملة عن الـWeb APIs](https://developer.mozilla.org/en-US/docs/Web/API)) كلها ادوات تم دمجها داخل المتصفح "browser"، وتم جعلها متاحة لنا عند كتابة الاكواد بجافاسكريبت فى بيئة المتصفح.

ولاننا نقوم دائما بالعمل داخل بيئة عمل "environment" معينة، يخيل لنا انها جزء من اللغة. لكن هذا غير صحيح بالمرة.

لذلك اذا تسألت لماذا يمكن استخدام `fetch` فى جافاسكريبت عند العمل داخل المتصفح (لكن تحتاج تنزيل حزمة "package" معينة عند العمل ببيئة الـNodeJS)، فهذا هو السبب. شخص ما خيل له ان `fetch` فكرة جيدة، فبتالى قرر ان يبنى نظير لها فى بيئة  الـNodeJS.

لازلت لم تفهم! اجل؟

الان، فهمنا من هو المساعد المجهول لجافاسكريب، وكيف تم توظيفه للقيام بهذا العمل الاضافى عن جافا سكريبت.

اتضح أن البيئة هي التي تتولى هذا العمل الاضافى، وكيفية قيام البيئة بهذا العمل، هي استخدام الوظائف المدمجة بها. على سبيل المثال `fetch` أو `setTimeout` في بيئة المتصفح.

## What happens to the work?

Great. So the environment takes on the work. Then what?

At some point you need to get the results back. But let's think about how this would work.

Let's go back to the juggling example from the beginning. Imagine you asked for a new ball, and a friend just started throwing the ball at you when you weren't ready.

That would be a disaster. Maybe you could get lucky and catch it and get it into your routine effectively. But theres a large chance that it may cause you to drop all of your balls and crash your routine. Wouldn't it be better if you gave strict instructions on when to receive the ball?

As it turns out, there are strict rules surrounding when JavaScript can receive delegated work.

Those rules are governed by the event loop and involve the microtask and macrotask queue. Yes, I know. It's a lot. But bear with me.

![](https://www.freecodecamp.org/news/content/images/2020/08/autodraw-31_08_2020.png)

Alright. So when we delegate asynchronous code to the browser, the browser takes and runs the code and takes on that workload. But there may be multiple tasks that are given to the browser, so we need to make sure that we can prioritise these tasks.

This is where the microtask queue and the macrotask queue come in play. The browser will take the work, do it, then place the result in one of the two queues based on the type of work it receives.

Promises, for example, are placed in the microtask queue and have a higher priority.

Events and setTimeout are examples of work that is put in the macrotask queue, and have a lower priority.

Now once the work is done, and is placed in one of the two queues, the event loop will run back and forth and check whether or not JavaScript is ready to receive the results.

Only when JavaScript is done running all its synchronous code, and is good and ready, will the event loop start picking from the queues and handing the functions back to JavaScript to run.

So let's take a look at an example:

```
setTimeout(() => console.log("hello"), 0)

fetch("https://someapi/data").then(response => response.json())
                             .then(data => console.log(data))

console.log("What soup?")
```

What will the order be here?

1.  Firstly, setTimeout is delegated to the browser, which does the work and puts the resulting function in the macrotask queue.
2.  Secondly fetch is delegated to the browser, which takes the work. It retrieves the data from the endpoint and puts the resulting functions in the microtask queue.
3.  Javascript logs out "What soup"?
4.  The event loop checks whether or not JavaScript is ready to receive the results from the queued work.
5.  When the console.log is done, JavaScript is ready. The event loop picks queued functions from the microtask queue, which has a higher priority, and gives them back to JavaScript to execute.
6.  After the microtask queue is empty, the setTimeout callback is taken out of the macrotask queue and given back to JavaScript to execute.

```
In console:
// What soup?
// the data from the api
// hello
```

## Promises

Now you should have a good deal of knowledge about how asynchronous code is handled by JavaScript and the browser environment. So let's talk about promises.

A promise is a JavaScript construct that represents a future unknown value. Conceptually, a promise is just JavaScript promising to return  _a value_. It could be the result from an API call, or it could be an error object from a failed network request. You're guaranteed to get something.

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

A promise can have the following states:

-   fulfilled - action successfully completed
-   rejected - action failed
-   pending - neither action has been completed
-   settled - has been fulfilled or rejected

A promise receives a resolve and a reject function that can be called to trigger one of these states.

One of the big selling points of promises is that we can chain functions that we want to happen on success (resolve) or failure (reject):

-   To register a function to run on success we use .then
-   To register a function to run on failure we use .catch

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

Perfect. Now let's take a closer look at what this looks like under the hood, using fetch as an example:

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

So we can use promises to do asynchronous work, and to be sure that we can handle any result from those promises. That is the value proposition. If you want to know more about promises you can read more about them  [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)  and  [here](https://web.dev/promises/).

When we use promises, we chain our functions onto the promise to handle the different scenarios.

This works, but we still need to handle our logic inside callbacks (nested functions) once we get our results back. What if we could use promises but write synchronous looking code? It turns out we can.

## Async/Await

Async/Await is a way of writing promises that allows us to write  _asynchronous code in a synchronous way._ Let's have a look.

```
const getData = async () => {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos/1")
    const data = await response.json()

    console.log(data)
}

getData()
```

Nothing has changed under the hood here. We are still using promises to fetch data, but now it looks synchronous, and we no longer have .then and .catch blocks.

Async / Await is actually just syntactic sugar providing a way to create code that is easier to reason about, without changing the underlying dynamic.

Let's take a look at how it works.

Async/Await lets us use  [generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator)  to  _pause_  the execution of a function. When we are using async / await we are not blocking because the function is yielding the control back over to the main program.

Then when the promise resolves we are using the generator to yield control back to the asynchronous function with the value from the resolved promise.[](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/async%20%26%20performance/ch4.md)

[You can read more here for a great overview](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/async%20%26%20performance/ch4.md)  of generators and asynchronous code.

In effect, we can now write asynchronous code that looks like synchronous code. Which means that it is easier to reason about, and we can use synchronous tools for error handling such as try / catch:

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

Alright. So how do we use it? In order to use async / await we need to prepend the function with async. This does not make it an asynchronous function, it merely allows us to use await inside of it.

Failing to provide the async keyword will result in a syntax error when trying to use await inside a regular function.

```javascript
const getData = async () => {
	console.log("We can use await in this function")
}
```

Because of this, we can not use async / await on top level code. But async and await are still just syntactic sugar over promises. So we can handle top level cases with promise chaining:

```
async function getData() {
  let response = await fetch('http://apiurl.com');
}

// getData is a promise
getData().then(res => console.log(res)).catch(err => console.log(err);
```

This exposes another interesting fact about async / await. When defining a function as async,  _it will always return a promise._

Using async / await can seem like magic at first. But like any magic, it's just sufficiently advanced technology that has evolved over the years. Hopefully now you have a solid grasp of the fundamentals, and can use async / await with confidence.

# Conclusion

If you made it here, congrats. You just added a key piece of knowledge about JavaScript and how it works with its environments to your toolbox.

This is definitely a confusing subject, and the lines are not always clear. But now you hopefully have a grasp on how JavaScript works with asynchronous code in the browser, and a stronger grasp over both promises and async / await.

If you enjoyed this article, you might also enjoy my  [youtube channel](https://www.youtube.com/channel/UCZTeUahnA2GMoo_YpTBFo9A?view_as=subscriber). I currently have a  [web fundamentals series](https://www.youtube.com/watch?v=kmvg9C8hVa0&list=PL_kr51suci7XVVw4SJLZ0QQBAsL2K8Opy) going where I go through  [HTTP](https://www.youtube.com/watch?v=0ykAOzJb-U8&t=19s),  [building web servers from scratch](https://www.youtube.com/watch?v=R5uwuG1wPR8)  and more.

There's also a series going on  [building an entire app with React](https://www.youtube.com/playlist?list=PL_kr51suci7WkVde-b09G4XHEWQrmzcpJ), if that is your jam. And I plan to add much more content here in the future going in depth on JavaScript topics.

And if you want to say hi or chat about web development, you could always reach out to me on twitter at @foseberg. Thanks for reading!
