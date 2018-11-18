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
2. [Schema.org](https://schema.org/) – это словарь семантической разметки данных, поддерживаемый всеми ведущими поисковыми системами. Ее цель – помогать поисковым роботам лучше понимать содержание страницы и, тем самым, улучшать результаты выдачи.
    ```html
    <div itemscope itemtype ="http://schema.org/Movie">
        <h1 itemprop="name">Avatar</h1>
        <span>Director: <span itemprop="director">James Cameron</span> (born August 16, 1954)</span>
        <span itemprop="genre">Science fiction</span>
        <a href="../movies/avatar-theatrical-trailer.html" itemprop="trailer">Trailer</a>
    </div>
    ```