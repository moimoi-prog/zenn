---
title: "何も考えずに継承を使うべきではない理由についてまとめてみた"
emoji: "🐥"
type: "tech"
topics: []
published: false
---

こんにちは、おみです。
オブジェクト指向の学習を進めていくと、継承は使うべきではないという記事を見かけることがよくあります。
私自身業務で継承を乱用したプログラムを作成した結果大失敗したことがあるので、それ以来むやみに使わない方がいいものだとなんとなく感じていましたが、今回は

- なぜ継承を乱用すべきではないか
- 継承を使っていいシチュエーションはなにか
- 継承がだめなら代わりに何を使うべきか

の3点について、まとめてみたので解説していきます。

※記事中で使用されているコードは、dartで記述されています。

### 継承とは...
- オブジェクト指向の3大要素の1つ。
- 親となるクラスAの変数やメソッドを引き継いだ子クラスBを作成することを指します。
- この時、クラスAとクラスBには「継承関係」があると言います。

以降の内容では、クラスAをスーパークラス、クラスBをサブクラスとして記述していきます。

### 継承を使いたくなるシチュエーション
継承を使いたくなるシチュエーションとして、例えば以下のようなパターンが挙げられるかと思います。
1. 共通の処理を記述したスーパークラスを用意し、それぞれのサブクラスで使いたい場合(機能の共有)


2. スーパークラスを継承したそれぞれのサブクラスのインスタンスを、まとめて管理したい場合(クラスの抽象化)

継承について解説している記事の多くは、親クラスの「機能」を引き継いだ子クラスを作成するという胸の解説を行なっているため、≒機能を使い回すものだと認識されてしまっていそう。

### 乱用することによる問題点
1. 共通の処理をスーパークラスに持たせすぎてしまった結果、修正の影響が広範囲に及び、怖くて修正することができないクラス(所謂神様クラス)が出来上がってしまう。
2. has-a関係で継承を使った場合

多くのプログラム言語は多重継承ができないため、スーパークラスに多くの機能を持たせがちになってしまうということはありそう。

### 継承を使っていいシチュエーション

1. リスコフの置換原則に満たしている場合
2. 今後変更されることがないと言い切れる場合

であれば、
is-a関係とhas-a関係とは
is-a関係  ... サブクラスはスーパークラスの一種であるという関係
has-a関係 ... サブクラスはスーパークラスを含んでいるという関係

ただし、システム中で扱うデータを扱うクラスは機能の追加や変更によりis-a関係が崩れることがあるので、そういったクラスには継承を使うべきではないと考えます。

例えば...会社の物を管理するシステムの場合

ここに実例を記述する


このように、こういったデータクラスは仕様変更によりリスコフの法則を満たさなくなる可能性があるので、継承を使うべきではない


何を使用するか
1. 移譲(別のオブジェクトに委ねる)
2. インターフェース(仕様の継承)
3. mixin(機能の拡張)