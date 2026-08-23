# Kang Daeun

### Backend Developer interested in Financial IT & Reliable Systems

🎓 Computer Engineering @ Dankook University  
📚 **GPA 4.36 / 4.5 · Top of Class**

기능 구현을 넘어 **동시성, 데이터 정합성, 성능, 운영 안정성**을 고민하는 백엔드 개발자를 지향합니다.

특히 실제 사용자가 있는 서비스를 운영하며 발생하는 문제를 재현하고,
측정과 실험을 통해 개선하는 과정에 관심이 있습니다.

---

## 🚀 Featured Projects

### 🎓 [Course Registration Practice System](https://github.com/lab412sugang2/sugang)

**3-person team · Development Contribution 100%**  
**Role:** Backend / Infra / Deployment / Operations

`Java` `Spring Boot` `JPA` `MySQL` `Docker` `Micrometer` `Prometheus` `Grafana` `k6`

실제 사용자 환경에서 운영한 수강신청 연습 서비스입니다.

- Spring Boot 기반 **전체 백엔드 구현**
- 수강신청 비즈니스 로직 및 DB 구조 설계
- 학점 제한 / 시간표 충돌 / 중복 신청 / 폐강 / 정원 초과 검증 구현
- 정원 10명에 100개 동시 요청을 보내 **Race Condition 재현**
- 기존 로직에서 정원 초과 및 신청 카운터 불일치 현상 확인
- 비관적 락 / 낙관적 락 / Conditional UPDATE 방식 비교
- **Conditional UPDATE 기반 원자적 정원 제어 적용**
- 동일 조건에서 `10 success / 90 full rejected / 0 oversubscription` 검증
- 신청 INSERT 실패 시 정원 카운터까지 함께 Rollback되는 트랜잭션 검증
- 동시 중복 신청에 UNIQUE Constraint를 최종 방어선으로 적용
- k6 부하 테스트를 통한 병목 구간 분리 및 성능 측정
- Micrometer / Prometheus / Grafana 기반 모니터링 구축
- 서버 시간 기준 로그인 제어 및 경계 시간 오류 개선
- Docker / Render / Railway / MySQL 환경 배포 및 운영

**Keywords**

`Concurrency` `Transaction` `Data Consistency` `Performance Test` `Monitoring`

---

### 🌏 [TOMO — Cultural Email Copilot](https://github.com/tomo-likelion/tomo-backend)

**Backend 2-person collaboration · Contribution ~85%**

`Python` `FastAPI` `PostgreSQL` `SQLAlchemy` `Alembic` `OpenAI API` `Docker`

수신자의 국가, 언어, 업무 관계를 고려해
이메일의 문화적 위험을 분석하고 적절한 표현을 추천하는 AI 이메일 서비스입니다.

- 수신자 프로필 등록 / 조회 REST API 구현
- OpenAI Responses API 기반 이메일 문화적 맥락 분석
- Structured Outputs를 활용한 구조화된 LLM 응답 처리
- LLM 결과의 위험도 과소평가 문제를 **백엔드 보정 로직**으로 개선
- PostgreSQL 기반 데이터 영속화
- SQLAlchemy 모델 및 Repository 구조 설계
- Alembic 기반 DB Migration 구성
- 외부 LLM 실패 / 환경 설정 오류 / 미등록 사용자 예외 처리
- 운영 DB와 테스트 DB 환경 분리
- 분석 및 위험도 산정 테스트 작성

**6 Pull Requests Merged**

**Keywords**

`LLM Integration` `REST API` `PostgreSQL` `Testing`

---

### 🚑 [SuperSave](https://github.com/Programming-G1/supersave)

**Team Project · Contribution ~40%**

`Java` `Spring Boot` `JPA` `PostgreSQL` `Redis` `Gemini`

실시간 병상 정보와 AI 판단을 활용한
응급실 이송 의사결정 지원 서비스입니다.

- 프론트엔드 정적 리소스와 Spring Boot 백엔드 통합
- 구급대원 이송 요청과 병원 관리자 처리 흐름 구현
- AI 기반 중증도 판단 기능 적용
- 외부 AI 장애 시 fallback 처리
- JPA 기반 이송 데이터 영속화
- MySQL 중심 구조에서 **PostgreSQL / Supabase로 Migration**
- Redis 기반 병원 정보 캐싱 구조 활용
- 실행 환경 및 API 연동 구조 개선

**9 Pull Requests Merged**

---

### 🔐 [HALO](https://github.com/hell-course/halo)

**Team Project · Contribution ~55%**

`Java` `Spring Boot` `Spring Security` `JWT` `PostgreSQL` `pgvector` `Gemini`

AI를 활용해 아이디어와 유사한 서비스를 탐색하고
시장조사를 지원하는 서비스입니다.

- Spring Security + JWT 기반 회원가입 / 로그인 구현
- BCrypt 기반 비밀번호 암호화
- 인증이 필요한 API 접근 제어
- Gemini 기반 시장 분석 기능 구현
- 외부 API 직접 연동 및 JSON 응답 처리
- 실패 상황을 고려한 fallback 처리
- Embedding 생성 및 Vector Search 기능 구현
- PostgreSQL / pgvector 기반 유사 서비스 검색
- API Key 환경변수 분리

**4 Pull Requests Merged**

---

## 🌱 Open Source Contribution

### [Micrometer](https://github.com/micrometer-metrics/micrometer)

Spring 생태계에서 널리 사용되는 Metrics Facade인
**Micrometer 공식 프로젝트에 기여했습니다.**

🔗 [PR #7241 — StatsD Unix Domain Socket configuration guide](https://github.com/micrometer-metrics/micrometer/pull/7241)

- 기존 Issue #5730 기반으로 문제 파악
- StatsD Registry의 Unix Domain Socket 설정 방법 문서화
- Java 설정 예제 추가
- Spring Boot `application.yml` 설정 예제 추가
- **Merged into upstream**

---

## 🛠 Tech Stack

### Backend

`Java` `Spring Boot` `Spring Data JPA` `Spring Security`  
`Python` `FastAPI`

### Database

`MySQL` `PostgreSQL` `Redis`

### Infrastructure & Monitoring

`Docker` `Render` `Railway`  
`Micrometer` `Prometheus` `Grafana` `k6`

### AI / Data

`OpenAI API` `Gemini API`  
`SQLAlchemy` `pgvector`

---

## 📚 Current Focus

- Financial IT Backend
- Database Transaction & Concurrency Control
- Data Consistency
- Spring Backend Architecture
- Performance Testing & Monitoring
- Algorithms & Data Structures
- Automated Trading System Development

---

> **Building backend systems that stay correct under real-world load.**
