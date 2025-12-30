# 🚀 Vercelデプロイ手順（GitHubリポジトリから）

リポジトリ: https://github.com/NikoToRA/NanobananaDMAT

## 📋 前提条件

✅ GitHubリポジトリにプッシュ済み（完了済み！）  
✅ Vercelアカウントが必要

## 🎯 方法1: Vercelダッシュボードから（最も簡単・推奨）

### ステップ1: Vercelにログイン

1. [Vercel](https://vercel.com)にアクセス
2. 「Sign Up」または「Log In」をクリック
3. **「Continue with GitHub」を選択**（GitHubアカウントでログイン）

### ステップ2: プロジェクトをインポート

1. ダッシュボードで **「Add New...」→ 「Project」** をクリック
2. 「Import Git Repository」で **「NanobananaDMAT」** を選択
   - もしくは検索バーで `NikoToRA/NanobananaDMAT` を検索
3. **「Import」** をクリック

### ステップ3: プロジェクト設定

Vercelが自動検出しますが、確認してください：

- **Framework Preset**: Other
- **Root Directory**: `./`（そのまま）
- **Build Command**: （空欄でOK）
- **Output Directory**: （空欄でOK）
- **Install Command**: `npm install`

**そのまま「Deploy」をクリック！**

### ステップ4: 環境変数を設定

⚠️ **デプロイが完了する前に設定してもOKですが、設定後は再デプロイが必要です**

1. プロジェクトページで **「Settings」** タブをクリック
2. 左メニューから **「Environment Variables」** を選択
3. 以下の環境変数を追加：

#### Gemini APIを使う場合：
```
Name: GEMINI_API_KEY
Value: あなたのGemini APIキー
Environment: Production, Preview, Development（すべてチェック）
```

#### Replicate APIを使う場合（推奨）：
```
Name: REPLICATE_API_TOKEN
Value: あなたのReplicate APIトークン
Environment: Production, Preview, Development（すべてチェック）
```

4. **「Save」** をクリック

### ステップ5: 再デプロイ（環境変数を設定した場合）

1. プロジェクトページの上部で **「Deployments」** タブをクリック
2. 最新のデプロイメントの右側の **「⋯」** メニューをクリック
3. **「Redeploy」** を選択
4. 「Use existing Build Cache」のチェックを外す（推奨）
5. **「Redeploy」** をクリック

### ステップ6: デプロイ完了！

デプロイが完了すると、URLが表示されます：

```
✅ Production: https://nanobananadmat.vercel.app
```

このURLを参加者に共有するだけ！

---

## 🎯 方法2: Vercel CLIから（開発者向け）

### ステップ1: Vercel CLIをインストール

```bash
npm i -g vercel
```

### ステップ2: ログイン

```bash
vercel login
```

ブラウザが開くので、GitHubアカウントでログイン

### ステップ3: プロジェクトにリンク

```bash
cd "/Users/suguruhirayama/Desktop/DMAT研修"
vercel link
```

**質問に答える：**
- Set up and deploy? → `Y`
- Which scope? → 自分のアカウントを選択
- Link to existing project? → `Y`
- What's the name of your existing project? → `nanobananadmat` など
- In which directory is your code located? → `./`

### ステップ4: 環境変数を設定

```bash
vercel env add GEMINI_API_KEY
# または
vercel env add REPLICATE_API_TOKEN
```

プロンプトで：
- Value: あなたのAPIキーを入力
- Environment: `Production, Preview, Development`（すべて選択）

### ステップ5: デプロイ

```bash
vercel --prod
```

---

## ✅ デプロイ後の確認

1. 表示されたURLにアクセス
2. 画像生成が動作するか確認
3. エラーが出る場合は、環境変数が正しく設定されているか確認

## 🔄 コードを更新した場合

GitHubにプッシュすると、自動的にVercelでも再デプロイされます：

```bash
git add .
git commit -m "更新内容"
git push
```

Vercelが自動的にデプロイを開始します！

## 📝 カスタムドメイン

デフォルトのURLは `https://nanobananadmat.vercel.app` のようになりますが、
カスタムドメインも設定可能です（研修会用には不要）。

## 🗑️ 研修会後の削除

研修会が終わったら、プロジェクトを削除できます：

1. Vercelダッシュボードでプロジェクトを開く
2. **「Settings」** → 一番下の **「Delete Project」**
3. 確認して削除

無料プランなので、削除しなくても問題ありません。

---

## 🆘 トラブルシューティング

### 環境変数が反映されない

→ 環境変数を設定した後、必ず **再デプロイ** してください。

### デプロイが失敗する

→ 「Deployments」タブでログを確認してください。通常は環境変数が設定されていない場合に失敗します。

### APIキーを変更したい

→ 「Settings」→ 「Environment Variables」で既存の変数を編集し、再デプロイしてください。

