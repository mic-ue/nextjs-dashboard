# データベースの初期データ投入（シーディング）手順まとめ
- 目的: Vercel Postgres (Neon) データベースにテーブルを作成し、初期データを投入する。
- 公式の手順ではわかりにくかったためメモ
  - [vercel公式の手順](https://vercel.com/mics-projects-1ea8090b/nextjs-dashboard/integrations/neon/icfg_LYIyupUnKrdS56SFbCiusIWf/resources/storage/store_K06unKAZMT7iDgkf/guides)
  - [Nuxt.js公式の手順](https://nextjs.org/learn/dashboard-app/setting-up-your-database#seed-your-database)

- 前提: Vercel Postgres (Neon)の用意は済んでいるものとする。

## 1. Vercel CLIでプロジェクトをリンクする
```
    pnpm install @neondatabase/serverless
    pnpm install -g vercel
    pnpm vercel link
```
質問には基本的に Y (Yes) や自分のアカウント、プロジェクト名を選択して進める。

## 2. 環境変数を取得する
```
    npx vercel env pull .env.development.local
```
.env ファイルが作成され、データベース接続情報 (POSTGRES_URL 等) が自動設定される。

## 3. 開発サーバーを起動する
```
    pnpm run dev
```

## 4. シーディングを実行する
- ブラウザで http://localhost:3000/seed にアクセスする。
- 画面に {"message": "Database seeded successfully"} と表示されれば成功。

## 仕組み:
app/seed/route.ts ファイルが実行され、コード内のSQL（CREATE TABLE, INSERT）がデータベースに対して発行される。