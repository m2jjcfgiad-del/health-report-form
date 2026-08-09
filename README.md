# 体調報告フォーム

ラジオボタン／チェックボックスで選択すると、そのままコピペできる報告文を生成する静的サイト。
`index.html` 1ファイルのみで動作（外部通信なし・入力内容はどこにも送信されません）。

## 設計方針

- **毎回すべて未選択の状態から始まる。** 初期値や前回の選択を残さないのは、体調が悪いときに
  「前回のまま送る」流れが生まれるのを防ぐため。ブラウザの入力復元や「戻る」操作で選択が
  復活した場合も、`pageshow` で強制的にクリアする。
- 全項目が埋まるまでコピーボタンは押せない（未選択のまま報告されるのを防ぐ）。
- 端末に保存されるのは氏名のみ（localStorage）。それ以外は保持しない。

## GitHub Pages での公開手順

新しく作った GitHub アカウントで:

1. リポジトリを新規作成（例: `health-report-form`）。Public にする（Free プランでは Private だと Pages が使えません）。
2. `index.html` をアップロード（Web の "uploading an existing file" でOK）。
3. Settings → Pages → Build and deployment → Source を **Deploy from a branch**、Branch を `main` / `/ (root)` にして Save。
4. 1〜2分待つと `https://<ユーザー名>.github.io/health-report-form/` で公開される。

## ローカルからコマンドで push する場合

このフォルダで:

```
git init
git add .
git commit -m "体調報告フォーム"
git branch -M main
git remote add origin https://github.com/<新しいユーザー名>/health-report-form.git
git push -u origin main
```

※ 既存アカウント（aoirobook）の認証情報が残っていると、そちらで push されてしまうことがあります。
Windows の場合は「資格情報マネージャー」→ Windows 資格情報 → `git:https://github.com` を削除してから
push すると、新しいアカウントで認証し直せます。

## カスタマイズ

`index.html` 冒頭の JavaScript にある以下の配列を書き換えるだけで選択肢を変更できます。

- `CONDITIONS` … ① 体調
- `SYMPTOMS` … ② 自覚症状
- `LEVELS` … ③ 水分 / ④ 食事 / ⑤ 睡眠・休養
- `DEFAULTS` … 初期選択値
