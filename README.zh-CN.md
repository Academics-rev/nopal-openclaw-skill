[English](README.md) | [한국어](README.ko.md) | 简体中文 | [日本語](README.ja.md)

# nopal-openclaw-skill

这是一个参考 `nopal` 设计、面向 OpenClaw 的 Google Workspace 编排技能。

这个版本针对已经使用 `gog` 处理 Google Workspace 任务的 OpenClaw 环境进行了调整，重点支持以下服务之间的自然语言编排：

- Gmail
- Calendar
- Drive
- Docs
- Sheets
- Contacts

## 文件说明

- `nopal-openclaw/SKILL.md` — 技能说明文件
- `nopal-openclaw/references/recipes.md` — 多步骤工作流参考示例
- `dist/nopal-openclaw.skill` — 打包后的技能文件

## 特点

- 默认优先使用 `gog`
- 仅在服务不受支持时，才将 `gws` 作为补充方案
- 面向自然语言请求而设计，例如发邮件、安排会议、查找 Drive 文件、汇总 Sheets 内容，以及创建 Docs 文档
