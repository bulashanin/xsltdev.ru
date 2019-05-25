---
layout: default
title: label
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;label&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<label>`** _(от англ. **label** -- метка, ярлык)_ устанавливает связь между определённой меткой, в качестве которой обычно выступает текст, и элементом формы ([`<input>`](/html/input/), [`<select>`](/html/select/), [`<textarea>`](/html/textarea/)).

Такая связь необходима, чтобы изменять значения элементов формы при щелчке курсором мыши на текст. Кроме того, с помощью `<label>` можно устанавливать горячие клавиши на клавиатуре и переходить на активный элемент подобно ссылкам.

Существует два способа связывания объекта и метки. Первый заключается в использовании идентификатора `id` внутри элемента формы и указании его имени в качестве атрибута `for` элемента `<label>`. При втором способе элемент формы помещается внутрь контейнера `<label>`.

## Синтаксис

```html
<input id="<идентификатор>" /><label for="<идентификатор>">Текст</label> <label><input /> Текст</label>
```

Закрывающий тег обязателен.

## Атрибуты

- `for` -- Идентификатор элемента, с которым следует установить связь.

Также для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

### for

Задаёт уникальный идентификатор, определяемый с помощью атрибута `id` элемента [`<input>`](/html/input/), с которым следует установить связь. Атрибут `for` необходимо задавать в том случае, когда элемент формы и текст разделены. Если `<input>` размещается внутри контейнера `<label>`, то применять атрибут `for` не требуется.

**Синтаксис**

```html
<label for="<идентификатор>">...</label>
```

**Значения**

Имя идентификатора. Такое имя чувствительно к регистру, поэтому его следует писать так же, как оно описано внутри элемента `<input>`.

**Значение по умолчанию**

Нет.

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/forms.html#the-label-element)
- [HTML 5](http://www.w3.org/TR/html5/forms.html#the-label-element)
- [HTML 4.01 Specification](http://www.w3.org/TR/html401/interact/forms.html#h-17.9.1)

## Описание и примеры

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>LABEL</title>
  </head>
  <body>
    <form action="handler.php">
      <p><b>Выберите напиток</b></p>
      <p>
        <input type="checkbox" id="check1" /><label for="check1">Коньяк</label><br />
        <input type="checkbox" id="check2" /><label for="check2">Арманьяк</label><br />
        <input type="checkbox" id="check3" /><label for="check3">Кальвадос</label><br />
      </p>
    </form>
  </body>
</html>
```
