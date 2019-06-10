---
layout: default
title: function-available
nav_order: 12
parent: XPath
---

<!-- prettier-ignore-start -->
# function-available()
{: .no_toc }
<!-- prettier-ignore-end -->

Функция **`function-available`** принимает на вход строку, представляющую имя функции и возвращает `true`, если эта функция может быть вызвана и `false` — если нет.

<!-- prettier-ignore -->
1. TOC
{:toc}

## Синтаксис

### XPath 1.0

```
boolean function-available( string )
```

## Описание и примеры

При использовании функций расширения всегда есть вероятность того, что это расширение в силу каких-либо причин поддерживаться данным процессором не будет. Чаще всего это случается, во-первых, когда процессор просто физически не в состоянии вызвать эту функцию (например, процессор, написанный на C++, вряд ли будет содержать средства для выполнения Java-кода), во-вторых, когда расширение недоступно (например, процессор не в состоянии найти указанный Java-класс или динамическую библиотеку), и в-третьих, когда пространство имен объявлено неверно (например, с URI `java:de.fzi.xslt.rot` вместо `xalan://de.fzi.xslt.rot`). Результатом обращения к неподдерживаемому расширению будет, естественно, ошибка.

XSLT позволяет избежать подобного рода ошибок путем предварительной проверки наличия заданной функции расширения. Для этой цели служит стандартная функция `function-available` (от англ. function is available — функция доступна).

Строковый аргумент этой функции представляет расширенное имя функции, он должен соответствовать продукции `QName`, то есть иметь вид `имя` или `префикс:имя`. В первом случае `function-available` проверяет, реализована ли в данном процессоре стандартная функция с таким именем, например `function-available('concat')` скорее всего, возвратит `true`.

В случае, если аргумент `function-available` имеет вид `префикс:имя`, функция `function-available` проверяет доступность указанной функции расширения. Например, для того, чтобы проверить, может ли в данном контексте быть вызвана функция `rot:X`, необходимо вычислить выражение

```
function-available('rot:X')
```

В данном случае `true` будет означать, что функция `rot:X` может быть вызвана, `false` — что функция в силу каких-то причин недоступна.

Функция `function-available` может помочь в создании преобразований, которые используют расширения, но при этом в некоторой степени сохраняют переносимость между различными процессорами. Достаточно написать несколько вариантов вызова функции расширения для каждого из процессоров, на которых преобразование должно работать, а затем использовать вариант с доступной данному процессору функцией расширения.

### Пример

Для того чтобы обеспечить работоспособность расширения, реализованного классом `de.fzi.xslt.rot` в наиболее распространенных XSLT-процессорах, написанных на Java (как-то: Saxon, Xalan и Oracle XSLT Processor), прежде всего необходимо объявить соответствующие пространства имен:

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns="http://www.w3.org/2000/svg" xmlns:saxon="java:de.fzi.xslt.rot" xmlns:xalan="xalan://de.fzi.xslt.rot" xmlns:oracle="http://www.oracle.com/XSL/Transform/java/de.fzi.xslt.rot" exclude-result-prefixes="saxon xalan oracle">
...
```

Префикс `saxon` соответствует интерфейсу расширений в XSLT-процессоре Saxon, префикс `xalan` — процессору Xalan и префикс `oracle` — Oracle XSLT Processor.

Теперь осталось только найти поддерживаемый вариант расширения и произвести соответствующий вызов.

Листинг 10.9

```xml
<xsl:choose>
    <xsl:when test="function-available('saxon:X') ">
        <line x1="{saxon:X($x1, $y1, $alpha) + 100}" y1="{saxon:Y($x1, $y1, $alpha) + 100}" x2="{saxon:X($x2, $y2, $alpha) + 100}" y2="{saxon:Y($x2, $y2, $alpha) + 100}"/>
    </xsl:when>
    <xsl:when test="function-available('xalan:X')">
        <line x1="{xalan:X($x1, $y1, $alpha) + 100}" y1="{xalan:Y($x1, $y1, $alpha) + 100}" x2="{xalan:X($x2, $y2, $alpha) + 100}" y2="{xalan:Y($x2, $y2, $alpha) + 100}"/>
    </xsl:when>
    <xsl:when test="function-available('oracle:X')">
        <line x1="{oracle:X($x1, $y1, $alpha) + 100}" y1="{oracle:Y($x1, $y1, $alpha) + 100}" x2="{oracle:X($x2, $y2, $alpha) + 100}" y2="{oracle:Y($x2, $y2, $alpha) + 100}"/>
    </xsl:when>
    <xsl:otherwise>
        <xsl:message terminate="yes">
            <xsl:text>Necessary extension function is not available.</xsl:text>
            <xsl:text> Supported processors are:</xsl:text>
            <xsl:text> Saxon, Xalan, Oracle XSLT Processor.</xsl:text>
        </xsl:message>
    </xsl:otherwise>
</xsl:choose>
```

В случае, если хотя бы одна из функций `saxon:X`, `xalan:X`, `oracle:X` будет доступна при обработке, она будет использована процессором для создания атрибутов элемента `line`. В противном случае, процессор прервет выполнение преобразования и выведет указанное в элементе [`xsl:message`](/xslt/xsl-message/) сообщение.

Нельзя не согласиться с тем, что приведенный выше способ не отличается элегантностью. Реализовывать свой вариант для каждого существующего процессора может быть довольно трудоемкой задачей — но такова уж плата за возможности расширений.

## Ссылки

- [function-available()](https://developer.mozilla.org/en-US/docs/Web/XPath/Functions/function-available) на MDN
