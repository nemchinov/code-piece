1. `tsc file.ts`
1. Union
    ```javascript
    const isUnionType: boolean | string | number = true;
    const isUnionType: boolean | string | number = 'string';
    let isStringLiteral: 'one' | 'two' | 'three';

    isStringLiteral = 'one';
    ```
1. Комбинирование
    ```javascript
    function extend<T, U>(a: T, b: U): T & U {
        return Object.assign({}, a, b);
    }
    ```
1. Приведение типов
    ```javascript
    const str: string = <string>new String('TypeScript');
    ```
1.  Типы
    - void
    - never
    ```javascript
    function fail(message: string): never {
        throw new Error(message);
    }
    ```
    - Array `const isArrayOfStrings: string[] = ['a', 'b']; const isArrayOfStrings: Array<string> = ['a', 'b'];`
    - Tuple или кортеж `const tuple: [number, string, boolean] = [1234, 'TypeScript Types', true];`
    - Enum или перечисление `enum Days { Sat=1, Sun, Mon, Tue, Wed, Thu, Fri };`
1. Интерфейсы - это объявлние, схожее с классом, но не имеющее реализации методов. С его помощью вы можете описывать свойства и методы объектов. Объявление интерфейса начинается с ключевого слова interface. Затем идёт имя интерфейса, которые принято начинать с заглавной буквы I. 
    ```javascript
    interface IServer {
        hostname: string;
        location: string;
        active: boolean;
        public_address: string;
    }
    const server: IServer = {
        hostname: 'Pikachu',
        location: 'RM1',
        active: true,
        public_address: 'string'
    }
    interface IServer {
        hostname: string;
        location: string;
        active: boolean;
        public_address: IPublicAddress;
    }
    interface IResponse {
        readonly status: number;
    }

    interface ISlackResponse extends IResponse {
        ok: boolean;
    }

    interface ICache {
        size: number;
        first: ICacheItem;
        last?: ICacheitem;
        items: {
            [item: string]: ICacheItem;
        };
    }
    ```
1. Класс
    ```javascript
    interface ICacheItem {
        mtime: number;
        content: string;
    }

    interface IFileCache {
        set: (key: string, value: ICacheItem) => void;
        get: (key: string) => ICacheItem;
    }

    class FileCache implements IFileCache {
        store = new Map();
        static PI: number = 3.14;

        set(key: string, value: ICacheItem): void {
            this.store.set(key, value);
        }

        get(key: string): ICacheItem {
            return this.store.get(key);
        }
    }

    class User {
        readonly id: number;
        constructor(private name: string, private age: number) { }
        
        public displayInfo(): void {
            console.log("name: " + this.name + "; age: " + this.age);
        }
    }

    class Employee extends User {
    
        company: string;
        work(name: string, age: number): void {
            super(name, age);
            console.log(this.name + " работает в компании " + this.company);
        }
    }

    abstract class Figure {
        getArea(): void{
            console.log("Not Implemented")
        }
    }

    ```
1. Обобщения
    ```javascript
    function getId<T>(id: T): T {
        
        return id;
    }
    let result1 = getId<number>(5);
    // class UserInfo<T extends User>
    ```
1. Пространства имен
    ```javascript
    namespace Personnel {
        export class Employee {
        
            constructor(public name: string){
            }
        }
        export namespace Clients {
            export class VipClient {
            
                constructor(public name: string){
                }
            }
        }
    }
    let alice = new Personnel.Employee("Alice");
    ```
1. Export `export {Device, Phone, Call as Devices};`
1. Заголовочные файлы `.d.ts`
    ```javascript
    // globals.d.ts
    declare var globalVar: string;
    // app.ts
    /// <reference path="globals.d.ts" />
    class Utility {
        static displayGlobalVar() {
            console.log(globalVar);
        }
    }
    ```
1. Декораторы
    ```javascript
    function sealed(constructor: Function) {
        console.log("sealed decorator");
        Object.seal(constructor);
        Object.seal(constructor.prototype);
    }
    
    @sealed
    class User ...
    ```
