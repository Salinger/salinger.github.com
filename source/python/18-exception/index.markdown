---
layout: page
title: "18. 例外"
date: 2014-02-03 16:33
comments: false
sharing: true
footer: true
---

たとえ文や式が構文的に正しくても、実行しようとしたときにエラーが発生するかもしれない。実行中に検出されたエラーは 例外 (exception) と呼ばれ、常に致命的とは限らない。

Python プログラムで例外を補足するには以下のように書きます。

```
try:
    proc_A
except:
    proc_B
finally:
    proc_C
```

tryで囲んだ部分でエラーが起こった場合、exceptの部分が実行される。except節でエラーを回避する処理を書けば、処理を継続できる。

例外が起こっても起こらなくても、finally節が最終的に実行される。この部分は省略できる。特定のエラーのみを補足することもできる。

```
try:
    proc_A
except ValueError:
    proc_B
```

上記の場合、ValueErrorが発生した場合のみexcept節が実行される。エラーの一覧は[このページ](http://docs.python.jp/2/library/exceptions.html#bltin-exceptions)に。

よく問題になるのが、文字列処理やファイル操作時のエラー。ゴミが混ざったデータをパースする場合、きっちり例外処理を行いましょう。