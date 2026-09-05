<div align="center">

# 👋 Kang Daeun

### Backend Developer · Financial IT · Reliable Systems

**“실제 사용 환경에서 발생하는 문제를 재현하고, 측정하고, 개선합니다.”**

🎓 Computer Engineering @ Dankook University
📚 GPA **4.36 / 4.5 · Top of Class**

<br>

`Java` `Spring Boot` `JPA` `MySQL` `Redis` `Docker`

</div>

---

## ⚡ At a Glance

|                           |                              |
| ------------------------- | ---------------------------- |
| 👥 **4,000+ Users**       | 실제 사용자가 이용한 수강신청 연습 서비스 운영   |
| 🔒 **0 Oversubscription** | 100개 동시 요청 환경에서 정원 동시성 문제 해결 |
| 🌱 **Open Source**        | Micrometer 공식 프로젝트 PR Merged |

---

## 🚀 Featured Projects

### 🎓 Course Registration Practice System

> **“수강신청에서 가장 위험한 순간은 사용자가 동시에 몰리는 순간이라고 생각했습니다.”**

`Java` `Spring Boot` `JPA` `MySQL` `Docker` `k6` `Micrometer` `Prometheus` `Grafana`

실제 사용자 **4,000명 이상**이 이용한 수강신청 연습 서비스입니다.

단순히 기능을 구현하는 데서 끝내지 않고,
실제 수강신청처럼 요청이 한순간에 몰렸을 때 어떤 문제가 생기는지 직접 실험했습니다.

### Problem

정원 10명인 강의에 **100개의 동시 요청**을 발생시켜

* Race Condition
* 정원 초과
* 신청 카운터 불일치

문제를 재현했습니다.

### Experiment

동일한 환경에서 세 가지 방식을 비교했습니다.

`Pessimistic Lock`
→ `Optimistic Lock`
→ `Conditional UPDATE`

### Result

**Conditional UPDATE 기반 원자적 정원 제어 적용**

`10 Success` · `90 Full Rejected` · `0 Oversubscription`

추가로

* 신청 INSERT 실패 시 정원 카운터까지 Rollback되는 트랜잭션 검증
* UNIQUE Constraint를 이용한 중복 신청 최종 방어
* k6 기반 부하 테스트
* Micrometer / Prometheus / Grafana 기반 모니터링
* 서버 시간 기준 로그인 제어 및 경계 시간 오류 개선

까지 진행했습니다.

🔗 [Repository](https://github.com/lab412sugang2/sugang)

---

### 🌏 TOMO — Cultural Email Copilot

> **“번역은 맞아도, 표현은 틀릴 수 있다는 문제에서 시작했습니다.”**

`Python` `FastAPI` `PostgreSQL` `SQLAlchemy` `Alembic` `OpenAI Responses API`

수신자의 국가·언어·업무 관계를 고려해
이메일의 문화적 위험을 분석하고 적절한 표현을 추천하는 AI 서비스입니다.

**Backend Contribution ~85%**

* 수신자 프로필 및 이메일 분석 REST API 구현
* OpenAI Responses API 연동
* Structured Outputs 기반 구조화된 LLM 응답 처리
* LLM의 위험도 과소평가 문제를 백엔드 보정 로직으로 개선
* PostgreSQL / SQLAlchemy 기반 데이터 계층 설계
* Alembic 기반 DB Migration
* 운영 DB / 테스트 DB 환경 분리
* 외부 LLM 실패 및 예외 상황 처리
* 분석 및 위험도 산정 테스트 작성

**6 Pull Requests Merged**

🔗 [Repository](https://github.com/tomo-likelion/tomo-backend)

---

### 🚑 SuperSave

> **“응급실을 찾는 시간을 줄이면 실제 의사결정도 빨라질 수 있다고 생각했습니다.”**

`Java` `Spring Boot` `JPA` `PostgreSQL` `Redis` `Gemini`

실시간 병상 정보와 AI 판단을 활용한
응급실 이송 의사결정 지원 서비스입니다.

* 구급대원 이송 요청 / 병원 관리자 처리 흐름 구현
* AI 기반 중증도 판단 기능 적용
* 외부 AI 장애 시 fallback 처리
* JPA 기반 이송 데이터 영속화
* PostgreSQL / Supabase Migration
* Redis 기반 병원 정보 캐싱
* 실행 환경 및 API 연동 구조 개선

**9 Pull Requests Merged**

🔗 [Repository](https://github.com/Programming-G1/supersave)

---

## 🌱 Open Source

### Micrometer

> **Issue → Codebase Analysis → Documentation → Review → Merge**

Spring 생태계에서 널리 사용되는 Metrics Facade인
**Micrometer 공식 프로젝트에 기여했습니다.**

**PR #7241 — StatsD Unix Domain Socket Configuration Guide**

* 기존 Issue 분석
* StatsD Registry UDS 설정 방법 문서화
* Java configuration example 추가
* Spring Boot `application.yml` example 추가
* **Merged into upstream**

🔗 [Merged Pull Request](https://github.com/micrometer-metrics/micrometer/pull/7241)

---

## 🛠 Tech Stack

### Backend

`Java` `Spring Boot` `Spring Data JPA` `Spring Security`
`Python` `FastAPI`

### Database

`MySQL` `PostgreSQL` `Redis`

### Infrastructure & Observability

`Docker` `k6` `Micrometer` `Prometheus` `Grafana`

### AI / Data

`OpenAI API` `Gemini API` `pgvector`

---

## 🧠 Currently Exploring

`Financial IT Backend` · `Transaction & Concurrency`

`Data Consistency` · `Performance Engineering`

`Trading Systems` · `Algorithms & CS`

---

<div align="center">

### Build → Break → Measure → Improve

**Backend systems that stay correct under real-world load.**

</div>
