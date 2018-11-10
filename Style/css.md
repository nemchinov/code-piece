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
2. Grid element
    ```css
    grid-column: 3 / span 2; /* растянуть на две колонки */
    grid-row: 2;
    grid-column-start: 1;
    grid-column-end: 2;
    grid-row-start: 2;
    grid-row-end: 4;
    justify-self: center;
    align-self: right;
    ```