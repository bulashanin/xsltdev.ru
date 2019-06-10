---
layout: default
title: xsl:message
nav_order: 18
parent: XSLT
---

<!-- prettier-ignore-start -->
# xsl:message
{: .no_toc }
<!-- prettier-ignore-end -->

Элемент **`xsl:message`** указывает процессору на то, что он должен вывести сообщение, которое является результатом обработки шаблона, содержащегося в этом элементе.

Механизм вывода сообщения зависит от реализации того или иного процессора и может быть различным — от вывода текста сообщения на экран до вызова внешнего модуля для обработки сообщения.

<!-- prettier-ignore -->
1. TOC
{:toc}

## Синтаксис

### XSLT 1.0

```xml
<xsl:message
    terminate = "yes | no">
    <!-- Content: template -->
</xsl:message>
```

Атрибуты:

- `terminate` — _необязательный_ атрибут, указывает на то, должен ли процессор прекратить дальнейшую обработку документа или нет. Значением этого атрибута по умолчанию является "`no`", что означает, что процессор должен просто вывести сообщения и продолжать дальнейшее выполнение шаблона. Если же в `xsl:message` указано `terminate="yes"`, то процессор, выведя сообщение, прервет обработку. Этот прием может использоваться, например, для того, чтобы проверять входящие документы на соответствие определенной схеме.

### XSLT 2.0

```xml
<xsl:message
    select? = expression
    terminate? = { "yes" | "no" }>
    <!-- Content: sequence-constructor -->
</xsl:message>
```

Атрибуты:

- `terminate` — _необязательный_ атрибут, если атрибут содержит значение `yes`, процессор XSLT прерывает выполнение после выдачи сообщения. По умолчанию используется значение `no`; если `<xsl:message>` не прерывает работу процессора, то обработка продолжается после отправки сообщения. В XSLT 2.0 значение атрибута `terminate` может быть шаблоном значения атрибута, то есть может вычисляться на стадии выполнения.
- `select` — _необязательный_ атрибут, выражение XPath, определяющее содержимое сообщения.

### XSLT 3.0

```xml
<xsl:message
    select? = expression
    terminate? = { boolean }
    error-code? = { eqname } >
    <!-- Content: sequence-constructor -->
</xsl:message>
```

## Описание и примеры

### Пример 1

Иногда в процессе отладки преобразования бывает полезно выводить сообщения о том, какой элемент обрабатывается в данный момент.

Листинг 8.5. Входящий документ

```xml
<a><b><c><d/></c></b></a>
```

Листинг 8.6. Преобразование

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:template match="*">
        <element name="{name()}">
            <xsl:message>
                <xsl:text>Processing element </xsl:text>
                <xsl:value-of select="name()"/>
                <xsl:if test="parent::*">
                    <xsl:text> which has a parent element </xsl:text>
                    <xsl:value-of select="name(..)"/>
                </xsl:if>
                <xsl:text>.</xsl:text>
            </xsl:message>
            <xsl:apply-templates/>
        </element>
    </xsl:template>
</xsl:stylesheet>
```

Листинг 8.7. Выходящий документ

```xml
<element name="a">
    <element name="b">
        <element name="c">
            <element name="d"/>
        </element>
    </element>
</element>
```

Листинг 8.8. Сообщения процессора

```
Processing element a.
Processing element b which has a parent element a.
Processing element c which has a parent element b.
Processing element d which has a parent element c.
```

Атрибут `terminate` указывает на то, должен ли процессор прекратить дальнейшую обработку документа или нет. Значением этого атрибута по умолчанию является "`no`", что означает, что процессор должен просто вывести сообщения и продолжать дальнейшее выполнение шаблона. Если же в `xsl:message` указано `terminate="yes"`, то процессор, выведя сообщение, прервет обработку. Этот прием может использоваться, например, для того, чтобы проверять входящие документы на соответствие определенной схеме.

### Пример 2

При помощи `xsl:message` мы можем запретить обработку документов, которые не имеют в корне элемент с именем "`html`" в любом регистре символов.

Листинг 8.9. Шаблон преобразования

```xml
<xsl:template match="/">
    <xsl:if test="translate(name(*),'html','HTML')!='HTML'">
        <xsl:message terminate="yes">
            <xsl:text>Document has no root HTML element.</xsl:text>
        </xsl:message>
    </xsl:if>
</xsl:template>
```

Если мы будем обрабатывать документ вида

```xml
<hTmL>
    <body/>
</hTmL>
```

обработка не будет прервана, в то время как преобразование документа

```xml
<ht-ml>
    <body/>
</ht-ml>
```

будет прервано сообщением:

```
Document has no root HTML element:
Processing terminated using xsl:message
```

## См. также

- [`xsl:function`](/xslt/xsl-function/) -- определяет функцию.

## Ссылки

- [`xsl:message`](https://developer.mozilla.org/en-US/docs/Web/XSLT/import) на MDN
- [`xsl:message`](https://msdn.microsoft.com/en-us/library/ms256441.aspx) на MSDN
