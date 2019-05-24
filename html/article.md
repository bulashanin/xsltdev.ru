---
layout: default
title: article
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# article
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<article>`** _(от англ. **article** - статья)_ задаёт содержание сайта вроде новости, статьи, записи блога, форума и др.

## Синтаксис

```html
<article>
  ...
</article>
```

Закрывающий тег обязателен.

## Атрибуты

Для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/sections.html#the-article-element)
- [HTML5.1](http://www.w3.org/html/wg/drafts/html/master/sections.html#the-article-element)
- [HTML5](http://www.w3.org/TR/html5/sections.html#the-article-element)

## Описание и примеры

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>article</title>
  </head>

  <body>
    <header>
      <h1>Следы невиданных зверей</h1>
    </header>
    <article>
      <p>История о том, как возле столовой появились загадочные розовые следы с шестью пальцами, и почему это случилось.</p>
    </article>
  </body>
</html>
```
