# GitHub Copilot チートシート（VS Code 版）

VS Code で GitHub Copilot を使う人向けの、コマンド網羅チートシート。スラッシュコマンド `/`・チャット参加者 `@`・コンテキスト/ツール `#`・Copilot CLI コマンドを、準備と注意点つきでまとめる。

> **記載方針**
> - 出典は **公式ドキュメントのみ**（`code.visualstudio.com` / `docs.github.com` / `github.blog`(公式リリースノート)）。非公式サイトは一切参照しない。
> - 各表の下に出典 URL を明記する。表内の各行はその出典に基づく。
> - 内容は **2026年6月時点**。Copilot は更新が速いので、コマンドはチャット欄で `/` `@` `#` を打って実際の候補を確認し、最新は各出典で確認すること。
> - VS Code のドキュメントはサイト改編が進み、現行の正本チートシートは [`docs/agents/reference/ai-features-cheat-sheet`](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet)。

---

## 目次

- [1. チャットの開き方とショートカット](#1-チャットの開き方とショートカット)
- [2. チャットのサーフェス（4種類）](#2-チャットのサーフェス4種類)
- [3. スラッシュコマンド `/`（VS Code チャット）](#3-スラッシュコマンド-vs-code-チャット)
- [4. セッション分析 `/chronicle`](#4-セッション分析-chronicle)
- [5. チャット参加者 `@`](#5-チャット参加者-)
- [6. コンテキスト変数 `#`](#6-コンテキスト変数-)
- [7. エージェント用ツール `#`](#7-エージェント用ツール-)
- [8. Copilot CLI コマンド（VS Code 連携）](#8-copilot-cli-コマンドvs-code-連携)
- [9. 他 IDE のコマンド差分（参考）](#9-他-ide-のコマンド差分参考)
- [10. エディタの AI 機能・ソース管理・レビュー](#10-エディタの-ai-機能ソース管理レビュー)
- [11. カスタマイズの仕組み](#11-カスタマイズの仕組み)
- [12. 注意点](#12-注意点)
- [出典一覧](#出典一覧)

---

## 1. チャットの開き方とショートカット

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

## 2. チャットのサーフェス（4種類）

| サーフェス | 用途 | 開き方 |
|------------|------|--------|
| **Agents Window** | 複数プロジェクトをまたいだ大きめのタスクを、まとめて指揮できる専用画面 | タイトルバー「Open in Agents」/ コマンド `Chat: Open Agents Window` / ターミナル `code --agents` |
| **Chat View** | サイドバーに常駐する、コード作業のメイン相棒 | チャットアイコン / コマンド `Chat: Open Chat` / `Ctrl+Alt+I`（Mac: `⌃⌘I`） |
| **Inline Chat** | エディタやターミナルで、その場でサッと編集・提案してくれる | `Ctrl+I`（Mac: `⌘I`） |
| **Quick Chat** | エディタ上部にパッと出る軽量パネル。ちょい聞きに便利 | `Ctrl+Shift+Alt+L`（Mac: `⇧⌥⌘L`） |

> **出典:** [Use Copilot Chat in VS Code — VS Code Docs](https://code.visualstudio.com/docs/copilot/chat/copilot-chat) / [Chat agent mode — VS Code Docs](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode)

---

## 3. スラッシュコマンド `/`（VS Code チャット）

チャット入力欄で `/` を打つと利用可能なコマンド一覧が出る。

### コード操作系

| コマンド | 説明 |
|----------|------|
| `/doc` | コードにドキュメントコメントを付けてくれる（インラインチャット） |
| `/explain` | 「このコード何してる？」に答える。コードブロック・ファイル・概念を説明してくれる |
| `/fix` | バグやコンパイラ/リンタのエラーを直してくれる |
| `/tests` | ファイル全体や選んだメソッド・関数のテストを書いてくれる |
| `/setupTests` | テストフレームワークの導入・初期設定を手伝ってくれる |
| `/fixTestFailure` | 落ちたテストを分析して、直し方を出してくれる |

### セッション管理系

| コマンド | 説明 |
|----------|------|
| `/clear` | 履歴をリセットして、新しいセッションを始める |
| `/compact` | 話が長くなった時に、会話を要約して圧縮しコンテキストを節約（`/compact <指示>` で条件付き圧縮も可） |
| `/fork` | 今の会話を引き継いだまま、別ルートの新セッションに枝分かれする |
| `/debug` | Chat Debug ビューを開いて、チャットログを覗ける |
| `/troubleshoot` | うまく動かない時、エージェントのデバッグログを AI に分析させる（プレビュー） |
| `/help`※ | Copilot の基本的な使い方をサッと確認できる |

### 生成・スキャフォールド系

| コマンド | 説明 |
|----------|------|
| `/new` | 新しいワークスペースやファイルを一から作ってくれる |
| `/newNotebook` | やりたいことを伝えると、Jupyter ノートブックを用意してくれる |
| `/init` | プロジェクト用のカスタム指示（instructions）を作る・更新してくれる |
| `/plan` | 複雑な作業に入る前に、詳しい実装プランを立ててくれる |
| `/search` | Search ビューに入れる検索クエリを組み立ててくれる |
| `/startDebugging` | `launch.json` を作って、デバッグまで始めてくれる |

### カスタマイズ設定系

| コマンド | 説明 |
|----------|------|
| `/agents` | カスタムエージェントを設定できる（Configure Custom Agents メニュー） |
| `/instructions` | カスタム指示を設定できる |
| `/prompts` | 再利用できるプロンプトファイルを設定できる |
| `/skills` | エージェントスキルを設定できる |
| `/hooks` | フックを設定できる |
| `/create-instruction` | AI に手伝ってもらって instructions ファイルを作る |
| `/create-prompt` | Agent モードで、AI 補助でプロンプトファイルを作る |
| `/create-skill` | Agent モードでエージェントスキルを作る |
| `/create-agent` | Agent モードでカスタムエージェントを作る |
| `/create-hook` | フック設定を作る |

### 自動承認（YOLO）系

| コマンド | 説明 |
|----------|------|
| `/yolo`（= `/autoApprove`） | 毎回の確認をやめて、全ツール呼び出しを自動承認にする |
| `/disableYolo`（= `/disableAutoApprove`） | 自動承認をやめて、確認ありに戻す |

### 動的コマンド（スキル・プロンプト・プラグイン・MCP）

| コマンド | 説明 |
|----------|------|
| `/<skill name>` | 名前付きのエージェントスキルを呼び出して実行（例 `/webapp-testing for the login page`、引数も渡せる） |
| `/<prompt name>` | 保存してある再利用プロンプトを呼び出して実行 |
| `/<plugin name>:<skill>` | プラグイン配布のスキルを実行。プラグイン名が接頭辞として自動で付く（例 `/my-plugin:test-runner`） |
| `/<MCP server>.<prompt>` | MCP サーバーが用意した、事前構成済みのプロンプトテンプレートを呼び出す |

> **出典:** [AI features cheat sheet — VS Code Docs](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet) / [Custom agents](https://code.visualstudio.com/docs/copilot/customization/custom-agents) / [Prompt files](https://code.visualstudio.com/docs/copilot/customization/prompt-files) / [Agent skills](https://code.visualstudio.com/docs/copilot/customization/agent-skills) / [MCP servers](https://code.visualstudio.com/docs/copilot/customization/mcp-servers)
> ※ `/help` は GitHub 公式チートシートに VS Code 向けとして記載（[GitHub Docs cheat sheet](https://docs.github.com/en/copilot/reference/cheat-sheet)）。VS Code 公式チートシートには未掲載。

---

## 4. セッション分析 `/chronicle`

`/chronicle` は、VS Code・Copilot CLI・コードレビュー・coding agent をまたいだ自分のセッション履歴を検索・分析するコマンド群。スタンドアップ報告生成、使い方のヒント、コスト分析、カスタム指示の改善提案などができる。チャット欄で自然言語の質問（例:「昨日どのファイルを編集した?」）も可能。

**前提:** セッション同期（session sync）が有効であること（既定で有効）。

> **記法の違いに注意:** **VS Code はコロン記法**（`/chronicle:standup`）、**Copilot CLI はスペース記法**（`/chronicle standup`）。サブコマンド名も一部異なる。

### VS Code（コロン記法）

| コマンド | 説明 |
|----------|------|
| `/chronicle:standup` | 「昨日なにやったっけ？」に答える。最近の作業をブランチ・リポジトリ別にまとめて、朝会の報告に使える文章にしてくれる |
| `/chronicle:tips` | 最近のセッション履歴（通常7日分）を見て、「ここはこう頼むと早い」と Copilot の使い方の改善案を出してくれる |
| `/chronicle:cost-tips` | トークン（コスト）をムダに使っている箇所を見つけて、節約ポイントを教えてくれる |
| `/chronicle:search <query>` | 「あの修正どこでやった？」を探す。キーワード・ファイルパス・PR/Issue 番号で過去のセッションを検索してくれる |
| `/chronicle:reindex` | 履歴が検索に出てこない時に、ローカルの索引を作り直してアカウントへ同期し直す |

> **出典:** [Query session history with chronicle — VS Code Docs](https://code.visualstudio.com/docs/agents/sessions/session-insights)

> Copilot CLI でのスペース記法（`/chronicle standup` 等、`improve` サブコマンドあり）は [8. Copilot CLI コマンド](#8-copilot-cli-コマンドvs-code-連携) を参照。

---

## 5. チャット参加者 `@`

特定ドメインの専門家を指定する。プロンプト内で `@` を打つ。

| 参加者 | 説明 | 出典 |
|--------|------|------|
| `@github` | GitHub のリポジトリ・Issue・PR について聞ける | VS Code / GitHub 両方 |
| `@terminal` | ターミナルやシェルコマンドについて聞ける | VS Code / GitHub 両方 |
| `@vscode` | VS Code 自体の機能・設定・拡張機能 API について聞ける | VS Code / GitHub 両方 |
| `@workspace` | 今のワークスペースのコード（構造・設計パターン）について聞ける | GitHub のみ記載 |
| `@azure` | Azure のサービスについて聞ける（パブリックプレビュー） | GitHub のみ記載 |

> **出典:** [AI features cheat sheet — VS Code Docs](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet)（`@github`/`@terminal`/`@vscode`）/ [GitHub Docs cheat sheet](https://docs.github.com/en/copilot/reference/cheat-sheet)（`@workspace`/`@azure` を含む）
> **メモ:** 2 つの公式ソースで掲載される参加者に差がある。利用バージョンによって使える参加者が異なるため、`@` を打って実際の候補を確認するのが確実。

---

## 6. コンテキスト変数 `#`

プロンプトに `#` でコンテキストを差し込む。`#` には「コンテキスト参照」と「ツール参照」（→ [7 章](#7-エージェント用ツール-)）の2系統がある。

### VS Code のコンテキスト参照

| 変数 | 説明 |
|------|------|
| `#file` | 指定したファイルを材料として渡す |
| `#folder` | フォルダーをまるごと材料として渡す |
| `#symbol` / `#sym:Name` | 関数やクラスなどのシンボルを材料として渡す（`#sym:` で名前指定して自動変換） |
| `#selection` | 今エディタで選んでいる範囲を渡す |
| `#codebase` | コードベース全体から、関連箇所を意味検索して渡す（自動管理インデックス） |
| `#changes` | ソース管理（Git）の変更内容を渡す |
| `#fetch` | 指定した Web URL の中身を取ってきて渡す |
| `#terminalSelection` | ターミナルの選択範囲・出力を渡す |
| `#problems` | Problems パネルのエラー・警告を渡す |
| `#web` | Web から最新情報を取ってくる |

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

## 7. エージェント用ツール `#`

Agent モードでは `#` でツール／ツールセットを指定できる。親ツール（`#edit` 等）とサブツール（`#edit/createFile` 等）の両方がある。本文（instructions・プロンプトファイル・エージェント定義）内でツールを参照する場合は `#tool:<tool-name>` 構文を使う（例 `#tool:web/fetch`）。

| ツールセット | 主なサブツール | 説明 |
|--------------|----------------|------|
| `#agent` | `runSubagent` | 別のエージェントに任せる／隔離したサブエージェントで動かす |
| `#browser` | — | 内蔵ブラウザでページを操作する（実験的） |
| `#edit` | `createFile` / `createDirectory` / `editFiles` / `editNotebook` | ファイルの作成・編集をやる系 |
| `#execute` | `runInTerminal` / `getTerminalOutput` / `createAndRunTask` / `runNotebookCell` / `testFailure` | コードやタスク、ターミナルを実行する系 |
| `#read` | `readFile` / `problems` / `terminalLastCommand` / `terminalSelection` / `getNotebookSummary` / `readNotebookCellOutput` | ファイルや出力を読み取る系 |
| `#search` | `codebase` / `fileSearch` / `textSearch` / `listDirectory` / `changes` / `usages` | ファイルやコードを探す系 |
| `#vscode` | `runCommand` / `extensions` / `installExtension` / `getProjectSetupInfo` / `askQuestions` / `VSCodeAPI` | VS Code の操作・拡張機能まわり系 |
| `#web` | `fetch` | Web の中身を取ってくる |

**単独ツール:**

| ツール | 説明 |
|--------|------|
| `#githubRepo` | GitHub リポジトリを意味ベースで検索してくれる |
| `#githubTextSearch` | GitHub のリポジトリ/組織を grep みたいにテキスト検索してくれる |
| `#newWorkspace` | 新しいワークスペースを作ってくれる |
| `#todos` | TODO リストで進捗を追いかけてくれる |
| `#rename` | LSP を使って、安全に正確なリネーム/リファクタをしてくれる |
| `#usages` | 参照検索・実装検索・定義ジャンプをまとめて引ける |
| `#debugEventsSnapshot` | デバッグイベントのスナップショットを材料として添える |

> **出典:** [AI features cheat sheet — VS Code Docs](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet) / [Chat tools](https://code.visualstudio.com/docs/chat/chat-tools) / [Chat modes（`#tool:` 構文）](https://code.visualstudio.com/docs/copilot/chat/chat-modes)
> **メモ:** ツールセットはユーザー定義もできる（複数ツールを束ねた `#<myset>`）。

---

## 8. Copilot CLI コマンド（VS Code 連携）

GitHub Copilot CLI は、VS Code の統合ターミナルで `copilot` と入力して起動する。CLI の対話セッション内で使うスラッシュコマンドは VS Code チャットとは別系統で、数が多い。

> **記法:** CLI の `/chronicle` は**スペース記法**（`/chronicle standup`）。VS Code チャットのコロン記法とは異なる。

### セッション・会話管理

| コマンド | 説明 |
|----------|------|
| `/clear [PROMPT]` | 履歴をリセットして、新しい会話を始める |
| `/compact [FOCUS]` | 会話が長くなった時に、要約してコンテキスト消費を減らす |
| `/context` | 今どれだけトークンを使っているか表示する |
| `/copy` | 直前の返答をクリップボードにコピーする |
| `/rename [NAME]` | 今のセッションに名前をつける（省略すると自動で命名） |
| `/resume [SESSION-ID]` | 一覧から過去のセッションを選んで再開する |
| `/search [QUERY]` | これまでの会話タイムラインを検索する |
| `/session [SUBCOMMAND]` | セッションを管理する（info/checkpoints/files/plan/rename/cleanup/prune/delete/delete-all） |
| `/share [FORMAT] [TYPE] [PATH]` | セッションを Markdown/HTML/gist で共有する |
| `/undo`・`/rewind` | 直前のターンを巻き戻して、ファイルの変更も元に戻す |
| `/usage` | このセッションの使用量・統計を表示する |
| `/restart` | セッションは残したまま、CLI を再起動する |
| `/ask QUESTION` | 履歴に残さず、サッと軽い質問をする |

### 作業・エージェント実行

| コマンド | 説明 |
|----------|------|
| `/plan [PROMPT]` | コードを書く前に、実装プランを立ててくれる |
| `/research TOPIC` | GitHub 検索と Web ソースで深掘りリサーチしてくれる |
| `/review [PROMPT]` | コードレビュー担当のエージェントが変更をチェックしてくれる |
| `/rubber-duck [PROMPT]` | ラバーダック相手にセカンドオピニオンをもらう |
| `/fleet [PROMPT]` | タスクを分けて、並列のサブエージェントに同時にやらせる |
| `/delegate [PROMPT]` | 作業をリモートに丸投げして、AI が PR まで作ってくれる（autopilot） |
| `/agent` | カスタムエージェントを一覧から選ぶ |
| `/diff` | 今の変更内容を確認する |
| `/pr [SUBCOMMAND]` | 今のブランチの PR を管理する（表示・作成・修正） |
| `/worktree [BRANCH]` | 新しい Git worktree を作って、そっちに移る |
| `/after [DELAY PROMPT]` | プロンプト/コマンドを、後で1回だけ実行するよう予約する |
| `/every [INTERVAL PROMPT]` | プロンプト/skill/コマンドを、一定間隔で繰り返すよう予約する |
| `/tasks` | 走っているタスク（サブエージェント/シェル）を見る・管理する |
| `/chronicle [SUBCOMMAND]` | 過去のセッション履歴を検索・要約する（`standup`/`tips`/`cost tips`/`search`/`improve`/`reindex`） |

### 設定・環境・権限

| コマンド | 説明 |
|----------|------|
| `/init` | このリポジトリ用のカスタム指示・エージェント機能を初期セットアップする |
| `/instructions` | カスタム指示ファイルを表示・オンオフする |
| `/settings [OPTION]` | 設定を開く・その場でいじる・リセットする |
| `/model`・`/models [MODEL]` | 使う AI モデルを選ぶ |
| `/mcp [SUBCOMMAND]` | MCP サーバの設定を管理する（show/add/edit/delete/disable/enable/auth/reload） |
| `/plugin [SUBCOMMAND]` | プラグインやマーケットプレイスを管理する |
| `/skills [SUBCOMMAND]` | skills を管理する |
| `/extensions [SUBCOMMAND]` | CLI 拡張を管理する |
| `/lsp [SUBCOMMAND]` | 言語サーバ（LSP）の設定を管理する |
| `/permissions [SUBCOMMAND]` | ツール/パスの承認状況を見る・クリアする |
| `/allow-all [on\|off\|show]` | 全権限（ツール/パス/URL）を一括で許可する |
| `/reset-allowed-tools` | 許可済みツールの一覧をリセットする |
| `/add-dir PATH` | アクセスを許可するディレクトリを追加する |
| `/list-dirs` | アクセスを許可したディレクトリを一覧する |
| `/sandbox [enable\|disable]` | シェルコマンドのサンドボックスを設定する |
| `/remote [on\|off]` | GitHub.com やモバイルからの監視・操作を表示/有効化する |
| `/experimental [on\|off\|show]` | 実験的機能をオンオフ・設定・表示する |
| `/cwd`・`/cd [PATH]` | 作業ディレクトリを変える/表示する |
| `/env` | 読み込み済みの環境（指示/MCP/skills/agents/plugins 等）を表示する |
| `/ide` | IDE のワークスペースに接続する |
| `/keep-alive [OPTION]` | マシンがスリープしないようにする |
| `/statusline` | ステータスラインに出す項目を設定する |
| `/theme [OPTION]` | カラーテーマを表示/設定する |
| `/terminal-setup` | 複数行入力できるように、ターミナルを設定する |

### アカウント・メンテ・その他

| コマンド | 説明 |
|----------|------|
| `/login`・`/logout` | Copilot にログイン/ログアウトする |
| `/user [SUBCOMMAND]` | 今の GitHub ユーザーを管理する |
| `/update`・`/upgrade` | CLI を最新版に更新する |
| `/downgrade VERSION` | 指定したバージョンの CLI を落として再起動する |
| `/version` | バージョン情報を表示して、更新がないか確認する |
| `/changelog [OPTIONS]` | CLI の変更履歴を表示する（AI 要約オプションあり） |
| `/feedback`・`/bug` | CLI へのフィードバックを送る |
| `/help` | 対話コマンドのヘルプを表示する |
| `/exit`・`/quit` | CLI を終了する |
| `/clikit [COMPONENT]`・`/tuikit [COMPONENT]` | CLI/TUI のデザイン部品をプレビューする |

> **出典:** [Copilot CLI command reference — GitHub Docs](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference) / [Use Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/use-copilot-cli) / [chronicle](https://docs.github.com/en/copilot/how-tos/copilot-cli/use-copilot-cli/chronicle) / [fleet](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/fleet) / [Copilot CLI in VS Code](https://code.visualstudio.com/docs/copilot/agents/copilot-cli)

---

## 9. 他 IDE のコマンド差分（参考）

VS Code 以外の IDE で使えるスラッシュコマンド（GitHub 公式チートシートより）。VS Code には無いものを中心に挙げる。

| コマンド | 対象 IDE | 説明 |
|----------|----------|------|
| `/optimize` | Visual Studio | 選んだコードの実行速度を分析して改善してくれる |
| `/simplify` | Xcode | 選んだコードをシンプルに書き直してくれる |
| `/doc` | Visual Studio / Xcode | このシンボルにドキュメントコメントを付けてくれる |
| `/clear`・`/delete`・`/new`・`/rename` | GitHub Web (Copilot Chat) | 会話のクリア・削除・新規作成・改名をする |

> **出典:** [GitHub Docs cheat sheet](https://docs.github.com/en/copilot/reference/cheat-sheet) / [Chat cheat sheet](https://docs.github.com/en/copilot/reference/chat-cheat-sheet)
> **メモ:** Eclipse 向けのスラッシュコマンド・参加者・変数は公式に記載なし。

---

## 10. エディタの AI 機能・ソース管理・レビュー

### エディタ AI 機能

| 機能 | 説明 |
|------|------|
| インライン補完 | 入力に合わせて、続きの候補を出してくれる |
| コードコメント | コメントに指示を書くと、それを汲んで補完してくれる |
| コンテキストメニュー | 右クリックから説明・修正・レビューを呼べる |
| Code Actions（電球） | リンタ/コンパイラのエラーに、直し方を提案してくれる |
| F2 リネーム | リネームする時に、AI が名前候補を出してくれる |

### エージェントの権限・拡張

| 機能 | 説明 |
|------|------|
| 権限レベル | Default Approvals / Bypass Approvals / Autopilot の3段階から選べる |
| ツール/ターミナルの自動承認 | 呼び出しを毎回確認せず、自動承認にできる |
| MCP 設定 | MCP サーバーをつないで、エージェントの機能を拡張できる |
| サードパーティエージェント | Claude Agent（プレビュー）/ OpenAI などを使える |
| メモリ機能 | 会話をまたいでメモを覚えておいて、後で思い出してくれる |

### ソース管理・コードレビュー

| 機能 | 説明 |
|------|------|
| `#changes` | 今の変更内容を、コンテキストに足す |
| コミットメッセージ生成 | 変更内容から、コミットメッセージを書いてくれる |
| PR 説明生成 | PR のタイトルと説明を書いてくれる |
| マージ競合 | Git のマージ競合の解決を、AI が手伝ってくれる |
| Review Selection / Code Review ボタン | 選んだコードや未コミットの変更をレビューしてくれる |

> **出典:** [AI features cheat sheet — VS Code Docs](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet)

---

## 11. カスタマイズの仕組み

| 機能 | 設定/呼び出し | 説明 |
|------|---------------|------|
| カスタム指示（instructions） | `/init`・`/instructions`・`/create-instruction` | 全タスク共通のルール・規約を決めておける（`.github/copilot-instructions.md` 等） |
| 再利用プロンプトファイル | `/prompts`・`/create-prompt` / 実行は `/<prompt name>` | よく使うプロンプトを `.prompt.md` に保存して、使い回せる |
| エージェントスキル | `/skills`・`/create-skill` / 実行は `/<skill name>` | 複数ステップの作業手順を、スキルとしてまとめられる |
| カスタムエージェント | `/agents`・`/create-agent` | チャットの振る舞い・使えるツール・口調を決められる |
| フック | `/hooks`・`/create-hook` | 節目ごとの処理を、自動で走らせられる |
| MCP サーバー | `/mcp`（CLI）/ プロンプトは `/<server>.<prompt>` | 外部のツールやプロンプトをつないで、機能を増やせる |
| プロンプトファイル内の入力変数 | `${input:変数名:プレースホルダ}`・`${selection}` | プロンプトに、ユーザー入力や選択範囲を差し込める |

> **出典:** [Customization overview](https://code.visualstudio.com/docs/copilot/customization/overview) / [Custom instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions) / [Prompt files](https://code.visualstudio.com/docs/copilot/customization/prompt-files) / [Agent skills](https://code.visualstudio.com/docs/copilot/customization/agent-skills) / [Custom agents](https://code.visualstudio.com/docs/copilot/customization/custom-agents) / [Hooks](https://code.visualstudio.com/docs/copilot/customization/hooks)

---

## 12. 注意点

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
