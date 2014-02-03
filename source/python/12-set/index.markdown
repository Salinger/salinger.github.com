---
layout: page
title: "12. 集合型"
date: 2014-02-03 16:32
comments: false
sharing: true
footer: true
---

## 集合型(set)
集合型は順序付けされていないオブジェクトのコレクションである。集合演算を行いたい場合に利用する。listを使用して集合演算処理を記述するよりも圧倒的に高速な場合がほとんど。そのような処理を行う場合は基本的にこちらを利用する。

setは変更可能、frozensetは変更不可能。

```
set([iterable])
```

で作成できる。使用例。

```
>>> s1 = set([1,2,2,3,4,5,6,6])
>>> s2 = set([3,7,9])
>>> s1
set([1, 2, 3, 4, 5, 6])
>>> s2
set([3, 7, 9])
>>> s1.union(s2)
set([1, 2, 3, 4, 5, 6, 7, 9])
>>> s1.intersection(s2)
set([3])
```

## よく使う演算子・メソッド等
* len(s)
    * set s の要素数を返す。

* x in s
    * x が s のメンバーに含まれるか確認する。

* x not in s
    * x が s のメンバーに含まれていないことを確認する。

* isdisjoint(other)
    * set が other と共通の要素を持たないとき、 True を返す。set はそれらの積集合が空集合となるときのみ、互いに素となる。

* issubset(other)
    * set の全ての要素が、 other に含まれるか確認します。set <= otherと等価

* set < other
    * set が other の真部分集合であるかを確認する。set <= other and set != other と等価。

* issuperset(other)
    * other の全ての要素が、 set に含まれるか確認する。set >= otherと等価。

* set > other
    * set が other の真上位集合であるかを確認する。set >= other and set != other と等価。

* union(other, ...)
    * set と全ての other の要素からなる新しい set を返す。set | other | ... と等価

* intersection(other, ...)
    * set と全ての other に共通する要素を持つ、新しい set を返す。set & other & ... と等価。

* difference(other, ...)
    * set に含まれて、かつ全ての other に含まれない要素を持つ、新しい set を返す。set - other - ... と等価。

* symmetric_difference(other)
    * set もしくは other のいずれか一方だけに含まれる要素を持つ新しい set を返す。set ^ other と等価。

* copy()
    * s の浅いコピーを新しい set として返す。

* update(other, ...)
    * 全ての other の要素を追加し、 set を更新する。set |= other | ... と等価。

* intersection_update(other, ...)
    * 元の set と 全ての other に共通する要素だけを残して set を更新する。set &= other & ... と等価。

* difference_update(other, ...)
    * other に含まれる要素を取り除き、 set を更新する。set -= other | ... と等価。

* symmetric_difference_update(other)
    * どちらかにのみ含まれて、共通には持たない要素のみで set を更新する。set ^= other と等価。

* add(elem)
    * 要素 elem を set に追加する。

* remove(elem)
    * 要素 elem を set から取り除く。もし elem が set に含まれなければ KeyError 。

* discard(elem)
    * 要素 elem が set に含まれていれば、取り除く。

* pop()
    * 任意に要素を set から返し、それを set から取り除く。set が空であれば、 KeyError 。

* clear()
    * set の全ての要素を取り除く。