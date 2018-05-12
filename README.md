# PHP＋Composer＋Symfony VScode debug from Docker

PHP＋Composer（＋Symfony）の為に構築したDocker環境です。

ホストOSから、VSCodeでリモートデバッグが可能です。

## Environment

ホストOSは、Macを想定しています。

Docker（docker-compose）と、VSCodeのインストール済みが前提条件です。

## Installation

1. Clone

2. `symfony/xdebug.ini`の`xdebug.remote_host`を、Macのコンピュータ名に置き換え。

3. `build.sh`と`up.sh`を実行してください。

4. 下記のURLで、Webサーバにアクセスできます。
	* http://localhost:8080

## Detail

* docker-composeコマンドのショートカット

	`down.sh`でコンテナの破棄、`stop.sh`でコンテナの停止です。

	`ps.sh`でコンテナの稼働状況を確認できます。

	含まれているShellファイルの殆どは、docker-composeコマンドのショートカットです。

* VSCodeについて

	VSCodeで`symfony/symfony.code-workspace`を開くと、PHPのデバッグ環境になります。

* Shellについて

	```sh
	# コンテナを操作（dockerユーザ）
	docker exec -it --user docker:docker --workdir /home/docker php7_composer_1 sh
	```

## Symfonyについて

* Symfonyプロジェクト作成 （--prefer-dist オプションはエラー）

	```sh
	## Skeleton 
	docker exec --user docker:docker --workdir /home/docker/project/symfony php7_composer_1 composer create-project symfony/website-skeleton skeleton
	```

	```sh
	## Demo
	docker exec --user docker:docker --workdir /home/docker/project/symfony php7_composer_1 composer create-project symfony/symfony-demo demo
	```

* Composer開発サーバインストール

	```sh
	docker exec --user docker:docker --workdir /home/docker/project/symfony/skeleton php7_composer_1 composer require server --dev
	```

* Composer開発サーバ起動

	```sh
	docker exec --user docker:docker --workdir /home/docker/project/symfony/skeleton php7_composer_1 php bin/console server:run 0.0.0.0:8080
	```

## Author
* [**@kght6123**](https://twitter.com/kght6123)

## Contacts

公開内容の詳細に関しては[**@kght6123**](https://twitter.com/kght6123)まで、お気軽にお問い合わせ下さい。

For more details on the public content please feel free to contact us at [**@kght6123**](https://twitter.com/kght6123).

## Copyright
**```Copyright (c) 2018 Hirotaka Koga```**
