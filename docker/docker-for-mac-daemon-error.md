# Docker for Mac 利用時にエラー発生

Docker for Mac を brew cask で導入し、いざ `docker run` しようとすると次のようなエラーが発生した。

```
docker: Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Docker for Mac のインストールは正常にできているようで `docker` コマンドや `docker-compose` コマンドを単発で実行する分には問題がない。調べてみると、Docker for Mac 導入以前の Docker 設定が悪影響を及ぼしていることがわかった。

[このフォーラム](https://forums.docker.com/t/docker-for-mac-cannot-connect-to-the-docker-daemon-is-the-docker-daemon-running-on-this-host/9182) を参考に `DOCKER_HOST` 環境変数を削除することで問題が解決した。
