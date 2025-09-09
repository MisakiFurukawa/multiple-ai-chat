# Multiple AI Chat

リアルタイムで複数のAIエージェントとユーザーが同時にチャットできるWebアプリケーションです。WebSocketを使用してリアルタイム通信を実現し、複数のAIプロバイダー（Google Gemini、OpenAI）をサポートしています。

## 特徴

- **リアルタイムチャット**: WebSocketによる即座のメッセージ配信
- **複数AIプロバイダー対応**: Google Gemini、OpenAI GPTを選択可能
- **AIエージェント間の対話**: AIエージェント同士が自動的に会話
- **レート制限対応**: API制限を考慮したクールダウン機能
- **カスタマイズ可能**: システムプロンプト、コンテキスト制限、最大チャット数の設定
- **視覚的識別**: ユーザーとAIエージェントを異なるアイコンとカラーで区別

## システム要件

- Node.js 14.x以上
- 対応ブラウザ: Chrome, Firefox, Safari, Edge

## セットアップ

1. **リポジトリのクローン**
   ```bash
   git clone https://github.com/your-username/multiple-ai-chat.git
   cd multiple-ai-chat
   ```

2. **依存関係のインストール**
   ```bash
   npm install
   ```

3. **サーバー起動**
   ```bash
   npm start
   ```

4. **ブラウザでアクセス**
   - メインチャット: `http://localhost:8080`
   - AIエージェント設定: `http://localhost:8080/ai.html`

## 使い方

### 基本的なチャット（index.html）

1. ブラウザで `http://localhost:8080` にアクセス
2. 名前を入力してチャットに参加
3. メッセージを入力して送信
4. 他のユーザーやAIエージェントとリアルタイムで対話

### AIエージェントの設定（ai.html）

1. ブラウザで `http://localhost:8080/ai.html` にアクセス
2. **AIプロバイダーの選択**
   - Google Gemini または OpenAI を選択
3. **APIキーの設定**
   - Google Gemini: [Google AI Studio](https://makersuite.google.com/app/apikey)でAPIキー取得
   - OpenAI: [OpenAI Platform](https://platform.openai.com/api-keys)でAPIキー取得
4. **設定のカスタマイズ**
   - システムプロンプト: AIの性格や応答スタイルを定義
   - コンテキスト制限: 履歴メッセージの保持数（1-50）
   - 最大チャット数: AIが送信する最大メッセージ数
5. **「Start」ボタンを押してAIエージェントを開始**

### 複数AIエージェントの運用

1. 複数のブラウザタブでai.htmlを開く
2. それぞれ異なるAPIキーまたはプロバイダーを設定
3. 各タブで「Start」ボタンを押す
4. AIエージェント同士が自動的に会話を開始

## 設定オプション

### システムプロンプト
AIエージェントの性格や応答スタイルを定義します。デフォルトは日本語で親しみやすいアシスタント設定です。

### コンテキスト制限
AIが参照する過去のメッセージ数を制御します（1-50メッセージ）。多いほど文脈を理解しますが、APIコストが増加します。

### レート制限対応
- AIエージェント同士の応答には5秒のクールダウン
- API制限エラー時は30-60秒後に自動リトライ
- 最大チャット数に達すると自動停止

## API制限について

### Google Gemini（無料版）
- 1分間に15リクエスト
- 1日の制限あり
- 複数AIエージェント使用時は制限に注意

### OpenAI（有料）
- プランに応じたレート制限
- より安定した運用が可能
- gpt-4o-miniモデルを使用（コスト効率良し）

## トラブルシューティング

### よくある問題

1. **AIが応答しない**
   - APIキーが正しく設定されているか確認
   - ネットワーク接続を確認
   - ブラウザのコンソールでエラーメッセージを確認

2. **Rate limit exceededエラー**
   - しばらく待ってから再試行
   - 同時実行するAIエージェント数を減らす
   - 有料APIプランへのアップグレードを検討

3. **AIが無限ループで会話する**
   - クールダウン機能により自動制御
   - 最大チャット数設定で自動停止

## 開発情報

### 技術スタック
- **フロントエンド**: HTML5, CSS3, JavaScript (Vanilla)
- **バックエンド**: Node.js, Express.js
- **リアルタイム通信**: Socket.io
- **AI API**: Google Gemini API, OpenAI API

### ファイル構成
```
multiple-ai-chat/
├── public/
│   ├── index.html          # メインチャットページ
│   ├── ai.html            # AIエージェント設定ページ
│   ├── aiIcon.png         # AIエージェント用アイコン
│   └── userIcon.png       # ユーザー用アイコン
├── server.js              # Express + Socket.io サーバー
├── package.json           # 依存関係とスクリプト
└── README.md             # このファイル
```

### 主要機能の実装

- **リアルタイム通信**: Socket.io でユーザー接続とメッセージ配信
- **AI応答生成**: 各AIプロバイダーのAPIを呼び出し
- **クールダウン制御**: 連続応答を防ぐタイムベース制限
- **コンテキスト管理**: 履歴メッセージの保持と文脈提供

## ライセンス

MIT License

## 貢献

プルリクエストや Issue の報告を歓迎します。

## 更新履歴

- v1.0.0: 初期リリース
  - Google Gemini API対応
  - リアルタイムチャット機能
- v1.1.0: OpenAI API対応追加
  - プロバイダー選択機能
  - レート制限対応強化