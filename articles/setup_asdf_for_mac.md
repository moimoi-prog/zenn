---
title: "プログラミング言語のバージョンをasdfで一括管理するようにした話"
emoji: "🗒"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: true
---

asdf というバージョン管理ツールを導入したので紹介します。

## 環境

OS ... macOS Monterey

## asdf とは

プログラミング言語や各種ツールのバージョン管理を行うことができる CLI ツールです。

特徴として

1. 言語やツールのバージョンを、ひとつのツールで管理できること
2. プロジェクトで使用する言語のバージョンを、ひとつの構成ファイルで指定できること

などが挙げられます。

https://asdf-vm.com/

## 導入前の課題

1. Flutter は fvm、Python は pyenv、Node.js は nvm etc ... というように、それぞれの言語で別々のツールを使用していたため、管理が煩雑になりがちな点
2. プロジェクトの切り替えと環境の切り替えが連動していないため、いちいち環境を切り替える必要があり面倒な点
3. コマンドを実行する前に fvm をつけるのがだるい点(flutter のみ)

asdf を導入すればこれらの課題を解決できるため導入しました。

## 導入方法

今回は Flutter を例にして解説していきます。

**asdf のインストール**

※homebrew がインストールされている前提

```bash
# asdfのインストール
$ brew install asdf

# asdfコマンドを使用可能にする(シェルによって異なります)
$ echo -e "\n. $(brew --prefix asdf)/asdf.sh" >> ${ZDOTDIR:-~}/.zshrc
```

**asdf で flutter で使用可能にする**

```bash
# 使用可能なpluginを確認
$ asdf plugin list all

# 検索したい場合は
$ asdf plugin list all | grep [search_word]

# 使用したいpluginをインストール(今回はFlutter)
$ asdf plugin add flutter

# インストール済みのプラグインのリストを確認する
$ asdf plugin list

# asdfで使用可能なflutterバージョンを確認
$ asdf list all flutter

# 使用したいバージョンをインストール
$ asdf install flutter 3.0.3-stable

# インストール済みのFlutterバージョンを確認
$ asdf list flutter
```

**プロジェクトで使用する Flutter バージョンを指定**

```bash
# プロジェクトのルートディレクトリに移動
$ cd 'path_to project_root_directory'

# Flutterバージョンを指定(変更する場合も同じ)
$ asdf local flutter 3.0.3-stable

# ここで.tool-versionsが作成される

# Android Studio
# > Preference
# > Languages & Frameworks
# > Flutter SDK Path
# にasdfでインストールしたFlutterのSDKパスを指定

# 指定したバージョンになっているか確認
$ flutter --version
```

最後にビルドして問題なければ完了です。
