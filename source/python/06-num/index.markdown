---
layout: page
title: "6. 数値"
date: 2014-02-03 16:19
comments: false
sharing: true
footer: true
---

### 数値型の確認
intで収まらない場合は自動でlongに変換されるので、 数値が大きい場合もあまり心配はいらない。

```
#int 型
>>> 100
100
100

#float 型
>>> 1.234
1.234
1.234

#complex 型
>>> 5 + 6j
5 + 6j
(5+6j)
```

### 算術演算子等

演算子|意味
:---|:---
x + y| 和
x - y| 差
x * y| 積
x / y| 商
x // y| 商（切り下げ）
x % y| 剰余
-x| 符号反転
+ x|  符号そのまま
abs(x)| 絶対値
int(x)| 整数に変換
long(x)| 長整数に変換
float(x)| 浮動小数点に変換
complex(re, im)| 虚数（実部 re, 虚部 im）に変換
c.conjugate()| 複素数 c の共役複素数
divmod(x,y)| (x // y, x % y)のペア
pow(x,y)| x の y 乗
x ** y| pow(x,y)と同義

### ビット列演算
intおよびlong型ではビット列演算が可能。 負の数はその値の2の補数値として扱われる。

演算子|意味
:---|:---
x &#124; y | 論理和
x ^ y| 排他的論理和
x & y|  論理積
x << n| n ビット左シフト
x >> n| n ビット右シフト
~x| ビット反転