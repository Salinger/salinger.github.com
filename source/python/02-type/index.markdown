---
layout: page
title: "2. 型"
date: 2014-02-03 16:13
comments: false
sharing: true
footer: true
---

Pythonは動的型付け言語なので、変数・引数・返り値等の型は実行時に決まる。

プログラムを書くときは現在どの型を扱っているのか、頭で考えながら書きましょう。

* bool 型
    * True や False を表す。

* 数値型
    * 数値型として int, long, float, complex がある。

* イテレータ型
    * コンテナの内容にわたって反復処理を行うための型。forでリストやディクショナリにアクセスする場合は自動的にこの型に変換される。

* シーケンス型
    * str, unicode, list, tuple, bytearray, buffer, xrange がある。

* 集合型
    * set, frozenset がある。

* マップ型
    * dictionary がある。

* ファイルオブジェクト
    * ファイル操作時に使用するオブジェクト。

* nullオブジェクト
    * None がある。

* その他
    * モジュール、関数、メソッド等も型。型自体も型(type型)。