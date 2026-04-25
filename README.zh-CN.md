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

## 安装方法

### 前提条件

- 已安装 OpenClaw
- 已安装并完成 `gog` 认证

### 安装到当前工作区

```bash
git clone https://github.com/Academics-rev/nopal-openclaw-skill.git
mkdir -p ~/.openclaw/workspace/skills
cp -r nopal-openclaw-skill/nopal-openclaw ~/.openclaw/workspace/skills/
```

安装完成后，建议重新开启一个 OpenClaw 会话，让新技能被正确加载。

### 作为本机共享技能安装

```bash
git clone https://github.com/Academics-rev/nopal-openclaw-skill.git
mkdir -p ~/.openclaw/skills
cp -r nopal-openclaw-skill/nopal-openclaw ~/.openclaw/skills/
```

如果你希望同一台机器上的多个工作区或多个代理共用这个技能，可以使用这种方式。

### 关于 `.skill` 文件

仓库中也包含 `dist/nopal-openclaw.skill`，用于打包和分发；不过在 OpenClaw 中，通常直接从 `skills/` 目录读取技能文件夹。

## 使用示例

```text
告诉我今天的日程
帮我总结未读邮件里重要的内容
在 Drive 里找到会议纪要并把链接发给我
创建一份会议纪要文档并分享给团队
读取这个表格，并整理成一份简短的报告文档
```

## 特点

- 默认优先使用 `gog`
- 仅在服务不受支持时，才将 `gws` 作为补充方案
- 面向自然语言请求而设计，例如发邮件、安排会议、查找 Drive 文件、汇总 Sheets 内容，以及创建 Docs 文档
