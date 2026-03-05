# TOKOWAKA 吉祥寺 - 予約システム

TOKOWAKA 吉祥寺パーソナルジムの無料カウンセリング予約システムです。  
**GitHub Pages + Google Apps Script (GAS)** 構成で動作します。

---

## 構成

```
/
├── index.html   ← 予約フォーム（GitHub Pagesで公開）
├── code.gs      ← GASにコピーして使用（GitHubには参照用）
└── README.md
```

---

## セットアップ手順

### 1. GASの設定

1. [Google Apps Script](https://script.google.com) を開く
2. 既存プロジェクトの `code.gs` の内容を本リポジトリの `code.gs` に置き換える
3. **デプロイ** → **新しいデプロイ** → 種類：**ウェブアプリ**
   - 実行者：`自分`
   - アクセス：`全員`
4. デプロイURLをコピー（`https://script.google.com/macros/s/〜/exec` 形式）

### 2. index.html の修正

`index.html` の先頭付近にある `GAS_URL` を書き換える：

```javascript
var GAS_URL = 'https://script.google.com/macros/s/【ここにデプロイURL】/exec';
```

### 3. GitHub Pages の設定

1. GitHubリポジトリの **Settings** → **Pages**
2. Source：`Deploy from a branch` → branch: `main` / `/(root)`
3. 数分後に `https://【ユーザー名】.github.io/【リポジトリ名】/` で公開される

---

## 動作確認

公開URLをスマホ・PCで開き、以下を確認：

- [ ] トレーナー一覧が表示される
- [ ] 日時選択で空き枠が表示される
- [ ] 予約送信後に完了画面が表示される
- [ ] お客様・トレーナーにメールが届く

---

## GASの主要関数

| 関数 | 説明 |
|------|------|
| `doGet` | JSONP APIエンドポイント（GitHub Pagesから呼び出し） |
| `getTrainers` | トレーナー一覧取得 |
| `getAvailableSlots` | 空き枠取得 |
| `makeReservation` | 予約確定・メール送信 |
| `syncAllTrainers` | ミラーカレンダー同期（15分ごと自動実行） |
| `setupTriggers` | トリガー設定（初回のみ実行） |
| `cancelReservation` | 予約キャンセル |

---

## 注意事項

- GASを更新したら**必ず新しいバージョンでデプロイ**し直してください
- デプロイURLが変わった場合は `index.html` の `GAS_URL` も更新してください
- `code.gs` にはカレンダーIDやメールアドレス等の個人情報が含まれます。リポジトリを **Private** にすることを推奨します
