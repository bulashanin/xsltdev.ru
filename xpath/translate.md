---
layout: default
title: translate
nav_order: 34
parent: XPath
---

<!-- prettier-ignore-start -->
# translate()
{: .no_toc }
<!-- prettier-ignore-end -->

Функция **`translate`** производит замену символов первого своего строкового аргумента, которые присутствуют во втором аргументе на соответствующие символы третьего аргумента.

<!-- prettier-ignore -->
1. TOC
{:toc}

## Синтаксис

### XPath 1.0

```
string translate( string, string, string )
```

## Описание и примеры

### Пример

```
translate('abcdefgh', 'aceg', 'ACEG') ? 'AbCdEfGh'
```

Если некоторый символ повторяется во втором аргументе несколько раз, учитывается только первое его появление.

### Пример

```
translate('abcdefgh', 'acaeaga', 'ACBECGD') ? 'AbCdEfGh'
```

Если второй аргумент длиннее третьего, символы, для которых нет соответствующей замены, удаляются из строки.

### Пример

```
translate('a b-c=d+e|f/g\h', 'aceg-=+|/\', 'ACEG') ? 'A bCdEfGh'
```

Если третий аргумент длиннее второго, остаток строки игнорируется.

### Пример

```
translate('abcdefgh', 'aceg', 'ACEGBDFH') ? ' AbCdEfGh'
```

Функцию `translate` можно использовать, например, для изменения регистра символов. Конечно, это будет работать только для тех языков, для которых такая функция будет записана, но и этого в большинстве случаев будет достаточно. В будущем предполагается включить в новые версии языка более мощные функции для работы с регистрами символов.

### Пример

Для того чтобы изменять регистр слов русского языка, мы можем определить две переменные, `lowercase` и `uppercase`, которые будут содержать строчные и прописные символы основного русского алфавита (мы включили в него букву ё — строчную ("ё") и прописную ("Ё"), хотя в соответствии с Unicode она относится к расширениям). Мы также создадим два именованных шаблона, которые будут менять регистр символов строкового параметра `str`. Для удобства использования мы вынесем определения переменных и шаблонов во внешний модуль `ru.xsl`.

Листинг 6.6. Преобразование ru.xsl

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:variable name="uppercase" select="concat('АБВГ', 'ДЕЁЖЗ', 'ИЙКЛ', 'МНОП', 'РСТУ', 'ФХЦЧ', 'ШЩЪЫ', 'ЬЭЮЯ')"/>
    <xsl:variable name="lowercase" select="concat('абвг', 'деёжз', 'ийкл', 'мноп', 'рсту', 'фхцч', 'шщъы', 'ьэюя')"/>
    <xsl:template name="lower">
        <xsl:param name="str"/>
        <xsl:value-of select="translate($str, $uppercase, $lowercase)"/>
    </xsl:template>
    <xsl:template name="upper">
        <xsl:param name="str"/>
        <xsl:value-of select="translate($str, $lowercase, $uppercase)"/>
    </xsl:template>
</xsl:stylesheet>
```

Использовать этот модуль можно, включив или импортировав его в основное преобразование элементами [`xsl:include`](/xslt/xsl-include/) или [`xsl:import`](/xslt/xsl-import/). После этого в основном преобразовании будут доступны переменные `lowercase` и `uppercase`, которые можно будет использовать в функции `translate` и шаблоны с именами `lower` и `upper`.

Использовать функцию `translate` с переменными `lowercase` и `uppercase` можно следующим образом:

```
translate('Дом', $uppercase, $lowercase) ? 'дом'
translate('Дом', $lowercase, $uppercase) ? 'ДОМ'
```

Именованные шаблоны можно вызывать элементом [`xsl:call-template`](/xslt/xsl-call-template/), передавая параметр при помощи [`xsl:with-param`](/xslt/xsl-with-param/). Например, следующий фрагмент шаблона

```xml
<xsl:call-template name="lower">
    <xsl:with-param name="str" select="'Дом'"/>
</xsl:call-template>
```

создаст в выходящем дереве текстовый узел со значением "дом".

## Ссылки

- [translate()](https://developer.mozilla.org/en-US/docs/Web/XPath/Functions/translate) на MDN
