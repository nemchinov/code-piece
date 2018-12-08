# [Pug](https://pugjs.org/api/getting-started.html)
1. [Pug online](https://pughtml.com/)
1. В Pug нет закрывающих тегов, вместо этого он использует строгую табуляцию (или отступы) для определения вложености тегов. Для закрытия тегов в конце необходимо добавить символ /: foo(bar='baz')/ - <foo bar="baz" />
    ```
    ul
        li Item A
        li Item B
        li Item C
    
    p
        = 'This code is <escaped>!'
    
    <p>This code is &lt;escaped&gt;!</p>

    - var title = "On Dogs: Man's Best Friend";
    - var author = "enlore";
    - var theGreat = "<span>escape!</span>";

    h1= title
    p Written with love by #{author}
    p This will be safe: !{theGreat}
    ```
1. Непосредственно в Pug можно вставлять элементы в HTML синтаксисе
    ```
    p This is plain old <em>text</em> content.
    ```
1. Большой текст
    ```
    p
        | The pipe always goes at the beginning of its own line,
        | not counting indentation.
    ```
1. Итоговый html на разных строках
    ```
    a(href='google.com') Google
    |
    |
    a(class='button' href='google.com') Google
    ```
1. Условия 
    `body(class=authenticated ? 'authed' : 'anon')`
    ```
    - var friends = 10
    case friends
        when 0
            p you have no friends
        when 1
            p you have a friend
        default
            p you have #{friends} friends

    - var values = [];
    ul
        each val in values
            li= val
        else
            li There are no values

    if user.description
        ...
    else if authorised
        ...
    else
        ...
    
    for link in links
        a(href="{{ link.url }}", class="{% if link.current %}current{% endif %}")
          = link.title|truncatechars:"50"
    ```
1. Объявление переменных 
    ```
    - var url = 'pug-test.html';
    a(href='/' + url) Link
    - var classes = ['foo', 'bar', 'baz']
    a.bang(class=classes class=['bing'])
    ```
1. Циклы
    ```
    ul
        each val, index in ['zero', 'one', 'two']
            li= index + ': ' + val
    
    - var n = 0;
    ul
        while n < 4
            li= n++
            
    - for (var x = 0; x < 3; x++)
        li item
    ```
1. Вставка сторонних файлов
    ```
    //- index.pug
    doctype html
        html
        head
            style
            include style.css
        body
            h1 My Site
            p Welcome to my super lame site.
            script
            include script.js
    ```
1. Наследование
    ```
    //- base.pug
    html
        head
            title My Site 
            block scripts
            script(src='/jquery.js')
        body
            block content
            block foot
            #footer
                p some footer content
                
        //- home.pug
        extends base.pug
        - var title = 'Animals'
        - var pets = ['cat', 'dog']
        block content
            h1= title // - or #{title} without =
            each petName in pets
                p= petName // -or #{petName} without =

    <!DOCTYPE html>
    <html>
        <head>
            <title>My site</title>
            <script src='/jquery.js'></script>
        </head>
        <body>
            <h1>Animals</h1>
            <p>cat</p>
            <p>dog</p>
            <div id='footer'>
                <p>some footer content</p>
            </div>
        </body>
    </html>
    ```
1.  Миксины
    ```
    mixin pet(name)
        li.pet= name
        if block
            block
        else
            p No content provided
    //- use
    ul
        +pet('cat')
        +pet('dog')
        +pet('pig')
    ```