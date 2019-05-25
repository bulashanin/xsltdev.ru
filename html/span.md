---
layout: default
title: span
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;span&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<span>`** _(от англ. **span** -- интервал)_ предназначен для выделения отдельных строк, символов или других строчных элементов для дальнейшего изменения их оформления с помощью стилей.

Например, внутри абзаца ([`<p>`](/html/p/)) можно изменить цвет и размер первого слова, если его выделить с помощью элемента `<span>` и задать для него желаемый стиль.

## Синтаксис

```html
<span>...</span>
```

Закрывающий тег обязателен.

## Атрибуты

Для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/semantics.html#the-span-element)
- [HTML 5](http://www.w3.org/TR/html5/text-level-semantics.html#the-span-element)
- [HTML 4.01 Specification](http://www.w3.org/TR/html401/struct/global.html#edef-SPAN)

## Описание и примеры

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>SPAN</title>
    <style>
      span {
        color: red; /* Красный цвет символов */
      }
    </style>
  </head>
  <body>
    <p>Разумные люди приспосабливаются к окружающему миру. Неразумные люди приспосабливают мир к себе. Вот почему прогресс определяется действиями неразумных людей.</p>
    <p>Автор: <span>Бернард Шоу</span></p>
  </body>
</html>
```
