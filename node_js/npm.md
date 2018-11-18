1. `npm i --save pkg` ~ `npm i -S pkg` ~ `npm i pkg` - добавляется по умолчанию
2. `npm i --save-dev pkg` ~ `npm i -D pkg`
3. `npm run test` ~ `npm test` ~ `npm t`
4. `npm ls --depth 0`, `npm ls --depth 0 | grep react`
5. `npm run env` - доступные переменные окружения
6. Pre and post commands with matching names will be run (e.g. premyscript, myscript, postmyscript)
7. `npm it` ~ `npm install && npm test`
8. `npm r` ~ `npm uninstall`
9. `npm install --no-save ava`
10. `npx pkg` - If the binary is already installed, it will be executed from node_modules/.bin, But if the binary is missing, it will be installed first.
11. `npx -p node@8 npm run build`
12. `npm help <command>`