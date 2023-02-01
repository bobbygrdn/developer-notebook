# Markdown CheatSheet

### Headers

```
# h1
## h2
### h3
#### h4
##### h5
###### h6
```

### Headers (setext style)

```
Header 1
========
Header 2
--------
```

### Blockquotes

```
> This is
> a blockquote
>
> > Nested
> > Blockquote
```

### Unordered Lists

```
* Item 1
* Item 2
    * item 3a
    * item 3b

or

- Item 1
- Item 2

or

+ Item 1
+ Item 2

or

- [ ] Checkbox off
- [x] Checkbox on
```

### Ordered Lists

```
1. Item 1
2. Item 2
    a. item 3a
    b. item 3b
```

### Links

```
[link](http://google.com)

[link][google]
[google]: http://google.com

<http://google.com>
```

### Emphasis

```
*italic*
_italic_

**bold**
__bold__

`inline code`
~~struck out~~
```

### Horizontal Line

```
Hyphens

---

Asterisks

***

Underscores

___
```

### Code

```
```javascript
console.log("This is a block code")
```
```

```
~~~css
.button { border: none; }
~~~
```

```
    4 space indent makes a code block
inline code
```
`Inline code` has back-ticks around it
```

### Tables

```
| Left column | Center column | Right column |
|:------------|:-------------:|-------------:|
| Cell 1      |   Centered    |        $1600 |
| Cell 2      |    Cell 3     |          $12 |

Simple style

Left column | Center column | Right column
:----------:|:-------------:|:-----------:
   Cell 1   |   Centered    |    $1600
   Cell 2   |    Cell 3     |     $12

A markdown table generator: tableconvert.com
```

### Images

```
![GitHub Logo](/images/logo.png)

![Alt Text](url)

Image with link
[![GitHub Logo](/images/logo.png)](https://github.com/)

[![Alt Text](image_url)](link_url)

Reference style
![alt text][logo]

[logo]: /images/logo.png "Logo Title"
```

### Backslash Escapes

```
Characters	Escape	Description
\	          \\	backslash
`	          \`	backtick
*	          \*	asterisk
_	          \_	underscore
{}	          \{}	curly braces
[]	          \[]	square brackets
()	          \()	parentheses
#	          \#	hash mark
+	          \+	plus sign
-	          \-	minus sign (hyphen)
.	          \.	dot
!	          \!	exclamation mark
```

### 