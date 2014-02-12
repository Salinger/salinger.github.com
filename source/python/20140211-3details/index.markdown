---
layout: page
title: "3系の変更点覚書"
date: 2014-02-11 22:27
comments: true
sharing: true
footer: true
---
## 3 系での変更点一覧

* Unicode 文字列がデフォルトに変更
* `print` が文から関数に変更
     * 詳しくは([公式ドキュメント](http://docs.python.jp/3.3/library/functions.html?highlight=print#print))に
* `exec` が文から関数に変更
     * 詳しくは([公式ドキュメント](http://docs.python.jp/3.3/library/functions.html?highlight=exec#exec))に
* 例外処理の構文(`try ... catch`)が一部変更
    * 例外オブジェクトを参照しないならば特に変更なし
    * 詳しくは [ここ](http://diveintopython3-ja.rdy.jp/porting-code-to-python-3-with-2to3.html#except) に情報あり
* 例外を送出する構文(`raise`, `throw`)が一部変更
    * 独自のエラーメッセージを出さずにエラーを送出するならば変更なし
    * 詳しくは [ここ](http://diveintopython3-ja.rdy.jp/porting-code-to-python-3-with-2to3.html#raise) に情報あり
* 関数や演算子の削除・改名など
    * `raw_input()` 関数 が `input()` 関数に改名
        * python 2 系にあった `input()` 関数は削除
    * `unicode()`, `unichr()` 関数の削除
    * file 型 / file 関数の削除
        * `open()`を使う
    * 演算子 `<>` の削除
        * `!=` を使う
    * 辞書の `has_key()` メソッドが削除
        * `in` を代わりに使う
    * `xrange()` 関数の削除
    * `long` 型の削除
        * `int` に統一
        * `sys.maxint` 定数はもはや正確でない
            * 一応代わりに `sys.maxsize` が利用できる
    * `os.getcwdu()` 関数は必要なくなった
        * 全て Unicode 文字列に統一されたので `os.getcwd()` で問題ない
    * `callable()` 関数が削除
        * `hasattr(x, '__call__')` を代わりに使う
    * `types` モジュールが返す定数の削除
        * 標準型の名前がそのまま返る。詳しくは[この表](http://diveintopython3-ja.rdy.jp/porting-code-to-python-3-with-2to3.html#types)を参照。
    * `basestring` データ型の削除
        * 文字列がUnicodeに統一されたため
    * `sys.exc_type`, `sys.exc_value`, `sys.exc_traceback` が `sys.exc_info()` というタプルに改名
* 8進数を表す構文が変更
    * Python 2 系: `0755`
    * Python 3 系: `0o755`
* 演算子 `/` の動作が変更
    * 整数ではなく浮動小数点を返
    * 演算子 `//` が2系の `/` と同じ動作
* byte 列表現の追加
    * Python 2 系: `str` (デフォルト) <-> `unicode`
    * Python 3 系: byte列表現 <-> `unicode` (デフォルト)
        * ただし byte列表現は
* バイナリファイルとテキストファイルの区別
    * Python 3 系では相互変換できない
        * Python 2 系: `open()` (バイナリ) <-> `codecs.open()` (Unicode文字列)
        * Python 3 系: `io.open()` (バイナリ) <-> `open()` (Unicode文字列) 
* 長さの違う配列に対する map の動作の変更
    * Python 2 系: 短い配列に None の値を補完して長い配列に合わせて処理する
    * Python 3 系: 短い配列に合わせて処理する
* pickle モジュールが後方互換性を持たない
    * Python 2 系: cPickle をインポート出来ない場合は pickle をインポート
    * Python 3 系: 常に pickle をインポートすればよい    
* リストを返していた関数の多くはイテレータを返す
    * map, filter, zip, range など
    * 代わりに imap, ifilter, izip が itertools から削除されている
* `apply()` 関数の廃止
    * Python 2 系: `apply(f,[a,b,c])` -> `f(a,b,c)`
    * Python 3 系: `f(*[a,b,c])` -> `f(a,b,c)`
        * 関数を直接呼び出し`*` を前に付けた引数のリストを渡せばよい。
* `reduce()` 関数がグローバルから functools モジュールの中に移動
    * `from functools import reduce` と書けばよい
* 辞書オブジェクトの一部メソッドが [view](http://docs.python.jp/3.3/library/stdtypes.html?highlight=dictionary#dictionary-view-objects) と呼ばれるイテレータのような動作をするオブジェクトを返す
    * `keys()`, `items()`, `values()`
* シーケンスの中の次の要素を返すグローバルな関数 `next()` 追加
    * メソッドを呼び出す代わりに使える
* 複数の引数をとるかわりにタプルを取る labmda 関数はアンパックされない
    * pyhton 2 系: `lambda (x, y): x + f(y)`
    * Python 3 系: `lambda x_y: x_y[0] + f(x_y[1])`
* リスト内包表記でタプルを丸括弧で括らなければならなくなった
    * Python 2 系: `[i for i in 1,2,3]`
    * Python 3 系: `[i for i in (1,2,3)]`
* オブジェクトの評価結果を取得する方法の変更
    * Python 2 系: `` `x` ``
    * Python 3 系: `repr(x)`
* メタクラスの定義方法の変更
    * Python 3系 ではクラス属性でメタクラスを定義できなくなった
* 再構成されたモジュール
    * urllib, urllib2, urlparse 等の統合
        * urllib に統合([公式ドキュメント](http://docs.python.jp/3.3/library/urllib.html))
    * dbm クローンの統合
        * dbm, gdbm, dbhash などは dbm に統合された([公式ドキュメント](http://docs.python.jp/3.3/library/dbm.html))。
    * httplib, Cookie, BaseHTTPServer などの統合。
        * http に統合([公式ドキュメント](http://docs.python.jp/3.3/library/http.html))。
    * xmlrpclib, DocXMLRPCServer, SimpleXMLRPCServer の統合。
xmlrpc
        * xmlrpc に統合([公式ドキュメント](http://docs.python.jp/3.3/library/xmlrpc.html?highlight=xmlrpc))。
    * cStringIO や StringIO が io に統合
    * Queue が queue に変更
    * SocketServer が socketserver に変更
    * ConfigPerser が configparser に変更
    * repr が reprlib に変更
    * commands が subprocess に変更
    * `__builtin__` が builtins に変更

## 従来のままでも動くが推奨スタイルが変更されたもの
* `set()` リテラル
    * Python 2 系: `set([1, 2, 3])`
    * Python 3 系: `{1, 2, 3}`
        * ただし、空集合は`set()`で作らなければならない
        * `{}` は空の辞書を表す
* `buffer()` 関数
    * Python 2 系: `y = buffer(x)`
    * Python 3 系: `y = memoryview(x)`
* 無限ループで `while 1:` ではなく `while True:` を用いる
    * python 2.3 まで本物のブール型を持っていなかっため前者が慣用的に用いられていた
* `type(x) == T` や `type(x) is T` ではなく `isinstance(x, T)` を用いる
* シーケンスをソートする場合

```
l = list(seq)
l.sort()
f(l)
```
ではなく

```
l = sorted(seq)
f(l)
```
をつかう。


ざっとまとめてみたが、ミス・漏れ等があるかもしれない。