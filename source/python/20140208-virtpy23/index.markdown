---
layout: page
title: "Python 3 系移行のための仮想環境構築(MacOSX + Homebrew + virtualenv)"
date: 2014-02-08 12:03
comments: true
sharing: true
footer: true
---

## はじめに
今回は Python 3 系への移行を念頭に置いて、Python 用の仮想環境の構築についてあれこれ調査した。具体的には2系と3系のうまいこと同居させて、パッケージ管理をきちんと行えるような環境を作る。なおMac（パッケージ管理はHomebrew）環境を対象としています。Linux系もパッケージ管理（aptやyum）の部分だけ置き換えれば基本的にはどうにかなるはず。

##  Python 2 と 3 のインストール
Homebrewを利用して Python 2系と3系をインストール。その後、デフォルトでインストールしてあるPythonではなく、HomebrewでインストールしたPythonが起動するようにする。既にPythonがHomebrewでインストールされている場合は、先に`$ brew upgrade`で最新版に更新しておく。以下のコマンドを実行。

```
$ brew update
$ brew install python
$ brew install python3
$ brew link --overwrite python

$ which python
/usr/local/bin/python
$ python
Python 2.7.6 (default, Jan 21 2013, 01:36:58) 
[GCC 4.2.1 Compatible Apple Clang 4.1 ((tags/Apple/clang-421.11.66))] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 

$ which python3
/usr/local/bin/python3
$ python3
Python 3.3.3 (default, Feb  7 2014, 23:35:24) 
[GCC 4.2.1 Compatible Apple LLVM 5.0 (clang-500.2.79)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

2系(コマンド: python)と3系(コマンド: python3)のインストール完了。
ちなみに、bashだと問題ないが、zsh 環境だとOSにデフォルトでインストール済みの方のPythonが起動してしまった。その場合、.zshrcに/usr/local/binを先に読むように、以下を記述する必要あり。

```
export PATH=/usr/local/bin:/usr/local/sbin:/sbin:/usr/sbin:${PATH}
```

## 仮想環境の構築
Python 2 系ではPython本体のバージョン管理はHomebrewに任せて、 pip + virutalenv でモジュール等を管理するのが一番楽だった。

Python 3.3 から venv (コマンド: pyvenv)という virtualenv と似た機能が追加された。が、2 系と環境を共存させるとなると面倒。 virtualenv が 3 系にも対応してるようなので、こちらを使うほうが良さそう。なので 2 系のときと同じく pip + virutalenv で環境を構築する。ベースのPythonインタープリタは2系のものを使うことにする。以下のコマンドを実行。

```
$ easy_install pip
$ pip install virtualenv
$ pip install virtualenvwrapper
$ mkdir ~/.virtualenvs
```

bash の場合 .bachrc に、zsh の場合 .zshrc に以下を記述

```
#virtualenv settings
export PATH=/usr/local/share/python:${PATH}
export WORKON_HOME=$HOME/.virtualenvs
. /usr/local/share/python/virtualenvwrapper.sh
```

リロードする。

```
$ source .zshrc 
```

仮想環境で作業する際には、以下の5つのコマンドを覚えておけばとりあえずはOK。

`$ mkvirtualenv ENV_NAME` で仮想環境作成

`$ workon` で仮想環境の一覧確認

`$ workon ENV_NAME` で指定の環境に入る

`$ deactivate` で仮想環境から脱出

`$ rmvirtualenv ENV_NAME` で仮想環境削除


テスト

```
$ pip freeze # 現在のモジュールの確認 (virtualenvなど)
$ mkvirtualenv test1 # test1という環境を作成
$ deactivate #環境から抜ける
$ mkvirtualenv test2 # test2という環境を作成
$ workon # 環境の一覧を確認
test1
test2
$ workon test1 # testを選択
$ pip install numpy # test1 にnumpyをインストール
$ pip freeze # nuupyのインストールを確認
$ deactivate 
$ pip freeze # 元の環境に影響がないのを確認
$ rmvirtualenv test1 # テスト環境を削除
$ rmvirtualenv test2
$ workon # 出力なし 削除完了
```

これで Python 2 系は問題なし。Python 3 系を使いたい場合、`--python /usr/local/bin/python3`オプションを指定すれば良い(筆者の環境だと`--python python3`でも問題なし)。

```
$ mkvirtualenv py2
$ mkvirtualenv py3 --python /usr/local/bin/python3
$ workon py2
$ python -V
Python 2.7.3
$ workon py3
$ python -V
Python 3.3.3
$ deactivate 
$ python -V
Python 2.7.3
```

これで2系と3系、それぞれで仮想環境を自由に切り替えられる。あとは仮想環境下に入って pip で必要なモジュールをインストールすればOK。

