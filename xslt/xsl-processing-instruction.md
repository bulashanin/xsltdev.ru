---
layout: default
title: xsl:processing-instruction
nav_order: 25
parent: XSLT
---

<!-- prettier-ignore-start -->
# xsl:processing-instruction
{: .no_toc }
<!-- prettier-ignore-end -->

Элемент **`xsl:processing-instruction`** создает в результирующем дереве узел инструкции по обработке.

<!-- prettier-ignore -->
1. TOC
{:toc}

## Синтаксис

### XSLT 1.0

```xml
<xsl:processing-instruction
    name = "ncname">
    <!-- Содержимое: шаблон -->
</xsl:processing-instruction>
```

Атрибуты:

- **`name`** — **обязательный** атрибут, определяет имя целевого приложения, которому будет адресована инструкция по обработке. В этом атрибуте может быть указан шаблон значения атрибута.

### XSLT 2.0 и XSLT 3.0

```xml
<xsl:processing-instruction
    name = "ncname"
    select = "expression">
    <!-- Content: sequence-constructor -->
</xsl:processing-instruction>
```

## Описание и примеры

### Пример

Элемент:

```xml
<xsl:processing-instruction name="servlet">
    <xsl:text>links="follow" session-timeout="7200000"</xsl:text>
</xsl:processing-instruction>
```

создаст в выходящем документе инструкцию по обработке вида:

```xml
<?servlet links="follow" session-timeout="7200000"?>
```

Содержимым создаваемой инструкции по обработке является результат выполнения шаблона, содержащегося внутри элемента `xsl:processing-instruction`. Этот результат должен содержать только текстовые узлы, в противном случае процессор может либо выдать ошибку, либо проигнорировать нетекстовые узлы вместе с их содержимым.

Инструкция по обработке не может содержать последовательности символов "`?>`", поскольку это было бы некорректно с точки зрения синтаксиса XML.

В случае, если результат выполнения шаблона содержит такую комбинацию, процессор может либо выдать ошибку, либо разделить символы "`?`" и "`>`" пробелом:"`? >`".

Имя инструкции по обработке, должно быть корректным XML-именем (но не равным при этом "`xml`" в любом регистре символов). Например, следующее определение будет совершенно корректным:

```xml
<xsl:processing-instruction name="_">
    <xsl:text>logout _</xsl:text>
</xsl:processing-instruction>
```

В результате получится следующая инструкция:

```xml
<?_ logout _?>
```

Для того чтобы создать в выходящем XML-документе инструкцию `xml-stylesheet`, которая используется для связывания документов со стилями и преобразованиями, можно воспользоваться следующим определением:

```xml
<xsl:processing-instruction name="xml-stylesheet">
    <xsl:text>href="style.xsl" type="text/xsl"</xsl:text>
</xsl:processing-instruction>
```

Результирующий документ будет содержать инструкцию по обработке в виде:

```xml
<?xml-stylesheet href="style.xsl" type="text/xsl"?>
```

Элемент `xsl:processing-instruction` не может создать декларацию XML, несмотря на то, что с точки зрения синтаксиса (но не семантики) она имеет форму инструкции по обработке. Для вывода XML-декларации следует использовать элемент [`xsl:output`](/xslt/xsl-output/).

## Ссылки

- [`xsl:processing-instruction`](https://developer.mozilla.org/en/XSLT/processing-instruction) на MDN
- [`xsl:processing-instruction`](https://msdn.microsoft.com/en-us/library/ms256461.aspx) на MSDN
