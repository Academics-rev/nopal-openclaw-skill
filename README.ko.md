[English](README.md) | 한국어 | [简体中文](README.zh-CN.md) | [日本語](README.ja.md)

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

## 설치 방법

### 사전 준비

- OpenClaw 설치
- `gog` 설치 및 인증 완료

### 현재 워크스페이스에 설치

```bash
git clone https://github.com/Academics-rev/nopal-openclaw-skill.git
mkdir -p ~/.openclaw/workspace/skills
cp -r nopal-openclaw-skill/nopal-openclaw ~/.openclaw/workspace/skills/
```

설치 후에는 OpenClaw가 스킬을 읽도록 **새 세션을 시작**하면 됩니다.

### 공용 로컬 스킬로 설치

```bash
git clone https://github.com/Academics-rev/nopal-openclaw-skill.git
mkdir -p ~/.openclaw/skills
cp -r nopal-openclaw-skill/nopal-openclaw ~/.openclaw/skills/
```

이 방식은 같은 컴퓨터에서 여러 워크스페이스나 에이전트가 함께 재사용할 때 적합합니다.

### `.skill` 파일에 대해

저장소에 `dist/nopal-openclaw.skill` 파일도 포함돼 있지만, OpenClaw에서는 보통 `skills/` 아래의 **스킬 폴더 자체를 직접 읽는 방식**으로 사용합니다.

## 실사용 예시

```text
오늘 일정 알려줘
읽지 않은 메일 중 중요한 것만 요약해줘
드라이브에서 회의록 찾아서 링크 보내줘
회의록 문서 만들고 팀원에게 공유해줘
이 시트 읽어서 짧은 보고서 문서로 정리해줘
```

## 특징

- 기본적으로 `gog`를 우선 사용합니다.
- 필요한 경우에만 `gws`를 보조적으로 사용합니다.
- 메일 발송, 일정 생성, 드라이브 파일 찾기, 시트 요약, 문서 작성 같은 자연어 요청에 맞춰 설계했습니다.
