# Express&TypeScript 環境構築

## プロジェクト作成

```
npm init -y
```

## express インストール

```
npm i express
```

## 開発環境に必要なパッケージをインストール

- nodemon：開発サーバーを自動で再起動してくれるライブラリ
- @types/node：node の型定義ファイル
- @types/express：express の型定義ファイル

```
npm i -D typescript
npm i -D ts-node
npm i -D nodemon
npm i -D @types/node
npm i -D @types/express
```

## TypeScript 初期化

```
npx tsc --init
```

## tsconfig.json の設定

rootDir のディレクトリをコンパイル対象とし、outDir のディレクトリを node 実行ファイルとする

```
{
  ...
  "outDir": "./dist",
  "rootDir": "./src",
  ...
}
```

## src ディレクトリ作成

このディレクトリに TypeScript のソースコードを格納

```
mkdir src
```

## app.ts 作成

src ディレクトリ配下に app.ts ファイルを作成する

```
touch src/app.ts
```

## app.ts ファイルに記述

```
import express from 'express';

const app = express();

const PORT = 3000;
app.listen(PORT, () => console.log(`server listen http://localhost:${PORT}`));
```

## 実行スクリプト追加

package.json に追加

- dev：開発サーバー起動
- build：本番用コンパイル
- start：本番サーバー起動

```
"scripts": {
  ...
  "dev": "nodemon src/app.ts",
  "build": "tsc",
  "start": "node dist/app.js",
  ...
}
```
