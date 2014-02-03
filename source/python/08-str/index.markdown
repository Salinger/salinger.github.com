---
layout: page
title: "8. 文字列"
date: 2014-02-03 16:31
comments: false
sharing: true
footer: true
---

## 文字列型について

(Python 3 系からはunicodeデフォルトに変更されているので注意)

シーケンス型のうち str, unicode が文字列。文字列リテラル(str型)は

```
'xyz'
```

もしくは
```
"xyz"
```

のように表す。

unicode文字列はほぼ文字列と同じ。マルチバイト文字を扱う場合はこの型を使うと、文字数等をうまいこと計算してくれる。

```
u'あいう'
```

もしくは

```
u"えお"
```

のように表す。


3重クオート
```
"""
Test1
Test2
Test3
"""
```

もしくは

```
'''
Test1
Test2
Test3
'''
```

中では改行文字がそのまま認識される。 改行文字をキャンセルする場合は\を文末に。

```
>>> a = '''
>>> This
>>> is\
>>> test!
>>> """
'\nThis\nistest!\n'
    
>>> s1 = 'あいうえお'
>>> s2 = u'あいうえお'
>>> len(s1)
15
>>> len(s2)
5
```

基本的に、日本語を扱う場合はその流れをunicode型で統一するのがベスト。 ただし、一部のモジュール（MeCab等）はstr型以外で動作しない場合があるので、 そのときはstr型に変換してやる。

ちなみにstr型とunicode型で同じ文字列「あいうえお」を==で比較した場合。

```
>>>u"あいうえお" == "あいうえお"
False
```

となる。バグの原因になりやすいので注意。

## エスケープシーケンス

文字列中では以下の文字は特別な意味を表す。

よく使うのは

記号 `\`, `'`, `"` のエスケープ、
改行コード `\n` (*nix) `\r\n` (Windows)、
タブ文字 `\t` あたり。

エスケープシーケンス|意味
:---|:---
\\| バックスラッシュ(\)
\'| 一重引用符(')
\"| 二重引用符(")
\a| ASCII 端末ベル
\b| ASCII バックスペース
\f| ASCII フォームフィード
\n| ASCII 行送り
\N{name} | Unicodeデータベースで名前nameを持つ文字 
\r| ASCII 復帰
\t| タブ文字
\uxxxx| 16bit Unicode の 16進数値 xxxx を持つ文字
\Uxxxxxxxx| 32bit Unicode の 16進数値 xxxxxxxx を持つ文字
\v| ASCII 垂直タブ
\ooo| 8進数値 ooo を持つ文字
\xhh| 16進数値 hh を持つ文字

## よく使う文字列メソッド
下記のメソッドと、シーケンス型の演算子でだいたいのことはできる。

* str.encode(encoding)
    * 文字列をencoding(例. "utf-8")でエンコードする。  

```
>>> u'あいうえお'.encode("utf-8")
'\xe3\x81\x82\xe3\x81\x84\xe3\x81\x86\xe3\x81\x88\xe3\x81\x8a'
```

*    str.decode(encoding)
    * 文字列をencoding(例. "utf-8")でデコードする。  

```
>>> a = '\xe3\x81\x82\xe3\x81\x84\xe3\x81\x86\xe3\x81\x88\xe3\x81\x8a'
>>> a.decode("utf-8")
あいうえお
```

* str(x)
    * str型に変換する  

```
>>> str(10)
'10'
```

* unicode(x)
    * unicode型に変換する  

```
>>>unicode("あいうえお")
>>> u'\u3042\u3044\u3046\u3048\u304a'
>>> print u'\u3042\u3044\u3046\u3048\u304a'
あいうえお
```

`UnicodeDecodeError: 'ascii' codec can't decode byte XXXX in position Y: ordinal not in range(128)` というエラーが帰ってきた場合、システムの標準文字コードがasciiになっている。

色々解決方法はあるが、一番手っ取り早い解決方法は、以下をプログラムの冒頭部分に記述する。

```
#!/usr/bin/env python
#-*- coding:utf-8 -*-
 
# ここから
import sys
reload(sys)
sys.setdefaultencoding('utf-8')
# ここまで
```

* str.find(sub[, start[, end]])
    * 文字列のスライス s[start,end] (start、endは省略可)にsubが含まれる場合はその最小値のインデックス、そうでない場合は-1を返す。  

* str.join(iterable)
    * iterable中の文字列をstrで結合した文字列を返す。  

```
>>> l = ['a','b','c']
>>> ",".join(l)
'a,b,c'
```

* str.lstrip([chars])
    * 文字列の先頭部分を除去したコピーを返す。引数 chars は除去される文字集合を指定する文字列。省略した場合は空白文字を除去。  


```
>>> "   this is test.\n".lstrip()
"this is test.\n".
```

* str.rstrip([chars])
    * 文字列の末尾部分を除去したコピーを返す。引数 chars は除去される文字集合を指定する文字列。省略した場合は空白文字を除去。  

```
>>> "this is test.\n".rstrip()
"this is test."
```

* str.strip([chars])
    * 文字列の先頭および末尾部分を除去したコピーを返す。引数 chars は除去される文字集合を指定する文字列。省略した場合は空白文字を除去。  

* str.split([sep[, maxsplit]])
    * sepを単語の境界として、文字列を単語に分解し、単語からなるリストを返す。maxsplitが与えられた場合、最大maxsplit回分割され、maxsplit + 1 の要素数のリストとなる。  
```
>>> '1,,2,3,4'.split(",")
['1', '', '2', '3', '4']
```

* str.splitlines([keepends])
    * 文字列を改行部分で分解し、各行からなるリストを返す。keepends が True の場合のみ改行コードを含んだままの文字列となる。  
