---
layout: default
title: xsl:for-each
nav_order: 13
parent: XSLT
---

<!-- prettier-ignore-start -->
# xsl:for-each
{: .no_toc }
<!-- prettier-ignore-end -->

Элемент **`xsl:for-each`** используется для создания в выходящем документе повторяемых частей структуры.

Обязательный атрибут `select` указывает выражение, результатом вычисления которого должно быть множество узлов. Шаблон, содержащийся в `xsl:for-each`, будет выполнен процессором для каждого узла этого множества.

<!-- prettier-ignore -->
1. TOC
{:toc}

## Синтаксис

### XSLT 1.0, XSLT 2.0 и XSLT 3.0

```xml
<xsl:for-each
    select = "выражение">
    <!-- Содержимое: (xsl:sort*, шаблон) -->
</xsl:for-each>
```

Атрибуты:

- **`select`** — **обязательный** атрибут, указывает выражение, результатом вычисления которого должно быть множество узлов. Шаблон, содержащийся в `xsl:for-each`, будет выполнен процессором для каждого узла этого множества. В XSLT 2.0 атрибут `select` выбирает объекты, к числу которых могут относиться как атомарные значения, так и узлы.

## Описание и примеры

### Пример

Мы можем использовать `xsl:for-each` для того, чтобы создать список гипертекстовых ссылок для документа вида.

Листинг 7.24. Входящий документ

```xml
<html>
    <head>
        <title>I'm just a simple page...</title>
    </head>
    <body>
        Please visit <a href="http://www.aaa.com">this link</a>.
        Or <a href="http://www.bbb.com">this one</a>.
        Or visit <a href="http://www.ccc.com">this site</a>.
        Or click <a href="http://www.ddd.com">here</a>.
    </body>
</html>
```

Будем считать, что в этом документе элементы гипертекстовых ссылок а являются потомками элемента `body`, который находится в элементе `html`.

Листинг 7.25. Шаблон преобразования

```xml
<xsl:template match="/">
    <links>
        <xsl:for-each select="/html/body//a">
            <a href="{@href}">
                <xsl:value-of select = "@href"/>
            </a>
        </xsl:for-each>
    </links>
</xsl:template>
```

Листинг 7.26. Результат преобразования

```xml
<links>
    <a href="http://www.aaa.com">http://www.aaa.com</a>
    <a href="http://www.bbb.com">http://www.bbb.com</a>
    <a href="http://www.ccc.com">http://www.ccc.com</a>
    <a href="http://www.ddd.com">http://www.ddd.com</a>
</links>
```

Элемент `xsl:for-each` изменяет контекст преобразования. Множество узлов, возвращаемое выражением в атрибуте `select`, становится текущим множеством узлов, а узел, шаблон для которого выполняется в данный момент, становится текущим узлом.

Как мы знаем, множества узлов в XSLT не имеют внутреннего порядка. Однако, обработка узлов в `xsl:for-each` будет происходить в так называемом порядке просмотра документа, который зависит от того, какое выражение использовалось для вычисления обрабатываемого множества. Порядок обработки множества узлов в `xsl:for-each` может быть также изменен элементами [`xsl:sort`](/xslt/xsl-sort/), которые могут присутствовать в `xsl:for-each`. Элемент `xsl:sort` задает сортировку обрабатываемого множества узлов, изменяя, таким образом, порядок просмотра, что часто бывает очень полезно.

## См. также

- [`xsl:sort`](/xslt/xsl-sort/) -- задает порядок сортировки
- [`xsl:apply-templates`](/xslt/xsl-apply-templates/)

## Ссылки

- [`xsl:for-each`](https://developer.mozilla.org/en/XSLT/for-each) на MDN
- [`xsl:for-each`](https://msdn.microsoft.com/en-us/library/ms256166.aspx) на MSDN
