# 割り勘精算計算機

割り勘の精算を **最小送金回数** で計算するPWA対応Webアプリです。

## 機能

- メンバー追加・削除
- 支払い入力・編集・削除
- Greedy法による最小送金プラン計算
- 端数切り捨て（全員均等負担）
- 結果コピー / LINE シェア / Discord Webhook 送信
- PayPay リンク自動付与
- localStorage による入力内容の自動保存・復元
- ダークモード対応
- PWA（オフライン動作・ホーム画面追加）

## ファイル構成

```
/
├── index.html          # メインアプリ
├── manifest.json       # PWA マニフェスト
├── service-worker.js   # オフラインキャッシュ
├── icons/
│   ├── icon-192.svg    # PWA アイコン 192×192
│   └── icon-512.svg    # PWA アイコン 512×512
└── README.md
```

## Discord Webhook URL の設定

`index.html` 冒頭の定数を書き換えてください。

```js
const DEFAULT_DISCORD_WEBHOOK_URL = 'https://discord.com/api/webhooks/...';
```

アプリ上の「💾 保存」ボタンを押すと localStorage に記録され、
次回以降はそのURLが自動補完されます。

## GitHub Pages へのデプロイ

### 1. リポジトリを作成

```bash
git init
git add .
git commit -m "initial commit"
gh repo create <repo-name> --public --source=. --push
```

### 2. GitHub Pages を有効化

1. リポジトリの **Settings** → **Pages** を開く
2. **Source** を `Deploy from a branch` に設定
3. **Branch** を `main` / `(root)` に設定して Save
4. 数分後に `https://<username>.github.io/<repo-name>/` で公開される

### 3. 更新時のデプロイ

```bash
git add .
git commit -m "update"
git push
```

Push するたびに GitHub Actions が自動デプロイします。

### Service Worker のキャッシュ更新

`service-worker.js` の `CACHE_NAME` のバージョン番号を上げてください。

```js
const CACHE_NAME = 'warikan-v2'; // v1 → v2 に変更
```

古いキャッシュが自動削除され、ユーザーが次回アクセス時に新版を取得します。

## ローカルで確認する

ファイルをそのままブラウザで開くと Service Worker が動作しません。
ローカルサーバーを立てて確認してください。

```bash
# Python 3
python -m http.server 8080

# Node.js (npx)
npx serve .
```

ブラウザで `http://localhost:8080` を開いてください。
