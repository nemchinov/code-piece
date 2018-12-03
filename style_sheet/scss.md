[Документация](https://sass-scss.ru/documentation/)

1. Переменные
    ```scss
    $font-stack:    Helvetica, sans-serif;
    $primary-color: #333;

    body {
        font: 100% $font-stack;
        color: $primary-color;
    }
    ```
1. Вложенность
    ```scss
    nav {
        ul {
            margin: 0;
            padding: 0;
            list-style: none;
        }
    }
    ```
1. Фрагментирование - подключаемые через @import файлы, имя начинается с `_`. `@import 'reset'; // _reset.scss`
   Использование дефолтных значений: `$message-color: blue !default;` - в результируещем коде не заменит переменнную если она уже была объявленна.
1. Миксины
    ```scss
    @mixin border-radius($radius) {
        -webkit-border-radius: $radius;
            -moz-border-radius: $radius;
                -ms-border-radius: $radius;
                    border-radius: $radius;
    }
    @function make-greener($value, $color: 50) {
        @return $value + rgb(0, $color, 0); // арифметика цветов, кстати, в порядке
    }

    .box { 
        @include border-radius(10px); // @include foobar($bottomPadding: 50px); - передаем значение определенного аргумента
    }
    ```
1. Расширение - в отличие от миксинов в css будет запись .massage, .error { ... } - отсутствие дублирования
    ```scss
    %message-shared {
        border: 1px solid #ccc;
        padding: 10px;
        color: #333;
    }

    .message {
        @extend %message-shared;
    }
    .error {
        @extend %message-shared;
    }
    ```
1. Операции
    ```scss
    width: 600px / 960px * 100%;
    $color: #010203; 
    color: $color;
    border-color: $color - #010101;
    &:hover { color: #010203 * 2; }
    background-image: url( $image_dir + 'pen.gif' ); 
    &:before { content: "Страница #{ $page }!"; }
    ```
1. Шаблоны в именах
    ```scss
    $alertClass: "error";
    
    p.message-#{$alertClass} {
        color: red;
    }
    ```
1. Циклы
    ```scss
    @each $name in 'save' 'cancel' 'help' {
        .icon-#{$name} {
            background-image: url('/images/#{$name}.png');
        }
    }
    $buttonConfig: 'save' 50px, 'cancel' 50px, 'help' 100px; // TODO: move to _settings.scss
    
    @each $tuple in $buttonConfig {
        .button-#{nth($tuple, 1)} {
            width: nth($tuple, 2);
        }
    }
    ```
1. Передача контента - декорация
    ```scss
    @mixin only-for-mobile {
        @media (max-width: 768px) {
            @content;
        }
    }
    
    @include only-for-mobile() {
        p {
            font-size: 150%;
        }
    } 
    ```
1. Переопределение
    ```scss
    @mixin message($class) {
        .message-#{$class} {
            border: 1px dotted yellow;
            color: yellow;
            margin: 20px;
            padding: 10px;
            @content;
        }
    }
    
    @include message("subtle") {
        margin: 5px;
    }
    ```