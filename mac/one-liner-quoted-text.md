# 一瞬で複数行テキストを引用形式に変換

macOS ではターミナル上でクリップボードを扱う `pbcopy` と `pbpaste` がある。これをうまく活用することで、単純な複数行テキストを引用形式 (`>` を先頭に付加する引用形式) に変換することができる。

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Donec iaculis purus commodo tortor finibus fermentum.
Integer sit amet magna lacinia elit pellentesque rhoncus nec at nulla.
In eget sapien ut ex condimentum euismod.
Maecenas mattis tellus sit amet massa lacinia lobortis.
```

このような複数行テキストがある場合、これをコピーした後にターミナル上で

```
pbpaste | sed -e "s/^/> /" | pbcopy
```

を実行することで

```
> Lorem ipsum dolor sit amet, consectetur adipiscing elit.
> Donec iaculis purus commodo tortor finibus fermentum.
> Integer sit amet magna lacinia elit pellentesque rhoncus nec at nulla.
> In eget sapien ut ex condimentum euismod.
> Maecenas mattis tellus sit amet massa lacinia lobortis.
```

のように全ての行の先頭に `>` を追加することができる。実行していることは非常にシンプルで、次の 3 つのコマンドをパイプでつなぎワンライナーとしている。

- `pbpaste`: クリップボードの内容をターミナルに送り込む
- `sed -e "s/^/> /"`: 行頭に `>` を追加する
- `pbcopy`: sed の結果をクリップボードに戻す

Redmine のコメントで任意の箇所を引用したい場合や、Slack で引用形式にしたい場合など、多くのシーンで活用できる。
