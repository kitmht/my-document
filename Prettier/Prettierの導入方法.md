# Prettier の導入

最低限の設定を行う

## インストール

```
npm i -D prettier
```

## 設定ファイル作成

設定ファイルは json で統一したいため拡張子 json で作成する

```
touch .prettierrc.json
```

## Prettier の設定

設定ファイルに以下の内容を追加する

- singleQuote・・・文字列をシングルクォートで囲む
- trailingComma・・・オブジェクト、配列の末尾にカンマを挿入する

色々設定してもわからなくなるので他の設定はデフォルトのまま

```
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

## 実行コマンドの設定

package.json にコマンドを追加する

基本的には src フォルダ配下のみを対象とする

「--write」でファイルの内容を書き換える
（チェックだけなら「--check」を使用する）

```
"scripts": {
  ...
  "format": "npx prettier --write ./src",
  ...
},
```
