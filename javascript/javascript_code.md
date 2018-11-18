1.  Реализация функции bind
    ```javascript
    Function.prototype.bind = function (self, ...arg) {
        return (...s) => {
            return this.call(self, ...arg.concat(s));
        };
    };
    ```
2. Тип объекта
    ```javascript
    Object.prototype.toString.call([1,2,3]) // [object Array]

    function type(value) {
        let regex = /^\[object (\S+?)\]$/;
        let matches = Object.prototype.toString.call(value).match(regex) || [];

        return (matches[1] || 'undefined').toLowerCase();
    }

    function getTag(any) {
        if (typeof any === 'object' && any !== null) {
            if (typeof any[Symbol.toStringTag] === 'string') {
                return any[Symbol.toStringTag];
            }
            if (typeof any.constructor === 'function' 
                    && typeof any.constructor.name === 'string') {
                return any.constructor.name;
            }
        }
        return Object.prototype.toString.call(any).match(/\[object\s(\w+)]/)[1];
        /*
        let kitten = {
            [Symbol.toStringTag]: 'Kitten'
        };
        getTag(kitten); //"Kitten"
        class Cat {
            get [Symbol.toStringTag]() {
                return 'Cat';
            }
        }
        function Dog(){}
        Dog.prototype[Symbol.toStringTag] = 'Dog';

        //Set, Map, Date или Error: Применение getTag к ним вернет "Function", потому что это и есть функции — конструкторы итерируемых коллекций, даты и ошибки. От экземпляров мы получим соответственно — "Set", "Map", "Date" и "Error".
        */
    }

    _isArray = (function() { 
        //works around issues in iframe environments where the Array global isn't shared, thus if the object originates in a different window/iframe, "(obj instanceof Array)" will evaluate false. We added some speed optimizations to avoid Object.prototype.toString.call() unless it's absolutely necessary because it's VERY slow (like 20x slower)
        let toString = Object.prototype.toString,
            array = toString.call([]);
        return function(obj) {
            return obj != null && (obj instanceof Array || (typeof(obj) === "object" && !!obj.push && toString.call(obj) === array));
        };
    }())
    ```
3. Автоупаковка (autoboxing). Когда вы пытаетесь вызвать свойство или метод для определенных примитивных типов, JavaScript преобразует его во временный объект-оболочку и получает доступ к его свойству или методу, не затрагивая сам оригинал.
    ```javascript
    const pet = new String("dog")
    pet.constructor === String; // true
    const foo = "bar";
    foo.length; // 3
    ```
4. Creates a base-64 encoded ASCII string from a "string" of binary data.
    ```javascript
    let encodedData = window.btoa("Hello, world"); // encode a string
    let decodedData = window.atob(encodedData); // decode the string
    ```
5. Неявное приведение типов
    * to String (Любые простые типы, кроме Symbol)
        ```javascript
        String(123) // явное преобразование
        123 + ''    // неявное преобразование
        ```
    * to Boolean (Boolean(v) === false, где v - '',0,-0,NaN,null,undefined,false)
        ```javascript
        Boolean(2)          // явное преобразование
        if (2) { ... }      // неявное преобразование в логическом контексте
        !!2                 // неявное преобразование логическим оператором
        2 || 'hello'        // неявное преобразование логическим оператором
        ```
        операторы, вроде || и && выполняют преобразование значений к логическому типу для внутренних целей, а возвращают значения исходных операндов, даже если они не являются логическими.
        ```javascript
        // это выражение возвращает число 123, а не true
        // 'hello' и 123 неявно преобразуются к логическому типу при работе оператора && для вычисления значения выражения
        let x = 'hello' && 123;   // x === 123
        ```
    * to Number, Преобразование к типу Number выполняют следующие операторы: 
        * `>, <, <=, >=`
        * Побитовые операторы `|, &, ^, ~`
        * `-, +, *, /, %`, оператор `+` не вызывает неявное преобразование к числовому типу, если хотя бы один оператор является строкой
        * Унарный оператор `+`
        * `==` (а также `!=`), если оба операнда НЕ являются строками
        ```javascript
        Number('123')   // явное преобразование
        +'123'          // неявное преобразование
        123 != '456'    // неявное преобразование
        4 > '5'         // неявное преобразование
        5/null          // неявное преобразование
        true | 0        // неявное преобразование
        ```
        null преобразуется в 0, в то время как undefined превращается в NaN
        Кроме Symbol
        При применении оператора == к null или undefined преобразования в число не производится. Значение null равно только null или undefined и не равно ничему больше
        Значение NaN не равно ничему, включая себя
6. Глубокое клонирование объектов
    ```javascript
    class StructuredCloner {
    constructor() {
        this.pendingClones_ = new Map();
        this.nextKey_ = 0;

        const channel = new MessageChannel();
        this.inPort_ = channel.port1;
        this.outPort_ = channel.port2;

        this.outPort_.onmessage = ({data: {key, value}}) => {
        const resolve = this.pendingClones_.get(key);
        resolve(value);
        this.pendingClones_.delete(key);
        };
        this.outPort_.start();
    }

    cloneAsync(value) {
        return new Promise(resolve => {
        const key = this.nextKey_++;
        this.pendingClones_.set(key, resolve);
        this.inPort_.postMessage({key, value});
        });
    }
    }

    const structuredCloneAsync = window.structuredCloneAsync =
        StructuredCloner.prototype.cloneAsync.bind(new StructuredCloner);


    const main = async () => {
    const original = { date: new Date(), number: Math.random() };
    original.self = original;

    const clone = await structuredCloneAsync(original);

    // different objects:
    console.assert(original !== clone);
    console.assert(original.date !== clone.date);

    // cyclical:
    console.assert(original.self === original);
    console.assert(clone.self === clone);

    // equivalent values:
    console.assert(original.number === clone.number);
    console.assert(Number(original.date) === Number(clone.date));

    console.log("Assertions complete.");
    };

    main();
    ```
    Через history API (медленно)
    ```javascript
    const structuredClone = obj => {
        const oldState = history.state;
        history.replaceState(obj, null);
        const clonedObj = history.state;
        history.replaceState(oldState, null);
        return clonedObj;
    };
    ```
7. String to array
    ```javascript
    const name = "Test text";
    const map = Array.prototype.map;

    const newName = map.call(name, eachLetter => {
        return `${eachLetter}`
    });
    ```
8. Create array length n
    ```javascript
    Array.apply(null, {length: N}).map(Number.call, Number);
    Array.apply(null, {length: N}).map((_, i) => i);
    Array.from(Array(10).keys());
    [...Array(10).keys()];
    Array.from({length: N}, (v, k) => k+1);
    Array(N).fill().map((e,i)=>i);
    ```
9. Замена небезопасных символов
    ```javascript
    str = str.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    ```