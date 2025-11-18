# Laravel 環境

## リポジトリの準備

### リポジトリの作成

「Use this template」ボタンをクリック

<img width="676" height="98" alt="image" src="https://github.com/user-attachments/assets/50fbee88-c21f-46a4-b2ec-43422d082eac" />

「Repository name」を入力して「Create repository」ボタンをクリックして作成

リポジトリ名は [リポジトリ命名規則](https://github.com/KIR-SHARE-ISSUES/template?tab=readme-ov-file#-%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E5%91%BD%E5%90%8D%E8%A6%8F%E5%89%87) を参照

<img width="667" height="361" alt="image" src="https://github.com/user-attachments/assets/153f3a15-91e4-49c2-88e6-9bd5c9ceb023" />

### リポジトリのクローン

Mac はターミナル、Windows は WSL ターミナルを開いて、ホームディレクトリへ移動

```bash
cd ~
```

クローン

```bash
git clone [url]
```

## 開発環境構築

### 1. クローンしたリポジトリへ移動

```bash
cd [リポジトリ名]
```

### 2. `.env` の作成

`.env.example` をコピーして `.env` ファイルを作成してください。

### 3. docker compose でコンテナ起動

```bash
docker compose up -d
```

### 4. Laravel 環境の構築

以下のコマンドで app コンテナに入って作業します

```bash
docker compose exec app bash
```

composer インストール

```bash
composer install
```

`artisan` コマンドで APP キーを作成

```bash
php artisan key:generate
```

http://localhost:8080 にアクセスして、Laravel の初期画面が表示されれば構築完了です。

以下のコマンドで app コンテナから出ることができます。

```
exit
```

### 5. コンテナの停止・削除コマンド

```bash
docker compose down
```

# フォーマッター（Laravel Pint）の使用

コードに統一感を持たせるため、コードフォーマッター [Laravel Pint](https://laravel.com/docs/11.x/pint) を使用します。<br />
Laravel Pint はすでに Laravel に入っているため、インストールなしで使用できます。<br />

## Laravel Pint の実行

コンテナに入って

```bash
docker compose exec app bash
```

Pint 実行

```bash
./vendor/bin/pint
```

Pint 使い方：https://laravel.com/docs/12.x/pint#running-pint

# 静的解析ツール（Larastan）の使用

また、コードの品質管理のため静的解析ツール [Larastan](https://github.com/larastan/larastan) を導入します。

## Larastan の実行

```bash
./vendor/bin/phpstan analyse --memory-limit=2G
```

詳細：[Laravel プロジェクトに静的解析ツール(Larastan)を導入](https://qiita.com/aosan/items/420e339d4b5941aac048#51-larastan%E3%81%A8%E3%81%AF)

# GitHub Actions を用いた Pint・Larastan の実行について

feature ブランチから develop ブランチへ PR を作成すると、
GitHub Actions により Pint と Larastan が自動的に実行され、ソースコードのチェックが行われます。

もし PR 上で「Some checks were not successful」と表示された場合は、
ローカルで Pint・Larastan を実行してコードを整えたうえで、再度プッシュしてください。
