---
layout: default
title: math​:highest
nav_order:
parent: EXSLT
---

<!-- prettier-ignore-start -->
1. TOC
{:toc}

# math​:highest()
{: .no_toc }
<!-- prettier-ignore-end -->

Поддержка браузерами:

- Mozilla Firefox 1.9+

## Синтаксис

```
math:highest(nodeSet)
```

## Описание и примеры

Функциональный подход:

```xml
<values>
	<value id="one">7</value>
	<value id="two">11</value>
	<value id="three">8</value>
	<value id="four">4</value>
</values>
```

```xml
<xsl:template match="values">
	<result>
		<xsl:text>Highest: </xsl:text>
		<xsl:value-of select="math:highest(value)/@id" />
	</result>
</xsl:template>
```

```xml
<result>Highest: two</result>
```

Шаблонный подход

```xml
<values>
	<value id="one">7</value>
	<value id="two">11</value>
	<value id="three">8</value>
	<value id="four">4</value>
</values>
```

```xml
<xsl:template match="values">
	<result>
		<xsl:text>Highest: </xsl:text>
		<xsl:call-template name="math:highest">
			<xsl:with-param name="nodes" select="value" />
		</xsl:call-template>
	</result>
</xsl:template>
```

```xml
<result>Highest: two</result>
```

## Ссылки

- [math​:highest()](https://developer.mozilla.org/en-US/docs/Web/EXSLT/math/highest) на MDN
