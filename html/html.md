1. JSON-LD — это способ передачи связанных данных (Linked Data, LD) с помощью текстового формата JSON. Страницы с разметкой JSON-LD облегчают структурирование данных машинами и распознавание понятий, что для владельцев сайтов важно в контексте поискового продвижения.
    ```json
    <script type="application/ld+json">
    {
        "@context": "http://schema.org/",
        "@type": "Organization",
        "name": "",
        "address": {
            "@type": "PostalAddress",
            "streetAddress": "",
            "addressLocality": "",
            "addressRegion": "",
            "postalCode": ""
        },
        "telephone": ""
    }
    </script>
    ``
1. [Schema.org](https://schema.org/) – это словарь семантической разметки данных, поддерживаемый всеми ведущими поисковыми системами. Ее цель – помогать поисковым роботам лучше понимать содержание страницы и, тем самым, улучшать результаты выдачи.
    ```html
    <div itemscope itemtype ="http://schema.org/Movie">
        <h1 itemprop="name">Avatar</h1>
        <span>Director: <span itemprop="director">James Cameron</span> (born August 16, 1954)</span>
        <span itemprop="genre">Science fiction</span>
        <a href="../movies/avatar-theatrical-trailer.html" itemprop="trailer">Trailer</a>
    </div>
    ```
# ARIA
 Технологический стандарт, разрабатываемый Консорциумом Всемирной паутины для предоставления возможности полноценного использования Интернета людьми с физическими ограничениями (нарушение работы органов зрения и опорно-двигательного аппарата). 

- For grouping widgets such as menus, tab panels, grids, or tree views, the parent element should be in the tab order (tabindex="0"), and each descendent choice/tab/cell/row should be removed from the tab order (tabindex="-1").
- When a custom control becomes disabled, remove it from the tab order by setting tabindex="-1".
- Use onkeydown to trap key events, not onkeypress
- Ensure that keyboard and mouse produce the same experience
- Ensure that the keyboard can be used to activate element
- Use alt-text 
    `<img src="bobby.jpg" alt="My dog Bobby playing fetch in the park">`

## Attributes
- aria-labelledby - This attribute is used to specify the name or label of the current element (ID of labelling element)
    `<div aria-labelledby="element1 element2 element3"></div>`
    ```html
    <label id="passLabel" for="pass">Password</label>
    <p id="passInstructions">Your password needs to be at least 8 characters long and have 1 number</p>

    <input id="pass" type="password" aria-describedby="passInstructions" aria-labelledby="passLabel">
    ```
- aria-label - This attribute is also used to specify the name of the current element and generate its "Accessible name". However, it is designed to be used where the label is not visible as another element on screen
    `<div aria-label="[Label text]"></div>`
    ```html
    <button aria-label="Close">X</button>
    ```
- aria-describedby - This attribute is used to specify more descriptive information about the current element. Unlike aria-labelledby, which expects a concisce name for the element, aria-describedby allows for a whole sentence or paragraph to give context to the element.
    `<div aria-describedby="[ID of element that contains the description]"></div>`
    ```html
    <article class="post-excerpt">
        <h2 id="postID123">Post Title</h2>
        <p>Lorem ipsum dolor sit amet...</p>
        <a aria-describedby="postID123" href="http://example.com/blog/123">Continue reading</a>
    </article>
    <section role="widget" aria-labelledby="widgetTitle" aria-describedby="widgetDesc">
        <h2 id="widgetTitle">Widget Title</h2>
        <p id="widgetDesc">Lorem ipsum dolor sit amet...</p>

        <p>Quos quidem tibi studiose et diligenter tractandos magnopere censeo</p>
        <p> Quae cum praeponunt, ut sit aliqua rerum selectio, naturam videntur sequi</p>
    </section>
    ```
## Roles
- banner
- contentinfo
- alert
- presentation
- ...
[more](https://developer.mozilla.org/ru/docs/Web/Accessibility/ARIA/ARIA_Techniques)

```html
<div role="contentinfo">
    This website was built by Georgie.
</div>
```

# Cемантические элементы HTML
- header - группирует вводные и навигационные элементы
    Элемент нельзя помещать внутрь элементов footer, address или другого элемента header
```html
<header>
  <h1>Site description</h1>
  <nav>
    <ul>
      <li><a href="">About</a>
      <li><a href="">Forum</a>
      <li><a href="">Download</a>
    </ul>
  </nav>
</header>
```
- nav - создание блока навигации веб-страницы или всего веб-сайта
```html
<nav>
  <p><a href="">...</a></p>
  <p><a href="">...</a></p>
</nav>
```
- article - используется для группировки записей — публикаций, статей, записей блога, комментариев. Если на странице присутствует только одна статья с заголовком и текстовым содержимым, она не нуждается в обёртке элементом article. Элемент рекомендуется использовать только в том случае, если содержимое элемента будет явно указано в схеме документа.
- section - универсальный раздел документа. Группирует тематическое содержимое и обычно содержит заголовок. Не является блоком-оберткой, для этих целей уместнее использовать элемент div. В качестве содержимого может выступать оглавление, разделы научных публикаций, программа мероприятия. Домашняя страница сайта также может быть поделена на секции — блок вводной информации, новости и контакты.
```html
<article>
  <h1>...</h1>
    <section>
      <h2>...</h2>
      <p>...</p>
    </section>
    <section>
      <h2>...</h2>
      <p>...</p>
    </section>
    <p>...</p>
</article>
```
- aside - группирует содержимое, связанное с окружающим его контентом напрямую, но которое можно счесть отдельным (т.е., удаление этого блока не повлияет на понимание основного содержимого)
- footer - представляет собой нижний колонтитул содержащей его секции или корневого элемента
```html
<footer>
  <address>...</address>
  <small>@2014...</small>
</footer>
```
- address - используется для определения контактной информации автора/владельца документа или статьи
- main - основное содержимое документа, должен быть уникальным и не повторяться во всех документах сайта. Элемент main не может быть потомком таких элементов как article, aside, footer, header или nav
- figure - автономный контент (необязательно с заголовком), являющийся самостоятельным элементом основного потока
```html
<figure>
    <img src="picture.jpg" alt="Осень">
    <figcaption>Осенний лес</figcaption>
</figure>
```
- figcaption - потомок элемента figure, содержит описание для тега
- time - определяет время (24 часа) или дату по григорианскому календарю с возможным указанием времени и смещения часового пояса
```html
<time datetime="2014-09-25"> 25 Сентября 2014</time>
<time datetime="2014-09-25T12:00"> 25 Сентября 2014</time>
```
- mark - выделяется по умолчанию желтым цветом (цвет фона и цвет шрифта в выделенном блоке можно изменить, задав определенные css-стили). С помощью данного тега можно отмечать важное содержимое, а также ключевые слова.
- wbr - одиночный тег, показывает браузеру место, где можно добавить разрыв длинной строки в случае необходимости.
