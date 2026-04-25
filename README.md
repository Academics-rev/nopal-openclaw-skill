English | [한국어](README.ko.md) | [简体中文](README.zh-CN.md) | [日本語](README.ja.md)

# nopal-openclaw-skill

An OpenClaw-native Google Workspace orchestration skill modeled after `nopal`.

This version is adapted for OpenClaw environments that already use `gog` for Google Workspace tasks. It focuses on practical orchestration across:

- Gmail
- Calendar
- Drive
- Docs
- Sheets
- Contacts

## Files

- `nopal-openclaw/SKILL.md` — main skill instructions
- `nopal-openclaw/references/recipes.md` — multi-step workflow recipes
- `dist/nopal-openclaw.skill` — packaged skill bundle

## Installation

### Prerequisites

- OpenClaw
- `gog` installed and authenticated

### Install into the current workspace

```bash
git clone https://github.com/Academics-rev/nopal-openclaw-skill.git
mkdir -p ~/.openclaw/workspace/skills
cp -r nopal-openclaw-skill/nopal-openclaw ~/.openclaw/workspace/skills/
```

Then start a new OpenClaw session so the skill is picked up.

### Install as a shared local skill

```bash
git clone https://github.com/Academics-rev/nopal-openclaw-skill.git
mkdir -p ~/.openclaw/skills
cp -r nopal-openclaw-skill/nopal-openclaw ~/.openclaw/skills/
```

Use this path if you want multiple workspaces or agents on the same machine to reuse the skill.

### Note about `.skill`

The repository includes `dist/nopal-openclaw.skill` for packaging and sharing, but OpenClaw uses the skill folder directly from `skills/`.

## Example requests

```text
check today's calendar
summarize the important unread emails
find the meeting notes in Drive and send me the link
create a meeting notes doc and share it with the team
read this sheet and turn it into a short report doc
```

## Notes

- Prefers `gog` first
- Uses `gws` only as an optional fallback for unsupported services
- Designed for natural-language requests such as sending mail, scheduling meetings, finding Drive files, summarizing Sheets, and creating Docs
