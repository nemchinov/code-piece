1. Копирование объекта через lodash cloneDeep
1. `./node_modules/.bin/<команда>` - запуск локально установленного модуля
1. Функция  sleep
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
1. Использование памяти
    ```javascript
        let usage = process.memoryUsage();
        usage.rss; // process resident set size
        usage.heapTotal; // v8 heap allocated ~ куча
        usage.heapUased; // heap used
        usage.rss - usage.heapTotal; // ~ stak
    ```
1. Ключи запуска приложения
    `--expose-gc` - add to global gc() function that will erquest garbage collector
    `--nouse-idle-notification` - not request GC