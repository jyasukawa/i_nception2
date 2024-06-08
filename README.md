vmのdockerバージョンアップ、firefox設定

1.srcsディレクトリに".env"ファイルを作成する。

(内容例)
DOMAIN_NAME=jyasukaw.42.fr

# certificates
CERT_PATH=/etc/nginx/ssl/inception.crt
PRIVKEY_PATH=/etc/nginx/ssl/inception.key
CERT_DETAILS="/C=JP/ST=Tokyo/L=Tokyo/O=42tokyo/OU=42cursus/CN=jyasukaw.42.fr"

# MYSQL SETUP
MYSQL_ROOT_PASSWORD=password
MYSQL_USER=jyasukaw
MYSQL_USER_PASSWORD=password

MYSQL_DATABASE_NAME=wordpress_db
MYSQL_HOST_NAME=mariadb # ここで3306につなげてる

# wordpress setup
WP_TITLE=inception

WP_ADMIN=jyasukaw
WP_ADMINPASS=password
WP_ADMINMAIL=jyasukaw@sample.com

WP_USER=tanaka
WP_USERPASS=password
WP_USERMAIL=tanaka@sample.com

# Makefile
MARIADB_VOLUME_PATH=/home/jyasukaw/data/mariadb
WORDPRESS_VOLUME_PATH=/home/jyasukaw/data/wordpress
COMPOSE_YML_PATH=./srcs/docker-compose.yml




2.ホストの追加
sudo cp /etc/hosts /etc/hosts.backup
sudo chmod 777 /etc/hosts
sudo echo "127.0.0.1 jyasukaw.42.fr" >> /etc/hosts
sudo chmod 644  /etc/hosts
-ホストの修正-
sudo chmod 777 /etc/hosts.backup
sudo cp /etc/hosts.backup /etc/hosts
sudo rm /etc/hosts.backup



wordpressへのアクセス
https://jyasukaw.42.fr
/wp-admin/
/wp-login.php/
/index.php


mariadbの操作
docker container exec -it mariadb_container mysql -u root -p
パスワードを求められるが、そのままenter→エラー
正しいパスワード→SELECT User FROM mysql.user;（rootしか使えないコマンド）
docker container exec -it mariadb_container mysql -u jyasukaw -p
USE wordpress_db
SHOW TABLES;