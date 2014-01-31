---
layout: page
title: "1. Mac + Homebrew 環境で Hello, world!"
date: 2014-01-31 16:29
comments: true
sharing: true
footer: true
---
## Mac homebrew 環境でのインストール方法
必要なものは

(1)Javaの実行環境: JDK 

(2)Leiningen: パッケージ管理兼ビルドツール。読み方は「ライニンゲン」。  
インストールする際にClojure本体も自動的にインストールされる。

### Javaの実行環境のインストール
[公式サイト](http://java.com/ja/)からダウンロード。インストーラーを実行する。

### Leiningen のインストール
    $ brew install leiningen

これで実行環境がインストールされた。

## Hello, world! の出力
REPL (Read-Eval-Print Loop): 対話型実行環境を起動して、画面にHello, world!を出力する。

### REPLの起動方法
    $ lein repl
    user=>

### Hello, world! を出力。
`user=>`となっているところに、

    (println "Hello, world!")

と入力してEnter。

    Hello, world!
    nil

1行目が出力結果。2行目が評価した式の返り値。
