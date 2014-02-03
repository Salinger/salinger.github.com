---
layout: page
title: "14. 標準入力"
date: 2014-02-03 16:32
comments: false
sharing: true
footer: true
---

* input([string])
    * 対話形式で一行ずつ整数(int)を端末から読む場合、この関数を利用する。入力されたものがそのまま戻り値となる。文字列を引数として与えると、入力時に出力される。

* raw_input([string])
    * 対話形式で一行ずつ文字列(str)を端末から読む場合、この関数を利用する。入力されたものがそのまま戻り値となる。文字列を引数として与えると、入力時に出力される。

* sys.stdin
    * 標準入力(stdin)から一行ずつ、最後まで読む場合はsysモジュールをインポートして、こちらを利用する。使用例はこんな感じ。

```
#!/usr/bin/env python
import sys
  
for line in sys.stdin:
    print line,
```