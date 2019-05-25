---
layout: default
title: p
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;p&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<p>`** _(от англ. **p**aragraph -- параграф)_ определяет текстовый абзац.

Элемент `<p>` является блочным, всегда начинается с новой строки, абзацы текста идущие друг за другом разделяются между собой отбивкой. Величиной отбивки можно управлять с помощью стилей. Если закрывающего тега нет, считается, что конец абзаца совпадает с началом следующего абзаца или другого блочного элемента.

## Синтаксис

```html
<p>Текст</p>
```

Закрывающий тег не обязателен.

## Атрибуты

Для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/semantics.html#the-p-element)
- [HTML 5](http://www.w3.org/TR/html5/grouping-content.html#the-p-element)
- [HTML 4.01 Specification](http://www.w3.org/TR/html401/struct/text.html#h-9.3.1)

## Описание и примеры

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>P</title>
  </head>
  <body>
    <p>Рекомендуется совершить прогулку на лодке по каналам города и Озеру Любви.</p>
    <p>Венгры страстно любят танцевать, особенно ценятся национальные танцы.</p>
    <p>Из первых блюд распространены супы-пюре и бульоны, но подают их редко.</p>
  </body>
</html>
```
