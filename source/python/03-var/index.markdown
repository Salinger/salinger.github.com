---
layout: page
title: "3. 変数"
date: 2014-02-03 16:15
comments: false
sharing: true
footer: true
---

変数はオブジェクトに付ける名札。以下例。

```
>>> a = 10
>>> string = "hello, world!"
>>> a
10
>>> string
'hello, world!'
```

変数名の大文字と小文字は区別される。

1文字目は 英文字 もしくは _ でなければならない。 2文字目以降は 英数文字 もしくは _ が使用できる。

C言語等と違い、使用する前に宣言は必要ないが、 一度も使用していない変数を代入せずに式の中で使用すると、NameErrorの例外が起こる。