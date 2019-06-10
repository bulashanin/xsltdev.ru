---
layout: default
title: system-property
nav_order: 33
parent: XPath
---

<!-- prettier-ignore-start -->
# system-property()
{: .no_toc }
<!-- prettier-ignore-end -->

Функция **`system-property`** возвращает значение свойства, которое определяется ее строковым параметром.

Аргумент этой функции должен представлять расширенное имя системного свойства. Если процессор не поддерживает свойство с таким именем, функция должна вернуть пустую строку.

<!-- prettier-ignore -->
1. TOC
{:toc}

## Синтаксис

### XPath 1.0

```
object system-property( string )
```

## Описание и примеры

Эта функция предназначена для получения информации об окружении, в котором производится преобразование. В стандарте языка указано, что все процессоры в обязательном порядке должны поддерживать следующие системные свойства:

- `xsl:version` — это свойство должно возвращать номер версии языка XSLT, которую поддерживает данный процессор.
- `xsl:vendor` — это свойство должно возвращать текстовую информацию о производителе используемого процессора.
- `xsl:vendor-uri` — это свойство должно возвращать URL производителя — как правило, `xsl:vendor-uri` — это адрес Web-сайта производителя процессора.

К сожалению, в первой версии языка XSLT процессоры обязаны поддерживать только эти свойства. Очень полезным, было бы, например, свойство, возвращающее имя преобразования или преобразовываемого файла. К сожалению, ничего подобного в стандарте не предусмотрено.

### Пример

В качестве примера приведем небольшой шаблон, выводящий в виде комментария информацию о процессоре.

Листинг 8.72. Шаблон, выводящий системную информацию

```xml
<xsl:template name="info">
    <xsl:comment>
        <xsl:text> | XSLT Version: </xsl:text>
        <xsl:value-of select="format-number(system-property('xsl:version'), '0.0')"/>
        <xsl:text> | XSLT Processor: </xsl:text>
        <xsl:value-of select="system-property('xsl:vendor')"/>
        <xsl:text> | URL: </xsl:text>
        <xsl:value-of select="system-property('xsl:vendor-url')"/>
        <xsl:text> +</xsl:text>
    </xsl:comment>
</xsl:template>
```

Процессор SAXON, написанный Майклом Кеем (Michael Kay), выводит следующий комментарий:

```
<!--
 | XSLT Version: 1.0
 | XSLT Processor: SAXON 6.0.2 from Michael Kay of ICL
 | URL: http://users.iclway.co.uk/mhkay/saxon/index.html
 +-->
```

Ожидается, что в будущих версиях XSLT набор системных свойств будет расширен. Кроме того, многие процессоры поддерживают дополнительные системные свойства, не оговоренные в спецификации.

## Ссылки

- [system-property()](https://developer.mozilla.org/en-US/docs/Web/XPath/Functions/system-property) на MDN
