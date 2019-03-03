1. Приоритеты каскада.
    * Важность
        * Объявления в таблицах стилей агента пользователя (например, стили браузера по умолчанию, используемые, когда никаких других стилей не задано).
        * Oбычные объявления в пользовательских таблицах стилей (настраиваемые стили, заданные пользователем).
        * Обычные объявления в авторских таблицах стилей (это стили, которые задаем мы - веб-разработчики).
        * Важные (Important) объявления в авторских таблицах стилей
        * Важные (Important) объявления в пользовательских таблицах стилей
    * Специфичность
        * Тысячи: Ставит единицу в этот столбец, если селектор внутри элемента \<style\> или объявление находится внутри атрибута style (такие объявления не имеют селекторов, и их специфичность всегда равна 1000.) В противном случае ставьте 0.
        * Сотни: Добавляет единицу в этот столбец за каждый селектор ID, содержащийся внутри составного селектора.
        * Десятки: Добавляет единицу в этот столбец за каждый селектор класса, атрибута или псевдо-класса, содержащийся в составном селекторе.
        * Единицы: Добавляет единицу в этот столбец за каждый селектор элемента или псевдо-элемента, содержащийся в составном селекторе.
    * Исходный порядок (побеждает последний)
1. CSS наследование
    * inherit : Это значение устанавливает для свойства элемента такое же значение, как и у его родителя.
    * initial : Это значение устанавливает свойство выбранного элемента равным тому, что задается для него в таблице стилей браузера по умолчанию. Если в таблице стилей браузера это значение не установлено, а исходно оно являлось наследуемым, то оно устанавливается равным inherit.
    * unset : Это значение сбрасывает свойство к его исходному значению, то есть если исходно оно является наследуемым, то оно работает как inherit, а в противном случае - как initial.

## Rules
1. Grid
    ```css
    display: grid;
    grid-template-columns: 100px 100px 100px 100px 100px;
    grid-template-rows: repeat(4, 1fr); 
    grid-template-columns: max-content 1fr 1fr; /* первая ячейка занимает сколько нужно ей места */
    grid-template-columns: min-content 1fr 1fr; /* первая ячейка занимает насколько можно мало места (слова переносятся на новую строку) */
    grid-auto-flow: column;
    grid-column-gap: 15px; 
    grid-row-gap: 15px;
    grid-template-areas:
        'x y y y y'
        'x center center center w'
        'x center center center w'
        'x z z z z';
    /*
    <div>
        <div style="grid-area: x">test</div>
        <div style="grid-area: y">test</div>
        <div style="grid-area: z">test</div>
        <div style="grid-area: w">test</div>
        <div style="grid-area: center">test</div>
    </div>
    */
    ```
1. Grid element
    ```css
    grid-column: 3 / span 2; /* растянуть на две колонки */
    grid-row: 2;
    grid-column-start: 1;
    grid-column-end: 2;
    grid-column: 1 / 2;
    grid-row-start: 3;
    grid-row-end: 4;
    grid-row: 3 / 4;
    grid-area: 1 / 3 / 2 / 4;
    grid-area: x; /* значение из grid-template-areas */
    justify-self: center;
    align-self: right;
    // display: subgrid; /* сделать вложенные элементы частью грид сетки */ пока не поддерживается
    ```
1. Resize
    ```css
    resize: horizontal;
    overflow: auto;
    ```
1. Flex-box - `display: flex;`
    - `flex-direction` - row, column
    - `justify-content` -  положение на оси: flex-start, center, space-between
    - `flex-wrap`
    - `align-items` - расположение по поперечной оси
    -  `align-item` - выравнивани если контент распологается в несколько строк
    - `order` - для элемента, позволяет изменить порядок
    - `flex-grow` -  позвляет элементу растягиваться при необходимости
    - `align-self` - расположение конкретного элемента по поперечной оси
1. Избавляет пользователей мыши от outline, но сохраняет его для пользователей клавиатуры и не учитывается браузерами, которые не поддерживают :focus-visible.
    ```css
    :focus:not(:focus-visible) { outline: none }
    ```xz
1. Скрыть пустные строки в таблице `table { empty-cells: hide; }`
1. Пользовательские свойства
    ```css
    :root {
        --netologyBrandColor: #800080;
    }

    button {
        --NETOLOGY-BRAND-COLOR: #800080;
        --netology-brand-color: #27ae60;
            
        border: 2px solid var(--NETOLOGY-BRAND-COLOR);
        color: var(--netology-brand-color);  
    }

    .element::before {
        --color: rgba(0, 0, 0, 1);
        --hex: #000000;
        --value: 20px;
        --number: 3;
        --text: "Hey, what's up?";
        --keyword: currentColor;
    }

    button {
        border: 2px solid var(--netologyBrandColor, #800080);
        color: var(--netologyBrandColor, #800080);
    }
    ```
