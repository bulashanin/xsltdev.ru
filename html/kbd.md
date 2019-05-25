---
layout: default
title: kbd
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;kbd&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<kbd>`** _(от англ. **k**ey**b**oar**d** -- клавиатура)_ используется для обозначения текста, который набирается на клавиатуре или для названия клавиш.

Браузеры обычно помечают текст в контейнере `<kbd>` моноширинным шрифтом.

## Синтаксис

```html
<kbd>Текст</kbd>
```

Закрывающий тег обязателен.

## Атрибуты

Для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/semantics.html#the-kbd-element)
- [HTML 5](http://www.w3.org/TR/html5/text-level-semantics.html#the-kbd-element)
- [HTML 4.01 Specification](http://www.w3.org/TR/html401/struct/text.html#h-9.2.1)

## Описание и примеры

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>KBD</title>
    <style>
      kbd {
        background: #ccc;
        border-radius: 3px;
        padding: 0 4px;
      }
    </style>
  </head>
  <body>
    <p>Для быстрого закрашивания выделенной области цветом переднего плана используйте комбинацию клавиш <kbd>Alt</kbd>+<kbd>Backspace</kbd> или <kbd>Alt</kbd>+<kbd>Delete</kbd>. Для закрашивания выделенной области фоновым цветом воспользуйтесь комбинацией <kbd>Ctrl</kbd>+<kbd>Backspace</kbd> или <kbd>Ctrl</kbd>+<kbd>Delete</kbd>.</p>
  </body>
</html>
```
