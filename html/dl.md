---
layout: default
title: dl
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;dl&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<dl>`** _(от англ. **d**efinition **l**ist - список определений, терминов)_ задает список терминов с описаниями и входит в тройку элементов `<dl>`, `<dt>`, `<dd>`. Каждый такой список начинается с контейнера `<dl>`, куда входит элемент [`<dt>`](/html/dt/), задающий термин, и элемент [`<dd>`](/html/dd/) задающий описание этого термина.

## Синтаксис

```html
<dl>
  <dt>Термин 1</dt>
  <dd>Описание термина 1</dd>
  <dt>Термин 2</dt>
  <dd>Описание термина 2</dd>
</dl>
```

Закрывающий тег обязателен.

## Атрибуты

Для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/grouping-content.html#the-dl-element)
- [HTML 5](http://www.w3.org/TR/html5/grouping-content.html#the-dl-element)
- [HTML 4.01 Specification](http://www.w3.org/TR/html401/struct/lists.html#h-10.3)

## Описание и примеры

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Список описаний</title>
    <style>
      dd {
        font-style: italic; /* Курсивное начертание текста */
      }
      dt {
        margin-top: 1em; /* Отступ сверху */
      }
    </style>
  </head>
  <body>
    <dl>
      <dt>GIF</dt>
      <dd>Формат графических файлов, широко применяемый при создании сайтов. GIF использует 8-битный цвет и эффективно сжимает сплошные цветные области, при этом сохраняя детали изображения.</dd>
      <dt>JPEG</dt>
      <dd>Популярный формат графических файлов, широко применяемый при создании сайтов и хранения изображений. JPEG поддерживает 24-битный цвет и сохраняет яркость и оттенки цветов в фотографиях. Данный формат называют сжатием с потерями, поскольку алгоритм JPEG выборочно отвергает данные. Метод сжатия может исказить деталь в рисунке, особенно содержащий текст или изображение с чёткими краями. Формат JPEG не поддерживает прозрачность; когда вы сохраняете фотографию в формате JPEG, прозрачные пиксели заполняются определённым цветом.</dd>
    </dl>
  </body>
</html>
```
