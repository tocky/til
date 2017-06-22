# Mac で Crystal を使おうとしたときのエラー解決

macOS 10.12.5 の環境上で [des](https://github.com/at-grandpa/des) というツールを使おうとした際にライブラリが不足していることからエラーが発生した。なお、このツール自体が Crystal で作られているため、Crystal 実行環境としてのセットアップが必要であるようだ。

```
dyld: Library not loaded: /usr/local/opt/libyaml/lib/libyaml-0.2.dylib
  Referenced from: /usr/local/bin/des
  Reason: image not found

dyld: Library not loaded: /usr/local/opt/bdw-gc/lib/libgc.1.dylib
  Referenced from: /usr/local/bin/des
  Reason: image not found

dyld: Library not loaded: /usr/local/opt/libevent/lib/libevent-2.1.6.dylib
  Referenced from: /usr/local/bin/des
  Reason: image not found
```

調べてみると、いずれも Homebrew によってインストールできることがわかった。

```
brew install libyaml bdw-gc libevent
```
