---
layout: page
title: "15. ファイル入出力"
date: 2014-02-03 16:32
comments: false
sharing: true
footer: true
---

ファイル入出力を扱う際は、基本的にcodecsモジュールを使うようにする。プログラムの冒頭に

```
import codecs
```

を記述する。

## 読み込み
最初にファイルオブジェクトを取得する。

```
fin  = codecs.open(filename,"r","utf-8")
```

filenameには開くファイルの場所を記入。 "r" は読み込みモードを表す。 文字コードは基本的に"utf-8"を使用する。ただし、Windows環境でファイルを利用する場合は、 "sift-jis"を使用しなければならない場合あり。

読み込む場合は以下の様なメソッドが利用できる。

* fin.readline([size])
    * ファイルから一行全部を読み込む。終末の改行文字は文字列に残る。size 引数が与えられ、負でなければ、そのsizeバイト分だけ読み込む。

* fin.readlines([sizehint])
    * readline() を使ってに到達するまで読み出し、 EOF 読み出された行を含むリストを返す。オプションの sizehint 引数が存在すれば、 EOF まで読み出す代わりに完全な行を全体で大体 sizehint バイトになるように読み出す。

ファイルを1行ずつ読む場合は、次のように書くことも出来る。

```
for l in fin:
    proc_A
```

ファイルを読み込む場合、これが一番普通な方法。この方法なら、ファイルを一度に全部読み込まないので巨大なファイルも扱える。この書き方を推奨します。

処理が終わったら、

```
fin.close()
```

を実行して、ファイルを閉じる。

今いるディレクトリにあるtest.txtを開いて、 その内容を画面に表示する場合は次のように書ける。

```
fin = codecs.open("./test.txt","r","utf-8"):
try:
    for l in fin:
        print l
finally:
    fin.close()
```

withを使えばcloseメソッドを直接呼び出す必要がなくなる。 閉じ忘れが無くなるので、こっちを使うほうがいいかも。

```
from __future__ import with_statement
    
with codecs.open("./test.txt","r","utf-8") as fin
    for line in fin:
        print line
```

## 書き込み
まずファイルオブジェクトを取得。

```
fout = codecs.open(file_name,"w","utf-8")
```

filenameには開くファイルの場所を記入。

"w" は書き込みモード(同名ファイルがあれば上書き)を表す。

"a"にすると追記モード(同名ファイルがあれば追記)になる。

文字コードは基本的に"utf-8"を使用する。ただし、Windows環境でファイルを利用する場合は、 "sift-jis"を使用しなければならない場合あり。

書き込む場合は以下の様なメソッドが利用できる。

* fout.write(str)
    * 文字列をファイルに書き込む。戻り値はない。バッファリング によって、flush() または close() が呼び出されるまで、実際にファイル中に文字列が書き込まれないこともある。

* fout.writelines(sequence)
    * 文字列からなるシーケンスをファイルに書き込む。戻り値はない。行間の区切りを追加しないので注意。fout.write("".join(lines))と等価。

処理が終わったら、

```
fout.close()
```

を実行して、ファイルを閉じる。

今いるディレクトリにあるtest.txtを開いて、 文字列からなるリストの内容をファイルに出力する(改行も)場合、 次のように書ける。

```
l = ["This is ...", "for test...", "!"]
fout = codecs.open("./test.txt","w","utf-8"):
for line in l:
    fout.write(l + '\n')
fout.close()
```