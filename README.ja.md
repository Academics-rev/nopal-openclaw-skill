[English](README.md) | [한국어](README.ko.md) | [简体中文](README.zh-CN.md) | 日本語

# nopal-openclaw-skill

`nopal` を参考にして作られた、OpenClaw 向けの Google Workspace オーケストレーションスキルです。

このバージョンは、すでに `gog` を使って Google Workspace を扱っている OpenClaw 環境向けに調整されており、次のサービスを自然言語で連携させることを重視しています。

- Gmail
- Calendar
- Drive
- Docs
- Sheets
- Contacts

## ファイル構成

- `nopal-openclaw/SKILL.md` — スキル本体の説明
- `nopal-openclaw/references/recipes.md` — 複数ステップのワークフロー例
- `dist/nopal-openclaw.skill` — 配布用にパッケージ化したスキルファイル

## 特徴

- 基本的に `gog` を優先して使います
- 未対応のサービスに限って `gws` を補助的に使います
- メール送信、会議の予定作成、Drive ファイル検索、Sheets の要約、Docs の作成といった自然言語リクエストを想定して設計しています
