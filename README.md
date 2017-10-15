# swagger-eco

Swaggerのエコシステムを試す用のリポジトリ

## 注意

- specification/swagger.yamlはただのサンプルです
- docs配下はspecification/swagger.yamlを元にhtml-convertorで生成したファイルです

## docker-composeコマンド

```
ビルド
$ docker-compose build
起動
$ docker-compose up -d
停止
$ docker-compose down -v
状態確認
$ docker-compose ps
```

起動後に[http://localhost](http://localhost)にアクセスすると、簡単なトップ画面が表示される。


## codegen-cli

単体で実行する場合は以下のような感じで叩く。

```
$ docker run --rm -v ${PWD}/specification:/codegen-cli/specification swaggerapi/swagger-codegen-cli generate -i /codegen-cli/specification/swagger.yaml -l ruby -o /codegen-cli/specification/ruby
```

## html-convertor

ホストOSからコンテナにログイン
```
docker exec -it swaggereco_html-convertor_1 sh
```

コンテナでHTML生成するまでのコマンド

```
cd /html-convertor
java -jar swagger2markup-cli.jar convert -i specification/swagger.yaml -f docs/index
asciidoctor -a toc=left -D docs docs/index.adoc
```
