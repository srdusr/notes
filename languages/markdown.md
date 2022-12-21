# header/title `#`
## sub heading `##` or `###...` for even smaller headers
This is a normal body of text and to go the next line we need to  
press space twice or `tab` and then enter `<CR>`  
1. To make ordered list use a number and punctuation mark `1.`  

9999. `9999.` or any number will autocorrect to the next corresponding number being "2." in this case.  

- For an unordered list use a hyphen `-` to make a bullet.  
* An asterisk `*` could also be used.  
+ Or a plus sign `+`  
  - Indent by using 2 spaces or `Tab` or type html's `&nbsp;` / `&emsp;`  
    1. Depending on what level using a number (ordered list) `1.` ...  
    2. could have mixed results `2.`  

- [ ] A task list can be created with `- [ ]`  

- [x] And marked/ticked with `- [x]`  

<ul>  
  <li> 1, 2, 3 or any number in an unordered list use html: </li></ul>  

`<ul>`  
&emsp;`<li>` "number" `</li></ul>`  

`*` *Use asterisks around text to make it italic* `*`

`**` **Use two asterisks around text to make it bold** `**`

`~~` ~~Use two tildes around text to make a stikethrough (cancel out)~~ `~~`

To place emojis use two colons around the emoji's name `:joy:` :joy:

<font color='#af00d7'>Add color to font by:</font>  
`<font color='color'>`text`</font>`  

You might of noticed already the use of inline code being used like this ` `, we
use backticks with "code/text" inbetween ` `` `

```
  ```use 2 sets of three backticks to make a block of code```
```
```html
<p>for specific language syntax highlighting (this is html btw)...</p>
```
```python
print(" ```python
use three backticks followed by the name of the language
``` " # and three backticks again)
```

> To make a blockquote use greater-than sign aka "chevron" or "angle bracket" at the beginning `>`
>> Can also nest with `>>`

To comment out text we use `[//]: # ` followed by `"text to comment out"`  
Try viewing this in a raw format and through a parser to spot any differences.


[//]: # "lanigiro taht ton m'I esuaceb txet esrever emos tsuJ"

For definitions use:
```
term
: definition
```
Backslash escape characters that are available:
```
\   backslash
`   backtick
*   asterisk
_   underscore
{}  curly braces
[]  square brackets
()  parentheses
#   hash mark
+   plus sign
-   minus sign (hyphen)
.   dot
!   exclamation mark  
```

Horizontal rules can be made with three or more hyphens, asterisks or underscores. Recommend using spaces inbetween.  

`- - -`
- - -
| to | make | table |
| --- | --- | --- |
| use | three | hyphens |
| after | the | title(s) |
| automatic | zebra | striping |

```
| to | make | table |
| --- | --- | --- |
| use | three | hyphens |
| after | the | title(s) |
| automatic | zebra | striping |
```

[//]: # "[this is a description for a link](https://github.com/srdusr/notes/blob/main/languages/markdown.md) `[description](url)`"


[this is a description for a link with optional title/alt text](https://fwesh.yonle.repl.co/ "Rick Roll") `[description](url/ "title")`

The normal syntax to add an image is:
```
![title](path/to/example.jpg "Optional title")
```
or for windows:
```
![image](files://C:/Users/username/Desktop/example.png)
```
else if for remote link:
```
![Alt text](url)
```
To add image with specified scaling try using some html since some attibutes of styling aren't supported by sites like Github:
```html
<img src="http://....jpg" width="400" height="400" />
```
<img src="https://velog.velcdn.com/images/zmdlw/post/eb240f7b-ee94-49ae-8c22-b35873db6dc0/image.jpg" width="400" />

To create a footnote, add a caret symbol inside the square brackets followed by the same number to be used `[^1]` [^1]
[^1]: `[^1]:` Over here just add a colon before what ever reference/notes are
  going to be specified.
