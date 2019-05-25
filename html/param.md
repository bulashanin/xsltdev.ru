---
layout: default
title: param
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;param&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<param>`** _(от англ. **param**eter -- параметр)_ предназначен для передачи значений параметров Java-апплетам или объектам веб-страницы, созданным с помощью элементов `<applet>` или [`<object>`](/html/object/).

Такой подход позволяет прямо в коде HTML-документа изменять характеристики объекта без его дополнительной компиляции. Количество одновременно используемых элементов `<param>` может быть больше одного и для каждого из них задаётся пара «`имя=значение`» через атрибуты `name` и `value`.

## Синтаксис

```html
<param name="<имя>" value="<значение>" />
```

Закрывающий тег не требуется.

## Атрибуты

- `name` -- Имя параметра.
- `value` -- Значение параметра.

### name

Определяет уникальное имя параметра. Это имя должно быть программно заложено в код объекта.

**Синтаксис**

```html
<param name="<имя>" />
```

**Значения**

В качестве имени используется набор символов, включая числа и буквы.

**Значение по умолчанию**

Нет.

### value

Задаёт значение параметра. Этот атрибут не является обязательным, поскольку для объекта вполне может быть достаточно одного имени, задаваемым атрибутом `name`.

**Синтаксис**

```html
<param name="<имя>" value="<значение>" />
```

**Значения**

В качестве значения может использоваться строка или число.

**Значение по умолчанию**

Нет.

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/embedded-content.html#the-param-element)
- [HTML 5](http://www.w3.org/TR/html5/embedded-content-0.html#the-param-element)
- [HTML 4.01 Specification](http://www.w3.org/TR/html401/struct/objects.html#h-13.3.2)

## Описание и примеры

```html
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>PARAM</title>
  </head>
  <body>
    <p>
      <object classid="animation.class" width="500" height="200">
        <param name="bgcolor" value="#000000" />
        <param name="delay" value="1000" />
        <param name="loop" value="5" />
      </object>
    </p>
  </body>
</html>
```
