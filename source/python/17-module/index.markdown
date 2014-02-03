---
layout: page
title: "17. モジュール"
date: 2014-02-03 16:33
comments: false
sharing: true
footer: true
---
## 使用方法
Pythonでは標準で使用可能なモジュールとサードパーティ製のモジュールが存在する。
基本的に使用する場合は、ソースコードの冒頭部分で

```
import module_name
```

でインポートできる。

## from と as

```
from A import B
```

Aにはパッケージ名やモジュール名を指定する。

Bには取り込みたいパッケージやモジュール名またはクラスや関数名、変数名なども指定できる。

必要なもの以外をインポートすると、名前の衝突等予想外のトラブルが起こる場合があるので、必要なものだけインポートする方がbetter。

```
from A import *
```

Aに含まれるものをすべてインポート。Aにmethod_a()という関数がある場合、この方法ならmethod_a()と直接アクセスできるトラブルの元なので、この記法は何がインポートされるかわかっている場合以外は避けたほうが無難。

```
import A.B.C as D
```

長い名前のパッケージに含まれているものにシンプルな名前でアクセスできる。別名は混乱の元なので、やたらめったら使うのは避けたほうが良い。

## 自作モジュールのインポート
モジュールは以下の順に調べて、最も最初に見つかったものがインポートされる。

1. 実行中のファイルと同じフォルダ
2. カレントフォルダ
3. 環境変数「PYTHONPATH」に列挙したフォルダ
4. sys.pathに登録してあるフォルダ

同一ディレクトリにあるPythonのプログラムは以下のようにしてインポートできる。

* program_a.py

```
def aprint():
    print "This is from program_a.py"
    return
```

* program_b.py

```
#!/usr/bin/env python
#-*- coding:utf-8 -*-
import program_a
    program_a.aprint()
```

実行してみる。

```
$ python program_b.py
This is from program_a.py
```

## モジュールのドキュメント
以下のように3重引用符で囲んだ文字列をクラスや関数の直後に記入しておくと、 pydoc等で確認した時にわかりやすい形でクラスや関数の説明を表示してくれる。 きちんと各コメントを書いておくと、後に救われること多々あり。

以下の内容をtest.pyという名前で保存。

```
#/usr/bin/env python
#-*- coding:utf-8 -*-
"""
File info
"""
    
__author__ = "author <mail@example.com>"
__status__ = "dev"
__version__ = "1.0.0"
__date__    = "03 Feb. 2014"
    
TOP_LEVLE_VAR = 'var'
    
class TestClass(object):
    """
    Abstract of this class

    Details of this method ...
    """
        
    def test_method(self, x):
    """
    Abstract of this method
  
    Details of this method ...
    """
    return 5 * x * x + 2 * x + 1
```

test.py を保存したディレクトリでインタプリタを起動。インタプリタでhelp()を入力。

```
>>> help()
   
help> test
test
Help on module test:
   
NAME
    test - File info

FILE
    /Users/hoge/fuga/piyo/test.py
    
CLASSES
    __builtin__.object
        TestClass
    
    class TestClass(__builtin__.object)
     |  Abstract of this class
     |  
     |  Details of this method ...
     |  
     |  Methods defined here:
     |  
     |  test_method(self, x)
     |      Abstract of this method
     |      
     |      Details of this method ...
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  __dict__
     |      dictionary for instance variables (if defined)
     |  
     |  __weakref__
     |      list of weak references to the object (if defined)
    
DATA
    TOP_LEVLE_VAR = 'var'
    __author__ = 'author <mail@example.com>'
    __date__ = '03 Feb. 2014'
    __status__ = 'dev'
    __version__ = '1.0.0'
    
VERSION
    1.0.0
    
DATE
    03 Feb. 2014
    
AUTHOR
    author <mail@example.com>
```

## 役立つモジュール

### 標準モジュール
代表的なものをあげておく。ここであげたものはひと通り[ドキュメント](http://docs.python.jp/2.7/library/index.html)に目を通しておくとよい。他にもいろいろある。

* [re](http://docs.python.jp/2.7/library/re.html): 正規表現に関するモジュール
* [datetime](http://docs.python.jp/2.7/library/datetime.html): 日付に関連するモジュール
* [calender](http://docs.python.jp/2.7/library/calendar.html): カレンダーに関するモジュール
* [mutex](http://docs.python.jp/2.7/library/mutex.html): 並列処理時の排他制御に関するモジュール
* [pprint](http://docs.python.jp/2.7/library/pprint.html): 入れ子のリストやディレクトリの表示が見やすいprint
* [copy](http://docs.python.jp/2.7/library/copy.html): 浅いコピーと深いコピーを扱うモジュール
* [math](http://docs.python.jp/2.7/library/math.html): 数学関連のモジュール
* [random](http://docs.python.jp/2.7/library/random.html): 乱数生成に関するモジュール
* [os.path](http://docs.python.jp/2.7/library/os.path.html): ディレクトリ名やファイル名に関するモジュール
* [shutil](http://docs.python.jp/2.7/library/shutil.html): 高レベルなファイル操作(圧縮ファイルの操作等も)
* [sqlite3](http://docs.python.jp/2.7/library/sqlite3.html): SQLiteデータベース用モジュール
* [time](http://docs.python.jp/2.7/library/time.html): 時刻データのためのモジュール
* [argparse](http://docs.python.jp/2.7/library/argparse.html): コマンドラインオプション、引数などのパーサ
* [multiprocessing](http://docs.python.jp/2.7/library/multiprocessing.html): 並列処理のためのモジュール
* [cPickle](http://docs.python.jp/2.7/library/pickle.html#module-cPickle): データの永続化
* [json](http://docs.python.jp/2.7/library/json.html): JSON形式のエンコードおよびデコード
* [urllib](http://docs.python.jp/2.7/library/urllib.html): URLによる任意リソースへのアクセス
* [urllib2](http://docs.python.jp/2.7/library/urllib2.html): URLを開くための拡張可能なライブラリ
* [sys](http://docs.python.jp/2.7/library/sys.html): システムパラメータと関数
* [pydoc](http://docs.python.jp/2.7/library/pydoc.html): 開発ドキュメント生成とオンラインヘルプに関するモジュール
* [unittest](http://docs.python.jp/2.7/library/unittest.html): ユニットテストフレームワーク
* [pdb](http://docs.python.jp/2.7/library/pdb.html): デバッグ用モジュール

### サードパーティのプログラム&Python用モジュール
個人的にお世話になったプログラムとそのバインディングモジュールたち。 詳細なインストール方法はそれぞれ異なるので各モジュールのページを参照のこと。 ただし、メジャーなモジュールはpip(Pythonのモジュール管理用プログラム)でインストール可能。 基本的にpipでインストール可能なものはpipでインストールすること。

```
$ pip install modulename
```

検索する場合、

```
$ pip search modulename
```

もしpipがインストールされていない場合は、

```
$ easy_install pip
```

でインストールできるはず。ただし情報が古いかもしれないので、上手くいかない場合はググってください。また各モジュールの使い方は公式ドキュメントを見るかググってください。

* [MeCab](http://mecab.googlecode.com/svn/trunk/mecab/doc/index.html): 日本語の形態素解析エンジンのモジュール。
* [CaboCha](http://code.google.com/p/cabocha/): Support Vector Machines に基づく日本語係り受け解析器のモジュール。
* [LIBSVM](http://www.csie.ntu.edu.tw/~cjlin/libsvm/): Support Vector Machine(SVM)に関するモジュール。
* [NLTK](http://nltk.org/): 自然言語処理に関するモジュール。
* [NumPy&SciPy](http://docs.scipy.org/doc/): 数値計算・科学計算に関するモジュール。大規模な行列演算や、高速な計算アルゴリズムが使用できる。
* [PLI](http://www.pythonware.com/products/pil/): Python Imaging Library 強力な画像処理用モジュール。
* [Matplotlib](http://matplotlib.org/): 作図（主にグラフ）用のモジュール。
* [Beautiful Soup](http://www.crummy.com/software/BeautifulSoup/): HTLMやXML等のパーサ。標準モジュールにある各種パーサよりもこちらを使うことを推奨します。
* [mechanize](http://wwwsearch.sourceforge.net/mechanize/): Webから情報をクロールするときに超便利。

