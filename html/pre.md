---
layout: default
title: pre
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;pre&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<pre>`** _(от англ. **pre**formatted -- предварительно отформатированный)_ определяет блок предварительно форматированного текста.

Такой текст отображается обычно моноширинным шрифтом и со всеми пробелами между словами. По умолчанию, любое количество пробелов идущих в коде подряд, на веб-странице показывается как один. Элемент `<pre>` позволяет обойти эту особенность и отображать текст как требуется разработчику.

## Синтаксис

```html
<pre>Текст</pre>
```

Закрывающий тег обязателен.

## Атрибуты

Для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/semantics.html#the-pre-element)
- [HTML 5](http://www.w3.org/TR/html5/grouping-content.html#the-pre-element)
- [HTML 4.01 Specification](http://www.w3.org/TR/html401/struct/text.html#h-9.3.4)

## Описание и примеры

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>PRE</title>
  </head>
  <body>
    <pre>
-                -----  
-----           |-----
||----|          ----||  
||-----         -----||  
||-----|       |-----||
|| -----       ------||
||- ----|     |------||
||---||--     -------||
||--|| --|   |-------||
|| -|| |--   --- - --||
|| -||  --|-|--| - ---|
|---||  |-----| |-----|
|---||   |----  |-----| 
|----|    ---   |-----|
|-----          ------| 
</pre
    >
  </body>
</html>
```
