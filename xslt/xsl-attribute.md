---
layout: default
title: xsl:attribute
nav_order: 3
parent: XSLT
---

<!-- prettier-ignore-start -->
# xsl:attribute
{: .no_toc }
<!-- prettier-ignore-end -->

Элемент **`xsl:attribute`** служит для создания узлов атрибутов в выходном документе.

<!-- prettier-ignore -->
1. TOC
{:toc}

## Синтаксис

### XSLT 1.0

```xml
<xsl:attribute
	name = "имя"
	namespace = "пространство имен">
	<!-- Содержимое: template -->
</xsl:attribute>
```

Атрибуты:

- **`name`** — **обязательный** атрибут, указывает имя создаваемого атрибута. Может содержать шаблон значения, т. е. имя атрибута может быть вычислено во время выполнения.
- `namespace` — _необязательный_ атрибут, указывает URI пространства имен создаваемого атрибута. Может содержать шаблон значения, что позволяет вычислять пространство имен создаваемого элемента при помощи выражений.

### XSLT 2.0 и XSLT 3.0

```xml
<xsl:attribute
	name = "qname"
	namespace = "uri-reference"
	select = "expression"
	separator = "string"
	type = "qname"
	validation = "strict | lax | preserve | strip">
	<!-- Content: sequence-constructor -->
</xsl:attribute>
```

Атрибуты:

- **`name`** — **обязательный** атрибут, определяет имя атрибута.
- `namespace` — _необязательный_ атрибут, определяет URI-адрес пространства имен, которое должно использоваться для данного атрибута в выходном документе. Вы не можете управлять префиксом пространства имен; атрибут `namespace` позволяет задать только URI-адрес.
- `select` — _необязательный_ атрибут, выражение XPath, определяющее содержимое атрибута. Если элемент `<xsl:attribute>` содержит атрибут `select`, то сам элемент должен быть пустым.
- `separator` — _необязательный_ атрибут, определяет символы для разделения множественных значений, генерируемых инструкцией `<xsl:attribute>`. Если элемент `<xsl:attribute>` содержит атрибут `select`, по умолчанию в качестве разделителя используется пробел (`#x20`). Без атрибута `select` по умолчанию используется строка нулевой длины (""). Атрибут `separator` переопределяет значение по умолчанию независимо от того, присутствует атрибут `select` или нет.
- `type` — _необязательный_ атрибут, определяет тип данных атрибута. Им может быть любой из встроенных типов данных или же тип данных, определенный в схеме (при использовании схемосовместимого процессора XSLT 2.0). Атрибуты `type` и `validation` являются взаимоисключающими.
- `validation` — _необязательный_ атрибут, определяет способ проверки значения нового атрибута. Атрибут `validation` имеет четыре допустимых значения: `strict`, `lax`, `preserve` и `strip`. Поскольку мы создаем атрибут, а не элемент или итоговый документ, некоторые стандартные особенности атрибута `validation` здесь не действуют. Значения `strip` и `preserve` в данном случае ни на что не влияют. Они соответственно указывают, должно ли обозначение типа атрибута удаляться или сохраняться в сгенерированном атрибуте. Для атрибутов проверка не выполняется, и они имеют обозначение типа `xs:untypedAtomic`. Атрибут `validation="strict"` означает, что процессор XSLT должен искать во всех объявленных схемах глобальное объявление атрибута (`<xs:attribute>`) с таким же именем, как у данного атрибута. Если процессору не удается найти подходящий элемент `<xs:attribute>`, происходит фатальная ошибка. Если же процессор находит объявление атрибута, он проверяет по нему сгенерированное значение. Последнее значение `validation="lax"` работает аналогично `validation="strict"`, но если процессору не удается найти объявление атрибута ни в одной из объявленных схем, ошибка не происходит. В этом случае атрибут имеет обозначение типа `xs:untypedAtomic`. Атрибуты `validation` и `type` являются взаимоисключающими.

Особенности обращения с `xsl:attribute`:

- Атрибуты могут создаваться только в узлах элементов. Если атрибут создается в узле, который не является узлом элемента, процессор может либо выдать ошибку, либо проигнорировать создаваемый атрибут.
- Атрибуты могут содержать только текстовые узлы. Процессор может либо выдать ошибку, либо проигнорировать нетекстовые узлы.
- Узлы атрибутов должны быть первыми узлами, которые создаются в элементах. XSLT не разрешает создавать атрибуты после того, как в элемент включены дочерние узлы других типов.
- В случае, когда документ преобразуется в другой XML-документ, символы перевода строки в элементе заменяются символьными сущностями.

### Пример 1

Покажем, как преобразовать структуру вида:

```xml
<element name="record">
	<attribute name="fieldcount" value="12" />
	<attribute name="title" value="Aggregation" />
</element>
```

в элемент `<record fieldcount="12" title="Aggregation"/>`.

Для достижения цели воспользуемся следующим преобразованием:

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

	<xsl:template match="element">
		<xsl:element name="{@name}">
			<xsl:apply-templates select="attribute"/>
		</xsl:element>
	</xsl:template>

	<xsl:template match="attribute">
		<xsl:attribute name="{@name}">
			<xsl:value-of select="@value"/>
		</xsl:attribute>
	</xsl:template>

</xsl:stylesheet>
```

Элемент `xsl:attribute` не может использоваться где угодно: узлы атрибутов должны создаваться только как дочерние узлы узлов элементов. Более того, узлы атрибутов должны создаваться до создания дочерних узлов других типов — текста, элементов и так далее. Таким образом, `xsl:attribute` может быть использован в содержимом любого из следующих родителей:

- литерального элемента результата;
- элемента [`xsl:element`](/xslt/xsl-element/);
- элемента [`xsl:copy`](/xslt/xsl-copy/) в случае, если текущий, копируемый узел является элементом;
- элемента [`xsl:attribute-set`](/xslt/xsl-attribute-set/) в случае определения именованного набора атрибутов.

При этом, `xsl:attribute` не обязан использоваться только в качестве их непосредственного дочернего элемента. Главное, чтобы атрибуты создавались в элементах и только в элементах.

Элемент `xsl:attribute` также не может использоваться для генерации объявлений пространств имен. В соответствии с технической рекомендацией XSLT, `xsl:attribute` не может создавать атрибуты, имена которых имеют префикс `xmlns`.

Если атрибут создается в элементе, который уже имеет атрибут с таким же именем, старый атрибут будет переопределен новым значением.

### Пример 2

Фрагмент шаблона:

```xml
<а href="http://www.aaa.com">
	<xsl:attribute name="href">
		<xsl:text>http://www.bbb.com</xsl:text>
	</xsl:attribute>
</a>
```

Результат: `<a href="http://www.bbb.com" />`.

Поскольку атрибут может содержать только текст, результатом выполнения содержимого `xsl:attribute` тоже должны быть только текстовые узлы. Процессор в лучшем случае проигнорирует нетекстовые узлы, в худшем выведет сообщение об ошибке, прервав дальнейшую обработку, так что следует очень внимательно относиться к содержимому `xsl:attribute`.

Текстовое значение атрибута может задаваться не только символьными данными. Оно может генерироваться также элементами XSLT, такими, как, например, [`xsl:text`](/xslt/xsl-text/) и [`xsl:value-of`](/xslt/xsl-value-of/). То есть вполне корректным будет следующее определение:

```xml
<xsl:attribute name="href">
	<xsl:text>http://</xsl:text>
	<xsl:value-of select="concat('www', '.', 'bbb')" />
	<xsl:text>.com</xsl:text>
</xsl:attribute>
```

В том случае, если текстовое значение атрибута содержит символы перевода строки, при генерации атрибута они будут заменены сущностями, то есть определение

```xml
<xsl:attribute name="href">а
b</xsl:attribute>
```

создаст атрибут с именем `href` и значением `<code>a&</code><code>#xA;b</code>`:

```xml
<а href="a&<!--  -->#xA;b" />
```

Техническая рекомендация объясняет такую ситуацию следующим образом: в соответствии со стандартом языка XML, символы перевода строки должны нормализоваться в значениях атрибутов пробелами, сущности же нормализовать не нужно. Но если бы символ перевода строки нормализовался в XSLT при выводе пробелом, то определения:

```xml
<xsl:attribute name="href">a b</xsl:attribute>
```

и

```xml
<xsl:attribute name="href">a&<!-- -->#xA;b</xsl:attribute>
```

(из-за особенностей парсера пример следует читать без пустого комментария)

были бы эквивалентны, что не отражает реального положения вещей. Для того чтобы исправить эту несуразицу, символ перевода строки при выводе в атрибуте нормализуется в XSLT символьной сущностью.

### Пример 3

Следующий короткий пример демонстрирует применение новых атрибутов `select` и `separator`. В таблице стилей диапазонное выражение XPath 2.0 (выражение "`to`") используется для присваивания последовательности значений атрибуту `example`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- attribute2.xsl -->
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
	<xsl:output method="xml" omit-xml-declaration="yes"/>
	<xsl:template match="/">
		<sampledoc>
			<xsl:attribute name="example" select="1 to 7" separator=", "/>
		</sampledoc>
	</xsl:template>
</xsl:stylesheet>
```

Таблица стилей генерирует очень короткий документ:

```xml
<sampledoc example="1, 2, 3, 4, 5, 6, 7"/>
```

Благодаря атрибуту XSLT 2.0 `separator` вам не придется самостоятельно реализовывать логику следующего вида:

```xml
<xsl:for-each>
	<xsl:value-of select="."/>
	<xsl:if test="position() != last()">
		<xsl:text>, </xsl:text>
	</xsl:if>
</xsl:for-each>
```

### Пример 4

В последнем примере используются схемосовместимые атрибуты `<xsl:attribute>`. Наша таблица стилей содержит импортированную схему, определяющую новый тип данных; атрибут `<xsl:attribute>` используется для создания атрибутов с этим типом данных. Таблица стилей выглядит так:

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- attribute3.xsl -->
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:zip="http://www.oreilly.com/xslt/zip" xmlns:xs="http://www.w3.org/2001/XMLSchema" exclude-result-prefixes="xs">
	<xsl:output method="xml" indent="yes"/>
	<xsl:import-schema namespace="http://www.oreilly.com/xslt/zip">
		<xsd:schema xmlns="http://www.oreilly.com/xslt/zip" targetNamespace="http://www.oreilly.com/xslt/zip" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
			<xsd:simpleType name="zipcode">
				<xsd:restriction base="xsd:string">
					<xsd:pattern value="[0-9]{5}(-[0-9]{4})?"/>
				</xsd:restriction>
			</xsd:simpleType>
		</xsd:schema>
	</xsl:import-schema>
	<xsl:template match="/">
		<postcodes>
			<xsl:for-each select="postcodes/postcode">
				<postcode>
					<xsl:choose>
						<xsl:when test=". castable as zip:zipcode">
							<xsl:attribute name="zip:zip" type="zip:zipcode">
								<xsl:value-of select=". cast as zip:zipcode"/>
							</xsl:attribute>
						</xsl:when>
						<xsl:otherwise>
							<xsl:attribute name="other" type="xs:string">
								<xsl:value-of select="."/>
							</xsl:attribute>
						</xsl:otherwise>
					</xsl:choose>
				</postcode>
			</xsl:for-each>
		</postcodes>
	</xsl:template>
</xsl:stylesheet>
```

Таблица стилей используется для обработки следующего документа:

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- postcodes.xml -->
<postcodes>
	<postcode>3S8 E0X</postcode>
	<postcode>37174</postcode>
	<postcode>NSW 3829</postcode>
	<postcode>27516</postcode>
</postcodes>
```

Таблица стилей использует оператор XPath `castable as` для определения того, может ли значение из исходного документа быть преобразовано в значение `zip:zipcode`. Если проверка дает положительный результат, мы создаем новый атрибут с типом данных `zip:zipcode`. Результат:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<postcodes xmlns:zip="http://www.oreilly.com/xslt/zip">
	<postcode other="3S8 E0X"/>
	<postcode zip:zip="37174"/>
	<postcode other="NSW 3829"/>
	<postcode zip:zip="27516"/>
</postcodes>
```

Два атрибута из сгенерированного набора уточняются пространством имен и содержат значения соответствующего типа данных.

### См. также

- [`xsl:attribute-set`](/xslt/xsl-attribute-set/) -- определяет именованный набор атрибутов.

### Ссылки

- [`xsl:attribute`](https://developer.mozilla.org/en/XSLT/attribute) на MDN
- [`xsl:attribute`](https://msdn.microsoft.com/en-us/library/ms256165.aspx) на MSDN
