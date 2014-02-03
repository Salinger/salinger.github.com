---
layout: page
title: "13. 制御構文"
date: 2014-02-03 16:32
comments: false
sharing: true
footer: true
---

### pass
何もしない場合に

```
pass
```

と書く。仮決めした中身の関数を記述しておく場合等に使用。

### print

```
print exp1[, exp2[,...]]
```

でexpを画面に出力。通常は改行文字が自動的に付加されるが末尾に","でキャンセル可。

```
>>> print "abc","def","ghi"
abc def ghi
```

### return

```
return exp1[, exp2, [...]]
```

でexpを返す。finally節を伴うtry文の外に処理が引き渡されると関数から抜ける前にfinnlay節が実行される。

### yield
関数定義中でreturnの代わりに使用すると、通常の関数ではなくジェネレータ関数になる。関数が終了しても、関数中のすべてのローカル変数が保存されたままになる。

### raise
```
raise [exp1[,...]]
```

例外expを送出する。詳細は後述。

### break
for ループや while ループ中の最も内側のループを終了させる。finally節を伴うtry文の外に処理が引き渡されると関数から抜ける前にfinnlay節が実行される。

### continue
for ループや while ループ中の最も内側の次周期の処理を開始させる。

### import
モジュールを探し、必要なら初期化する。fromを使う形式と使わない形式がある。詳細は後述。

### global

```
global exp1[, ...]
```

列挙した識別子をグローバル変数として解釈する。大域変数はトラブルの元になりやすいので非推奨。

### exec
一連の文字列もしくはファイルオブジェクトをPython実行文として実行する。

### if
条件分岐のために使用。

```
if cond:
    proc_A
elif cond:
    proc_B
else:
    proc_C
```

condの部分にはブール型を返す式を記述する。式を順に評価していき、condが真になった最初の部分を実行する。すべて偽なら、else節がある場合その部分が実行される。

### while
式が真の間、実行を繰り返す。

```
while cond:
    proc_A
else:
    proc_B
```

式が偽であれば、else節がある場合にはそれを実行しループ終了。

### for
シーケンス内の要素に渡って反復処理を行う。

```
for x in iter:
    proc_A
```

ループ回数を指定したい場合はrange()が使える

```
for x in range(5):
    proc_A
```

とすると5回ループが繰り返される(xは0 ~ 4に順次更新される)。range()は指定した範囲の数列リストを作成するための関数。

```
>>> range(5)
[0, 1, 2, 3, 4]
>>> range(1,5)
[1, 2, 3, 4]
>>> range(1,10,2)
[1, 3, 5, 7, 9]
```

iterの部分にディクショナリを指定すると全keyを順にたどることが出来る。

```
>>> for x in {"a":1,"b":2,"c":3}:
        print x
a
b
c
```

### try
例外処理を行う。下記のように記述する。詳細は後述。

```
try:
    proc_A
except state:
    proc_B
finally:
    proc_C
```

### with
ファイルオープン時などに使用。詳細は後述。

### 関数定義

```
def function_name([arg1,[,arg2[,...]]]):
    proc_A
```

このように定義する。詳細は後述。

### クラス定義

```
class class_A (inheritance):
    class_variable_A
    class_variable_B
    ...
    
    def __init__(self[,arg1[,...]]):
        proc_A
     
    def class_methodA(self[,arg1[,...]]):
        proc_B
```

このように定義する。詳細は後述。