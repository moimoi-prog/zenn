---
title: "Flutter: iOSでSelectableTextで文字を選択するとクラッシュする"
emoji: "📘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ['Flutter', 'iOS', 'Android']
published: false
---
iOsでSelectableTextで文字を表示し、選択しようとしたところエラーが発生しました。

```dart
No CupertinoLocalizations found.
```

#### 対処方法
localizationsDelegatesを指定している箇所に下記を追加するとエラー発生しなくなります。
```dart
GlobalCupertinoLocalizations.delegate,
```

実装例
'''dart
MaterialApp.router(
  localizationsDelegates: const [
    GlobalCupertinoLocalizations.delegate,
  ],
)
'''
