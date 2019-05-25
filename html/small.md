---
layout: default
title: small
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;small&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<small>`** _(от англ. **small** -- маленький)_ используется для сносок и комментариев, написанных обычно мелким текстом. К ним могут относиться предостережения, информация о лицензии, авторских правах и др.

В HTML4 `<small>` уменьшает размер шрифта на единицу по сравнению с обычным текстом. В HTML4 размер шрифта измеряется в условных единицах от 1 до 7, средний размер текста, используемый по умолчанию, принят 3. Таким образом, добавление `<small>` уменьшает текст на одну условную единицу. Допускается применение вложенных элементов `<small>`, при этом размер шрифта будет меньше с каждым вложенным уровнем, но не может быть меньше, чем 1.

## Синтаксис

```html
<small>Текст</small>
```

Закрывающий тег обязателен.

## Атрибуты

Для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/semantics.html#the-small-element)
- [HTML 5](http://www.w3.org/TR/html5/semantics.html#the-small-element)
- [HTML 4.01 Specification](http://www.w3.org/TR/html401//present/graphics.html#edef-SMALL)

## Описание и примеры

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>SMALL</title>
  </head>
  <body>
    <p>
      <big><big>Большая кошка</big></big>
    </p>
    <p>Из семейства кошачьих самая большая кошка это совсем не <small>лев</small>, как можно было бы подумать исходя из титула «царя зверей». А уссурийский тигр, вес которого достигает 300 килограмм. Тигр уступает по <small>размерам</small> и <small>весу</small> только другому наземному хищнику, белому медведю.</p>
  </body>
</html>
```
