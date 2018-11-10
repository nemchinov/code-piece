1. Использование `сonst/let`
2. Использоваение  spread оператора для хэшей и массивов
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