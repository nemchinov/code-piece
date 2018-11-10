1. Types
    ```javascript
    true + false
    12 / "6"
    "number" + 15 + 3
    15 + 3 + "number"
    [1] > null
    "foo" + + "bar"
    'true' == true
    false == 'false'
    null == ''
    !!"false" == !!"true"
    [‘x’] == ‘x’
    [] + null + 1
    0 || "0" && {}
    [1,2,3] == [1,2,3]
    {}+[]+{}+[1]
    !+[]+[]+![]
    new Date(0) - 0
    new Date(0) + 0
    ```
    Answer:
    ```javascript
    true + false             // 1
    12 / "6"                 // 2
    "number" + 15 + 3        // 'number153'
    15 + 3 + "number"        // '18number'
    [1] > null               // true
    "foo" + + "bar"          // 'fooNaN' - унарный плюс
    'true' == true           // false
    false == 'false'         // false
    null == ''               // false
    !!"false" == !!"true"    // true
    ['x'] == 'x'             // true 
    [] + null + 1            // 'null1'
    0 || "0" && {}           // {}
    [1,2,3] == [1,2,3]       // false
    {}+[]+{}+[1]             // '0[object Object]1'
    !+[]+[]+![]              // 'truefalse'
    new Date(0) - 0          // 0
    new Date(0) + 0          // 'Thu Jan 01 1970 02:00:00(EET)0'
    ```