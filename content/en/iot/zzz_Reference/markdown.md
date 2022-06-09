---
title: "Markdown Cheat Sheet"
linkTitle: "Markdown Cheat Sheet"
type: docs
weight: 100
description: >
    Ronan using this to see how browser formats various things.
    Taken from https://www.markdownguide.org/cheat-sheet/
---
# Markdown Cheat Sheet

Thanks for visiting [The Markdown Guide](https://www.markdownguide.org)!

This Markdown cheat sheet provides a quick overview of all the Markdown syntax elements. It can’t cover every edge case, so if you need more information about any of these elements, refer to the reference guides for [basic syntax](https://www.markdownguide.org/basic-syntax) and [extended syntax](https://www.markdownguide.org/extended-syntax).

## Basic Syntax

These are the elements outlined in John Gruber’s original design document. All Markdown applications support these elements.

### Heading

# H1
## H2
### H3

### Bold

**bold text**

### Italic

*italicized text*

### Blockquote

> blockquote

### Ordered List

1. First item
2. Second item
3. Third item

### Unordered List

- First item
- Second item
- Third item

### Code

`code`

### Horizontal Rule

---

### Link

[Markdown Guide](https://www.markdownguide.org)

### Image

![alt text](https://www.markdownguide.org/assets/images/tux.png)

## Extended Syntax

These elements extend the basic syntax by adding additional features. Not all Markdown applications support these elements.

### Table

| Syntax | Description |
| ----------- | ----------- |
| Header | Title |
| Paragraph | Text |

### Fenced Code Block

```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

### Footnote

Here's a sentence with a footnote. [^1]

[^1]: This is the footnote.

### Heading ID

### My Great Heading {#custom-id}

### Definition List

term
: definition

### Strikethrough

~~The world is flat.~~

### Task List

- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media

### Emoji

That is so funny! :joy:

(See also [Copying and Pasting Emoji](https://www.markdownguide.org/extended-syntax/#copying-and-pasting-emoji))

### Highlight

I need to highlight these ==very important words==.

### Subscript

H~2~O

### Superscript

X^2^


### Others (Ronan)

<span style="color:black"> Colors: </span>\
<span style="color:red"> Richard <span style="color:orange"> Of <span style="color:yellow"> York <span style="color:green"> Gave <span style="color:blue"> Battle <span style="color:indigo"> In <span style="color:violet"> Vain </span>.

Arm color palette:\
<span style="color:#ff6b00"> Orange </span>\
<span style="color:#ffc700"> Yellow </span>\
<span style="color:#95d600"> Green </span>\
<span style="color:#90c1de"> Light blue </span>\
<span style="color:#0091bd"> Darker blue </span>\
<span style="color:#002b49"> Blackish </span>\
<span style="color:#333e48"> Dark grey </span>\
<span style="color:#7d868c"> Medium Grey </span>\
<span style="color:#e5eceb"> Light Grey </span>

These are two seperate lines close together.
But they don't show up as two lines close together :sad:

Maybe these are two lines close together?\
Yes, these really are two lines close together!
