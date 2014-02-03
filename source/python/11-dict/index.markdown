---
layout: page
title: "11. ディクショナリ"
date: 2014-02-03 16:32
comments: false
sharing: true
footer: true
---
## ディクショナリ（辞書）について
key と value のペアを扱うためのdictionary型。 以下のように定義できる。

```
>>> dic = {
        u"あ": 0,
        u"い": 1,
        u"う": 2,
    }
>>> dic
{u'\u3042': 0, u'\u3044': 1, u'\u3046': 2}
>>> dic[u"あ"]
0
>>> dic[u"う"]
2
```

最後の要素の末尾の`,`はあってもなくても良い。

こんな感じで要素を追加できる。

```
>>> dic[u"りすと"] = [1,2,3,4,5]
>>> dic[u"りすと"]
[1,2,3,4,5]
```

## よく使う演算子・メソッド等
* len(dict)
    * ディクショナリ dict に含まれる項目数を返す。

* dict[key]
    * ディクショナリ dict のキー key の項目を返す。もし key が存在しなければ、 KeyError 。

* dict[key] = value
    * ディクショナリ dict[key] に value を設定する。

* del dict[key]
    * ディクショナリ dict から dict[key] を削除。もし key が存在しなければ、 KeyError。

* key in dict
    * dict がキー key を持っていれば True を返す。そうでなければ、 False を返す。

* key not in dict
    * not key in dict と等価。

* iter(dict)
    * ディクショナリ dict の全てのキーに渡って、イテレータを返します。これは iterkeys() メソッドへのショートカットです。

* dict.clear()
    * ディクショナリの全ての項目を消去。

* dict.copy()
    * ディクショナリの浅いコピーを返します。

* dict.get(key[, default])
    * もし key がディクショナリにあれば、 key に対する値を返す。そうでなければ、 default を返す。default が与えられなかった場合、デフォルトでは None となる。そのため、このメソッドは KeyError を送出することはない。

* dict.has_key(key)
    * ディクショナリに key が存在するかを確認する。has_key() は key in d と等価。

* dict.items()
    * ディクショナリのコピーを (key, value) の対のリストとして返す。

* dict.keys()
    * ディクショナリのキーのリストのコピーを返します。 dict.items() の Note も参照下さい。

* dict.pop(key[, default])
    * もし key がディクショナリに存在すれば、その値をディクショナリから除去して返す。そうでなければ、default を返す。default が与えらず、かつ、 key が辞書に存在しなければ KeyError 。

* dict.popitem()
    * 任意の (key, value) の対をディクショナリから除去して返す。

* dict.setdefault(key[, default])
    * もし、 key がディクショナリに存在すれば、その値を返します。そうでなければ、値を default として key を挿入し、 default を返す。default のデフォルト値は None 。

* dict.update([other])
    * ディクショナリの内容を other のキーと値で更新する。既存のキーは上書きされる。返り値は None。

* dict.values()
    * ディクショナリの値のリストのコピーを返す。