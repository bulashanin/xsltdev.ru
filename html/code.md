---
layout: default
title: code
nav_order:
parent: HTML
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# &lt;code&gt;
{: .no_toc }
<!-- prettier-ignore-end -->

Тег **`<code>`** _(от англ. **code** - код)_ предназначен для отображения одной или нескольких строк текста, который представляет собой программный код.

Сюда относятся имена переменных, ключевые слова, тексты функции и т. д. Браузеры обычно отображают содержимое контейнера `<code>` как моноширинный текст уменьшенного размера.

В отличие от элемента [`<pre>`](/html/pre/) дополнительные пробелы внутри контейнера `<code>` не учитываются, так же, как и переносы текста. Для разметки кода программы элементы `<code>` и `<pre>` комбинируют.

## Синтаксис

```html
<code>Текст</code>
```

Закрывающий тег обязателен.

## Атрибуты

Для этого элемента доступны [универсальные атрибуты](/lib/uni-attr/) и [события](/lib/events/).

## Спецификации

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/semantics.html#the-code-element)
- [HTML5](http://www.w3.org/TR/html5/text-level-semantics.html#the-code-element)
- [HTML 4.01 Specification](http://www.w3.org/TR/html401/struct/text.html#h-9.2.1)

## Описание и примеры

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>CODE</title>
  </head>
  <body>
    <p>Код программы</p>
    <pre>
	  <code>
		function checkParent (src, dest) {
		  while (src != null) {
			if (src.tagName == dest) return src
		      src = src.parentElement
			}
		  return null
		}
	  </code>
	</pre>
  </body>
</html>
```
