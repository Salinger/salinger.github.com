---
layout: page
title: "7. シーケンス"
date: 2014-02-03 16:29
comments: false
sharing: true
footer: true
---

シーケンス型には str, unicode, list, tuple, bytearray, buffer, xrange 型が存在する。

これらには以下の演算子や比較演算子などが適用出来る。

演算子|意味
:---|:---
x in s|  s のある要素が x と等しい場合 True 、そうでなければ False 。
x not in s| s のある要素が x と等しい場合 True 、そうでなければ False 。
s + t| s と t の結合
s * n, n * s| s の浅いコピー n 個からなる結合
s[i]| s の 0 から数えて i 番目の要素
s[i:j]| s の i 番目から j 番目までのスライス
s[i:j:k]| s の i 番目から j 番目まで、k 毎のスライス
len(s)| s の長さ
min(s)| s の最小の要素
max(s)| s の最大の要素
s.index(i)| s の中で最初にiが現れる場所のインデックス
s.count(i)| s の中にiが現れる数
