# backend

담당: BE (이우진, 손수연, 최다인, 현준혁)

업무 API입니다. Spring Boot와 Spring AI로 만들고, Agent의 Tool Calling과 Audit Log를 담당합니다.

프로젝트 생성은 2회차 멘토링(11.28) 전에 API 명세 초안을 정한 뒤 진행합니다.

## 정해 둘 것
- 패키지 구조 (예: `com.finagent.{도메인}.{controller,service,repository,dto}`, `com.finagent.agent.tool`)
- LLM·Vector DB 구현체는 인터페이스로 분리하고 `application-{profile}.yml`에서 선택
- 설정 파일은 [config-repo](https://github.com/cnsFinalProject/config-repo)의 `backend-{profile}.yml`
