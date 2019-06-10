---
layout: default
title: document
nav_order: 7
parent: XPath
---

<!-- prettier-ignore-start -->
# document()
{: .no_toc }
<!-- prettier-ignore-end -->

Функция **`document`** позволяет обращаться к внешним документам по их URI.

<!-- prettier-ignore -->
1. TOC
{:toc}

## Синтаксис

### XPath 1.0

```
node-set document( object, node-set? )
```

## Описание и примеры

Функция `document` возвращает множество узлов. В простейшем случае это множество будет состоять из корневого узла внешнего документа. Функцию `document` можно использовать в более сложных XPath-выражениях, например в выражениях фильтрации. Так функция

```xml
<xsl:copy-of select="document('http://www.w3.org')/html/body/a"/>
```

скопирует все элементы а, находящиеся в теле (`/html/body`) внешнего документа.

Базовый сценарий использования функции `document` очень прост: ей передается строка, содержащая URI внешнего ресурса, а результатом является множество узлов, состоящее из корня внешнего документа. Однако на этом возможности `document` не заканчиваются. Мы рассмотрим несколько вариантов вызова функции `document` с параметрами различного типа.

### Вызов document( string )

В случае если функции `document` передана строка, возвращаемое множество будет состоять из корневого узла внешнего документа. URI этого документа как раз и сообщается строковым аргументом функции `document`.

Интересной особенностью является возможность передать пустую строку:

```
document('')
```

В этом случае `document` возвратит корневой узел самого преобразования. При помощи `document('')` можно получать доступ к информации, хранящейся в самом преобразовании (оно ведь тоже является ХМL-документом). К сожалению, перед обращением к документу не существует способа проверить его существование. Процессор может либо выдать ошибку, либо возвратить пустое множество.

#### Пример

Листинг 8.61. Преобразование

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:user="urn:user-namespace">
    <user:data>
        <item>1</item>
        <item>2</item>
    </user:data>
    <xsl:variable name="data" select="document('')/xsl:stylesheet/user:data"/>
    <xsl:template match="/">
        <xsl:copy-of select="$data/item"/>
    </xsl:template>
</xsl:stylesheet>
```

Листинг 8.62. Выходной документ

```xml
<item xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:user="urn:user-namespace">1</item>
<item xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:user="urn:user-namespace">2</item>
```

### Вызов document( node-set )

Передавая функции `document` множество узлов, можно получить доступ к нескольким документам, URI которых являются строковыми значениями узлов множества. Это, в частности, позволяет обращаться к документам, URI которых указаны в узлах обрабатываемого документа. Например, в контексте элемента

```xml
<а href="http://www.w3.org">...</а>
```

вполне корректным вызовом функции `document` будет `document(@href)`.

Выражение `@href` — здесь возвращает множество, состоящее из единственного узла атрибута. Его строковое значение (`"http://www.w3.org"`) будет использовано как URI внешнего документа. Результирующее множество узлов будет содержать единственный корневой узел документа, расположенного по адресу `http://www.w3.org`.

Приведем еще один пример. XPath-выражение `//a/@href` возвращает множество всех атрибутов `href` элементов `а` текущего документа. Тогда множество `document(//a/@href)` будет содержать корневые узлы всех документов, на которые ссылается посредством элементов а текущий документ.

### Вызов document( string, node-set )

URI, которые передаются функции `document`, могут быть как абсолютными, так и относительными, например `document('doc.xml')` возвратит корень документа `doc.xml`, находящегося в том же каталоге, что и само преобразование.

Функция `document` позволяет менять "точку отсчета" относительных URI. Если в качестве второго аргумента функции `document` передано множество узлов, то относительные идентификаторы ресурсов будут отсчитываться от базового адреса первого (в порядке просмотра документа) узла этого множества.

Базовым URI узла дерева является:

- если элемент или инструкция по обработке принадлежит внешней сущности, базовым URI соответствующего узла будет URI внешней сущности;
- иначе базовым URI является URI документа;
- базовым URI текстового узла, узла атрибута, комментария или пространства имен является базовый URI родительского элемента.

Поясним вышесказанное на примерах.

Конструкция

```xml
<xsl:copy-of select="document('doc.xml')"/>
```

копирует в выходящий документ `doc.xml`, находящийся в одном каталоге вместе с преобразованием.

Несмотря на то, что в следующем определении [`xsl:for-each`](/xslt/xsl-for-each/) меняет контекст, `document('doc.xml')` все равно возвращает корень документа `doc.xml`, находящегося в одном с преобразованием каталоге:

```xml
<xsl:for-each select="document('a/data.xml')">
    <xsl:copy-of select="document('doc.xml')"/>
</xsl:for-each>
```

В следующей конструкции `document('doc.xml', /)` копирует документ `a/doc.xml`, поскольку в качестве базового URI используется URI корня документа `a/data.xml`:

```xml
<xsl:for-each select="document('a/data.xml')">
    <xsl:copy-of select="document('doc.xml', /)"/>
</xsl:for-each>
```

Того же самого эффекта можно достичь следующим образом:

```xml
<xsl:copy-of select="document('doc.xml', document('a/data.xml'))"/>
```

В следующей конструкции за базовый URI опять принимается URI самого преобразования (вернее, его корневого узла):

```xml
<xsl:copy-of select="document('doc.xml', document(''))"/>
```

Протестируем теперь все это вместе в одном преобразовании.

Листинг 8.63. Преобразование

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:template match="/">
        <xsl:copy-of select="document('doc.xml')"/>
        <xsl:for-each select="document('a/data.xml')">
            <xsl:copy-of select="document('doc.xml')"/>
        </xsl:for-each>
        <xsl:for-each select="document('a/data.xml')">
            <xsl:copy-of select="document('doc.xml', /)"/>
        </xsl:for-each>
        <xsl:copy-of select="document('doc.xml', document('a/data.xml'))"/>
        <xsl:for-each select="document('a/data.xml')">
            <xsl:copy-of select="document('doc.xml', document(''))"/>
        </xsl:for-each>
    </xsl:template>
</xsl:stylesheet>
```

Листинг 8.64. Документ `doc.xml`

```xml
<doc>doc.xml</doc>
```

Листинг 8.65. Документ `a/doc.xml`

```xml
<doc>a/doc.xml</doc>
```

Листинг 8.66. Выходящий документ

```xml
<doc>doc.xml</doc>
<doc>doc.xml</doc>
<doc>a/doc.xml</doc>
<doc>a/doc.xml</doc>
<doc>doc.xml</doc>
```

### Вызов document( node-set, node-set )

Если функции `document` передаются два множества узлов, то вычисление результата можно описать примерно следующим образом:

- каждый из узлов первого аргумента преобразуется в строковый вид;
- для каждого из полученных значений выполняется вызов типа document(string, node-set);
- результирующие множества объединяются.

Иными словами, `document(node-set, node-set)` работает через `document(string, node-set)` точно так же, как `document(node-set)` работает через `document(string)`. Разница лишь в том, что в первом случае базовый URI будет изменен.

## Ссылки

- [document()](https://developer.mozilla.org/en-US/docs/Web/XPath/Functions/document) на MDN
