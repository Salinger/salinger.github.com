---
layout: page
title: "2to3 と 3to2"
date: 2014-02-11 22:28
comments: true
sharing: true
footer: true
---

## 2to3
[2to3](http://docs.python.jp/3.3/library/2to3.html#module-lib2to3) は Python 2.x のソースコードを読み込み、一連の 変換プログラム を適用して Python 3.x のコードに変換するプログラムです。Python 2.6 以降に含まれています。

```
$ 2to3 example.py
```

を実行すると、ソースの差分が表示される。

```
$ 2to3 -w example.py
```

で変更点をソースコードに上書きする(オリジナルのバックアップも作成される)。

具体的な内部処理の説明は[このページ](http://docs.python.jp/2.7/library/2to3.html)が詳しい。

`__future__` モジュールを利用して、Python 2 系のプログラムを作成すれば、比較的楽に変換できるはず。ただし、文字列周り(byte列の扱い)でトラブりやすいので注意。

## 3to2
[3to2](https://bitbucket.org/amentajo/lib3to2/overview) は有志作成のプログラムです。Python 3.x のソースコードを読み込み、一連の 変換プログラム を適用して Python 2.x のコードに変換するプログラムです。

## まとめ
これらのモジュールを使うと、1つのソースコードで両バージョン対応のプログラムを作成することが出来る。が、既存のものを全自動でというわけにもいかない。