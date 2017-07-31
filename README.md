# Wordpress Containerの作り方

Docker containerでWordpressを動かす方法について。
Docker Hubより公式のWordpressとMariaDBのコンテナを利用。

MariaDBのコンテナは `docker-entrypoint-initdb.d` 内に置かれた、
`.sql` ファイルを実行するため必要なSQLファイルを `docker-entrypoint-initdb.d` に設定。

Wordpressのコンテンツは `wp-content` に入っているため、
それ以外の部分については公式のWordpressコンテナのものを利用。
（通常Wordpressのデータ移行の際には `wp-config.php` の設定変更も必要だが、
　公式のWordpressコンテナは `wp-config.php` を環境変数から自動生成するため今回は不要）

## 必要なツール

* git
* docker
* docker-compose

## 作り方

- 1. `docker-entrypoint-initdb.d` にダンプされたWordpressのSQLを配置
- 2. `wp-content` の内部 `git pull` や `git checkout`
     などで最新のコードや動かしたいブランチのコードにする
- 3. `docker-compose.yml` 内部のmariadbやwordpressの設定を変更する

## 動かし方

### フロントで起動と停止

* 起動： `docker-compose up`
* 停止： `Ctrl+c`

### バックエンドで起動

* 起動： `docker-compose up -d`
* ログ閲覧： `docker-compose logs [--follow | -f] [wordpress | mariadb]`
* 停止： `docker-compose stop`

### コンテナの削除(コンテナを停止後のみ可能)

`docker-compose rm -f`
