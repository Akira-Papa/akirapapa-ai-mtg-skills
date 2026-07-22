# ai-mtg-skills — 天才会議 for AI Coding Agents

「AIに4人の架空キャラで会議させる」天才会議プロンプトv2を、
**Claude Code / Codex CLI / Cursor** で使える **skills / agents / rules / commands** として体系化したツールキットです。

オープンソースであり、[MITライセンス](LICENSE)で公開しています。

## 🎬 紹介動画

### 🇯🇵 日本語 — 天才会議プロンプト2.0(Fable5で進化した会議設計図)

https://github.com/user-attachments/assets/726f31a5-6d36-41be-9b13-b951de45ef74

### 🇺🇸 English — Genius Meeting Prompt 2.0

https://github.com/user-attachments/assets/a0f9ca2a-19d5-4ff7-b4fd-6847464a7014

### 🇨🇳 中文 — 天才会议提示词 2.0

https://github.com/user-attachments/assets/bd78c700-3474-4526-9cb3-e0f3181751a7

動画ファイル本体は [videos/](videos/) にも同梱しています。

v1が「反論させるプロンプト」なら、v2は「**会議そのものを設計させるプロンプト**」。
このリポジトリはさらに一歩進めて、「**会議を用途別のツールにする**」ことを狙っています。

## セットアップ

会議スキルの**正典は `.claude/skills/<スキル名>/SKILL.md`**(ツール非依存の純Markdown)で、
各ツール用の設定はそれを参照する薄いアダプタになっています。

### Claude Code
このフォルダを開くだけです。`CLAUDE.md` と `.claude/` 配下(skills / agents)が自動で読み込まれ、
`/kaigi` などがそのまま使えます。他プロジェクトで使う場合は `.claude/skills/` と `.claude/agents/` をコピー
(`~/.claude/skills/` へ置けば全プロジェクト共通)。

### Codex CLI
`.codex/skills/<スキル名>/SKILL.md` に**フル装備のスキル一式**(参考資料含む)を同梱しています。
プロジェクト指示 `AGENTS.md` も自動で読み込まれるため、リポジトリを開いて「天才会議して」と頼めばそのまま動きます。
スラッシュコマンドとして使う場合は、同梱のプロンプトをコピーしてください:

```bash
mkdir -p ~/.codex/prompts && cp .codex/prompts/*.md ~/.codex/prompts/
```

これで Codex 内から `/kaigi <テーマ>` などが使えます。
(`kaigi-parallel` はサブエージェント非対応環境向けのフォールバック手順入りです)

### Cursor
このリポジトリを開くだけです。`.cursor/commands/`(`/kaigi` などのスラッシュコマンド)と
`.cursor/rules/kaigi-framework.mdc`(会議系依頼で自動適用されるルール)が有効になります。
`AGENTS.md` も読み込まれます。

## 使い方

```
/kaigi 新規SaaSの価格プランを従量課金にすべきか
/kaigi-lite 朝会を面白くするアイデア
/code-kaigi src/auth/ の直近の変更
/arch-kaigi イベント駆動にするかRESTポーリングで済ませるか
/premortem 3ヶ月後、このリリースは大失敗していた。なぜか
/red-team 「マイクロサービス化する」というこの結論を攻撃して
/incident-kaigi 昨日の本番障害(タイムライン貼り付け)
/estimate-kaigi ユーザー招待機能の実装
/naming-kaigi この課金モジュールの名前
/kaigi-parallel 来期のプロダクト戦略(重要判断・並列実行版)
```

## 設計思想(v2の4フェーズ)

```
Phase 0  事前分析     … 本当の論点/思考の罠3つ/利害と因縁を持つキャラ設計
Phase 1  会議の実行   … 弁証法サイクル(テーゼ→アンチテーゼ→ジンテーゼ)を最低3周
Phase 2  自己批判     … 議論されなかった視点/結論の弱点/5人目のキャラ乱入
Phase 3  構造化議事録 … 結論1文/論点ツリー/弁証法の軌跡/意思決定マトリクス/アクション/未解決の問い
```

各スキルはこの骨格を用途別に特殊化しています。詳細は各 `SKILL.md` を参照。

## ファイル構成

```
CLAUDE.md                       Claude Code 用の共通ルール
AGENTS.md                       Codex CLI / その他エージェント用の共通ルール
LICENSE                         MITライセンス
videos/                         紹介動画(日本語/英語/中国語)
.claude/
  skills/                       ★ 会議スキルの正典(ツール非依存Markdown)
    kaigi/                      汎用v2フル版
      SKILL.md
      references/
        v2-prompt.md            原典プロンプト(正典の正典)
        biases.md               思考の罠カタログ(24種+症状+脱出の一言)
        persona-design.md       利害と因縁を持つペルソナ設計法
        dialectic.md            弁証法サイクル実践ガイド
    kaigi-lite/                 v1相当の軽量版
    kaigi-parallel/             サブエージェント並列実行版
    code-kaigi/                 コードレビュー会議
    arch-kaigi/                 アーキテクチャ決定会議(ADR出力)
    premortem/                  プレモータム会議
    red-team/                   結論攻撃・5人目召喚
    incident-kaigi/             障害ふりかえり会議
    estimate-kaigi/             見積もり会議
    naming-kaigi/               命名決定会議
  agents/                       並列会議用ペルソナ(思考プロトコル・罠の自己点検付き)
    kaigi-genius.md             天才役
    kaigi-novice.md             初心者役
    kaigi-optimist.md           ポジティブ役
    kaigi-worrier.md            心配性役
    kaigi-redteam.md            5人目・悪魔の代弁者
    kaigi-facilitator.md        ファシリテーター/議事録係
.codex/
  skills/                       Codex 用スキル一式(.claude/skills と同内容 + 並列版フォールバック)
    kaigi/
      SKILL.md
      references/               参考資料(罠カタログ・ペルソナ設計法・弁証法・原典)
    ...(全10スキル)
  prompts/                      Codex CLI 用カスタムプロンプト(~/.codex/prompts へコピー)
.cursor/
  commands/                     Cursor 用スラッシュコマンド(開くだけで有効)
  rules/
    kaigi-framework.mdc         Cursor 用共通ルール(会議系依頼で自動適用)
```

## ⚠️ 注意

AIの議論を鵜呑みにしないこと。Phase 2 でAI自身が結論を批判しますが、
**「多段階で検証したから正しいはず」と思うことこそが最大の罠**です。
決めるのは、現場を知っている人間です。

## License

MIT License — 詳細は [LICENSE](LICENSE) をご覧ください。
複製・改変・再配布・商用利用、すべて自由です。
