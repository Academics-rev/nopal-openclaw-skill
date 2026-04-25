[English](README.md) | 한국어

# nopal-openclaw-skill

`nopal`을 참고해 만든 **OpenClaw용 Google Workspace 오케스트레이션 스킬**입니다.

이 버전은 이미 `gog`를 쓰고 있는 OpenClaw 환경에 맞춰 조정되어 있으며, 다음 작업을 자연어로 연결하는 데 초점을 둡니다.

- Gmail
- Calendar
- Drive
- Docs
- Sheets
- Contacts

## 파일 구성

- `nopal-openclaw/SKILL.md` — 스킬 본문
- `nopal-openclaw/references/recipes.md` — 복합 작업 레시피
- `dist/nopal-openclaw.skill` — 배포용 패키지 파일

## 특징

- 기본적으로 `gog`를 우선 사용합니다.
- 필요한 경우에만 `gws`를 보조적으로 사용합니다.
- 메일 발송, 일정 생성, 드라이브 파일 찾기, 시트 요약, 문서 작성 같은 자연어 요청에 맞춰 설계했습니다.
