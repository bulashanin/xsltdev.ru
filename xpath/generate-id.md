---
layout: default
title: generate-id
nav_order: 13
parent: XPath
---

<!-- prettier-ignore-start -->
# generate-id()
{: .no_toc }
<!-- prettier-ignore-end -->

Функция **`generate-id`** возвращает уникальный строковый идентификатор первого в порядке просмотра документа узла, передаваемого ей в виде аргумента.

Если аргумент опущен, функция возвращает уникальный идентификатор контекстного узла. Если аргументом является пустое множество, функция должна возвращать пустую строку.

<!-- prettier-ignore -->
1. TOC
{:toc}

## Синтаксис

### XPath 1.0

```
string generate-id( node-set? )
```

## Описание и примеры

Функция `generate-id` обладает следующими свойствами.

- Функция `generate-id` возвращает для двух узлов один и тот же идентификатор тогда и только тогда, когда эти два узла совпадают. Это означает, что во время выполнения одного преобразования функция `generate-id` будет возвращать один идентификатор для одного и того же узла, а для разных узлов `generate-id` обязательно возвратит разные идентификаторы.
- Возвращаемый идентификатор состоит только из цифр и букв ASCII и начинается буквой, то есть синтаксически является корректным XML-именем и может использоваться как имя элемента, атрибута, как значение ID-атрибута или в любом другом месте, где могут использоваться имена XML.

Кроме этого спецификация оговаривает следующие важные положения, которые мы приведем ниже.

- Процессор не обязан генерировать один и тот же идентификатор при разных выполнениях преобразования одного и того же документа. Иными словами, если в понедельник процессор X при выполнении преобразования Y сгенерирует для узла Z документа D идентификатор I, то во вторник тот же процессор X при выполнении того же преобразования Y с тем же документом D может сгенерировать для того же самого узла Z совершенно другой, отличный от I идентификатор.
- Форма возвращаемого идентификатора может быть произвольной, но при этом она должна удовлетворять описанному выше синтаксису. Это означает, что каждый процессор может по-своему генерировать идентификатор. Спецификация не определяет никакого стандартного метода реализации функции `generate-id`.
- Генерируемый идентификатор может совпадать, а может и не совпадать со значениями уникальных атрибутов, то есть атрибутов, тип данных которых объявлен в блоке DTD как ID.

Помимо очевидного применения, например, для явного задания уникального идентификатора в выходящем документе, функция `generate-id` совершено неожиданным образом облегчает задачи группировки.

### Пример

Предположим, что в наших XML-документах изменилась логическая схема: теперь каждый элемент `item` должен обладать уникальным атрибутом `id`.

Выполнить задачу конвертации может простое преобразование.

Листинг 8.70. Преобразование

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:template match="@*|node()">
        <xsl:copy>
            <xsl:apply-templates select="@*|node()"/>
        </xsl:copy>
    </xsl:template>
    <xsl:template match="item">
        <xsl:copy>
            <xsl:attribute name="id">
                <xsl:text><xsl:value-of select="generate-id()"/><xsl:text>
            </xsl:attribute>
            <xsl:apply-templates select="@*|node()"/>
        </xsl:copy>
    </xsl:template>
</xsl:stylesheet>
```

В выходящем документе элементы `item` будут иметь уникальные идентификаторы.

Листинг 8.71. Выходящий документ

```
<?xml version="1.0" encoding="utf-8"?>
<items>
    <item id="b1b1b2" source="a" name="A"/>
    <item id="b1b1b4" source="b" name="B"/>
    ...
    <item id="b1b1c34" source="a" name="F"/>
</items>
```

Сразу оговоримся, что этот способ будет работать не всегда: `generate-id` создает идентификатор, который является уникальным среди всех остальных идентификаторов узлов, а не среди всех значений уникальных атрибутов документа. Так что если бы какой-либо элемент имел ID-атрибут со значением `b1b1b4`, выходящий документ перестал бы быть правильным. Однако же, если в документе до преобразования вообще не было уникальных атрибутов, все будет в порядке.

## Ссылки

- [generate-id()](https://developer.mozilla.org/en-US/docs/Web/XPath/Functions/generate-id) на MDN
