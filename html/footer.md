---
layout: default
title: footer
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;footer&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<footer>`** _(от англ. **footer** - нижний колонтитул)_ задаёт «подвал» сайта или раздела, в нём может располагаться имя автора, дата документа, контактная и правовая информация.

## Синтаксис

```html
<footer></footer>
```

Закрывающий тег обязателен.

## Атрибуты

Для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/semantics#the-footer-element)
- [HTML 5](http://www.w3.org/TR/html5/sections.html#the-footer-element)

## Описание и примеры

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>footer</title>
  </head>
  <body>
    <header>
      <h1>Персональный сайт Кристины Ветровой</h1>
    </header>
    <article>
      <h2>Добро пожаловать!</h2>
      <p>Рада приветствовать вас на своем сайте.</p>
    </article>
    <footer>
      Copyright Кристина Ветрова
    </footer>
  </body>
</html>
```
