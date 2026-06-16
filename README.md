# GitHub Copilot チートシート（VS Code 版）

VS Code で GitHub Copilot を使う人向けの、コマンド網羅チートシート。スラッシュコマンド `/`・チャット参加者 `@`・コンテキスト/ツール `#`・Copilot CLI コマンドを、準備と注意点つきでまとめる。

> **記載方針**
> - 出典は **公式ドキュメントのみ**（`code.visualstudio.com` / `docs.github.com` / `github.blog`(公式リリースノート)）。非公式サイトは一切参照しない。
> - 各表の下に出典 URL を明記する。表内の各行はその出典に基づく。
> - 内容は **2026年6月時点**。Copilot は更新が速いので、コマンドはチャット欄で `/` `@` `#` を打って実際の候補を確認し、最新は各出典で確認すること。
> - VS Code のドキュメントはサイト改編が進み、現行の正本チートシートは [`docs/agents/reference/ai-features-cheat-sheet`](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet)。

---

## 目次

- [1. 準備（前提条件とセットアップ）](#1-準備前提条件とセットアップ)
- [2. チャットの開き方とショートカット](#2-チャットの開き方とショートカット)
- [3. チャットのサーフェス（4種類）](#3-チャットのサーフェス4種類)
- [4. スラッシュコマンド `/`（VS Code チャット）](#4-スラッシュコマンド-vs-code-チャット)
- [5. セッション分析 `/chronicle`](#5-セッション分析-chronicle)
- [6. チャット参加者 `@`](#6-チャット参加者-)
- [7. コンテキスト変数 `#`](#7-コンテキスト変数-)
- [8. エージェント用ツール `#`](#8-エージェント用ツール-)
- [9. Copilot CLI コマンド（VS Code 連携）](#9-copilot-cli-コマンドvs-code-連携)
- [10. 他 IDE のコマンド差分（参考）](#10-他-ide-のコマンド差分参考)
- [11. 新機能タイムライン（バージョン別）](#11-新機能タイムラインバージョン別)
- [12. エディタの AI 機能・ソース管理・レビュー](#12-エディタの-ai-機能ソース管理レビュー)
- [13. カスタマイズの仕組み](#13-カスタマイズの仕組み)
- [14. 注意点](#14-注意点)
- [出典一覧](#出典一覧)

---

## 1. 準備（前提条件とセットアップ）

GitHub Copilot を使うには GitHub アカウントと Copilot へのアクセス（サブスクリプション、または無料プラン）が必要。VS Code には Copilot 機能が組み込まれている。

### セットアップ手順

1. **Copilot 機能を有効化** — ステータスバーの Copilot アイコンにマウスを乗せ **「Use AI Features」** を選択。
2. **サインイン** — 認証方法を選んで指示に従う。GitHub Enterprise は **「Continue with GHE.com」** からインスタンス URL を入力。
3. **プラン選択** — 契約済みならそのサブスクリプションを使用。未契約なら **Copilot Free プラン**（インライン補完と AI クレジットに月間上限）に登録される。
4. **動作確認** — サインインすれば利用可能。チャットで `/init` を実行するとプロジェクト用のカスタム指示（instructions）を設定できる。

### 注意

- 有料プランの新規登録は **2026年4月20日時点で一時停止**中（出典ページ記載）。
- 無料版はテレメトリが既定で有効。設定で無効化可能。

> **出典:** [Set up GitHub Copilot in VS Code — VS Code Docs](https://code.visualstudio.com/docs/copilot/setup)

---

## 2. チャットの開き方とショートカット

| 操作 | Windows / Linux | Mac |
|------|-----------------|-----|
| チャットビューを開く | `Ctrl+Alt+I` | `⌃⌘I` |
| インラインチャット | `Ctrl+I` | `⌘I` |
| インライン/チャット内のボイスチャット | `Ctrl+I`（長押し） | `⌘I`（長押し） |
| クイックチャット | `Ctrl+Shift+Alt+L` | `⇧⌥⌘L` |
| 新しいチャットセッション | `Ctrl+N` | `⌘N` |
| エージェント利用に切替 | `Ctrl+Shift+I`（Linux: `Ctrl+Shift+Alt+I`） | `⇧⌘I` |
| 補完候補を確定 / 破棄 | `Tab` / `Escape` | `Tab` / `Escape` |
| AI でリネーム | `F2` | `F2` |
| モデルピッカー | `Ctrl+Alt+.` | `⌥⌘.` |

> **出典:** [AI features cheat sheet — VS Code Docs](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet)

---

## 3. チャットのサーフェス（4種類）

| サーフェス | 用途 | 開き方 |
|------------|------|--------|
| **Agents Window** | 複数プロジェクトをまたぐ高レベルなタスクのオーケストレーション専用画面 | タイトルバー「Open in Agents」/ コマンド `Chat: Open Agents Window` / ターミナル `code --agents` |
| **Chat View** | サイドバー統合のコード中心アシスタント | チャットアイコン / コマンド `Chat: Open Chat` / `Ctrl+Alt+I`（Mac: `⌃⌘I`） |
| **Inline Chat** | エディタ内・ターミナルでのその場の編集・提案 | `Ctrl+I`（Mac: `⌘I`） |
| **Quick Chat** | エディタ上部の軽量パネル。手早いやり取り | `Ctrl+Shift+Alt+L`（Mac: `⇧⌥⌘L`） |

> **出典:** [Use Copilot Chat in VS Code — VS Code Docs](https://code.visualstudio.com/docs/copilot/chat/copilot-chat) / [Chat agent mode — VS Code Docs](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode)

---

## 4. スラッシュコマンド `/`（VS Code チャット）

チャット入力欄で `/` を打つと利用可能なコマンド一覧が出る。

### コード操作系

| コマンド | 説明 |
|----------|------|
| `/doc` | インラインチャットでコードのドキュメントコメントを生成 |
| `/explain` | コードブロック・ファイル・概念を説明 |
| `/fix` | コードの修正、コンパイラ/リンタエラーの解決を依頼 |
| `/tests` | 全体または選択メソッド・関数のテストを生成 |
| `/setupTests` | テストフレームワークのセットアップを支援 |
| `/fixTestFailure` | 失敗テストを分析して修正案を出す |

### セッション管理系

| コマンド | 説明 |
|----------|------|
| `/clear` | チャットビューで新しいセッションを開始 |
| `/compact` | 会話コンテキストを要約して圧縮（`/compact <指示>` で条件付き圧縮も可） |
| `/fork` | 会話履歴を引き継いだ独立した新セッションに分岐 |
| `/debug` | Chat Debug ビューを表示してチャットログを確認 |
| `/troubleshoot` | エージェントのデバッグログを AI に分析させる（プレビュー） |
| `/help`※ | Copilot 利用の基本クイックリファレンス |

### 生成・スキャフォールド系

| コマンド | 説明 |
|----------|------|
| `/new` | 新しいワークスペースまたはファイルを生成 |
| `/newNotebook` | 要件に基づき新しい Jupyter ノートブックを生成 |
| `/init` | ワークスペースの instructions を生成・更新 |
| `/plan` | 複雑なコーディングタスクの詳細な実装計画を作成 |
| `/search` | Search ビュー用の検索クエリを生成 |
| `/startDebugging` | `launch.json` を生成してデバッグを開始 |

### カスタマイズ設定系

| コマンド | 説明 |
|----------|------|
| `/agents` | カスタムエージェントを設定（Configure Custom Agents メニュー） |
| `/instructions` | カスタム指示を設定 |
| `/prompts` | 再利用可能なプロンプトファイルを設定 |
| `/skills` | エージェントスキルを設定 |
| `/hooks` | フックを設定 |
| `/create-instruction` | AI 補助で instructions ファイルを生成 |
| `/create-prompt` | Agent モードで AI 補助でプロンプトファイルを生成 |
| `/create-skill` | Agent モードでエージェントスキルを生成 |
| `/create-agent` | Agent モードでカスタムエージェントを生成 |
| `/create-hook` | フック設定を生成 |

### 自動承認（YOLO）系

| コマンド | 説明 |
|----------|------|
| `/yolo`（= `/autoApprove`） | すべてのツール呼び出しのグローバル自動承認を有効化 |
| `/disableYolo`（= `/disableAutoApprove`） | グローバル自動承認を無効化 |

### 動的コマンド（スキル・プロンプト・プラグイン・MCP）

| コマンド | 説明 |
|----------|------|
| `/<skill name>` | 名前付きエージェントスキルを実行（例 `/webapp-testing for the login page`、引数も渡せる） |
| `/<prompt name>` | 名前付き再利用プロンプトを実行 |
| `/<plugin name>:<skill>` | プラグイン配布スキル。プラグイン名が接頭辞として自動付与（例 `/my-plugin:test-runner`） |
| `/<MCP server>.<prompt>` | MCP サーバーが提供する事前構成プロンプトテンプレートを呼び出す |

> **出典:** [AI features cheat sheet — VS Code Docs](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet) / [Custom agents](https://code.visualstudio.com/docs/copilot/customization/custom-agents) / [Prompt files](https://code.visualstudio.com/docs/copilot/customization/prompt-files) / [Agent skills](https://code.visualstudio.com/docs/copilot/customization/agent-skills) / [MCP servers](https://code.visualstudio.com/docs/copilot/customization/mcp-servers)
> ※ `/help` は GitHub 公式チートシートに VS Code 向けとして記載（[GitHub Docs cheat sheet](https://docs.github.com/en/copilot/reference/cheat-sheet)）。VS Code 公式チートシートには未掲載。

---

## 5. セッション分析 `/chronicle`

`/chronicle` は、VS Code・Copilot CLI・コードレビュー・coding agent をまたいだ自分のセッション履歴を検索・分析するコマンド群。スタンドアップ報告生成、使い方のヒント、コスト分析、カスタム指示の改善提案などができる。チャット欄で自然言語の質問（例:「昨日どのファイルを編集した?」）も可能。

**前提:** セッション同期（session sync）が有効であること（既定で有効）。

> **記法の違いに注意:** **VS Code はコロン記法**（`/chronicle:standup`）、**Copilot CLI はスペース記法**（`/chronicle standup`）。サブコマンド名も一部異なる。

### VS Code（コロン記法）

| コマンド | 説明 |
|----------|------|
| `/chronicle:standup` | 最近のセッションをブランチ・リポジトリ別にまとめたスタンドアップ報告にする |
| `/chronicle:tips` | 最近のセッション履歴（通常7日分）を分析し、Copilot をより効果的に使う方法を提案 |
| `/chronicle:cost-tips` | トークン消費とコストを削減できる箇所を特定 |
| `/chronicle:search <query>` | キーワード・ファイルパス・PR/Issue 参照でセッションを検索 |
| `/chronicle:reindex` | ローカルのセッションインデックスを再構築しアカウントへ同期 |

> **出典:** [Query session history with chronicle — VS Code Docs](https://code.visualstudio.com/docs/agents/sessions/session-insights)

> Copilot CLI でのスペース記法（`/chronicle standup` 等、`improve` サブコマンドあり）は [9. Copilot CLI コマンド](#9-copilot-cli-コマンドvs-code-連携) を参照。

---

## 6. チャット参加者 `@`

特定ドメインの専門家を指定する。プロンプト内で `@` を打つ。

| 参加者 | 説明 | 出典 |
|--------|------|------|
| `@github` | GitHub リポジトリ・Issue・PR について尋ねる | VS Code / GitHub 両方 |
| `@terminal` | 統合ターミナル・シェルコマンドについて尋ねる | VS Code / GitHub 両方 |
| `@vscode` | VS Code の機能・設定・拡張機能 API について尋ねる | VS Code / GitHub 両方 |
| `@workspace` | ワークスペースのコード（構造・設計パターン）について尋ねる | GitHub のみ記載 |
| `@azure` | Azure サービスについて尋ねる（パブリックプレビュー） | GitHub のみ記載 |

> **出典:** [AI features cheat sheet — VS Code Docs](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet)（`@github`/`@terminal`/`@vscode`）/ [GitHub Docs cheat sheet](https://docs.github.com/en/copilot/reference/cheat-sheet)（`@workspace`/`@azure` を含む）
> **メモ:** 2 つの公式ソースで掲載される参加者に差がある。利用バージョンによって使える参加者が異なるため、`@` を打って実際の候補を確認するのが確実。

---

## 7. コンテキスト変数 `#`

プロンプトに `#` でコンテキストを差し込む。`#` には「コンテキスト参照」と「ツール参照」（→ [8 章](#8-エージェント用ツール-)）の2系統がある。

### VS Code のコンテキスト参照

| 変数 | 説明 |
|------|------|
| `#file` | 特定ファイルを参照 |
| `#folder` | フォルダー全体を参照 |
| `#symbol` / `#sym:Name` | コードシンボルを参照（`#sym:` で名前指定して自動変換） |
| `#selection` | 現在のエディタ選択範囲 |
| `#codebase` | コードベース全体（自動管理インデックスへのセマンティック検索） |
| `#changes` | ソース管理の変更を参照 |
| `#fetch` | Web URL のコンテンツを取得して参照 |
| `#terminalSelection` | ターミナルの選択範囲・出力を参照 |
| `#problems` | Problems パネルの問題を参照 |
| `#web` | Web 上の最新情報を取得 |

> **出典:** [AI features cheat sheet](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet) / [Manage chat context](https://code.visualstudio.com/docs/chat/copilot-chat-context) / [Chat tools](https://code.visualstudio.com/docs/chat/chat-tools)

### GitHub 公式チートシート掲載のチャット変数（別系統）

`#block` / `#class` / `#comment` / `#file` / `#function` / `#line` / `#path` / `#project` / `#selection` / `#sym`（それぞれ現在のブロック・クラス・コメント・ファイル・関数・行・パス・プロジェクト・選択・シンボルを参照）。

> **出典:** [GitHub Docs cheat sheet](https://docs.github.com/en/copilot/reference/cheat-sheet)
> **メモ:** 上記 GitHub 側の変数群は VS Code 公式チートシートの記載と一部異なる。混同せず、`#` を打って実候補を確認すること。

### コンテキストの追加方法

- ファイル/フォルダー/Problems 項目をチャットビューにドラッグ＆ドロップ
- `#<file|folder|symbol>` と入力して直接参照
- **「Add Context...」** ボタンから選択

---

## 8. エージェント用ツール `#`

Agent モードでは `#` でツール／ツールセットを指定できる。親ツール（`#edit` 等）とサブツール（`#edit/createFile` 等）の両方がある。本文（instructions・プロンプトファイル・エージェント定義）内でツールを参照する場合は `#tool:<tool-name>` 構文を使う（例 `#tool:web/fetch`）。

| ツールセット | 主なサブツール | 説明 |
|--------------|----------------|------|
| `#agent` | `runSubagent` | 他エージェントへ委譲 / 隔離サブエージェントで実行 |
| `#browser` | — | 統合ブラウザのページ操作（実験的） |
| `#edit` | `createFile` / `createDirectory` / `editFiles` / `editNotebook` | ワークスペースの編集系 |
| `#execute` | `runInTerminal` / `getTerminalOutput` / `createAndRunTask` / `runNotebookCell` / `testFailure` | コード・タスク・ターミナル実行系 |
| `#read` | `readFile` / `problems` / `terminalLastCommand` / `terminalSelection` / `getNotebookSummary` / `readNotebookCellOutput` | 読み取り系 |
| `#search` | `codebase` / `fileSearch` / `textSearch` / `listDirectory` / `changes` / `usages` | ファイル・コード検索系 |
| `#vscode` | `runCommand` / `extensions` / `installExtension` / `getProjectSetupInfo` / `askQuestions` / `VSCodeAPI` | VS Code 操作・拡張機能系 |
| `#web` | `fetch` | Web コンテンツ取得 |

**単独ツール:**

| ツール | 説明 |
|--------|------|
| `#githubRepo` | GitHub リポジトリをセマンティック検索 |
| `#githubTextSearch` | GitHub リポジトリ/組織を grep 風にテキスト検索 |
| `#newWorkspace` | 新規ワークスペースを作成 |
| `#todos` | TODO リストで進捗を追跡 |
| `#rename` | LSP を使った高精度なリネーム/リファクタ |
| `#usages` | 参照検索・実装検索・定義移動の統合 |
| `#debugEventsSnapshot` | デバッグイベントのスナップショットをコンテキスト添付 |

> **出典:** [AI features cheat sheet — VS Code Docs](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet) / [Chat tools](https://code.visualstudio.com/docs/chat/chat-tools) / [Chat modes（`#tool:` 構文）](https://code.visualstudio.com/docs/copilot/chat/chat-modes)
> **メモ:** ツールセットはユーザー定義もできる（複数ツールを束ねた `#<myset>`）。

---

## 9. Copilot CLI コマンド（VS Code 連携）

GitHub Copilot CLI は、VS Code の統合ターミナルで `copilot` と入力して起動する。CLI の対話セッション内で使うスラッシュコマンドは VS Code チャットとは別系統で、数が多い。

> **記法:** CLI の `/chronicle` は**スペース記法**（`/chronicle standup`）。VS Code チャットのコロン記法とは異なる。

### セッション・会話管理

| コマンド | 説明 |
|----------|------|
| `/clear [PROMPT]` | 新しい会話を開始 |
| `/compact [FOCUS]` | 会話履歴を要約してコンテキスト消費を削減 |
| `/context` | コンテキストウィンドウのトークン使用量を表示 |
| `/copy` | 直前の応答をクリップボードにコピー |
| `/rename [NAME]` | 現セッションの名前変更（省略時は自動命名） |
| `/resume [SESSION-ID]` | 一覧から別セッションへ切替 |
| `/search [QUERY]` | 会話タイムラインを検索 |
| `/session [SUBCOMMAND]` | セッション管理（info/checkpoints/files/plan/rename/cleanup/prune/delete/delete-all） |
| `/share [FORMAT] [TYPE] [PATH]` | セッションを Markdown/HTML/gist に共有 |
| `/undo`・`/rewind` | 直前のターンを巻き戻しファイル変更を戻す |
| `/usage` | セッション使用量メトリクス・統計を表示 |
| `/restart` | セッションを保持したまま CLI を再起動 |
| `/ask QUESTION` | 履歴に残さず軽い質問をする |

### 作業・エージェント実行

| コマンド | 説明 |
|----------|------|
| `/plan [PROMPT]` | コーディング前に実装計画を作成 |
| `/research TOPIC` | GitHub 検索と Web ソースで深掘りリサーチ |
| `/review [PROMPT]` | コードレビューエージェントで変更を分析 |
| `/rubber-duck [PROMPT]` | ラバーダックエージェントにセカンドオピニオンを相談 |
| `/fleet [PROMPT]` | タスクの一部を並列サブエージェントで実行 |
| `/delegate [PROMPT]` | 変更をリモートに委任し AI 生成 PR を作成（autopilot） |
| `/agent` | カスタムエージェントを一覧・選択 |
| `/diff` | カレントの変更をレビュー |
| `/pr [SUBCOMMAND]` | カレントブランチの PR を管理（表示・作成・修正） |
| `/worktree [BRANCH]` | 新しい Git worktree を作成して切替 |
| `/after [DELAY PROMPT]` | 単発のプロンプト/コマンドをスケジュール |
| `/every [INTERVAL PROMPT]` | 繰り返しプロンプト/skill/コマンドをスケジュール |
| `/tasks` | タスク（サブエージェント/シェル）の表示・管理 |
| `/chronicle [SUBCOMMAND]` | セッション履歴ツール（`standup`/`tips`/`cost tips`/`search`/`improve`/`reindex`） |

### 設定・環境・権限

| コマンド | 説明 |
|----------|------|
| `/init` | リポジトリ向けカスタム指示・エージェント機能を初期化 |
| `/instructions` | カスタム指示ファイルの表示・トグル |
| `/settings [OPTION]` | 設定ダイアログを開く/インライン設定/リセット |
| `/model`・`/models [MODEL]` | 使用する AI モデルを選択 |
| `/mcp [SUBCOMMAND]` | MCP サーバ設定を管理（show/add/edit/delete/disable/enable/auth/reload） |
| `/plugin [SUBCOMMAND]` | プラグイン/マーケットプレイス管理 |
| `/skills [SUBCOMMAND]` | skills を管理 |
| `/extensions [SUBCOMMAND]` | CLI 拡張を管理 |
| `/lsp [SUBCOMMAND]` | 言語サーバ設定を管理 |
| `/permissions [SUBCOMMAND]` | ツール/パス承認の表示・クリア |
| `/allow-all [on\|off\|show]` | 全権限（ツール/パス/URL）を有効化 |
| `/reset-allowed-tools` | 許可ツールのリストをリセット |
| `/add-dir PATH` | ファイルアクセス許可リストにディレクトリを追加 |
| `/list-dirs` | アクセス許可済みディレクトリを一覧 |
| `/sandbox [enable\|disable]` | シェルコマンドのサンドボックスを設定 |
| `/remote [on\|off]` | リモート操作（GitHub.com/モバイルから監視・操作）の状態表示/有効化 |
| `/experimental [on\|off\|show]` | 実験的機能のトグル/設定/表示 |
| `/cwd`・`/cd [PATH]` | 作業ディレクトリを変更/表示 |
| `/env` | 読み込み済み環境詳細（指示/MCP/skills/agents/plugins 等）を表示 |
| `/ide` | IDE ワークスペースに接続 |
| `/keep-alive [OPTION]` | マシンのスリープを防止 |
| `/statusline` | ステータスラインの表示項目を設定 |
| `/theme [OPTION]` | カラーモードの表示/設定 |
| `/terminal-setup` | 複数行入力対応のためターミナルを設定 |

### アカウント・メンテ・その他

| コマンド | 説明 |
|----------|------|
| `/login`・`/logout` | Copilot にログイン/ログアウト |
| `/user [SUBCOMMAND]` | 現在の GitHub ユーザーを管理 |
| `/update`・`/upgrade` | CLI を最新に更新 |
| `/downgrade VERSION` | 指定バージョンの CLI を DL して再起動 |
| `/version` | バージョン情報表示と更新チェック |
| `/changelog [OPTIONS]` | CLI の変更履歴を表示（AI 要約オプションあり） |
| `/feedback`・`/bug` | CLI へのフィードバック送信 |
| `/help` | 対話コマンドのヘルプ表示 |
| `/exit`・`/quit` | CLI を終了 |
| `/clikit [COMPONENT]`・`/tuikit [COMPONENT]` | CLI/TUI のデザインコンポーネントをプレビュー |

> **出典:** [Copilot CLI command reference — GitHub Docs](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference) / [Use Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/use-copilot-cli) / [chronicle](https://docs.github.com/en/copilot/how-tos/copilot-cli/use-copilot-cli/chronicle) / [fleet](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/fleet) / [Copilot CLI in VS Code](https://code.visualstudio.com/docs/copilot/agents/copilot-cli)

---

## 10. 他 IDE のコマンド差分（参考）

VS Code 以外の IDE で使えるスラッシュコマンド（GitHub 公式チートシートより）。VS Code には無いものを中心に挙げる。

| コマンド | 対象 IDE | 説明 |
|----------|----------|------|
| `/optimize` | Visual Studio | 選択コードの実行時間を分析・改善 |
| `/simplify` | Xcode | 現在の選択コードを簡略化 |
| `/doc` | Visual Studio / Xcode | このシンボルのドキュメントコメントを追加 |
| `/clear`・`/delete`・`/new`・`/rename` | GitHub Web (Copilot Chat) | 会話のクリア・削除・新規・改名 |

> **出典:** [GitHub Docs cheat sheet](https://docs.github.com/en/copilot/reference/cheat-sheet) / [Chat cheat sheet](https://docs.github.com/en/copilot/reference/chat-cheat-sheet)
> **メモ:** Eclipse 向けのスラッシュコマンド・参加者・変数は公式に記載なし。

---

## 11. 新機能タイムライン（バージョン別）

公式リリースノートで追加・変更が確認できた主なコマンド（VS Code）。

| コマンド | 種別 | 内容 | 時期 |
|----------|------|------|------|
| `/autoApprove`・`/disableAutoApprove`（別名 `/yolo`・`/disableYolo`） | `/` | 全ツールのグローバル自動承認トグル | v1.110（2026年2月） |
| `/compact` | `/` | 会話履歴の手動圧縮（`/compact <指示>` 可） | v1.110 |
| `/fork` | `/` | 会話履歴を引き継いだ分岐セッション | v1.110 導入 → v1.111 で手動フォーク強化 |
| `/create-prompt`・`/create-instruction`・`/create-skill`・`/create-agent`・`/create-hook` | `/` | チャットから各種カスタマイズファイルを生成 | v1.110 |
| `/troubleshoot` | `/` | エージェントのデバッグログをチャットで分析（プレビュー） | v1.112 |
| `/remote on`/`off` | `/` | CLI セッションを GitHub.com/モバイルから監視・操作（実験的） | 2026年3月（April releases 記事） |
| `/settings` | `/` | Copilot CLI 設定の一元化 | 2026年6月（May releases 記事） |
| `/chronicle`（+ サブコマンド） | `/` | セッション履歴の横断照会。実験的導入 → 拡充 | 2026年3月導入 → 5〜6月拡充 |
| `#codebase` | `#` | 単一の自動管理インデックスへの純セマンティック検索に変更 | 2026年2月（March releases 記事） |
| `#githubTextSearch` | `#` | リポジトリ/Org 横断の grep 風テキスト検索 | 2026年3月（April releases 記事） |
| `#rename` | `#` | LSP ベースの高精度リネーム | v1.110 |
| `#usages` | `#` | 参照ナビのパフォーマンス改善 | v1.110 |
| `#debugEventsSnapshot` | `#` | デバッグイベントのスナップショット添付 | v1.111 |
| `#sym:Name` | `#` | シンボル名の自動コンテキスト変換 | v1.112 |

> **出典:** [github.blog/changelog（VS Code 月次リリース）](https://github.blog/changelog/2026-06-03-github-copilot-in-visual-studio-code-may-releases/) / [/chronicle 告知](https://github.blog/changelog/2026-06-02-gain-insights-across-your-agent-sessions-with-chronicle/) / [VS Code v1.110](https://code.visualstudio.com/updates/v1_110) / [v1.111](https://code.visualstudio.com/updates/v1_111) / [v1.112](https://code.visualstudio.com/updates/v1_112)
> **メモ:** 「April releases」記事は公開日が 2026-05-06 で、記事タイトルの月と公開日が約1ヶ月ずれる。本表は記事内容に従って時期を記載。

---

## 12. エディタの AI 機能・ソース管理・レビュー

### エディタ AI 機能

| 機能 | 説明 |
|------|------|
| インライン補完 | 入力に合わせて補完候補を表示 |
| コードコメント | コメントに指示を書いて補完を引き出す |
| コンテキストメニュー | 右クリックで説明・修正・レビュー |
| Code Actions（電球） | リンタ/コンパイラエラーへの提案 |
| F2 リネーム | リネーム時に AI 提案を表示 |

### エージェントの権限・拡張

| 機能 | 説明 |
|------|------|
| 権限レベル | Default Approvals / Bypass Approvals / Autopilot |
| ツール/ターミナルの自動承認 | 呼び出しの自動承認を有効化 |
| MCP 設定 | MCP サーバーでエージェント機能を拡張 |
| サードパーティエージェント | Claude Agent（プレビュー）/ OpenAI など |
| メモリ機能 | 会話をまたいで永続的なメモを保存・想起 |

### ソース管理・コードレビュー

| 機能 | 説明 |
|------|------|
| `#changes` | 現在のソース管理の変更をコンテキストに追加 |
| コミットメッセージ生成 | 変更内容からコミットメッセージを生成 |
| PR 説明生成 | PR のタイトル・説明を生成 |
| マージ競合 | Git のマージ競合の解決を AI が支援 |
| Review Selection / Code Review ボタン | 選択コード/未コミット変更をレビュー |

> **出典:** [AI features cheat sheet — VS Code Docs](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet)

---

## 13. カスタマイズの仕組み

| 機能 | 設定/呼び出し | 説明 |
|------|---------------|------|
| カスタム指示（instructions） | `/init`・`/instructions`・`/create-instruction` | タスク共通のガイドライン・規約を定義（`.github/copilot-instructions.md` 等） |
| 再利用プロンプトファイル | `/prompts`・`/create-prompt` / 実行は `/<prompt name>` | よく使うプロンプトを `.prompt.md` として定義・再利用 |
| エージェントスキル | `/skills`・`/create-skill` / 実行は `/<skill name>` | 複数ステップのワークフローをスキル化 |
| カスタムエージェント | `/agents`・`/create-agent` | チャットの挙動・使えるツール・ペルソナを定義 |
| フック | `/hooks`・`/create-hook` | ライフサイクル自動化 |
| MCP サーバー | `/mcp`（CLI）/ プロンプトは `/<server>.<prompt>` | 外部ツール/プロンプトを接続して拡張 |
| プロンプトファイル内の入力変数 | `${input:変数名:プレースホルダ}`・`${selection}` | プロンプトにユーザー入力や選択範囲を埋め込む |

> **出典:** [Customization overview](https://code.visualstudio.com/docs/copilot/customization/overview) / [Custom instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions) / [Prompt files](https://code.visualstudio.com/docs/copilot/customization/prompt-files) / [Agent skills](https://code.visualstudio.com/docs/copilot/customization/agent-skills) / [Custom agents](https://code.visualstudio.com/docs/copilot/customization/custom-agents) / [Hooks](https://code.visualstudio.com/docs/copilot/customization/hooks)

---

## 14. 注意点

- **コマンド/参加者/ツールはバージョンで変わる。** チャット欄で `/`・`@`・`#` を打ち、実際に表示される候補を確認するのが最も確実。
- **「Ask / Edit / Agent モード」という組み込みモード名は、現行の VS Code 公式ドキュメントには明示されていない。** VS Code は用語を「カスタムエージェント」へ再編しており、エージェントへの切替はドロップダウン（agent target picker）または `Ctrl+Shift+I`（Mac: `⇧⌘I`）で行う、という記述まで。本書では推測でモード名を補わない。
- **2 つの公式ソースで内容に差がある。** GitHub 公式チートシートと VS Code 公式チートシートで、掲載されるスラッシュコマンド・参加者・変数が一部異なる（例: `@workspace`/`@azure` は GitHub 側のみ、`/help` も GitHub 側記載）。本書は両方を併記。
- **`/chronicle` は記法が2系統。** VS Code はコロン（`/chronicle:standup`）、CLI はスペース（`/chronicle standup`）。サブコマンドも一部差（`improve` は CLI 側に明示）。
- **VS Code のドキュメント URL が改編されている。** 旧 `docs/copilot/chat/*` の一部は 404 で、現行は `docs/chat/*`・`docs/agents/*` 系。正本チートシートは `docs/agents/reference/ai-features-cheat-sheet`。
- **自動承認（YOLO / Autopilot）はツール・ターミナルコマンドを確認なしで実行する。** 影響範囲を理解した上で使う（CLI ではサンドボックスとの併用が推奨）。
- **有料プランの新規登録は一時停止中**（出典ページ 2026年4月20日時点）。**無料版はテレメトリ既定有効**。

---

## 出典一覧

すべて公式ドキュメント／公式リリースノートのみ。

**Visual Studio Code 公式（code.visualstudio.com）**
- [Set up GitHub Copilot in VS Code](https://code.visualstudio.com/docs/copilot/setup)
- [AI features cheat sheet（現行正本）](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet)
- [GitHub Copilot in VS Code cheat sheet（旧パス・同等内容）](https://code.visualstudio.com/docs/copilot/reference/copilot-vscode-features)
- [Use Copilot Chat in VS Code](https://code.visualstudio.com/docs/copilot/chat/copilot-chat)
- [Chat agent mode](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode) / [Chat modes](https://code.visualstudio.com/docs/copilot/chat/chat-modes)
- [Manage chat context](https://code.visualstudio.com/docs/chat/copilot-chat-context) / [Chat tools](https://code.visualstudio.com/docs/chat/chat-tools)
- [Query session history with chronicle](https://code.visualstudio.com/docs/agents/sessions/session-insights)
- [Copilot CLI in VS Code](https://code.visualstudio.com/docs/copilot/agents/copilot-cli)
- Customization: [overview](https://code.visualstudio.com/docs/copilot/customization/overview) / [custom-instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions) / [prompt-files](https://code.visualstudio.com/docs/copilot/customization/prompt-files) / [agent-skills](https://code.visualstudio.com/docs/copilot/customization/agent-skills) / [custom-agents](https://code.visualstudio.com/docs/copilot/customization/custom-agents) / [hooks](https://code.visualstudio.com/docs/copilot/customization/hooks) / [mcp-servers](https://code.visualstudio.com/docs/copilot/customization/mcp-servers)
- Release notes: [v1.110](https://code.visualstudio.com/updates/v1_110) / [v1.111](https://code.visualstudio.com/updates/v1_111) / [v1.112](https://code.visualstudio.com/updates/v1_112)

**GitHub 公式（docs.github.com）**
- [GitHub Copilot Chat cheat sheet](https://docs.github.com/en/copilot/reference/cheat-sheet)
- [Copilot Chat cheat sheet（IDE 別）](https://docs.github.com/en/copilot/reference/chat-cheat-sheet)
- [Copilot CLI command reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference)
- [Use Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/use-copilot-cli) / [chronicle](https://docs.github.com/en/copilot/how-tos/copilot-cli/use-copilot-cli/chronicle) / [fleet](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/fleet)

**GitHub 公式リリースノート（github.blog/changelog）**
- [Gain insights across your agent sessions with /chronicle](https://github.blog/changelog/2026-06-02-gain-insights-across-your-agent-sessions-with-chronicle/)
- [VS Code May releases](https://github.blog/changelog/2026-06-03-github-copilot-in-visual-studio-code-may-releases/) / [April releases](https://github.blog/changelog/2026-05-06-github-copilot-in-visual-studio-code-april-releases/) / [March releases](https://github.blog/changelog/2026-04-08-github-copilot-in-visual-studio-code-march-releases/) / [v1.110 February release](https://github.blog/changelog/2026-03-06-github-copilot-in-visual-studio-code-v1-110-february-release/)

---

*本チートシートは上記公式ドキュメント（2026年6月時点）を基に作成。最新情報は必ず各出典で確認してください。*
