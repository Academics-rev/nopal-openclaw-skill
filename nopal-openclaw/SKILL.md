---
name: nopal-openclaw
description: "OpenClaw-native Google Workspace orchestrator modeled after nopal. Use when the user wants natural-language Google work across Gmail, Calendar, Drive, Docs, Sheets, Contacts, or chained Google workflows in this OpenClaw environment. Prefer gog first, and use gws only if it is installed and a required service is unsupported by gog. Strong triggers include: 메일 보내줘, 읽지 않은 메일 확인, 답장 초안 써줘, 오늘 일정 알려줘, 회의 잡아줘, 캘린더 일정 추가해줘, 회의록 문서 만들어줘, 드라이브 파일 찾아줘, 파일 업로드해줘, 링크 공유해줘, 시트 읽어서 요약해줘, 스프레드시트 만들어줘, 보고서 만들고 메일로 보내줘, nopal처럼 해줘, 구글 워크스페이스 작업해줘, send email, check calendar, create meeting, find Drive file, summarize sheet, create doc, share link."
---

# Nopal for OpenClaw

Use this skill as the practical OpenClaw version of nopal for this workspace.

## Core rule

- Prefer `gog` first in this environment.
- Use `gws` only if it is already installed/authenticated **and** the requested service is unsupported or clearly weaker in `gog`.
- Do not ask the user to choose between `gog` and `gws` unless that choice changes what is possible.

## Auto-trigger cues

This skill should trigger aggressively for natural-language Google Workspace requests, especially when the user asks to:

- read, search, summarize, draft, send, reply to, or organize **Gmail**
- check, create, update, cancel, or find **Calendar** events
- find, upload, move, rename, download, share, or link **Drive** files
- create, read, write, edit, export, or share **Docs**
- create, read, update, append, format, or summarize **Sheets**
- combine two or more Google actions in one request

Typical trigger phrases:

- "메일 보내줘"
- "읽지 않은 메일 확인해줘"
- "답장 초안 써줘"
- "오늘 일정 알려줘"
- "내일 회의 잡아줘"
- "회의록 문서 만들고 공유해줘"
- "드라이브에서 파일 찾아서 링크 보내줘"
- "시트 읽어서 요약해줘"
- "보고서 문서 만들고 메일로 보내줘"

## Service coverage in this environment

### Strong with `gog`

- Gmail
- Calendar
- Drive
- Docs
- Sheets
- Contacts

### Attempt only if `gws` exists and is healthy

- Slides
- Chat
- Tasks
- Meet-only features not covered well by `gog`

If a requested service falls in the second group and `gws` is unavailable, explain that clearly and offer the closest workable alternative.

## Tool choice by task

| Task type | Default path |
|---|---|
| 읽지 않은 메일/최근 메일 확인 | `gog gmail search` or `gog gmail messages search` |
| 메일 발송/초안/답장 | `gog gmail send` / `gog gmail drafts` |
| 일정 조회/검색 | `gog calendar events` / `gog calendar search` |
| 일정 생성/수정/취소 | `gog calendar create` / `gog calendar update` / `gog calendar delete` |
| 드라이브 파일 찾기/공유/링크 | `gog drive search` / `gog drive share` / `gog drive url` |
| 파일 업로드/폴더 생성 | `gog drive upload` / `gog drive mkdir` |
| 문서 생성/쓰기/편집 | `gog docs create` / `gog docs write` / `gog docs edit` |
| 시트 생성/조회/추가/수정 | `gog sheets create` / `get` / `append` / `update` |
| 복합 Google 워크플로 | `gog` 조합 우선, 필요 시 `gws` 보조 |

For multi-step Google requests, also read `references/recipes.md`.

## Workflow

### 1. Parse the request

Determine:
- which Google services are needed
- whether the task is read-only or write/modification
- whether the task is single-service or multi-step
- whether the user already specified account, recipients, file, time, or destination

Examples:
- "오늘 일정 알려줘" → Calendar, read-only
- "회의 잡고 참석자에게 메일 보내줘" → Calendar + Gmail, write + multi-step
- "드라이브에서 보고서 찾아서 링크 보내줘" → Drive + Gmail, mixed multi-step
- "시트 읽어서 보고서 문서 초안 만들어줘" → Sheets + Docs, mixed multi-step

### 2. Resolve obvious defaults quietly

Use sensible defaults instead of asking too much.

- default calendar: `primary`
- default meeting length: 1 hour
- default email format: plain text
- default Drive share role: `reader`
- default account: resolve from context and saved aliases first

Do not ask for values the user already implied.

### 3. Ask only for true gaps

Ask only when the task cannot be completed safely without more information, such as:
- recipient missing for email or sharing
- ambiguous target file/document/sheet
- unclear meeting time/date
- destructive action scope unclear
- account choice cannot be inferred from context

Good examples:
- "어느 파일을 보내면 될까요? 후보가 2개 있습니다."
- "받는 사람 이메일 주소를 알려주세요."
- "회의 시간을 1시간으로 잡아도 될까요?"

### 4. Read vs write rule

- Read-only queries can run immediately.
- Any action that sends, creates, edits, updates, shares, uploads, renames, moves, trashes, or deletes must be confirmed first.
- For multi-step write actions, show a short execution plan before running.

Good confirmation format:

- 실행 예정:
  1. 문서 생성
  2. 본문 작성
  3. 공유 링크 생성
  4. 메일 발송
- 이대로 진행할까요?

### 5. Execute in stable order

Typical order:
1. read/search source data
2. create or update artifacts
3. share or send notifications last

Common chains:
- Calendar → Docs/Drive → Gmail
- Drive → Gmail
- Sheets → Docs → Gmail
- Drive upload → share → URL → Gmail

## Fast paths for common requests

### Gmail-only

Use for:
- unread mail summary
- sender-based search
- reply draft creation
- follow-up email sending

Prefer:
- `gog gmail messages search` when per-message output matters
- `gog gmail search` when thread-level summary is enough
- `gog gmail drafts create` if the user wants review before send

### Calendar-only

Use for:
- today/tomorrow agenda
- create or move meetings
- conflict checking
- RSVP or cancellation

Prefer `gog calendar create` with explicit `--from` and `--to` values.
If attendees should receive invitations, use the appropriate update/notification flags.

### Drive + Gmail

Use for:
- find a file, create a share link, and email it
- upload a local file and notify someone
- shortlist candidate files before asking the user to pick one

### Docs + Drive + Gmail

Use for:
- create a Google Doc
- write the requested content
- share with viewer/writer permissions
- send the link or summary by email

### Sheets + Docs + Gmail

Use for:
- read a range or tab
- summarize the key numbers/findings
- optionally create a doc report
- optionally email the summary or link

## Practical rules

- Prefer `--json` when available and parse the result instead of scraping plain text.
- Resolve saved account aliases from context before asking again.
- If the user already named the target account, do not re-ask.
- If multiple search candidates appear, provide a short shortlist rather than raw dump.
- If the user asks to “send” but review is prudent, offer draft-first as the safer option.
- If a task crosses Gmail + Calendar + Drive/Docs/Sheets, treat it as an orchestration task, not as isolated single commands.

## When to use the installed upstream nopal bundle vs this skill

- Use **this skill** for actual OpenClaw execution in this environment.
- Treat the installed upstream `nopal` Claude bundle as a reference source, not the direct runtime contract.
- Do not rely on Claude-only slash-command behavior or `AskUserQuestion` patterns here.

## Output style

Be concise and operational.

For read tasks:
- summary first
- important bullets next
- offer one useful follow-up if helpful

For write tasks:
- short plan
- explicit confirmation
- execution result summary
- links or IDs only when useful to the user
