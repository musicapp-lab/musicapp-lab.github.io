# Pitch Patrol GitHub Pages Site

このフォルダは、音程ポリス (Pitch Patrol) の公開 developer / marketing site を GitHub Pages へ移すための静的ファイル一式です。アプリ本体のソースコードは含めず、App Store Connect と AdMob 向けの公開ページだけを切り出す前提です。

## 目的

- Marketing URL を GitHub Pages へ移す
- Privacy Policy URL と Support URL を GitHub Pages へ移す
- root の `app-ads.txt` を公開できるようにする
- アプリ本体 repo を公開せず、developer page 専用 repo に分離する

## 重要な前提

AdMob の crawler は developer website の `hostname` を見て `https://<hostname>/app-ads.txt` を取りに行きます。

そのため、GitHub Pages は次のどちらかで使うのが安全です。

1. GitHub user site: `<your-github-username>.github.io`
2. 独自ドメイン: `https://your-domain.example`

`pitch-patrol-site` のような project site だけを単独で作ると、`app-ads.txt` を repo の path 配下にしか置けず、root 配信の条件と噛み合いません。

## 推奨の移行形

### いちばん簡単

1. GitHub で public repo `<your-github-username>.github.io` を作る
2. このフォルダの中身を repo root へ入れる
3. `app-ads.txt` の publisher ID を AdMob の personalized snippet に置き換える
4. GitHub Pages を `main` branch / root で公開する
5. 公開 URL を確認する

想定 URL:

- Marketing URL: `https://<your-github-username>.github.io/`
- Support URL: `https://<your-github-username>.github.io/support.html`
- FAQ URL: `https://<your-github-username>.github.io/faq.html`
- Privacy URL: `https://<your-github-username>.github.io/privacy.html`
- app-ads.txt: `https://<your-github-username>.github.io/app-ads.txt`

### 既に user site がある場合

既存の `<your-github-username>.github.io` repo にこの app のページを追加してもよいです。

- `app-ads.txt` は repo root に置く
- app 用 HTML は `pitch-patrol/` のような subdirectory にまとめる
- App Store Connect の URL は `https://<your-github-username>.github.io/pitch-patrol/...` を使う

このフォルダの HTML は相対リンクなので、まとめて subdirectory へ移しても動かしやすい構成です。

## GitHub Pages 公開手順

1. GitHub で public repo を作る
2. このフォルダの中身を commit する
3. repo の `Settings -> Pages` を開く
4. `Build and deployment` で `Deploy from a branch` を選ぶ
5. branch を `main`、folder を `/ (root)` にする
6. 数分待って公開 URL を確認する

`.nojekyll` を入れてあるので、余計な Jekyll 変換を避けられます。

## 公開前に置き換えるもの

- `app-ads.txt` の `pub-REPLACE_WITH_ADMOB_PUBLISHER_ID`
- 必要ならトップページ本文の App Store 公開表現
- 必要なら連絡先や著作権表記

## App Store Connect に入れる候補

- Marketing URL: root
- Privacy Policy URL: `privacy.html`
- Support URL: `support.html` か `faq.html`

## 確認項目

1. root の `app-ads.txt` がブラウザで直接開ける
2. `support.html` と `privacy.html` が未ログイン状態で開ける
3. App Store Connect の Marketing / Support / Privacy URL が全部 200 で返る
4. AdMob 側で `app-ads.txt` status が検出される
