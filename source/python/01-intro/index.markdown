---
layout: page
title: "1. 下準備・はじめに"
date: 2014-02-03 16:10
comments: false
sharing: true
footer: true
---

## はじめに

Pythonは基本的にオブジェクト志向型言語である。すべての要素はオブジェクトとして扱われる。数値、変数、文字列、リスト等だけでなく、クラスもオブジェクト、関数もオブジェクト、型もオブジェクトである。

また高階関数を扱えるなど、関数型言語としても使える(高階関数: 関数（手続き）を引数にしたり、戻り値にできる関数)。

基本的にインデント（字下げ）で構文のブロックを構成する。インデントにはスペースもしくはタブが使用できる。コメントを記述する際は # を記述すればそれ以降から行末までコメントとなる。

```
# this is comment
```

## 本体のインストール
Mac(OS: Maverics)の場合、デフォルトで2.7.5がインストールされているはず。

バージョンの確認

```
python -V
Python 2.7.5
```

Linux系のOSの場合、ディストリビューションにもよるが、apt-getかyumでインストールできるはず。

私はWindows環境には詳しくないので、Windowsにインストールする場合はググってください。

## 実行(インタプリタ)
インタプリタを起動。

```
$ python
python
Python 2.7.5 (default, Nov  8 2013, 12:32:23) 
[GCC 4.2.1 Compatible Apple LLVM 5.0 (clang-500.2.79)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

あとは`>>>`の部分にコードを入力すれば実行される。

```
>>> print "Hello, world!"
print "Hello, world!"
Hello, world!
```

## 実行(ファイルに記述したコード)
`hello.py` に次の内容を記述。

```
#!/usr/bin/env python
#-*- coding:utf-8 -*-
print "Hello, world!"
```

実行してみる。

```
$ python hello.py
python hello.py 
Hello, world!
```
