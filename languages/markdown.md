# header/title `#`
## sub heading `##` or `###...` for even smaller headers
This is a normal body of text  
and to go the next line we need to press space twice or `tab` and then enter `<CR>`  
1. to make (ordered) list use a number and punctuation mark `1.`  

9999. `9999.` will autocorrect to the next corresponding number being "2."  

- to make (unordered) list use a hyphen `-` to make a bullet 
* asterisk `*` could also be used
+ or a plus sign `+`  

  - indent by using 2 spaces or `Tab`
    1. depending on what level using a number (ordered list) `1.` ...
    2. could have mixed results `2.`  

- [ ] A task list can be created with `- [ ]`  

- [x] and marked/ticked with `- [x]`  
<ul>
  <li>1993 the first version of HTML was written by Tim Berners-Lee </li> 

```html
<ul>
  <li>'number' use html if unordered list starts with a number</li>
```


`*` *use asterisks around text to make it italic* `*`

`**` **use two asterisks around text to make it bold** `**`

`~~` ~~use two tildes around text to make a stikethrough (cancel out)~~ `~~`


to place emojis use `:joy:` :joy:

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

> to make a blockquote use greater-than sign aka "chevron" or "angle bracket" at the beginning `>`
>> can also nest with `>>`

To comment out text we use `[//]: # ` followed by `"text to comment out"`
Try viewing this in a raw format and through a parser to spot any differences


[//]: # "lanigiro taht ton m'I esuaceb txet esrever emos tsuJ"

```
term
: definition
```
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


[this is a description for a link](https://so-much-pain.glitch.me/do-a-barrel-roll.html) `[description](url)`


The normal syntax to add an image is 
```
![title](path/to/file/example.png)
```
or for windows:
```
![image](files://C:/Users/username/Desktop/example.png)
```
else if for remote link:
```
![alt text](url)
```
To add image with specified scaling try using some html since some attibutes of styling aren't supported by sites like Github:
```html
<img src="http://....jpg" width="400" height="400" />
```
<img src="https://velog.velcdn.com/images/zmdlw/post/eb240f7b-ee94-49ae-8c22-b35873db6dc0/image.jpg" width="400" />

Here's a sentence with a footnote. [^1]
[^1]: This is the footnote.
