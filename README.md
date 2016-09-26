
# Sackerel

## > A integration tool of Mackerel and SakuraCloud

[Sackerel](https://github.com/sacloud/sackerel)用Dockerイメージ

![logo.png](logo.png "logo.png")


## `Dockerfile` links

- [`0.0.1`,`latest`(Dockerfile)](https://github.com/sacloud/sackerel-docker/tree/master/0.0.1/)

## 使い方(dockerコマンドを直接使う場合)

### 起動コマンド書式

```bash
docker run -d sacloud/sackerel [オプション]
```

### 実行例

必須パラメータ(さくらのクラウド[トークン、シークレット]、MackerelのAPIキー)をオプション指定しています。

```bash
docker run -d sacloud/sackerel  --token "Your Token" --secret "Your Secret" --apikey "Your APIKey"
```

パラメータは環境変数で渡すことも可能です。

```bash
docker run -d sacloud/sackerel -e SAKURACLOUD_ACCESS_TOKEN -e SAKURACLOUD_ACCESS_TOKEN_SECRET -e MACKEREL_APIKEY
```


指定できるパラメータについては[Options/オプションについて](https://github.com/sacloud/sackerel/raw/master/docs/Options.md)を参照してください。

### ヘルスチェック用Webサーバーを利用する場合

デフォルトで39700ポートでヘルスチェック用Webサーバーが起動します。
dockerコマンドから利用する場合は`-p`オプションを指定してください。

```bash
# コンテナの39700ポートをホストの39700ポートへ設定
docker run -d -p 39700:39700 sacloud/sackerel  --token "Your Token" --secret "Your Secret" --apikey "Your APIKey"
```



## 使い方(docker-composeを使う場合)

#### 1) 以下コマンドで`docker-compose.yml`と環境変数設定ファイルのひな形をダウンロードします。

```bash
curl -L https://github.com/sacloud/sackerel-docker/raw/master/docker-compose.yml > docker-compose.yml
curl -L https://github.com/sacloud/sackerel-docker/raw/master/env-sample > .env
```

#### 2) 環境変数設定ファイルを編集します。

このファイルで環境変数を設定しておくと`sackerel`コマンド実行時に
必要なオプションを省略できます。

```bash
vi .env
```

#### 3) docker-composeコマンドの実行

以下コマンドで`sackerel`を起動します。

#### 実行例

```bash
docker-compose up -d sackerel
```

### ヘルスチェック用Webサーバーを利用する場合

docker-composeファイルにてポートの設定を追記してください。

#### 記述例

```
sackerel:
  image: sacloud/sackerel
  env_file: .env
  ports:
    - "39700:39700"
```
