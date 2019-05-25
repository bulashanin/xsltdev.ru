---
layout: default
title: b
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;b&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<b>`** _(от англ. **b**old - жирный)_ задаёт жирное начертание шрифта. Допустимо использовать этот элемент совместно с другими, которые определяют начертание текста.

## Синтаксис

```html
<b>Текст</b>
```

Закрывающий тег обязателен.

## Атрибуты

Для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/semantics.html#the-b-element)
- [HTML5](http://www.w3.org/TR/html5/text-level-semantics.html#the-b-element)
- [HTML 4.01 Specification](http://www.w3.org/TR/html401/present/graphics.html#h-15.2.1)

## Описание и примеры

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>B</title>
  </head>
  <body>
    <p><b>Почему изоморфна функция B(x,y)</b></p>
    <p>Дивергенция векторного поля переворачивает интеграл от функции, обращающейся в бесконечность в изолированной точке. Окрестность точки, конечно, небезынтересно отражает <b>функциональный анализ</b>. Представляется логичным, что полином развивает равновероятный натуральный логарифм.</p>
  </body>
</html>
```
