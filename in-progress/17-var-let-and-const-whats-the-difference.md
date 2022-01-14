
# كلمات Var, Let وConst ما الفرق؟

A lot of shiny new features came out with ES2015 (ES6). And now, since it's 2020, it's assumed that a lot of JavaScript developers have become familiar with and have started using these features.

الكثير من المميزات الجديدة أضيفت الى جافا سكريبت الاصدار الحديث "ES2015/ES6". والان بما اننا فى سنة 2020, فمن المفترض ان الكثير من مطوري جافا سكريبت اصبحوا بالغعل على دراية وثيقة بها وبدوا فى استخدمها بالفعل.

While this assumption might be partially true, it's still possible that some of these features remain a mystery to some devs.
هذا الافتراض صحيح نسبيا، لكن تظل هذه المميزات غامضة لبعض المطورين. 

One of the features that came with ES6 is the addition of  `let`  and  `const`, which can be used for variable declaration. The question is, what makes them different from good ol'  `var`  which we've been using? If you are still not clear about this, then this article is for you.

بعض هذه المميزات، هى إضافة كلمتين جديدتين `let` و`const`، حيث تستخدمان للتصريح "declare" عن متغير "variable". السؤال هنا، ما الذى يجعلهما محتلفين عن كلمة `var` القديمة؟ اذا كانت هذه الاضافات الجديدة غير واضحة لك، فهذا المقال لاجلك انت. 

In this article, we'll discuss  `var`,  `let`  and  `const`  with respect to their scope, use, and hoisting. As you read, take note of the differences between them that I'll point out.

فى هذا المقال سوف نتحدث عن `var`,  `let`  و `const` مع توضيح معنى المجال/النطاق "scope"، و المقصود بعملية الرفع "hoisting". أثناء قراءتك للمقال، لاحظ جيدا الاختلافات المشار لها التى سوف تظهر معنا. 
## Var
##  كلمة Var

Before the advent of ES6,  `var`  declarations ruled. There are issues associated with variables declared with  `var`, though. That is why it was necessary for new ways to declare variables to emerge. First, let's get to understand  `var`  more before we discuss those issues.

قبل اطلاق الاصدار السادس "ES6" من لغة جافا سكريبت، كانت كلمة `var` تستخدم للتصريح "declaration" عن متغير "variable" ولم يكن هناك بديل لها. كان توجد مشاكل تحدث بسبب استخدام كلمة `var`، بالرغم من ذلك. لذلك كان هناك حاجة لطرق جديدة للتصريح "declare" عن متغير "variable". اولا، لنفهم كلمة `var` اكثر قبل الدخول فى المشاكل التى تسببها. 

### Scope of var
### النطاق الخاص بكلمة var 
**Scope**  essentially means where these variables are available for use.  `var`  declarations are globally scoped or function/locally scoped.

**كلمة نطاق** فى لغات البرمجة تعنى المكان المتاح فيه استخدام متغيرات "variables" ما. استخدام كلمة `var` للتصريح "declare" عن متغير "variable" ما، يجعل هذا المتغير "variable" متاح اما فى النطاق العام "global scope" او فى نطاق الدالة "function scope". 

The scope is global when a  `var`  variable is declared outside a function. This means that any variable that is declared with  `var`  outside a function block is available for use in the whole window.

النطاق "scope" يدعى بالنطاق العام "global scope" عند استخدام كلمة `var`  للتصريح "declare" عن متغير "variable" ما خارج دالة "function" ما. مما يعنى ان اى متغير "variable" تم التصريح "declaration" عنه بأستخدام كلمة `var` سوف يكون متاح للاستخدام او الوصول له فى الكائن الرئيسي للمتصفح "Window object". 

`var`  is function scoped when it is declared within a function. This means that it is available and can be accessed only within that function.

يمكن استنتاج ان كلمة `var` تصريح "declare" عن متغير "variable" فى نطاق "function" دالة ما "function scoped" وبالتالي، يكون هذا المتغير "variable" متاح حصريا فى نطاق "scope" هذه الدالة "function" فقط. 

To understand further, look at the example below.

للتوضيح اكثر، انظر الى المثال التالي.

```javascript
    var greeter = "hey hi";
    
    function newFunction() {
        var hello = "hello";
    }

```

Here,  `greeter`  is globally scoped because it exists outside a function while  `hello`  is function scoped. So we cannot access the variable  `hello`  outside of a function. So if we do this:

يوجد لدينا متغير "variable"  يدعي `greeter` عامي النطاق "globally scoped"، اى انه خارج الدالة "function". بينما المتغير `hello` دالى النطاق "function scoped" لذلك لا يمكن الوصول الى المتغير `hello` خارج نطاق الدالة "function". اذ حاولنا ذلك سوف يظهر الخطأ التالي: 

```javascript
    var tester = "hey hi";
    
    function newFunction() {
        var hello = "hello";
    }
    console.log(hello); // error: hello is not defined

```

We'll get an error which is as a result of  `hello`  not being available outside the function.

سوف نحصل على الخطأ التالي كنتيجة، لان المتغير "variable" المدعو `hello` لا يمكن الوصول لخ خارج الدلة "function" لانه دالى النطاق "function scoped". 

### var variables can be re-declared and updated
### المتغيرات "variables" التى تم التصريح عنها بأستخدام كلمة var، يمكن إعادة التصريح عنها "re-declared" وتحديث قيمتها "updated" 

This means that we can do this within the same scope and won't get an error.

هذا يعني اين يمكن القيام بالاتى فى نفس النطاق "scope"، ولن تحدث مشكلة. 

```javascript
    var greeter = "hey hi";
    var greeter = "say Hello instead";

```

and this also

وهذا ايضا

```javascript
    var greeter = "hey hi";
    greeter = "say Hello instead";

```

### Hoisting of var
### عملية رفع "Hoisting" المتغيرات المصرح عنها بأستخدام كلمة var 

Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution. This means that if we do this:

المقصود بعملية الرفع "Hoisting" فى جافا سكريبت ان المتغيرات "variables" والدوال "functions" التى تم التصريح عنها بأستخدام كلمة var، يتم رفعها لاعلى النطاق "scope" الخاص بها قبل عملية التنفيذ "code execution" الفعلي للكود. ذلك يعنى اذا قمنا بالاتى: 
```javascript
    console.log (greeter);
    var greeter = "say hello"

```

it is interpreted as this:

سوف يتم تفسيرها "interpreted" كالاتى:

```javascript
    var greeter;
    console.log(greeter); // greeter is undefined
    greeter = "say hello"

```

So  `var`  variables are hoisted to the top of their scope and initialized with a value of  `undefined`.

لذلك  فى جافا سكريبت ان المتغيرات "variables" والدوال "functions" التى تم التصريح عنها بأستخدام كلمة var، يتم رفعها "hoisted" لاعلى النطاق "scope" الخاص بها ويتم تعرفها "initialized" بقيمة "value" افتراضية او مبدئية `undefined`. 

### Problem with var
### المشكلة مع استخدام كلمة var 

There's a weakness that comes with `var`. I'll use the example below to explain:

يوجد عيب عند استخدامك لكلمة `var`. سوف اوضحه بأستخدام المثال الاتى:

```javascript
    var greeter = "hey hi";
    var times = 4;

    if (times > 3) {
        var greeter = "say Hello instead"; 
    }
    
    console.log(greeter) // "say Hello instead"

```

So, since  `times > 3`  returns true,  `greeter`  is redefined to  `"say Hello instead"`. While this is not a problem if you knowingly want  `greeter`  to be redefined, it becomes a problem when you do not realize that a variable  `greeter`  has already been defined before.

لاحظ، حيث ان الشرط "condition" الخاص بـ`if` صحيح، فبتالى المتغير `greeter` سوف يتم اعادة تعريفه "redefined" ليحمل القيمة `"say Hello instead"`. بينما هذا الامر ليس بمشكلة اذا كنت على دراية به مسبقا او تريد فعلا للمتغير `greeter` ان يتم اعادة تعريفه "redefined"،فأنه سوف يتحول لمشكلة كبيرة اذا كنت لم تكن عل علم ان المتغير `greeter` تم اعادة تعريفه  "redefined" بالفعل. 

If you have used  `greeter`  in other parts of your code, you might be surprised at the output you might get. This will likely cause a lot of bugs in your code. This is why  `let`  and  `const`  are necessary.

اذا تابعت استخدامك للمتغير `greeter` فى بقية اجزاء الكود البرمجي الخاص بك، فأنك سوف تفاجأ بنتائج التى سوف تظهر. هذا بالتأكد سوف يسبب الكثير من الاخطاء "bugs" البرمجية فى الكود البرمجي الخاص بك. وهنا أهمية دور كل من `let` و `const`. 
## Let

`let`  is now preferred for variable declaration. It's no surprise as it comes as an improvement to  `var`  declarations. It also solves the problem with  `var`  that we just covered. Let's consider why this is so.

### let is block scoped

A block is a chunk of code bounded by {}. A block lives in curly braces. Anything within curly braces is a block.

So a variable declared in a block with  `let`  is only available for use within that block. Let me explain this with an example:

```javascript
   let greeting = "say Hi";
   let times = 4;

   if (times > 3) {
        let hello = "say Hello instead";
        console.log(hello);// "say Hello instead"
    }
   console.log(hello) // hello is not defined

```

We see that using  `hello`  outside its block (the curly braces where it was defined) returns an error. This is because  `let`  variables are block scoped .

### let can be updated but not re-declared.

Just like  `var`, a variable declared with  `let`  can be updated within its scope. Unlike  `var`, a  `let`  variable cannot be re-declared within its scope. So while this will work:

```javascript
    let greeting = "say Hi";
    greeting = "say Hello instead";

```

this will return an error:

```javascript
    let greeting = "say Hi";
    let greeting = "say Hello instead"; // error: Identifier 'greeting' has already been declared

```

However, if the same variable is defined in different scopes, there will be no error:

```javascript
    let greeting = "say Hi";
    if (true) {
        let greeting = "say Hello instead";
        console.log(greeting); // "say Hello instead"
    }
    console.log(greeting); // "say Hi"

```

Why is there no error? This is because both instances are treated as different variables since they have different scopes.

This fact makes  `let`  a better choice than  `var`. When using  `let`, you don't have to bother if you have used a name for a variable before as a variable exists only within its scope.

Also, since a variable cannot be declared more than once within a scope, then the problem discussed earlier that occurs with  `var`  does not happen.

### Hoisting of let

Just like `var`,  `let`  declarations are hoisted to the top. Unlike  `var`  which is initialized as  `undefined`, the  `let`  keyword is not initialized. So if you try to use a  `let`  variable before declaration, you'll get a  `Reference Error`.

## Const

Variables declared with the  `const`  maintain constant values.  `const`  declarations share some similarities with  `let`  declarations.

### const declarations are block scoped

Like  `let`  declarations,  `const`  declarations can only be accessed within the block they were declared.

### const cannot be updated or re-declared

This means that the value of a variable declared with  `const`  remains the same within its scope. It cannot be updated or re-declared. So if we declare a variable with  `const`, we can neither do this:

```javascript
    const greeting = "say Hi";
    greeting = "say Hello instead";// error: Assignment to constant variable. 

```

nor this:

```javascript
    const greeting = "say Hi";
    const greeting = "say Hello instead";// error: Identifier 'greeting' has already been declared

```

Every  `const`  declaration, therefore, must be initialized at the time of declaration.

This behavior is somehow different when it comes to objects declared with  `const`. While a  `const`  object cannot be updated, the properties of this objects can be updated. Therefore, if we declare a  `const`  object as this:

```javascript
    const greeting = {
        message: "say Hi",
        times: 4
    }

```

while we cannot do this:

```javascript
    greeting = {
        words: "Hello",
        number: "five"
    } // error:  Assignment to constant variable.

```

we can do this:

```javascript
    greeting.message = "say Hello instead";

```

This will update the value of  `greeting.message`  without returning errors.

### Hoisting of const

Just like  `let`,  `const`  declarations are hoisted to the top but are not initialized.

So just in case you missed the differences, here they are:

-   `var`  declarations are globally scoped or function scoped while  `let`  and  `const`  are block scoped.
-   `var`  variables can be updated and re-declared within its scope;  `let`  variables can be updated but not re-declared;  `const`  variables can neither be updated nor re-declared.
-   They are all hoisted to the top of their scope. But while  `var`  variables are initialized with  `undefined`,  `let`  and  `const`  variables are not initialized.
-   While  `var`  and  `let`  can be declared without being initialized,  `const`  must be initialized during declaration.

Got any question or additions? Please let me know.

Thank you for reading :)