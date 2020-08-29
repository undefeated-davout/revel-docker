# 使い方

## Dockerコマンド

```
$ docker-compose build
$ docker-compose up -d
$ docker exec -it revel-docker.web /bin/bash
```

## revel実行コマンド

```
# webコンテナへログイン
$ docker exec -it revel-docker.web /bin/bash

# /go/src/ 直下にて下記コマンド実行
$ revel run code/
```

## デバッグコマンド

```
$ revel run code/
# 一旦[Ctrl + C]でrevel停止
$ dlv debug --headless --log code/app/tmp/main.go --listen 0.0.0.0:2345 --api-version=2 --accept-multiclient -- -port=9000 -importPath=code -runMode=dev
```

## ブラウザで確認するには
ブラウザで下記アドレスに接続する

### Mac

- http://localhost:9010/

## Docker停止コマンド

```
$ docker-compose down
```


## 2回目以降の起動

```
$ docker-compose up -d
$ docker exec -it revel-docker.web /bin/bash
$ revel run code/
```
