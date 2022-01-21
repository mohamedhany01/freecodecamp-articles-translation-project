
# كلمات Var, Let وConst ما الفرق؟

الكثير من المميزات الجديدة أضيفت الى جافا سكريبت الاصدار الحديث "ES2015/ES6". والان بما اننا فى سنة 2020, فمن المفترض ان الكثير من مطوري جافا سكريبت اصبحوا بالغعل على دراية وثيقة بها وبدوا فى استخدمها بالفعل.

هذا الافتراض صحيح نسبيا، لكن تظل هذه المميزات غامضة لبعض المطورين.

بعض هذه المميزات، هى إضافة كلمتين جديدتين `let` و`const`، حيث تستخدمان للتصريح "declare" عن متغير "variable". السؤال هنا، ما الذى يجعلهما محتلفين عن كلمة `var` القديمة؟ اذا كانت هذه الاضافات الجديدة غير واضحة لك، فهذا المقال لاجلك انت.

فى هذا المقال سوف نتحدث عن `var`,  `let`  و `const` مع توضيح معنى المجال/النطاق "scope"، و المقصود بعملية الرفع "hoisting". أثناء قراءتك للمقال، لاحظ جيدا الاختلافات المشار لها التى سوف تظهر معنا.


##  كلمة Var

قبل اطلاق الاصدار السادس "ES6" من لغة جافا سكريبت، كانت كلمة `var` تستخدم للتصريح "declaration" عن متغير "variable" ولم يكن هناك بديل لها. كان توجد مشاكل تحدث بسبب استخدام كلمة `var`، بالرغم من ذلك. لذلك كان هناك حاجة لطرق جديدة للتصريح "declare" عن متغير "variable". اولا، لنفهم كلمة `var` اكثر قبل الدخول فى المشاكل التى تسببها.


### النطاق الخاص بكلمة var

**كلمة نطاق** فى لغات البرمجة تعنى المكان المتاح فيه استخدام متغيرات "variables" ما. استخدام كلمة `var` للتصريح "declare" عن متغير "variable" ما، يجعل هذا المتغير "variable" متاح اما فى النطاق العام "global scope" او فى نطاق الدالة "function scope".

النطاق "scope" يدعى بالنطاق العام "global scope" عند استخدام كلمة `var`  للتصريح "declare" عن متغير "variable" ما خارج دالة "function" ما. مما يعنى ان اى متغير "variable" تم التصريح "declaration" عنه بأستخدام كلمة `var` سوف يكون متاح للاستخدام او الوصول له فى الكائن الرئيسي للمتصفح "Window object".

يمكن استنتاج ان كلمة `var` تصريح "declare" عن متغير "variable" فى نطاق "function" دالة ما "function scoped" وبالتالي، يكون هذا المتغير "variable" متاح حصريا فى نطاق "scope" هذه الدالة "function" فقط.

للتوضيح اكثر، انظر الى المثال التالي.

```javascript
    var greeter = "hey hi";

    function newFunction() {
        var hello = "hello";
    }

```

يوجد لدينا متغير "variable"  يدعي `greeter` عامي النطاق "globally scoped"، اى انه خارج الدالة "function". بينما المتغير `hello` دالى النطاق "function scoped" لذلك لا يمكن الوصول الى المتغير `hello` خارج نطاق الدالة "function". اذ حاولنا ذلك سوف يظهر الخطأ التالي:

```javascript
    var tester = "hey hi";

    function newFunction() {
        var hello = "hello";
    }
    console.log(hello); // error: hello is not defined

```

سوف نحصل على الخطأ التالي كنتيجة، لان المتغير "variable" المدعو `hello` لا يمكن الوصول لخارج الدلة "function" لانه دالى النطاق "function scoped".


### المتغيرات "variables" التى تم التصريح عنها بأستخدام كلمة var، يمكن إعادة التصريح عنها "re-declared" وتحديث قيمتها "updated"


هذا يعني اين يمكن القيام بالاتى فى نفس النطاق "scope"، ولن تحدث مشكلة.

```javascript
    var greeter = "hey hi";
    var greeter = "say Hello instead";

```

وهذا ايضا

```javascript
    var greeter = "hey hi";
    greeter = "say Hello instead";

```


### عملية رفع "Hoisting" المتغيرات المصرح عنها بأستخدام كلمة var

المقصود بعملية الرفع "Hoisting" فى جافا سكريبت ان المتغيرات "variables" والدوال "functions" التى تم التصريح عنها بأستخدام كلمة var، يتم رفعها لاعلى النطاق "scope" الخاص بها قبل عملية التنفيذ "code execution" الفعلي للكود. ذلك يعنى اذا قمنا بالاتى:
```javascript
    console.log (greeter);
    var greeter = "say hello"

```

سوف يتم تفسيرها "interpreted" كالاتى:

```javascript
    var greeter;
    console.log(greeter); // greeter is undefined
    greeter = "say hello"

```

لذلك  فى جافا سكريبت ان المتغيرات "variables" والدوال "functions" التى تم التصريح عنها بأستخدام كلمة var، يتم رفعها "hoisted" لاعلى النطاق "scope" الخاص بها ويتم تعرفها "initialized" بقيمة "value" افتراضية او مبدئية `undefined`.


### المشكلة مع استخدام كلمة var

يوجد عيب عند استخدامك لكلمة `var`. سوف اوضحه بأستخدام المثال الاتى:

```javascript
    var greeter = "hey hi";
    var times = 4;

    if (times > 3) {
        var greeter = "say Hello instead";
    }

    console.log(greeter) // "say Hello instead"

```

لاحظ، حيث ان الشرط "condition" الخاص بـ`if` صحيح، فبتالى المتغير `greeter` سوف يتم اعادة تعريفه "redefined" ليحمل القيمة `"say Hello instead"`. بينما هذا الامر ليس بمشكلة اذا كنت على دراية به مسبقا او تريد فعلا للمتغير `greeter` ان يتم اعادة تعريفه "redefined"،فأنه سوف يتحول لمشكلة كبيرة اذا كنت لم تكن عل علم ان المتغير `greeter` تم اعادة تعريفه  "redefined" بالفعل.

اذا تابعت استخدامك للمتغير `greeter` فى بقية اجزاء الكود البرمجي الخاص بك، فأنك سوف تفاجأ بنتائج التى سوف تظهر. هذا بالتأكد سوف يسبب الكثير من الاخطاء "bugs" البرمجية فى الكود البرمجي الخاص بك. وهنا أهمية دور كل من `let` و `const`.


## كلمة Let

للتصريح عن متغير جديد "variable declaration" فالافضل استخدام كلمة "let" . لانها تعتبر الان تحسين لكلمة `var` . بالاضافة لحلها للمشكلة السابق شرحها. لنتكتشف لماذا.


## كلمة Let كتلة النطاق "block scoped"

بالمقصد بكتلة "block" فى لغات البرمجة هو مجموعة من الاكواد البرمجية المحصورة فى ما مكان ما "bounded" وغالبا فى الجافا سكريبت تكون محاطة بـ `{}` اقواس معقوفة "curly braces" وبالتالى اى مجموعة من الاكواد المصحورة بين  اقواس معقوفة "curly braces" فهى كتلة برمجية "block".

اذا المتغير المصرح به "variable declared" بأستخدام كلمة `let`، متاح استخدامه فقط فى هذه الكتلة البرمجية "block". لنوضح ذلك بمثال:


```javascript
   let greeting = "say Hi";
   let times = 4;

   if (times > 3) {
        let hello = "say Hello instead";
        console.log(hello);// "say Hello instead"
    }
   console.log(hello) // hello is not defined

```

نحن نلاحظ ان استخدام المتغير `hello` خارج النطاق الكتلى "block scoped" الخاص به (المكان المعرف فيه بين  اقواس معقوفة "curly braces") يظهر لنا رسالة خطأ. نتيجة لان  المتغيرات المصرح بها بأستخدام `let` كتلة النطاق "block scoped".


### يمكن تحديث "updated" قيمة المتغيرات الخاصه بـ let، ولكن لا يمكن إعادة التصريح "re-declared" بها مرة اخرى


مثل استخدام `var`، المتغير المصرح به من قبل `let` يمكن تحديثه "تغير قيمته" فى نطاقه الكتلى "block scope". لكن لا يمكن إعادة التصريح "re-declared" به مرة اخرى مثل `var`:


```javascript
    let greeting = "say Hi";
    greeting = "say Hello instead";

```

سوف يظهر هذا الممثال رسالة خطأ

```javascript
    let greeting = "say Hi";
    let greeting = "say Hello instead"; // error: Identifier 'greeting' has already been declared

```

على الرغم من ذلك،  اذا تم تعريف "defined" بنفس المتغير فى نطاق كتلى "block scope" مختلف، فلا يوجد مشكلة:

```javascript
    let greeting = "say Hi";
    if (true) {
        let greeting = "say Hello instead";
        console.log(greeting); // "say Hello instead"
    }
    console.log(greeting); // "say Hi"

```

لماذا لا يوجد مشكلة؟ لان كل من المتغيرين يتم التعامل معه على حدة، لأن لديهم نطاقات "scopes" مختلفة.

الحقيقة التى تجعل من `let` افضل خيار من `var`، هى انه لا داعي للقلق إذا كنت قد استخدمت مسبقا اسمًا لمتغير من قبل لأن المتغير موجود فقط في نطاقه الخاص به.

ايضا، نظرًا لأنه لا يمكن التصريح  "declared" عن متغير أكثر من مرة داخل نطاق "scope" ما ، فإن المشكلة التي تمت مناقشتها مسبقًا والتي تحدث مع `var` لن تحدث مع `let`.


###  عملية رفع "Hoisting" متغيرات let

مثل `var`، المتغيرات المصرح بها "declarations" بأستخدام `let` يتم رفعها "hoisted" الى اعلى . لكن على عكس `var` لا يتم تعريف المتغيرات واعطائها قيمة افتراضية `undefined`. وكنتيجة اذا استخدمت متغير خاص بـ`let` قبل التصريح به "declaration"، سوف تصل على رسالة خطأ مرجع خاطئ `Reference Error` .


## كلمة Const

المتغيرات التى يتم التصريح بها بأستخدام `const` تحمل دائما قيم ثابتة "constant values" لا يمكن تغيرها. تتشارك المتغيرات الخاصه بـ`const` بعض التشابهات مع متغيرات `let`.


## متغيرات const كتلة النطاق "block scoped"

مثل متغيرات `let`، متغيرات  `const` يمكن الوصول لها فقط داخل النطاق  "block" الخاص بها.


###  لا يمكن تحديث "updated" قيمة المتغيرات الخاصه بـ const ولا يمكن إعادة التصريح "re-declared" بها مرة اخرى


هذا يعنى ان المتغيرات التى تم التصريح بها بأستخدام `const` تبقى كما هى فى نطاقها "scope". لا يمكن تحديث قيمتها ولا إعادة التصريح بها مرة اخري. لا يمكن تحديثها:

```javascript
    const greeting = "say Hi";
    greeting = "say Hello instead";// error: Assignment to constant variable.

```

ولا يمكن إعادة التصريح بها:

```javascript
    const greeting = "say Hi";
    const greeting = "say Hello instead";// error: Identifier 'greeting' has already been declared

```

كل تصريح بأستخدام `const` يتم تهيئته "initialized" فقط وقت التصريح "declaration".


هذا التأثير مختلف عند التعامل مع الكائنات "objects" عند التصريح بها بأستخدام `const`. بينما لا يمكن تحديث مرجع "reference" الكائن "object" نفسه، يمكن تحديث خصائص "properties" الكائن  بكل سهولة. وبالتالى اذا كان لدينا كائن  "object" كالاتى:

```javascript
    const greeting = {
        message: "say Hi",
        times: 4
    }

```

لا يمكن تحديث مرجع الكائن "object reference":

```javascript
    greeting = {
        words: "Hello",
        number: "five"
    } // error:  Assignment to constant variable.

```

لكن يمكن تحديث خصائص "properties" الكائن:

```javascript
    greeting.message = "say Hello instead";

```


وكنتيجة، الكود السابق سوف يحدث قيمة الخاصية  `greeting.message` بدون مشاكل.

###  عملية رفع "Hoisting" متغيرات const

مثل `let`، المتغيرات المصرح بها "declarations" بأستخدام `const` يتم رفعها "hoisted" الى اعلى . لكن  لا يتم تعريف المتغيرات.

و فى حالة نسيت بالاختلافات السابقة، يمكن تلخصها كالاتي:

- متغيرات `var` يمكن ان تكون عامية النطاق "globally scoped" او دالية النطاق "function scoped"، بينما `let`  و  `const` كتلية النطاق "block scoped".
-  متغيرات `var` يمكن تحديثها وإعادة التصريح بها فقط فى النطاق المحددة به; متغيرات `let` يمكن تحديثها وإعادة التصريح ايضا; متغيرات `const` لا يمكن تحديثها و ولا إعادة التصريح بها.
- كل من `let`، `const` و `var` يتم رفعهم لاعلى النطاق الخاص بهم. لكن متغيرات `var` تأخذ قيمة افتراضية `undefined`، بينما  مع `let`، `const` لا يحدث ذلك.
-   بينما يمكن التصريح بمتغيرات بأستخدام `var` و  `let` بدون إعطائهم قيمة مبدئية "initialized"، متغيرات `const` يجب ان يتم  إعطائها قيمة مبدئية "initialized".

اذا كان لديك أستفسار او اضافة، سوف اكون سعيد بها.

شكرا للقراءة :)
