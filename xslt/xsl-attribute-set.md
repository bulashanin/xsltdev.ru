---
layout: default
title: xsl:attribute-set
nav_order: 4
parent: XSLT
---

<!-- prettier-ignore-start -->
# xsl:attribute-set
{: .no_toc }
<!-- prettier-ignore-end -->

Элемент **`xsl:attribute-set`** определяет именованный набор атрибутов.

<!-- prettier-ignore -->
1. TOC
{:toc}

## Синтаксис

### XSLT 1.0 и 2.0

```xml
<xsl:attribute-set
	name = "имя"
	use-attribute-sets = "имена">
	<!-- Содержимое: xsl:attribute* -->
</xsl:attribute-set>
```

Атрибуты:

- **`name`** — **обязательный** атрибут, задает имя набора атрибутов.
- `use-attribute-sets` — _необязательный_ атрибут, задает перечень названий наборов атрибутов через пробел.

### XSLT 3.0

```xml
<xsl:attribute-set
	name = "eqname"
	use-attribute-sets = "eqnames"
	visibility = "public | private | final | abstract"
	streamable = "boolean" >
	<!-- Содержимое: xsl:attribute* -->
</xsl:attribute-set>
```

Атрибуты:

- **`name`** — **обязательный** атрибут
- `use-attribute-sets` — _необязательный_ атрибут
- `visibility` — _необязательный_ атрибут
- `streamable` — _необязательный_ атрибут

## Описание и примеры

Для того чтобы упростить создание в элементах целых наборов атрибутов, можно заранее определить их в элементе `xsl:attribute-set`. Обязательный атрибут `name` задает имя набора атрибутов. Элемент `xsl:attribute-set` содержит последовательность, состоящую из нуля или более элементов [`xsl:attribute`](/xslt/xsl-attribute/).

Именованные наборы атрибутов можно использовать, указывая их имена в значении атрибута `use-attribute-sets`, который может присутствовать в элементах [`xsl:element`](/xslt/xsl-element/), [`xsl:copy`](/xslt/xsl-copy/) и `xsl:attribute-set`, а также в литеральных результирующих элементах. В атрибуте `use-attribute-sets` через пробел перечисляются имена наборов атрибутов, которые должны быть использованы в данном элементе.

Включение набора атрибутов в элемент равносильно простому копированию элементов `xsl:attribute`, определенных в соответствующих элементах `xsl:attribute-set`.

### Пример 1

В следующем примере сперва создается именованный набор атрибутов `title-style`, а затем используется в правиле шаблона.

```xml
<xsl:attribute-set name="title-style">
	<xsl:attribute name="font-size">12pt</xsl:attribute>
	<xsl:attribute name="font-weight">bold</xsl:attribute>
</xsl:attribute-set>

<xsl:template match="chapter">
	<p quadding="start" xsl:use-attribute-sets="title-style">
		<xsl:value-of select="self::node()"/>
	</p>
</xsl:template>
```

### Пример 2

Предположим, что во входящем документе нам нужно вывести структуру, состоящую из элементов с именем `element`, атрибут name которых равен имени, атрибут `attr-count` — количеству атрибутов, а атрибут `node-count` — количеству дочерних узлов соответствующего элемента.

Входной документ:

```xml
<a b="1" c="2">
	<d e="3" f="4" g="5" />
</a>
```

Преобразование:

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
	<xsl:output indent="yes" />

	<xsl:attribute-set name="attrs">
		<xsl:attribute name="attr-count">
			<xsl:value-of select="count(@*)" />
		</xsl:attribute>
	</xsl:attribute-set>

	<xsl:attribute-set name="elements">
		<xsl:attribute name="name">
			<xsl:value-of select="name()" />
		</xsl:attribute>
		<xsl:attribute name="node-count">
			<xsl:value-of select="count(*)" />
		</xsl:attribute>
	</xsl:attribute-set>

	<xsl:template match="*">
		<xsl:element name="element" use-attribute-sets="elements attrs">
			<xsl:apply-templates select="*" />
		</xsl:element>
	</xsl:template>

</xsl:stylesheet>
```

Выходной документ:

```xml
<?xml version="1.0" encoding="utf-8"?>
<element name="a" node-count="1" attr-count="2">
	<element name="d" node-count="0" attr-count="3"/>
</element>
```

В этом преобразовании определение элемента:

```xml
<xsl:element name="element" use-attribute-sets="elements attrs">
	<xsl:apply-templates select="*"/>
</xsl:element>
```

равносильно определению:

```xml
<xsl:element name="element">
	<xsl:attribute name="name">
		<xsl:value-of select="name()"/>
	</xsl:attribute>
	<xsl:attribute name="node-count">
		<xsl:value-of select="count(*)"/>
	</xsl:attribute>
	<xsl:attribute name="attr-count">
		<xsl:value-of select="count(@*)"/>
	</xsl:attribute>
	<xsl:apply-templates select="*"/>
</xsl:element>
```

Как уже было сказано, элемент `xsl:attribute-set` может также использовать другие наборы атрибутов при помощи `use-attribute-sets`. Например, в предыдущем преобразовании набор атрибутов `elements` мог быть определен как:

```xml
<xsl:attribute-set name="elements" use-attribute-sets="attrs">
	<xsl:attribute name="name">
		<xsl:value-of select="name()" />
	</xsl:attribute>
	<xsl:attribute name="node-count">
		<xsl:value-of select="count(*)" />
	</xsl:attribute>
</xsl:attribute-set>
```

Тогда для достижения того же результата элемент с именем `element` мог быть создан с использованием только одного набора атрибутов:

```xml
<xsl:element name="element" use-attribute-sets="elements">
	<xsl:apply-templates select="*" />
</xsl:element>
```

## См. также

- [`xsl:attribute`](/xslt/xsl-attribute/) -- служит для создания узлов атрибутов.

## Ссылки

- [`xsl:attribute-set`](https://developer.mozilla.org/en/XSLT/attribute-set) на MDN
- [`xsl:attribute-set`](https://msdn.microsoft.com/en-us/library/ms256163.aspx) на MSDN
