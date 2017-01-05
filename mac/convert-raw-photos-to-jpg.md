# コマンドラインで RAW ファイルを JPEG に変換する方法

Mac には標準で `sips` というコマンドが導入されている。 `sips` は画像処理、画像加工を行うためのコマンドで、RAW から JPEG への変換もサポートしている。

単純にひとつのファイルを変換する場合

```
sips -s format jpeg IMG_1199.CR2 --out IMG_1199.jpg
```

複数ファイルを一括で変換するときにはワンライナーでこのような感じ (出力先は `jpg` ディレクトリを指定)

```
for i in *.CR2; do sips -s format jpeg $i --out "jpg/${i%.*}.jpg"; done
```

## 参考

- [sips(1) Mac OS X Manual Page](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/sips.1.html)
