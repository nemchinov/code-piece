1. Использование `сonst/let`
2. Использоваение spread оператора для хэшей и массивов
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
3. Ставить `;`
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
    
    ```