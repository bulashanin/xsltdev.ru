---
layout: default
title: xsl:apply-imports
nav_order: 1
parent: XSLT
---

<!-- prettier-ignore-start -->
# xsl:apply-imports
{: .no_toc }
<!-- prettier-ignore-end -->

Элемент **`xsl:apply-imports`** используется в шаблонах для применения правил, которые были импортированы во внешних модулях, но переопределены шаблонами основного преобразования.

<!-- prettier-ignore -->
1. TOC
{:toc}

## Синтаксис

### XSLT 1.0

```xml
<xsl:apply-imports />
```

### XSLT 2.0 и XSLT 3.0

```xml
<xsl:apply-imports>
    <!-- Контент: несколько элементов xsl:with-param -->
</xsl:apply-imports>
```

## Описание и примеры

При обработке стиля в каждой точке имеется некое текущее правило шаблона. Всякий раз, когда по образцу выбирается правило шаблона, для обработки оно становится текущим правилом шаблона. Когда обрабатывается элемент [`xsl:for-each`](/xslt/xsl-for-each/), то при обработке содержимого этого элемента `xsl:for-each` текущее правило шаблона становится нулевым.

`xsl:apply-imports` обрабатывает текущий узел используя лишь те правила шаблона, которые были импортированы в тот элемент стиля, где это текущее правило шаблона находится. Узел обрабатывается в режиме текущего правила шаблона. Если `xsl:apply-imports` обрабатывается когда текущее правило шаблона нулевое, фиксируется ошибка.

### Пример 1

Предположим что стиль `doc.xsl` содержит правило шаблона для элементов `example`:

```xml
<xsl:template match="example">
    <pre><xsl:apply-templates/></pre>
</xsl:template>
```

Другой стиль может импортировать `doc.xsl` и поменять обработку элементов `example` следующим образом:

```xml
<xsl:import href="doc.xsl"/>
<xsl:template match="example">
    <div style="border: solid red">
        <xsl:apply-imports/>
    </div>
</xsl:template>
```

В результате суммарного действия `example` должен преобразовываться в элемент следующего вида:

```xml
<div style="border: solid red"><pre>...</pre></div>
```

### Пример 2

Предположим, что в преобразованиях часто используется шаблон, который заменяет элементы `home` ссылками на сайт `http://www.xsltdev.ru`:

```xml
<xsl:template match="home">
    <a href="http://www.xsltdev.ru/">www.xsltdev.ru</a>
</xsl:template>
```

При необходимости этот шаблон может быть переопределен. К примеру, [ссылка](/html/a/) может выглядеть так: `Visit <a href="https://www.xsltdev.ru/">www.xsltdev.ru</a>`. Соответственно, шаблон будет иметь вид:

```xml
<xsl:template match="home">
    <xsl:text>Visit </xsl:text>
    <a href="https://www.xsltdev.ru/">www.xsltdev.ru</a>
</xsl:template>
```

Можно заметить, что оба шаблона имеют общую часть, которая выводит гипертекстовую ссылку. Эта часть может быть выведена во внешнее преобразование `home.xsl`:

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:template match="home">
        <a href="https://www.xsltdev.ru/">www.xsltdev.ru</a>
    </xsl:template>
</xsl:stylesheet>
```

Для того чтобы использовать внешний шаблон, основное преобразование должно импортировать его при помощи [`xsl:import`](/xslt/xsl-import/) и применять посредством `xsl:apply-imports`:

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:import href="home.xsl" />
    <xsl:template match="home">
        <xsl:text>Visit </xsl:text>
        <xsl:apply-imports />
    </xsl:template>
</xsl:stylesheet>
```

В XSLT 2.0 элемент `<xsl:apply-imports>` может содержать нуль или более элементов [`<xsl:with-param>`](/xslt/xsl-with-param/) для передачи параметров импортированному шаблону. Лишние параметры, передаваемые импортируемому шаблону, игнорируются. Но если импортированному шаблону не передается обязательный параметр, процессор XSLT выдает ошибку.

## См. также

- [`xsl:import`](/xslt/xsl-import/) -- импорт преобразований

## Ссылки

- [`xsl:apply-imports`](https://developer.mozilla.org/en/XSLT/apply-imports) на MDN
- [`xsl:apply-imports`](https://msdn.microsoft.com/en-us/library/ms256178.aspx) на MSDN
