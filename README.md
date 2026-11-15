# FinAgent — Agentic AI 기반 금융 생활 코치

LG CNS AM Inspire Camp 6기 최종 프로젝트 금융 도메인 팀 레포입니다. 멘토는 정상덕 멘토님입니다.

사회초년생·직장인이 거래내역을 올리면 Agent가 지출을 진단하고, 저축 목표를 시뮬레이션하고, 금융상품과 FAQ를 근거와 함께 안내합니다. 실제 계좌 연동과 투자 권유는 하지 않습니다.

> 기획은 바뀔 수 있습니다. 최신 기준은 항상 [docs/project-context.md](docs/project-context.md)입니다.

## 기술 스택 (멘토 계획서 기준, 확정 시 조정)

| 영역 | 기술 |
| --- | --- |
| Frontend | React ([FrontEnd](https://github.com/cnsFinalProject/FrontEnd) 레포) |
| Backend | Spring Boot, Spring AI |
| AI | LLM, Embedding, Vector DB, RAG (세부 미정) |
| DB | RDB (미정) |
| Infra | Docker, GitHub Actions, 클라우드 |

## 폴더 구조

```
backend/    업무 API (Spring Boot)
ai/         AI 서비스 (분리 여부 미정)
infra/      docker-compose, 배포 설정
data/       Mock 샘플, 평가 정답셋, 전처리 스크립트 (원본·개인정보는 커밋하지 않음)
docs/       기획·설계 문서, 협업 규칙
```

API 규격이 바뀔 때 BE·AI·문서를 한 PR에서 같이 고칠 수 있도록 서버 쪽과 문서는 이 레포 하나에서 관리합니다.

## 처음 합류했다면

1. [docs/project-context.md](docs/project-context.md) — 무엇을 만드는지, 무엇이 확정이고 무엇이 미정인지
2. [docs/협업규칙.md](docs/협업규칙.md) — 브랜치, 커밋, PR, 리뷰 규칙
3. [AGENTS.md](AGENTS.md) — AI 도구(Claude Code, Codex, Cursor, Copilot)가 자동으로 읽는 작업 규칙. 레포를 clone해서 AI를 레포 루트에서 실행하면 따로 설명하지 않아도 됩니다.

## 로컬 실행

서비스 코드가 올라오면 `infra/`의 docker-compose 기준으로 채웁니다.

## 팀

| 역할 | 팀원 | 담당 |
| --- | --- | --- |
| 팀장 | 손호성 | 일정·의사결정 |
| PM | 진성민 | `docs/`, 이슈·보드 |
| FE | 진성민, 탁유진 | [FrontEnd](https://github.com/cnsFinalProject/FrontEnd) |
| BE | 이우진, 손수연, 최다인, 현준혁 | `backend/` `ai/` `data/` |
| 클라우드 | 곽호윤 | `infra/`, [config-repo](https://github.com/cnsFinalProject/config-repo) |
