# 売上管理ダッシュボード

複数端末でデータ同期可能な売上管理ダッシュボードです。

## 🚀 機能

- ✅ **売上・案件管理**: クライアント別、事業別の売上管理
- ✅ **KPI表示**: 売上目標達成率、粗利率、入金状況などを可視化
- ✅ **グラフ表示**: 月別売上推移、事業別構成比
- ✅ **自動保存**: LocalStorageに自動保存
- ☁️ **クラウド同期**: Firebase使用で複数端末間でリアルタイム同期（設定必要）
- 📱 **レスポンシブ**: スマホ・タブレット・PCに対応
- 🎨 **テーマ切替**: ライト/ダーク/システム自動

## 📦 デプロイ

現在Vercelでホスティング中:
- URL: https://sales-management-sheet.vercel.app

## ☁️ Firebase同期の設定（オプション）

複数端末でデータを同期したい場合は、以下の手順でFirebaseを設定してください。

### 1. Firebaseプロジェクトを作成

1. [Firebase Console](https://console.firebase.google.com/) にアクセス
2. 「プロジェクトを追加」をクリック
3. プロジェクト名を入力（例: `sales-management-sheet`）
4. Google Analyticsは不要（スキップ可）
5. 「プロジェクトを作成」をクリック

### 2. Webアプリを追加

1. プロジェクトダッシュボードで **`</>`（Web）** アイコンをクリック
2. アプリのニックネームを入力（例: `売上管理アプリ`）
3. Firebase Hostingは不要（チェック不要）
4. 「アプリを登録」をクリック
5. **設定情報（firebaseConfig）が表示されます** - コピーしておく

### 3. Firestoreデータベースを有効化

1. 左メニューから **「Firestore Database」** を選択
2. 「データベースの作成」をクリック
3. **「テストモードで開始」** を選択
4. ロケーション: `asia-northeast1`（東京）を推奨
5. 「有効にする」をクリック

### 4. セキュリティルールを設定（推奨）

Firestoreの「ルール」タブで以下を設定:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /sales/{document} {
      // 全員が読み書き可能（プライベート利用の場合）
      allow read, write: if true;

      // 認証ユーザーのみ（より安全）
      // allow read, write: if request.auth != null;
    }
  }
}
```

### 5. アプリに設定を適用

`index.html` の以下の部分を編集:

```javascript
// 1. Firebase設定情報を入力
const FIREBASE_CONFIG = {
  apiKey: "YOUR_API_KEY_HERE",              // ← コピーした値に置き換え
  authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT_ID.appspot.com",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID"
};

// 2. Firebaseを有効化
const FIREBASE_ENABLED = true;  // ← false を true に変更
```

### 6. デプロイ

変更をGitHubにプッシュすると、Vercelが自動的に再デプロイします:

```bash
git add index.html
git commit -m "Enable Firebase sync"
git push origin main
```

## 🔧 ローカル開発

Firebaseなしでローカルストレージのみで使用することもできます（デフォルト設定）。

## 📝 ライセンス

MIT License

## 🙋 サポート

問題や質問がある場合は、GitHubのIssuesで報告してください。
