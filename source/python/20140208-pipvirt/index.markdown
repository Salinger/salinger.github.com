---
layout: page
title: "pip 1.5 + virtualenv によるパッケージの管理"
date: 2014-02-08 12:14
comments: true
sharing: true
footer: true
---

## はじめに
プロジェクト毎に必要なパッケージの管理を Python でやるにはどうしたらいいかをまとめた。Ruby の Gem パッケージの管理ツール Bundler と似たような事ができる。MacOSX の Homebrew 環境で作業は行っているが、virtualenv 環境を構築してしまえば Linux 等でも同じはず。

## virtualenv 環境の構築
まずは、virtualenv 環境を構築する。[こっちのページ](/python/20140208-virtpy23)を参照。

## pip について
Python のパッケージ管理ツール。virtualenv 環境を構築すれば自動的にインストール済み。
既にインストールされているpipのバージョン < 1.5の場合、`$ pip install -U pip`で1.5以上になるように更新しておく。

まず作業したいプロジェクト用の仮想環境を作る。

```
$ mkvirtualenv testenv
$ workon testenv
```

あとは仮想環境下で以下のようなコマンドを実行して、必要なパッケージのインストール、管理を行う。

### インストール済みのパッケージを確認
`$ pip list` で確認できる。

```
$ pip list
List (1.3.0)
mecab-python (0.994)
pip (1.5.2)
setuptools (2.1)
...
```

### pypi からパッケージを検索
[Python Package index(pypi)](https://pypi.python.org/pypi)とは、Python 用のソフトウェアリポジトリ。 Ruby の RubyGems 、Perl の CPAN みたいなもの。

`$ pip search SomePackage` で SomePackage を検索できる。

例:
```
$ pip search scipy
scipy                     - SciPy: Scientific Library for Python
scikit-image              - Image processing routines for SciPy
scipy-data_fitting        - Data fitting system with SciPy.
...
``` 

### インストール
`$ pip install PACKAGE_NAME` で PACKAGE_NAME を pypi から検索してインストールしてくれる。

例:
```
$ pip install SomePackage            # 最新 ver
$ pip install SomePackage==1.0.4     # 特定 ver
$ pip install 'SomePackage>=1.0.4'     # ある ver 以上
```

#### 開発版のインストール
開発版のパッケージをインストールしたい場合、以下のようにする。デフォルトで検索されるのは安定版のみ。

```
$ pip install --pre SomePackage
```

#### ファイルからインストール
手元のファイルやネット上のファイル(圧縮したままでOK)からもインストール可能。

```
$ pip install ./downloads/SomePackage-1.0.4.tar.gz
$ pip install http://my.package.repo/SomePackage-1.0.4.zip
```

#### リモートリポジトリからインストール
git リポジトリなどから直接パッケージをインストールすることも可能。

```
$ pip install -e git+https://git.repo/some_pkg.git#egg=SomePackage          # from git
$ pip install -e hg+https://hg.repo/some_pkg.git#egg=SomePackage            # from mercurial
$ pip install -e svn+svn://svn.repo/some_pkg/trunk/#egg=SomePackage         # from svn
$ pip install -e git+https://git.repo/some_pkg.git@feature#egg=SomePackage  # from 'feature' branch
$ pip install -e git+https://git.repo/some_repo.git@egg=subdir&subdirectory=subdir_path # install a python package from a repo subdirectory
```

#### ローカルミラーからインストール
ローカルのミラーからもインストール可能。
```
$ pip install --index-url http://my.package.repo/simple/ SomePackage # pypi は検索しない
$ pip install --extra-index-url http://my.package.repo/simple SomePackage # pypi も検索
```

#### proxy 環境下でのインストール
proxy 環境下の場合、

```
$ pip install SomePackage --proxy=username:passwd@proxy.example.com:8080
```

で proxy を通してインストール可能。

#### アップグレード
インストール済みのパッケージをアップグレードする場合は以下のコマンドを実行する。

```
pip install SomePackage -U
```


更新可能なパッケージは

```
pip list -o
```

で確認可能。

virtualenv環境の場合、

```
pip list -l
```
でシステム(仮想環境ではない場所)にインストールされているものを除外して、
仮想環境上にインストールしたパッケージのみ表示できる。

### アンインストール
```
$ pip uninstall SomePackage
```
で指定したパッケージを削除できる。

### freeze
現在インストールしてあるパッケージをテキストファイルに書き出して、後に一括インストールできるようにするためのコマンド。

```
$ pip freeze > requirements.txt
```

で書き出す。インストールする際は、

```
$ pip install -r requirements.txt
```

でインストール可能。

```
$ pip install -r requirements1.txt requirements2.txt
```

のように複数個のファイルも指定可能。

また、freezeで書きだしたファイルをまとめて削除することも可能。

```
$ pip uninstall -r requirements.txt
```

### 依存パッケージを1つのzipにまとめる
書き出し。
```
$ pip freeze > requirements.txt
$ pip bundle -r requirements.txt test.pybundle
```

別の環境でインストール。
```
$ pip install test.pybundle
```

## 参考文献等
[pip 1.5.2 documentation](http://www.pip-installer.org/en/latest/index.html)

[pipの使い方 (2014/1バージョン)](http://tdoc.info/blog/2014/01/15/pip.html), そこはかとなく書くよん。