<!--
---

[TOC]
-->
---

**Foreword**

This page tests possibilities.

---

## Sane list

- 'Apprenez à programmer en Python'
- "Automate the Boring Stuff with Python"

1. 'Apprenez à programmer en Python'
1. "Automate the Boring Stuff with Python"

- 'Apprenez à programmer en Python'
- "Automate the Boring Stuff with Python"

## Smart symbols

+/-  -->  <--  <-->  =/=  1/4  1st 2nd 3rd 4th (c) (tm)
'a' "b"  «c»  ... - -- ---

## Sub/Superscripts

Enter superscript: 2^10^ is 1024.

<sup>superscript</sup>

`pip install MarkdownSuperscript`

Enter subscript: The molecular composition of water is H~2~O.

<sub>subscript</sub>

`pip install MarkdownSubscript`

## Embed videos

[!embed](https://www.youtube.com/watch?v=nzzHc9J39mw)

`pip install pyembed-markdown`.
Add `pyembed.markdown`.

## Build tables

|   |   |
|---|---|
|a  |b  |
|c  |d  |

Without outside borders:

First Header | Second Header | Third Header
------------ | ------------- | ------------
Content Cell | Content Cell  | Content Cell
Content Cell | Content Cell  | Content Cell


With outside borders:

| First Header | Second Header | Third Header |
| ------------ | ------------- | ------------ |
| Content Cell | Content Cell  | Content Cell |
| Content Cell | Content Cell  | Content Cell |

Aligned:

First Header | Second Header | Third Header
:----------- | :-----------: | -----------:
Left         | Center        | Right
Left         | Center        | Right

## Arithmatex

Inline: $\frac{1}{n}$ and...

Block:

$$\sqrt{9}$$

## Footnotes

Lorem ipsum[^1]

[^1]: Lorem ipsum

Lorem ipsum Lorem ipsum[^2]

[^2]: 
    Lorem ipsum 2.1
    Lorem ipsum 2.2

## Admonition

!!! tip
    Lorem ipsum

## Code block

```python
a=1
b=1
print(a)
```

## Code hilite
    
~~~python hl_lines="1 2"
a=1
b=1
print(a)
~~~

## Inline code hilite

`#!python a=1`

## Bold italic

***Lorem ipsum***

## Underline

^^Lorem ipsum^^

## Highlight

==Lorem ipsum==

## Emoji

:smile:

