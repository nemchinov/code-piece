1.  Реализация функции bind
    ```javascript
    Function.prototype.bind = function (self, ...arg) {
        return (...s) => {
            return this.call(self, ...arg.concat(s));
        };
    };
    ```