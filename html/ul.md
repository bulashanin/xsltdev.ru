---
layout: default
title: ul
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;ul&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<ul>`** _(от англ. **u**nordered **l**ist -- неупорядоченный список)_ устанавливает маркированный (неупорядоченный) список.

Каждый пункт списка должен начинаться с элемента [`<li>`](/html/li/).

## Синтаксис

```html
<ul>
  <li>пункт маркированного списка</li>
</ul>
```

Закрывающий тег обязателен.

## Атрибуты

Для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/semantics.html#the-ul-element)
- [HTML 5](http://www.w3.org/TR/html5/grouping-content.html#the-ul-element)

## Описание и примеры

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>UL</title>
  </head>
  <body>
    <ul>
      <li>Баал</li>
      <li>Агарес</li>
      <li>Марбас</li>
      <li>Пруфлас</li>
      <li>Аамон</li>
    </ul>
  </body>
</html>
```
