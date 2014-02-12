---
layout: page
title: "__future__ モジュールについて"
date: 2014-02-11 22:27
comments: true
sharing: true
footer: true
---
いきなり 3 系に移行するのはちょっと心配…という場合、まず2 系 + `__future__` モジュールを使うのが良さそう。`__future__` モジュールは Python 2 系用のモジュール。Python 3 系に実装されている Python 2 系 と互換性の無い機能をPython 2 系で使用できるようにする。

以下、`__future__` モジュールに実装されている機能を利用しつつ、Python 3 系での大きな変更点を確認してゆく。

## print_function
3系では `print` は文から関数 `print()`になった。また予約語からも削除された。

```
>>> from __future__ import print_function
from __future__ import print_function
>>> print('abc')
print('abc')
abc
>>> print('abc','def','ghi')
print('abc','def','ghi')
abc def ghi
```

2系で改行文字を出力しない場合は `print "hoge",` のように記述していたが、3系ではもっと汎用的に記述できる。`end=''`の`''`の部分を任意の文字列で置き換えられる。

```
>>> print('abc', end='')
print('abc', end='')
abc>>>
```

また、ファイルへの出力も引数で指定すれば可能。

```
>>> f = open("test.txt", "w")
f = open("test.txt", "w")
>>> print("Spam and Egg and Spam", file=f)
print("HogeHoge, PiyoPiyo", file=f)
```

## unicode_literals
Python 3 系では文字列は基本的にすべてユニコードとして扱う。日本語等の扱いが相当楽になる。`u'日本語'`と書いていたものは全て`'日本語'`と書けば良い。逆に以前の通常の文字列を取り扱いたい場合`b'日本語'`のように`b''`の形で書く(byte列表現)。

```
>>> from __future__ import unicode_literals
from __future__ import unicode_literals
>>> "abc"
"abc"
u'abc'
>>> b'abc'
b'abc'
'abc'
>>> 
```

注意：

byte列表現を取り扱う際、インデックスの参照結果が2系と3系で異なる。詳しくは[ここ](http://docs.python.jp/3.3/howto/pyporting.html#bytes-literals)を参照。

### division
2系では割り算の演算子 `/` は小数点以下切り捨てだったが、3系では小数点以下をそのまま扱える。

切り捨てたい場合、新演算子の `//` を利用する。

```
>>> from __future__ import division
from __future__ import division
>>> 1/2
1/2
0.5
>>> 1//2
1//2
0
```

## future_builtins
このモジュールは、Python 3 系 では異なった動作をする Python 2 系 のビルトイン名前空間に追加できない関数を提供する([future_builtins — Python 3 のビルトイン](http://docs.python.jp/2/library/future_builtins.html))。

* ascii(object)
    * 引数で与えた値と等価なリテラル表記文字列を返す。つまり repr() と同じ値。Python 3 では、 repr() は表示可能なUnicode文字をエスケープせずに返し、 ascii() はその文字列をバックスラッシュでエスケープする。repr() の代わりに利用することで、ASCII文字列を必要としていることを明示できる。

```
>>> from future_builtins import *
from future_builtins import *
>>> from __future__ import unicode_literals
from __future__ import unicode_literals
>>> ascii("text")
ascii("text")
"u'text'"
>>> ascii("テスト")
ascii("テスト")
"u'\\u30c6\\u30b9\\u30c8'"
```
* map(function, iterables, ...)
    * iterables の要素を引数として funtion を呼び出すイテレータを作成する。function が None の場合、引数のタプルを返す。itertools.imap() と同じ動作。

```
>>> from future_builtins import *
from future_builtins import *
>>> map(lambda x: x ** 2, range(10))
map(lambda x: x ** 2, range(10))
<itertools.imap object at 0x1017cd4d0>
>>> list(map(lambda x: x ** 2, range(10)))
list(map(lambda x: x ** 2, range(10)))
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

* filter(function, iterable)
    * function が True となる要素だけを返すイテレータを作成する。function が None の場合、値が真のものだけを返す。itertools.ifilter() と同じ動作。

```
>>> from future_builtins import *
from future_builtins import *
>>> filter(lambda x: x%2, range(10))
filter(lambda x: x%2, range(10))
<itertools.ifilter object at 0x1017cd790>
>>> list(filter(lambda x: x%2, range(10)))
list(filter(lambda x: x%2, range(10)))
[1, 3, 5, 7, 9]
```
* zip(iterables, ...)
    * 各 iterable の要素をまとめるイテレータを作成する。itertools.izip() と同じ動作。
```
>>> zip([1, 2, 3, 4, 5],[5, 4, 3, 2, 1])
zip([1, 2, 3, 4, 5],[5, 4, 3, 2, 1])
<itertools.izip object at 0x1017ccb48>
>>> list(zip([1, 2, 3, 4, 5],[5, 4, 3, 2, 1]))
list(zip([1, 2, 3, 4, 5],[5, 4, 3, 2, 1]))
[(1, 5), (2, 4), (3, 3), (4, 2), (5, 1)]
```

* hex(object)
    * ビルトイン hex() と同じように動作するが、 `__hex__()` の代わりに、 `__index__()` メソッドを利用して整数を取得し、それを16進数文字列に変換する。

* oct(object)
    * ビルトイン oct() と同じように動作するが、 `__oct__()` の代わりに、 `__index__()` メソッドを利用して整数を取得し、それを16進数文字列に変換する。

## absolute_import
Python 3 では相対インポートではなく、絶対インポート優先になる。標準モジュールと同名のモジュールがカレントディレクトリにある場合、Python 2 系ではカレントディレクトリのモジュールが優先されていたので、これを使うことで標準モジュールを意図せず上書きしてしまう可能性がなくなる。

以下のディレクトリ構成を仮定する。
```
top_dir
|--__init__.py
|--main.py
|--modules1
|   |--foo.py
|   |--bar.py
|
|--modules2
    |--hoge.py
    |--piyo.py
```

`piyo.py`から`hoge.py`と`foo.py`の相対インポートを明示的に行いたい場合、

```
>>> from __future__ import absolute_import
>>> from . import hoge.py
>>> from ..modules1 import foo.py
```

のようにする。

## with_statement
with 構文はPython 2.6 以降ではデフォルトで有効。Python 2.5 を使っている場合にこれを import してやる必要がある。

以下のコードのようにファイル読み込みの際に with 構文を使うと、close()を自分で呼び出す必要がなく、ブロックを抜けると自動でclose()を呼ぶ。例外処理等を行いやすいので読み書きする際には with 構文を使うべき。

```
with open('test.txt', 'w') as f:
    f.write("This is test!\n")
``` 

with 構文についての細かい解説[このページ](http://d.hatena.ne.jp/reiki4040/20130331/1364723288)が詳しい。

## nested_scopes
Python 2.0 から 2.1 でスコープルールに大きな変更点があった。2.1以降のバージョンを使っている場合問題になることはないので説明は略 ([PEP 227](http://docs.python.jp/3.3/whatsnew/2.1.html#pep-227-nested-scopes))。

## 最後にまとめ
現状の2系最新版 Python 2.7 を使う場合、出来る限り `__future__` モジュールを import しておいて3系の機能に今のうちから慣れておきましょう。

```
from __future__ import print_function
from __future__ import unicode_literals
from __future__ import absolute_import
from __future__ import generators
from __future__ import division
```
