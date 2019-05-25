---
layout: default
title: map
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;map&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<map>`** _(от англ. **map** -- карта)_ служит контейнером для элементов [`<area>`](/html/area/), которые определяют активные области для карт-изображений.

Такие области устанавливают невидимые зоны на изображении, являющиеся ссылками на HTML-документы. Цель использования `<map>` — в связывании элемента [`<img>`](/html/img/) с клиентской картой-изображением. Эта связь определяется применением единого идентификатора как в `<img>`, задаваемого атрибутом `usemap`, так и в `<map>`, устанавливаемого атрибутом `name`.

## Синтаксис

```html
<map name="<имя>">
  <area />
</map>
```

Закрывающий тег обязателен.

## Атрибуты

- `name` - Имя карты-изображения.

### name

Имя идентификатора, которое однозначно определяет карту-изображение. Значение атрибута `name` элемента `<map>` должно соответствовать имени в `usemap`. При этом значение атрибута `usemap` у [`<img>`](/html/img/) начинается с символа решётки.

**Синтаксис**

```html
<map name="<идентификатор>">...</map>
```

**Значения**

Любое подходящее уникальное имя, оно чувствительно к регистру.

**Значение по умолчанию**

Нет.

## Спецификации

- [HTML Living Standard](https://html.spec.whatwg.org/multipage/embedded-content.html#the-map-element)
- [HTML 5](http://www.w3.org/TR/html5/embedded-content-0.html#the-map-element)
- [HTML 4.01 Specification](http://www.w3.org/TR/html401/struct/objects.html#h-13.6.1)

## Описание и примеры

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>MAP</title>
    <style>
      #title {
        line-height: 0; /* Изменяем межстрочное расстояние */
      }
      #title img {
        border: none; /* Убираем рамку вокруг изображения */
      }
    </style>
  </head>
  <body>
    <div id="title">
      <img src="image/ecctitle.png" width="640" height="158" alt="Детский образовательный центр" /><br />
      <img src="image/navigate.png" width="640" height="30" alt="Навигация по сайту" usemap="#Navigation" />
    </div>
    <p>
      <map name="Navigation">
        <area shape="poly" coords="113,24,211,24,233,0,137,0" href="page/inform.html" alt="Информация" />
        <area shape="poly" coords="210,24,233,0,329,0,307,24" href="page/activity.html" alt="Мероприятия" />
        <area shape="poly" coords="304,24,385,24,407,0,329,0" href="page/depart.html" alt="Отделения" />
        <area shape="poly" coords="384,24,449,24,473,0,406,0" href="page/techinfo.html" alt="Техническая информация" />
        <area shape="poly" coords="449,24,501,24,525,0,473,0" href="page/study.html" alt="Обучение" />
        <area shape="poly" coords="501,24,560,24,583,0,525,0" href="page/work.html" alt="Работа" />
        <area shape="poly" coords="560,24,615,24,639,0,585,0" href="page/misk.html" alt="Разное" />
      </map>
    </p>
  </body>
</html>
```
