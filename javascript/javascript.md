# From reading
1. Метки (Не советуют использовать, лучшим решением будет улучшение алгоритма)
    ```javascript
    top:
    for (i = 0; i < items.length; i++){
    for (j = 0; j < tests.length; j++)
        if (!tests[j].pass(items[i]))
            continue top;

    labl: {
        break labl;
    }
    ```
2. Spread оператора для хэшей и массивов
    ```javascript
    const propName = 'default',
        anotherHash = {
            test: 2
        },
        props = {
           name: 'test',
            [propName]: 1,
            ...anotherHash
        };
    ```
4. BigInt 1n, 2n...
5. Для своих объектов определять функцию `toString`
6. Использовать оператор строго равенства `===` и явное приведение типов
7. Кастомное преобразование типов для своего объекта
    ```javascript
    class Disk {
        constructor(capacity){
            this.capacity = capacity;
        }

        [Symbol.toPrimitive](hint){
            switch (hint) {
            case 'string':
                return 'Capacity: ' + this.capacity + ' bytes';

            case 'number':
                // преобразование в KiB
                return this.capacity / 1024;

            default:
                // считаем преобразование в число стандартным
                return this.capacity / 1024;
            }
        }
    }

    // 1MiB диск
    let disk = new Disk(1024 * 1024);

    console.log(String(disk))  // Capacity: 1048576 bytes
    console.log(disk + '')     // '1024'
    console.log(+disk);        // 1024
    console.log(disk > 1000);  // true
    ```
8. Задавать тип объекта
    ```javascript
    let kitten = {
            [Symbol.toStringTag]: 'Kitten'
        };
    getTag(kitten); //"Kitten"
    ///
    class Cat {
        get [Symbol.toStringTag]() {
            return 'Cat';
        }
    }
    ///
    function Dog(){}
    Dog.prototype[Symbol.toStringTag] = 'Dog';
    ```
9. Console:
    ```javascript
    console.log('I like %s but I do not like %s.', 'Skittles', 'pus');// %o - object, %s - string, %d - number
    console.log('%cHello', 'color: white; background-color: orange; padding: 2px 5px; border-radius: 2px');
    console.dir() // or dir at console
    console.warn()
    console.table([{
        id: "7cb1-e041b126-f3b8",
        seller: "WAL0412",
        buyer: "WAL3023",
        price: 203450,
        time: 1539688433
        },
        {
        id: "1d4c-31f8f14b-1571",
        seller: "WAL0452",
        buyer: "WAL3023",
        price: 348299,
        time: 1539688433
        },
        {
        id: "b12c-b3adf58f-809f",
        seller: "WAL0012",
        buyer: "WAL2025",
        price: 59240,
        time: 1539688433
    }])
    console.assert(5 == 4, 'Error');
    console.count('prime'); // console.countReset()
    console.trace();
    console.time('slowFunction'); // console.timeEnd('slowFunction');
    console.group('Group'); // console.log(1); console.groupEnd();
    $_ - результат предыдущего выполнения в консоли
    $0 - $4 - список последних выделенных элементов
    setTimeout(function(){debugger; }, 3000) - к примеру можно навести на элемент, который исчезает, когда сработает дебагер - можно будет изучить его детально не боясь что он исчезнет
    ```
10. Promises
    ```javascript
    const promise = new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(); // Change status to 'fulfilled'
        }, 2000);
    })
    promise.then(onSuccess)
        .catch(onError)
        .finally(onFinally);
    Promise.all(iterable);
    Promise.race(iterable);//выполнено или отклонено с результатом исполнения первого выполненного или отклонённого итерируемого обещания
    Promise.reject(reason);
    Promise.resolve(value);
    ```
11. Async Await
    ```javascript
    async function add1(x) {
        const a = await resolveAfter2Seconds(20);
        const b = await resolveAfter2Seconds(30);
        return x + a + b;
    }

    add1(10).then(v => {
        console.log(v);  // prints 60 after 4 seconds.
    });

    async function add2(x) {
        const a = resolveAfter2Seconds(20);
        const b = resolveAfter2Seconds(30);
        return x + await a + await b;
    }
    ```
12. Значение по умолчанию
    ```javascript
    (a, b = 0.7) => a + b;
    ```
13. Map/WeakMap(каждый ключ объект), Set/WeakSet
    ```javascript
    let myMap = new Map();
    let keyFunc = function() {};
    myMap.set(keyFunc, "значение, связанное с keyFunc");
    myMap.get(keyFunc);
    let mySet = new Set([1, 1, 2, 2, 3, 3]); //1,2,3
    ```
14. Classes
    ```javascript
    class Task extends Parent {
        constructor() { super(); }

        showId() { }

        static loadAll() { }
    }
    ```
15. Итераторы
    ```javascript
    let arr = [11,12,13];
    let itr = arr[Symbol.iterator]();
    itr.next(); // { value: 11, done: false }
    ```
16. Генераторы
    ```javascript
    function *infiniteNumbers() {
        var n = 1;
        while (true) {
            yield n++;
        }
    }

    var numbers = infiniteNumbers(); // возвращает перебираемый объект

    numbers.next(); // { value: 1, done: false }
    numbers.next(); // { value: 2, done: false }
    numbers.next(); // { value: 3, done: false }
    ```
17. Void
    ```javascript
    void(0);// undefined
    void function () {} ();
    void async function() {}();
    ```
18. Запятая - возвращается последний операнд
19. Array
    ```javascript
    [1, 2, 3, 4, 5].copyWithin(0, 3); // [4, 5, 3, 4, 5]
    Array.reduceRight(); // reduce с конца
    Array.reverse(); // обратный порядок массива
    Array.lastIndexOf(); // индекс последнего вхождения
    Array.from(arrayLike[, mapFn[, thisArg]]); // создание массива из итерируемых объектов
    arr.entries(); // итератор по парам ключ/значение
    Array(3).fill(4);// [4, 4, 4], arr.fill(value[, start = 0[, end = this.length]])
    arr.find(callback[, thisArg]); // возвращает первй элемент подходящий под условие
    arr.findIndex(callback[, thisArg]); //возвращает индекс первого элемента подходящего под условие
    arr.includes(searchElement[, fromIndex = 0]); // проверка на вхождение элемента
    arr.keys(); // итератор по индексам массива
    arr.values(); // итератор по значениям массива
    // экспериментальные
    var newArray = arr.flat(depth); // уменьшение глубины массива, flatMap
    ```
20. window.setTimeout(func, [, delay, param1, param2, ...]);
21. HTMLElement.dataset - доступ к атрибутам элемента
22. Строки
    ```javascript
    String.prototype.charAt();
    String.prototype.charCodeAt();
    str.endsWith(searchString[, position]);
    str.includes(searchString[, position]);
    str.repeat(count);
    str.startsWith(searchString[, position]);
    str.substr(start[, length]);
    str.substring(indexA[, indexB]);
    str.trim(); //trimLeft(), trimRight()
    // experiment
    'abc'.padEnd(10, "foo");  // "abcfoofoof", padStart
    ```
23. Object
    - `Object.freeze`
24. Контекст выполнения - окружение, в котором производится выполнение кода на JavaScript
    - Глобальный
    - Функции
    - Функции eval  

    Стадии создания:
    - Определяется значение this и осуществляется привязка this (this binding).
    - Создаётся компонент LexicalEnvironment (лексическое окружение).
    - Создаётся компонент VariableEnvironment (окружение переменных).

    В контексте выполнения функции значение this зависит от того, как именно была вызвана функция. Если она вызвана в виде метода объекта, тогда значение this привязано к этому объекту. В других случаях this привязывается к глобальному объекту или устанавливается в undefined (в строгом режиме).
    
    Стек выполнения (execution stack), стек вызовов (call stack) - LIFO-стек, который используется для хранения контекстов выполнения, создаваемых в ходе работы кода.
    
    Лексическое окружение - состоит из записи окружения (Environment Record) и ссылки на внешнее лексическое окружение, которая может принимать значение null.
    - Глобальное окружение (Ссылка глобального окружения на внешнее окружение представлена значением null)
    - Окружение функции
    
    Окружение переменных (Variable Environment) - В ES6 существует одно различие между компонентами LexicalEnvironment и VariableEnvironment. Оно заключается в том, что первое используется для хранения объявлений функций и переменных, объявленных с помощью ключевых слов let и const, а второе — только для хранения привязок переменных, объявленных с использованием ключевого слова var.
25. Hoisting - всплытие.
26. Web worker
    ```javascript
    const myWorker = new Worker('worker.js');
    myWorker.postMessage('Hello!');
    myWorker.onmessage = function(e) {
        console.log(e.data);
    }
    // worker
    self.onmessage = function(e) {
        console.log(e.data);

        // Send message to main file
        self.postMessage(workerResult);
    }
    ```
27. Service workers
    ```javascript
    navigator.serviceWorker.register('/service-worker.js');
    /* service-worker.js */

    // Install, activate, fetch (Listen for network requests from the main document)
    self.addEventListener('fetch', function(event) {
        event.respondWith(
            caches.match(event.request);
        );
    });
    ```
28. Обработка ошибок
    ```javascript
    throw new Error('something went wrong'); 
    const myError = new Error('please improve your code'); // myError.message, myError.stack
    try { } catch (err) { } finally { }
    Promise.resolve(1).catch((err) => {});
    ```

# Patterns
1. Паттерн Ice Factory
    ```javascript
    export default function makeShoppingCart({db}) {
        return Object.freeze({
            addProduct,
            empty,
            getProducts,
            removeProduct,
            // другие
        })
        function addProduct (product) {
            db.push(product)
        }
        
        function empty () {
            db = []
        }
        function getProducts () {
            return Object
            .freeze(db)
        }
        function removeProduct (id) {
            // удалить товар
        }
        // другие функции
    }
    // someOtherModule.js
    const db = []
    const cart = makeShoppingCart({ db })
    cart.addProduct({ 
        name: 'foo', 
        price: 9.99
    })
    ```
2. [Декораторы](https://tproger.ru/translations/decorators-with-factory-functions/)
    ```javascript
    function logDuration(fn) {
        return function decorator(...args) {
            let start = Date.now();
            let result = fn.apply(this, args);
            let duration = Date.now() - start;
            console.log(fn.name + "() duration : " + duration);
            return result;
        }
    }
    function createAuthorizeDecorator(currentUser) {
        return function authorize(fn) {
            return function decorator(...args) {
            if (currentUser.isAuthenticated()) {
                return fn.apply(this, args);
            } else {
                throw "Not authorized to execute " + fn.name + "()";
            }
            }
        }
    }
    function decorateMethods(obj, ...decorators) {
        function decorateMethod(fnName) {
            if (typeof(obj[fnName]) === "function") {
            obj[fnName] = _.compose(...decorators)(obj[fnName]);
            }
        }
        Object.keys(obj).forEach(decorateMethod);
        return obj;
    }
    function decorateAndFreeze(obj, ...args) {
        decorateMethods(obj, ...args);
        return Object.freeze(obj);
    }
    function TodoStore() { 
        function get() { }
        function add(todo) { }
        function edit(id, todo) { }
        function remove(id) { }
            
        return decorateAndFreeze({
            get,
            add,
            edit,
            remove
        }, logDuration, authorize);  
    }
    ```