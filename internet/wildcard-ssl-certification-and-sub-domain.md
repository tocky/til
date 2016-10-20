# ワイルドカード SSL 証明書とサブドメイン

SSL 証明書にはドメインに完全マッチする形のものと、任意のサブドメインに対して使用できるワイルドカードのものとがある。ワイルドカードの証明書の場合には `*.example.com` のように、任意のサブドメインを利用できるようになっているわけだが、このサブドメインが多階層である場合には注意が必要。

例えば `*.example.com` という証明書を発行済である場合

* `www.example.com`
* `sub.example.com`

といった 1 階層のサブドメインは証明書を適用可能である。しかし、次に示すような多階層の場合には、証明書発行機関や証明書の種類によって、使用できるケースとできないケースとがある。

* `xxx.www.example.com`
* `foo.bar.buzz.example.com`

---

## 参考

* [ワイルドカード証明書｜DigiCert SSL/TLS 証明書｜DigiCert](https://www.digicert.ne.jp/ssl/wildcard-ssl-certificates.html)
* [ワイルドカード証明書について « ValueSSLサポート](http://faq.valuessl.net/?cat=55#1192)
