# 시스템 아키텍처

> 1회차 산출물. LLM·Vector DB·AI 서비스 분리 여부가 정해지면 갱신합니다 ([project-context.md](../project-context.md) 4절).

```
[React FrontEnd] --REST--> [Spring Boot API + Spring AI Agent] --> [RDB]
                                   |-- Tool 실행 (분류·현금흐름·시뮬레이션·상품비교)
                                   |-- RAG 검색 --> [Vector DB]  (FastAPI 분리 여부 미정)
                                   |-- LLM 호출 --> [LLM]        (Ollama / 외부 API 미정)
                                   `-- Audit Log
```
