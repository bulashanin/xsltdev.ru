---
layout: default
title: xsl:copy-of
nav_order: 9
parent: XSLT
---

<!-- prettier-ignore-start -->
# xsl:copy-of
{: .no_toc }
<!-- prettier-ignore-end -->

Использование элемента **`xsl:copy-of`** полностью аналогично использованию элемента [`xsl:value-of`](/xslt/xsl-value-of/) за тем исключением, что `xsl:copy-of` при выводе значения выражения преобразует его к строке не во всех случаях.

<!-- prettier-ignore -->
1. TOC
{:toc}

## Синтаксис

### XSLT 1.0

```xml
<xsl:copy-of
    select = "выражение" />
```

Атрибуты:

- **`select`** — **обязательный** атрибут, выражение вычисляет набор копируемых узлов.

### XSLT 2.0 и XSLT 3.0

```xml
    <xsl:copy-of
        select = expression
        copy-namespaces? = "yes" | "no"
        type? = qname
        validation? = "strict" | "lax" | "preserve" | "strip" />
```

Атрибуты:

- **`select`** — **обязательный** атрибут, содержит выражение XPath, определяющее узлы, копируемые в выходной документ.
- `copy-namespaces` — _необязательный_ атрибут, определяет, должны ли копироваться пространства имен. Применяется только при копировании узлов элементов. Допустимые значения: `yes` (используется по-умолчанию) и `no`.
- `type` — _необязательный_ атрибут, определяет тип данных копируемого узла. Им может быть любой из встроенных типов данных или же тип данных, определенный в схеме (при использовании схемосовместимого процессора XSLT 2.0). Атрибуты `type` и `validation` являются взаимоисключающими.
- `validation` — _необязательный_ атрибут, определяет способ проверки значения нового атрибута. Атрибут `validation` имеет четыре допустимых значения: `strict`, `lax`, `preserve` и `strip`. Атрибут `validation="strict"` означает, что процессор XSLT должен искать во всех объявленных схемах объявление узла (`<xs:attribute>` или `<xs:element>`) с таким же именем, как у копируемого узла. Если процессору не удается найти подходящее объявление, происходит фатальная ошибка. Если же процессор находит объявление узла, он проверяет по нему значение копируемого узла. Значение `validation="lax"` работает аналогично `validation="strict"`, но если процессору не удается найти объявление копируемого узла ни в одной из объявленных схем, ошибка не происходит. В этом случае скопированному атрибуту или элементу присваивается обозначение типа `xs:untypedAtomic` или `xs:untyped` соответственно. Со значением `validation="preserve"` все скопированные узлы сохраняют свои обозначения типов. Наконец, значение `validation="strip"` удаляет все обозначения типов из всех скопированных узлов. Скопированные узлы атрибутов будут иметь обозначение типа `xs:untypedAtomic`, а скопированные узлы элементов – обозначение типа `xs:untyped`. Атрибуты `validation` и `type` являются взаимоисключающими.

## Описание и примеры

Поведение `xsl:copy-of` зависит от того, какой тип данных возвращает выражение.

- Если результат вычисления имеет булевый, числовой или строковый тип, то `xsl:copy-of` выводит его в виде текстового узла. В этом случае поведение `xsl:copy-of` абсолютно не отличается от поведения элемента [`xsl:value-of`](/xslt/xsl-value-of/).
- Если результатом вычисления выражения является множество узлов `(node-set)`, то `xsl:copy-of` копирует в выходящий документ все узлы в порядке просмотра документа вместе с их потомками.
- Если результатом вычисления является результирующий фрагмент дерева, то он копируется в выходящий документ в неизмененном виде.

### Пример

Рассмотрим пример.

Листинг 7.20. Входящий документ

```xml
<values>
    <boolean>false</boolean>
    <string>text</string>
    <number>3.14</number>
    <node-set>
        <item>10</item>
        <item>20</item>
        <item>30</item>
    </node-set>
    <tree>
        text
        <root>
            text
            <branch>
                text
                <leaf />
                <leaf />
            </branch>
            <leaf/>
        </root>
    </tree>
</values>
```

Листинг 7.21. Преобразование

```xml
<xsl:stylesheet
    version="1.0"
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

<xsl:template match="/">
    <xsl:variable name="boolean" select="values/boolean='true'"/>
    <xsl:variable name="string" select="string(values/string)"/>
    <xsl:variable name="number" select="number(values/number)"/>
    <xsl:variable name="node-set" select="values/node-set/*"/>
    <xsl:variable name="tree">
        <xsl:copy-of select="values/tree/*"/>
    </xsl:variable>

    <xsl:text> Value-of boolean:</xsl:text>
    <xsl:value-of select="$boolean"/>
    <xsl:text> Copy-of boolean:</xsl:text>
    <xsl:copy-of select="$boolean"/>

    <xsl:text> Value-of string:</xsl:text>
    <xsl:value-of select="$string"/>
    <xsl:text> Copy-of string:</xsl:text>
    <xsl:copy-of select="$string"/>

    <xsl:text> Value-of number:</xsl:text>
    <xsl:value-of select="$number"/>
    <xsl:text> Copy-of number:</xsl:text>
    <xsl:copy-of select="$number"/>

    <xsl:text> Value-of node-set:</xsl:text>
    <xsl:value-of select="$node-set"/>
    <xsl:text> Copy-of node-set:</xsl:text>
    <xsl:copy-of select="$node-set"/>

    <xsl:text> Value-of tree:</xsl:text>
    <xsl:value-of select="$tree"/>
    <xsl:text> Copy-of tree:</xsl:text>
    <xsl:copy-of select="$tree"/>
</xsl:template>

</xsl:stylesheet>
```

Листинг 7.22. Выходящий документ

```
Value-of boolean:false
Copy-of boolean:false
Value-of string:text
Copy-of string:text
Value-of number:3.14
Copy-of number:3.14
Value-of node-set:10
Copy-of node-set:<item>10</item><item>20</item><item>30</item>
Value-of tree:
    text
        text
Copy-of tree:<root>
    text
    <branch>
        text
        <leaf/>
        <leaf/>
    </branch>
    <leaf/>
</root>
```

Учтите, что в XSLT 1.0 и 2.0 поведение этого элемента различно:

Для XSLT 1.0:

- Если атрибут `select` определяет фрагмент дерева результата, то весь фрагмент копируется в дерево результата.
- Если атрибут `select` определяет набор узлов, то все узлы набора копируются в дерево результата в порядке документа. В отличие от [`<xsl:copy>`](/xslt/xsl-copy/), узел копируется полностью – со всеми узлами пространств имен, атрибутов и дочерними узлами.
- Если атрибут `select` определяет нечто отличное от фрагмента дерева результата или набора узлов, это «нечто» преобразуется в строку и вставляется в дерево результата.

Для XSLT 2.0:

- Если атрибут `select` определяет элемент, то этот элемент со всеми потомками и атрибутами копируется в выходной документ. По умолчанию узлы пространства имен элемента тоже копируются, хотя это поведение можно изменить при помощи атрибута `copy-namespaces`.
- Если атрибут `select` указывает на узел документа, этот узел документа со всеми потомками копируется в выходной документ.
- Все остальные типы узлов (узлы атрибутов, пространств имен, текста, комментариев и инструкций по обработке) копируются в выходной документ.
- Атомарные значения присоединяются к итоговой последовательности.

## См. также

- [`xsl:value-of`](/xslt/xsl-value-of/)
- [`xsl:copy`](/xslt/xsl-copy/)

## Ссылки

- [`xsl:copy-of`](https://developer.mozilla.org/en/XSLT/copy-of) на MDN
- [`xsl:copy-of`](https://msdn.microsoft.com/en-us/library/ms256183.aspx) на MSDN
