# Nopal OpenClaw Recipes

Read this file when the request spans **two or more Google services** or needs a short execution plan before running.

## 1. unread-mail-summary

**Use when:**
- "읽지 않은 메일 확인해줘"
- "최근 메일 중 중요한 것만 요약해줘"

**Pattern:**
1. Search recent unread mail
2. If needed, switch from thread search to message search
3. Summarize only the important items

**Typical commands:**
- `gog gmail search 'is:unread newer_than:7d' --max 10`
- `gog gmail messages search 'is:unread newer_than:7d' --max 20`

## 2. schedule-and-notify

**Use when:**
- "내일 회의 잡아줘"
- "회의 만들고 참석자에게 안내 메일 보내줘"

**Pattern:**
1. Confirm date/time/attendees if missing
2. Create calendar event
3. If requested, send a separate email with agenda or notes

**Typical commands:**
- `gog calendar create primary --summary '팀 회의' --from <iso> --to <iso> --attendees a@b.com,c@d.com --with-meet --send-updates all`
- `gog gmail send --to a@b.com --subject '회의 안내' --body-file ./message.txt`

## 3. create-doc-and-share

**Use when:**
- "회의록 문서 만들어줘"
- "보고서 초안 문서 만들고 공유해줘"

**Pattern:**
1. Create a Google Doc
2. Write the initial content
3. Share it with the requested permission
4. Return the doc link or email it if requested

**Typical commands:**
- `gog docs create '회의록 초안' --json`
- `gog docs write <docId> --file ./draft.md`
- `gog drive share <fileId> --to=user --email someone@example.com --role writer`
- `gog drive url <fileId>`

## 4. find-drive-file-and-send-link

**Use when:**
- "드라이브에서 파일 찾아줘"
- "파일 링크를 메일로 보내줘"

**Pattern:**
1. Search Drive
2. If multiple candidates exist, shortlist them
3. Share if needed
4. Get URL
5. Send link by email if requested

**Typical commands:**
- `gog drive search 'Quarterly Report' --max 10`
- `gog drive share <fileId> --to=user --email recipient@example.com --role reader`
- `gog drive url <fileId>`
- `gog gmail send --to recipient@example.com --subject '파일 링크' --body '링크: ...'`

## 5. sheet-summary-to-doc

**Use when:**
- "시트 읽어서 요약해줘"
- "시트 내용을 보고 보고서 문서 만들어줘"

**Pattern:**
1. Read the relevant range or metadata
2. Summarize the important numbers or rows
3. If requested, create a Doc and write the summary there
4. Share or send after confirmation

**Typical commands:**
- `gog sheets metadata <sheetId> --json`
- `gog sheets get <sheetId> 'Tab!A1:D20' --json`
- `gog docs create '요약 보고서' --json`
- `gog docs write <docId> --file ./summary.txt`

## 6. upload-and-share

**Use when:**
- "이 파일 드라이브에 올려줘"
- "업로드하고 링크 보내줘"

**Pattern:**
1. Upload file to Drive
2. Move or place into the target folder if needed
3. Share with the requested audience
4. Return or send the URL

**Typical commands:**
- `gog drive upload ./local-file.pdf --json`
- `gog drive share <fileId> --to=user --email recipient@example.com --role reader`
- `gog drive url <fileId>`

## 7. sheet-create-and-fill

**Use when:**
- "스프레드시트 만들어줘"
- "표 만들고 데이터 넣어줘"

**Pattern:**
1. Create spreadsheet
2. Add headers or initial rows
3. Update formatting or additional ranges if needed
4. Share if requested

**Typical commands:**
- `gog sheets create '프로젝트 현황' --sheets Summary,Raw --json`
- `gog sheets append <sheetId> 'Summary!A1:C' --values-json '[["항목","상태","메모"]]'`
- `gog drive share <sheetId> --to=user --email recipient@example.com --role writer`

## 8. draft-first-email

**Use when:**
- the user wants a send action but review is likely useful
- the content is sensitive or long

**Pattern:**
1. Draft instead of send
2. Show summary of draft contents
3. Send only after explicit approval

**Typical commands:**
- `gog gmail drafts create --to recipient@example.com --subject '초안' --body-file ./draft.txt`
- `gog gmail drafts send <draftId>`
