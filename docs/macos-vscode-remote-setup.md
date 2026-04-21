# MacBook の VSCode を スマホから操作する方法

## 概要

MacBook で動く Claude Code を、外出先のスマホから操作するための方法をまとめたガイドです。

---

## 方法 1：Claude モバイルアプリ（GitHub 経由）

### できること
- 外出先からタスク開始・モニタリング可能
- GitHub リポジトリへの作業委任が可能
- Web 版で実行中のタスクに介入・指示出し可能

### できないこと
- ローカルファイルの操作（GitHub リポジトリのみ対応）
- ローカルの MacBook VSCode を直接操作

### 使い方
1. Claude モバイルアプリを iPhone にインストール
2. GitHub アカウントと連携
3. リポジトリを選択してタスクを委任

---

## 方法 2：Moshi アプリ（SSH 接続）

**アプリ：** [Moshi - SSH & Mosh Terminal](https://getmoshi.app/)

### 特徴
- iPhone/iPad から MacBook のターミナルに SSH 接続
- Mosh プロトコルで通信が不安定でも切れにくい
- 音声入力対応（歩きながら指示も可能）
- 作業完了時にスマホへ通知
- Face ID 認証対応

### メリット
- ローカルファイルも操作可能
- Claude Code のセッションを引き継ぎ可能

### デメリット
- Apple 製品専用（Android 不可）
- SSH 環境のセットアップが必要
- 現在ベータ版（将来一部有料化予定）

---

## 方法 3：Chrome Remote Desktop（リモートデスクトップ）

### 特徴
- 無料・設定が簡単
- MacBook の画面そのものをスマホに映す
- 同じ Google アカウントがあれば使える

### 設定手順

#### MacBook 側
1. Chrome で `remotedesktop.google.com/access` を開く
2. 「リモートアクセスの設定」→「＋」ボタン
3. 拡張機能をインストール
4. Mac に名前をつけて PIN（6桁以上）を設定

#### スマホ側
1. App Store で「Chrome Remote Desktop」をインストール
2. 同じ Google アカウントでログイン
3. Mac の名前をタップ → PIN を入力
4. MacBook の画面が映る

### 注意点
- MacBook の電源が入っていてスリープしていないこと
- 同じ Wi-Fi でなくてもOK（外出先からも使える）

---

## 外出先から Moshi を使う場合：Tailscale が必要

同じ Wi-Fi 内なら Tailscale 不要。外出先からアクセスするには Tailscale をセットアップする。

### Tailscale セットアップ（MacBook）

```bash
brew install tailscale
tailscale up
```

スマホにも Tailscale アプリを入れ、同じアカウントでログインする。

### MacBook のローカル IP 確認（家の Wi-Fi 内のみ）

```bash
ipconfig getifaddr en0
```

---

## 比較まとめ

| 方法 | 外出先から | ローカルファイル操作 | 難易度 | 費用 |
|------|-----------|---------------------|--------|------|
| Claude モバイルアプリ | ✅ | ❌（GitHub のみ） | 低 | 無料 |
| Moshi + Tailscale | ✅ | ✅ | 中 | 無料（現在） |
| Chrome Remote Desktop | ✅ | ✅ | 低 | 無料 |
| Moshi（家の Wi-Fi 内のみ） | ❌ | ✅ | 低 | 無料（現在） |

---

## Claude Code のインストール（MacBook）

```bash
npm install -g @anthropic-ai/claude-code
```

初回起動時にブラウザが開き、Anthropic アカウントでログインする。

```bash
# プロジェクトディレクトリに移動
cd ~/your-project

# 起動
claude
```
