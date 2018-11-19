1. Копирование объекта через lodash cloneDeep
2. `./node_modules/.bin/<команда>` - запуск локально установленного модуля
3. Функция  sleep
    ```javascript
    const exec = require('child_process').execSync;
    const sleep = time => (
        (time = parseInt(time)),
        (time > 0
                ? exec(`sleep ${time}`)
                : null
        )
    );
    const sleep = (delay, ms=delay+new Date().getTime()) => {while (new Date<ms){}};
    sleep(1000);
    ```