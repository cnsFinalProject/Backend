# FinAgent 프로젝트 컨텍스트 (AI·신규 팀원 공통 기준 문서)

> 이 문서가 **기획의 단일 기준(Single Source of Truth)** 입니다.
> 기획이 바뀌면 코드보다 이 문서를 먼저 고치고, 맨 아래 "변경 이력"에 한 줄 남깁니다.
> AI 도구(Claude Code, Codex, Cursor, Copilot)는 모든 레포의 `AGENTS.md`를 통해 이 문서를 읽습니다.

## 상태 표기
| 표기 | 뜻 | AI가 할 일 |
| --- | --- | --- |
| ✅ 확정 | 팀·멘토가 합의함 | 그대로 따른다 |
| 🟡 가안 | 현재 방향이지만 바뀔 수 있음 | 따르되, 바꾸기 쉬운 구조로 만든다 (인터페이스·설정으로 분리) |
| ⬜ 미정 | 아직 안 정함 | **임의로 정하지 말고** 사용자에게 묻거나 `TODO(결정필요)`로 남긴다 |

## 1. 한 줄 소개
- ✅ 프로젝트명: **FinAgent — Agentic AI 기반 금융 생활 코치 서비스**
- ✅ 과정: LG CNS AM Inspire Camp 6기 최종 프로젝트 (금융 도메인, 멘토: 정상덕)
- ✅ 페르소나: 사회초년생·직장인
- ⬜ 차별점: 기존 서비스 pain-point 조사 후 작성 (11/20 확정 예정)

## 2. 범위
| 구분 | 내용 | 상태 |
| --- | --- | --- |
| 포함 | 거래내역 CSV 분석, 예산·저축 목표, 금융상품 탐색, 금융 FAQ/RAG 응답 | ✅ |
| 제외 | 실제 계좌 연동, 실거래, 투자 권유, 신용평가 자동 결정 | ✅ |
| 데이터 | Mock 거래내역, 상품 메타데이터, 약관·FAQ 샘플, 금융 용어 사전 | 🟡 수집처 미정 |

## 3. Agent 흐름
```
사용자 질문 → 질문 분류(Planner) → Tool 선택·실행 → RAG 근거 확인
           → 응답 생성(근거·한계·고지 표시) → Audit Log 기록
```

| Tool | 목적 | 상태 |
| --- | --- | --- |
| `classify_transactions` | 거래 분류 | 🟡 |
| `analyze_cashflow` | 현금 흐름 분석 | 🟡 |
| `retrieve_finance_docs` | 금융 문서 검색(RAG) | 🟡 |
| `compare_products` | 상품 비교 | 🟡 |
| `simulate_saving_goal` | 저축 목표 시뮬레이션 | 🟡 |
| `risk_notice_checker` | 위험 표현·고지 점검 | ⬜ Tool로 둘지, 모든 응답 후처리로 둘지 미정 |

상세 입출력은 [agent/tool-명세서.md](agent/tool-명세서.md).

## 4. 기술 스택
| 영역 | 기술 | 상태 |
| --- | --- | --- |
| Frontend | React (TypeScript 여부 미정) | 🟡 |
| Backend | Spring Boot, Spring AI | ✅ 멘토 필수 |
| AI 서비스 | FastAPI 별도 서비스 여부 | ⬜ Spring AI만으로 갈지 결정 필요 |
| LLM | Ollama(로컬) vs 외부 LLM API | ⬜ 멘토 질문 중 |
| Embedding / Vector DB | 후보 비교 후 2회차에 선정 | ⬜ |
| RDB | PostgreSQL 또는 MySQL | ⬜ |
| API 문서 | Swagger / OpenAPI | ✅ |
| Infra | Docker, GitHub Actions, 클라우드(AWS 예상) | 🟡 |
| 협업 | GitHub Issues/Projects, Jira, Notion, Figma | 🟡 |

## 5. 레포 구성
| 레포 | 역할 |
| --- | --- |
| `Backend` | 업무 API(`backend/`), AI 서비스(`ai/`), 인프라(`infra/`), 데이터(`data/`), **모든 기획·설계 문서(`docs/`)** |
| `FrontEnd` | React 화면 |
| `config-repo` | Config Server 설정 파일 (`서비스이름-프로필.yml`) |
| `.github` | 조직 소개, 공통 이슈·PR 템플릿 |

## 6. 팀과 역할
| 역할 | 담당 | 맡는 레포·폴더 | 상태 |
| --- | --- | --- | --- |
| 팀장 | 손호성 | 전체 일정·의사결정, 레포·브랜치 보호 관리 | ✅ |
| PM | 진성민 | `Backend/docs/` (기획·요구사항·WBS·회의록), 이슈·Projects 보드 | ✅ |
| FE | 진성민, 탁유진 | `FrontEnd` 레포 | ✅ |
| BE | 이우진, 손수연, 최다인, 현준혁 | `Backend/backend/`, `Backend/ai/`, `Backend/data/` | ✅ |
| 클라우드 | 곽호윤 | `Backend/infra/`, `config-repo`, GitHub Actions·Secrets | ✅ |

- ⬜ BE 4명 안의 세부 분담(Agent·Tool, RAG·AI, 업무 API, 데이터)은 미정. 정해지면 이 표에 적는다.
- PR 리뷰어는 해당 폴더 담당자 중 1명 이상을 지정한다. 문서(`docs/`) 변경은 PM, `infra/`·`config-repo` 변경은 클라우드 담당이 승인한다.

## 7. 마일스톤
| 회차 | 날짜 | 목표 | 산출물 |
| --- | --- | --- | --- |
| 1 | 11.14 | 상세 기획 | 요구사항·수행계획·Tool 명세 초안, 아키텍처 초안 |
| 2 | 11.28 | 기본 연동 | FE/BE 개발 가이드, Swagger 초안, Greeting + 단일 Tool Demo |
| 3 | 12.12 | 핵심 기능 | Tool 기능 Demo, Swagger 보완, 화면 기획, 중간 발표 |
| 4 | 12.19 | 통합·품질 | 통합 Demo, 테스트 시나리오·결과 초안 |
| 5 | 01.16 | 마무리 | 최종 Demo, 발표자료, 테스트 결과서, 운영 가이드 |

## 8. 절대 규칙 (금융 도메인)
1. 모든 Agent 응답에 **"투자 권유가 아님"** 고지를 붙인다.
2. 금액 계산·집계는 **LLM이 아니라 코드(Tool)** 가 한다. LLM은 결과를 설명만 한다.
3. 실제 개인정보·계좌번호를 쓰지 않는다. Mock 데이터만 쓰고, 로그에는 마스킹한다.
4. RAG 근거가 없으면 지어내지 않고 "근거 없음"이라고 답한다.
5. API 키·DB 비밀번호는 `.env`/Secrets로만 관리하고 커밋하지 않는다.

## 9. 미결정 사항 (멘토·팀 확인 필요)
- [ ] Ollama 사용 가능 여부
- [ ] AI 서비스를 FastAPI로 분리할지
- [ ] Vector DB·Embedding 모델 선정
- [ ] RDB 선정
- [ ] 데이터 수집처 (리서치 기관, 공공데이터 등)
- [ ] 서비스 차별점 (11/20)
- [ ] `risk_notice_checker` 적용 방식

## 변경 이력
| 날짜 | 바뀐 내용 | 작성 |
| --- | --- | --- |
| 2026-11-14 | 최초 작성 (멘토 계획서·1회차 초안 기준) | 손호성 |
| 2026-11-16 | 팀 구조 확정: 팀장 손호성, PM 진성민, BE 4명(현준혁 포함), 클라우드 곽호윤 | 손호성 |
