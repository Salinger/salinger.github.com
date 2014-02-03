---
layout: page
title: "19. オブジェクト指向プログラミング"
date: 2014-02-03 16:33
comments: false
sharing: true
footer: true
---

## オブジェクト指向とは

オブジェクト指向プログラミングの基本的な考え方は[各自で調べてください](https://www.google.co.jp/search?client=safari&rls=en&q=%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E6%8C%87%E5%90%91%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0&ie=UTF-8&oe=UTF-8&gws_rd=cr&ei=vGhZUqTlMcyfkwXC4ICoDQ)。

データと手続きをまとめてオブジェクトとして扱うことで、

「命令」中心の考え方から、「対象（オブジェクト）」中心の考え方

にできる。Pythonではすべてが「オブジェクト」。オブジェクトを定義するものがクラス。

## クラスの定義とインスタンス化
もっとも単純な定義
```
class ClassName (object):
    <文-1>
    ...
    <文-N>

class MyClass (object):
    i = 1

    def f(self):
        return "hello, world!"
```

クラスはオブジェクトのひな形であり、インスタンス化することで各種属性(メンバ・メソッド)の参照が可能になる。

```
>>> x = MyClass()
>>> x.i
1
>>> x.f()
"hello, world!"
```

ちなみに、Pythonの場合クラス定義の外で定義された関数をクラス内で利用することも可能。

```
def hello(self):
    return "hello, world!"

class MyClass (object):
    i = 1
    f = hello
```

## クラス変数とクラスメソッド
クラス変数・クラスメソッドは全インスタンスで共有される。

```
class MyClass (object):
    i = 1
    j = 2
```

のように、クラスのフィールドにベタ書きするとクラス変数になる。この場合、どこかのインスタンスでiやjを変更した場合、他のインスタンスのiやjの値も変化する。

各インスタンス毎に独立したインスタンス変数は以下のようにして定義できる。

```
class MyClass (object):
    def __init__(self, a, b):
        self.x = a
        self.y = b
```

この場合、どこかのインスタンスでxやyを変更しても、他のインスタンスのxやyの値はそのままである。

クラスメソッドを定義すると、インスタンス化せずにそのメソッドを使用できる。以下のようにメソッドの前に@clssmethodをつけるとクラスメソッドとして定義できる。

```
class MyClass (object):
    @classmethod
    def say_hello(cls,x):
        print "Hello " + x + " !"
    
>>> MyClass.say_hello(u"さりんじゃー")
Hello さりんじゃー !
```
    
## コンストラクタとデストラクタ
コンストラクタはインスタンス作成時に実行されるメソッド。デストラクタはインスタンス破棄時に実行されるメソッド。デストラクタの実行タイミングについてはガベージコレクション任せ。

コンストラクタは

```
def __init__(self[,arg1[,...]]):
    <文>
```

デストラクタは

```
def __del__(self):
    <文>
```

で定義できる。

コンストラクタでインスタンスの各メンバの初期化等を行う。

```
class MyClass (object):
    def __init__(self,x,y):
        self.x = x
        self.y = y

    def mul(self):
        return self.x * self.y 
    
>>> x = MyClass(2,4)
>>> x.mul()
8
```

## 継承
クラスに「親子関係」を持たせる機能。子は親が定義そたインスタンス変数やメソッドを引き継ぐ。

プログラムを作る場合、いままで作ったプログラムと同じような機能が必要になることがあるが、継承を使うことでその機能を受け継ぎ、新規・変更される機能のみをプログラムすることが可能になる。

クラスを継承する場合、その元になるクラスを「スーパークラス」または「ベースクラス」と呼ぶ。そして、継承したクラスを「サブクラス」と呼ぶ。

list を継承してクラスを作成し、値が追加された際にprint出力するようにする。

```
class PrintList (list):
    def __init__(self):
        list.__init__(self)

    def append(self,value):
        list.append(self,value)
        print u"Added value：" + str(value)
    
>>> plist = PrintList()
>>> plist.append(1)
Added value：1
>>> plist.append("hoge")
Added value：hoge
>>> plist.append(u"ぴよ")
Added value：ぴよ
>>> plist
[1, 'hoge', u'\u3074\u3088']
```

Pythonは多重継承も可能 FooとBarの定義

```
class Foo:
    def __init__(self, x):
        self.a = x
    
    def get_a(self): return self.a
    def method_1(self): print 'Foo.method_1'
    
class Bar:
    def __init__(self, x):
        self.b = x

    def get_b(self): return self.b
    def method_1(self): print 'Bar.method_1'
```

FooとBarを継承したクラスBazの定義

```
class Baz(Foo, Bar):
    def __init__(self, x, y):
        Foo.__init__(self, x)
        Bar.__init__(self, y)
    
>>> obj = Baz(1, 2)
>>> obj
<__main__.Baz instance at ...>
>>> obj.get_a()
1
>>> obj.get_b()
2
>>> obj.method_1()
Foo.method_1
```

メソッドの探索はスーパークラスを定義したカッコの先頭 (左側) から順番に行われ、
最初に見つかったメソッドが実行される。したがって、クラスの順番を逆にすると、今度は Bar の method_1() が実行されて Bar.method_1 と表示される。

## 演算子のオーバーロード

演算子として用いられる + 等で特定の手続きを実行することができる。

[演算子一覧](http://docs.python.jp/2/library/operator.html)

`__XXX__` のようなメソッドをクラスに定義する。

例えば、+ 演算子の場合、

```
class MyClass (object):
    def __init__(self):
        self.x = 10

    def __add__(self,other):
        return self.x * 2 + other
    
>>> x = MyClass()
>>> x + 10
30
```

演算子のオーバーロードを利用して、関数として呼ばれたときの振る舞いも `__call__`メソッドを定義することで定義できる。

```
class MyClass(object):
    def __call__(self,x,y):
        return x * 10 + y
    
>>> x = MyClass()
>>> x(1,2)
12
```