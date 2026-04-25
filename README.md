English | [한국어](README.ko.md)

# nopal-openclaw-skill

An OpenClaw-native Google Workspace orchestration skill modeled after `nopal`.

This version is adapted for OpenClaw environments that already use `gog` for Google Workspace work. It focuses on practical orchestration across:

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

## Notes

- Prefers `gog` first
- Uses `gws` only as an optional fallback for unsupported services
- Designed for natural-language requests like sending mail, scheduling meetings, finding Drive files, summarizing Sheets, and creating Docs
