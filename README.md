# 概要

Laravel を動かす Docker 開発環境

# 環境

- nginx
- PHP 7.4
- MySQL 8
- Supervisor
- cron
- node

# how to use

## 初期設定

`src`内に Laravel プロジェクトを配置する

`.env.example`(docker-compose と同一階層のもの)をコピーし`.env`にする。

ポートや DB などをお好みの形にする

## 立ち上げ

初回

```
docker-compose up -d --build
```

二回目

```
docker-compose up -d
```

## コンテナに入る

app(php cron supervisor)コンテナ

```
docker-compose exec app bash
```

nginx コンテナ

```
docker-compose exec nginx bash
```

db コンテナ

```
docker-compose exec db bash
```

## artisan コマンド

Host から叩く場合

```
docker-compose exec app php artisan migrate
```

ゲストから叩く場合

```
docker-compose exec app bash
php artisan migrate
```

## SQL クライアントから DB に接続

`.env`(docker-compose と同一階層のもの)をで指定している、ポートやユーザ名、パスを用い、localhost に接続
