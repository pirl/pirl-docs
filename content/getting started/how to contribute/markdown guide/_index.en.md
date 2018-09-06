---
title: Markdown Guide
weight: 5
---

## Introduction

To contribute to PIRL documentation you'll have to use ["markdown"](https://daringfireball.net/projects/markdown/syntax) formatting. Markdown is one of many ways to do documentation. It's probably not the best and certainly not the worst. It's easy to get into and allow for a self-consistent documentation cycle.

Below you'll find some examples of how to use markdown along with our recommendations and best practices. Please use our recommendations when composing PIRL documentation so that it looks well put together with the rest of the content. Also, make sure to take look at [Style Guide]({{< ref "/getting started/how to contribute/style guide" >}}) for additional guidelines regarding content formatting.

## Example Markdown Document

Below is an example document using markdown. This document will be rendered by the software to display as desrcibed.

![Magic](/getting started/how to contribute/markdown guide/images/sample.jpg)

## Basic Markdown Guide

### Main Title

The main document title is displayed at the top of the document using the largest font. In markdown, the title goes at the very top of the document in between the **`---`** section as shown below for this very document.

```
---
title: Markdown Guide
weight: 5
---
```

### Headers

Headers are usually sized from H1 (largest) to H6 (smallest). Markdown is no different. The number representing the size of the header is represented by a **`#`**. A single **`#`** is equivalent to **H1**, two **`##`** is equivalent to **H2**, etc.

```
# This is an H1 tag
## This is an H2 tag
### This is an H3 tag
#### This is an H4 tag
##### This is an H5 tag
###### This is an H6 tag
```

> **PIRL TIP:** The major sections of a document start with **##** or H2

### Emphasis

To *italicize* text, use a single set of asterisks around it. To mark text as **bold**, use a set of two asterisks around it. To strike out some text, use two tildes **(~)** around it.

```
*This text will be italicized*
**This text will be in bold**
~~Did I say something wrong?~~
```

*This text will be italicized*

**This text will be in bold**

~~Did I say something wrong?~~
