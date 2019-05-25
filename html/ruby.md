---
layout: default
title: ruby
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;ruby&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<ruby>`** предназначен для добавления небольшой аннотации сверху или снизу от заданного текста. Такая форма записи преимущественно используется для идеографической письменности вроде китайского языка, но может применяться и для других языков, если требуется написать один текст над другим.

Сам элемент `<ruby>` выступает контейнером для [`<rt>`](/html/rt/), он и формирует аннотацию к тексту, после которого идёт; а также [`<rp>`](/html/rp/), этот элемент предназначен для браузеров, которые не поддерживают `<ruby>`.

Название происходит от слова «рубин», которым в типографии обозначается небольшой шрифт.

## Синтаксис

```html
<ruby>
  текст
  <rt>аннотация</rt>
</ruby>
```

Закрывающий тег обязателен.

## Атрибуты

Для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/semantics.html#the-ruby-element)
- [HTML 5](http://www.w3.org/TR/html5/text-level-semantics.html#the-ruby-element)

## Описание и примеры

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>ruby</title>
    <style>
      p:lang(zh-CN) {
        font-size: 2em;
      }
    </style>
  </head>
  <body>
    <p lang="zh-CN">
      <ruby> 汉<rt>hàn</rt> 字<rt>zì</rt> </ruby>
    </p>
  </body>
</html>
```
