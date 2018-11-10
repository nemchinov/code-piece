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