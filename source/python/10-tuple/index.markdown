---
layout: page
title: "10. タプル"
date: 2014-02-03 16:32
comments: false
sharing: true
footer: true
---
タプルは不変(イミュータブル)なシーケンス型。リストと異なり、各要素の変更は出来ない。 以下のように定義できる。

```
t = (1,2,3,4,5)
```

リストと同様の操作ができる。

```
>>> t[2]
3
>>> t[1:4]
(2, 3, 4)
>>> t[2:]
(3, 4, 5)
```

ただし、要素を変更しようとするとエラー。

```
>>> t[2] = 8
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

他のシーケンス型をタプルに変換できる。
```
>>> tuple([iterable])
```

確認。

```
>>> l = [1,2,3,4,5]
>>> t = tuple(l)
>>> t
(1,2,3,4,5)
```