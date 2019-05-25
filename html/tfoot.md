---
layout: default
title: tfoot
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;tfoot&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<tfoot>`** _(от англ. **t**able **foot** -- подвал таблицы)_ предназначен для хранения одной или нескольких строк, которые представлены внизу таблицы.

Хотя `<tfoot>` в исходном коде должен быть определён до элемента [`<tbody>`](/html/tbody/), браузеры отображают его в самом низу таблицы.

В пределах таблицы разрешается использовать только один элемент `<tfoot>`.

## Синтаксис

```html
<table>
  <thead>
    ...
  </thead>
  <tfoot>
    <tr>
      <td>...</td>
    </tr>
  </tfoot>
  <tbody>
    ...
  </tbody>
</table>
```

Закрывающий тег не обязателен.

## Атрибуты

Для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/tables.html#the-tfoot-element)
- [HTML 5](http://www.w3.org/TR/html5/tabular-data.html#the-tfoot-element)

## Описание и примеры

```html
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>TFOOT</title>
  </head>
  <body>
    <table width="600">
      <tfoot align="center" style="background: #ffc">
        <tr>
          <td>Ячейка 1, расположенная в TFOOT</td>
          <td>Ячейка 2, расположенная в TFOOT</td>
        </tr>
      </tfoot>
      <tbody align="right" style="background: silver">
        <tr>
          <td>Ячейка 3, расположенная в TBODY</td>
          <td>Ячейка 4, расположенная в TBODY</td>
        </tr>
      </tbody>
    </table>
  </body>
</html>
```
