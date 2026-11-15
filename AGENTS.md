# AGENTS.md — FinAgent Backend 레포 AI 작업 가이드

이 파일은 Claude Code, Codex, Cursor, Copilot 등 AI 코딩 도구가 가장 먼저 읽는 규칙입니다.
사람 팀원도 같은 내용을 따릅니다.

## 0. 작업 전에 반드시 읽을 것
1. [docs/project-context.md](docs/project-context.md) — 기획 기준. ✅확정 / 🟡가안 / ⬜미정 표기를 확인한다.
2. [docs/협업규칙.md](docs/협업규칙.md) — 브랜치·커밋·PR 규칙.
3. 작업과 관련된 문서: 요구사항(`docs/requirements/`), Tool 명세(`docs/agent/`), API(`docs/api/`), 데이터(`docs/data/`).

## 1. 기획 변경에 대비하는 원칙
- ⬜미정 항목(LLM 종류, Vector DB, RDB 등)은 **임의로 정하지 않는다.** 사용자에게 묻거나 `TODO(결정필요): ...`로 남긴다.
- 🟡가안 항목은 갈아끼우기 쉽게 만든다: LLM·Vector DB·외부 API는 인터페이스 뒤에 두고, 구현체는 설정(`application-{profile}.yml`, `.env`)으로 고른다.
- 요구사항·Tool 명세에 없는 기능을 새로 만들지 않는다. 필요하면 문서 수정부터 제안한다.
- 문서와 코드가 다르면 코드를 고치기 전에 사용자에게 알린다.

## 2. 폴더 구조
```
backend/    Spring Boot 업무 API (Spring AI로 Agent·Tool Calling·Audit Log)
ai/         (가안) FastAPI AI 서비스 — RAG·임베딩. Spring AI만 쓰기로 하면 비운다
infra/      docker-compose, 배포 설정
data/       sample/ Mock 데이터, eval/ 평가 정답셋, 전처리 스크립트. 원본은 data/raw/ (커밋 금지)
docs/       기획·설계 문서 전부
```

| docs 폴더 | 내용 |
| --- | --- |
| `project-context.md` | 기획 단일 기준 (확정/가안/미정) |
| `협업규칙.md` | 브랜치·커밋·PR·리뷰 |
| `planning/` | 수행 계획서, WBS |
| `requirements/` | 요구사항 정의서 (FR-xx, NFR-xx) |
| `agent/` | Agent Tool 명세서, 프롬프트 |
| `architecture/` | 시스템 아키텍처 |
| `api/` | API 명세 (Swagger 보조 설명) |
| `data/` | 테이블·데이터셋 명세, 보안 가이드 |
| `decisions/` | 의사결정 기록 (ADR) |
| `meetings/` | 스크럼·멘토링 회의록 |
| `retro/` | 회차별 회고 |

## 3. 코드 규칙 (금융 도메인)
- 금액 계산·집계·시뮬레이션은 **코드(Tool)** 에서 한다. LLM이 만든 숫자를 그대로 믿지 않는다.
- 금액은 `BigDecimal`(Java) / `Decimal`(Python)을 쓴다. `double`/`float` 금지.
- Agent 응답에는 근거(RAG 출처)와 "투자 권유가 아님" 고지를 포함한다.
- 로그·프롬프트에 개인정보(이름, 계좌번호, 전화번호)를 남기지 않는다. 필요하면 마스킹한다.
- 비밀 값은 `.env` / 환경 변수로만. 새 설정을 추가하면 `.env.example`에 키 이름만 추가한다.
- 새 Tool을 만들거나 바꾸면 `docs/agent/tool-명세서.md`의 입력·출력·호출 조건을 같이 고친다.
- API를 바꾸면 Swagger 주석과 `docs/api/`를 같이 고치고, FrontEnd 레포에 영향이 있으면 PR 본문에 적는다.

## 4. Git 규칙 요약
- 브랜치: `feat|fix|refactor|docs|chore/WBS번호-영문-작업명` (예: `feat/2.3.1-cashflow-api`), `develop`에서 분기.
- 커밋: `[Add|Fix|Refactor|Docs]_WBS번호/요약` + 다음 줄부터 `- 변경 내용`.
- PR: `develop` 대상, 본문에 `Closes #이슈번호` 필수, PR 1개 = 이슈 1개.
- `main`/`develop`에 직접 push, force push 금지. AI는 사용자가 시킬 때만 커밋·push 한다.

## 5. AI에게 시킬 때 좋은 요청 예시
- "docs/agent/tool-명세서.md 의 analyze_cashflow 명세대로 Spring AI Tool을 만들어줘. WBS 2.3.1."
- "project-context.md 기준으로 ⬜미정인 부분은 TODO로 남기고 나머지만 구현해줘."
- "이번 변경을 협업규칙 형식의 커밋 메시지와 PR 본문으로 써줘."
