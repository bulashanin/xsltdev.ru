---
layout: default
title: ceiling
nav_order: 2
parent: XPath
---

<!-- prettier-ignore-start -->
# ceiling()
{: .no_toc }
<!-- prettier-ignore-end -->

Функция **`ceiling`** возвращает наименьшее число (ближайшее в отрицательной бесконечности), которое не меньше значения представленного аргумента и является целым.

<!-- prettier-ignore -->
1. TOC
{:toc}

## Синтаксис

### XPath 1.0

```
number ceiling( number )
```

### XPath 2.0

```
numeric? ceiling(numeric?)
```

### Ввод

Число.

#### XPath 1.0

Если аргумент не является числом, он преобразуется в число так, как если бы он был обработан функцией [`number()`](/xpath/number/). Если аргумент не удается преобразовать в число, функция `ceiling()` возвращает значение NaN («нечисло»).

#### XPath 2.0

В XSLT 2.0 аргумент должен относиться к одному из четырех числовых типов (`xs:float`, `xs:decimal`, `xs:double` или `xs:integer`). В противном случае процессор XSLT выдает ошибку. Результат функции `ceiling()` относится к тому же типу, что и ее аргумент.

### Вывод

Наименьшее целое, не меньшее аргумента.

Если аргумент не может быть преобразован в число, в XSLT 1.0 функция `ceiling()` возвращает `NaN`.

Если аргумент не может быть преобразован в число, в XSLT 2.0 функция `ceiling()` выдает ошибку.

### Где определяется

- XPath 1.0 — XPath, раздел 4.4 «Number Functions».
- XPath 2.0 — XQuery 1.0 and XPath 2.0 Functions and Operators, раздел 6.4 «Functions on Numeric Values».

## Описание и примеры

### Пример 1

```
ceiling(2.3) ? 3
ceiling(-2.3) ? -2
ceiling(-1 div 0) ? -Infinity
ceiling(-1 div (-1 div 0)) ? 0
```

### Пример 2

Следующая таблица стилей демонстрирует результаты вызова функции `ceiling()` для разных значений. В качестве входных данных будет использоваться следующий документ XML:

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- chocolate.xml -->
<report month="8" year="2006">
	<title>Chocolate bar sales</title>
	<brand>
		<name>Lindt</name>
		<units>27408</units>
	</brand>
	<brand>
		<name>Callebaut</name>
		<units>8203</units>
	</brand>
	<brand>
		<name>Valrhona</name>
		<units>22101</units>
	</brand>
	<brand>
		<name>Perugina</name>
		<units>14336</units>
	</brand>
	<brand>
		<name>Ghirardelli</name>
		<units>19268</units>
	</brand>
</report>
```

Таблица стилей, использующая функцию `ceiling()`:

```xml
<?xml version="1.0"?>
<!-- ceiling.xsl -->
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
	<xsl:output method="text"/>
	<xsl:template match="/">
		<xsl:text>
Tests of the ceiling() function:
</xsl:text>
		<xsl:text> ceiling(7.983) = </xsl:text>
		<xsl:value-of select="ceiling(7.983)"/>
		<xsl:text>
ceiling(-7.893) = </xsl:text>
		<xsl:value-of select="ceiling(-7.893)"/>
		<xsl:text>
ceiling(avg(/report/brand/units)) = </xsl:text>
		<xsl:value-of select="ceiling(avg(/report/brand/units))"/>
		<xsl:text>
ceiling('blue') = </xsl:text>
		<xsl:value-of version="1.0" select="ceiling('blue')"/>
	</xsl:template>
</xsl:stylesheet>
```

Результат преобразования документа XML по таблице стилей:

```
Tests of the ceiling() function:
ceiling(7.983) = 8
ceiling(-7.893) = -7
ceiling(avg(/report/brand/units)) = 18264
ceiling('blue') = NaN
```

В последнем тесте в последнем элементе [`<xsl:value-of>`](/xslt/xsl-value-of/) мы указали версию "1.0". В режиме XSLT 1.0 функция возвращает результат `NaN` («нечисло»). При попытке обработать этот элемент [`<xsl:value-of>`](/xslt/xsl-value-of/) в режиме XSLT 2.0 происходит ошибка.

## См. также

- [floor()](/xpath/floor/) -- округление до ближайшего не большего целого
- [number()](/xpath/number/) -- конвертирует аргумент в числовой тип
- [round()](/xpath/round/) -- округляет число до ближайшего целого
- [sum()](/xpath/sum/) -- суммирует значения узлов

## Ссылки

- [ceiling()](https://docs.microsoft.com/en-us/previous-versions/dotnet/netframework-4.0/ms256087%28v%3dvs.100%29) на MDN
- [ceiling()](https://developer.mozilla.org/en/XPath/Functions/ceiling) на MSDN
