<div align="center">

# Kang Daeun

### Backend Developer · Financial IT · Reliable Systems


Computer Engineering @ Dankook University  
**GPA 4.36 / 4.5 · Top of Class**

`Java` `Spring Boot` `JPA` `MySQL` `PostgreSQL` `Redis` `Docker`

</div>

---

## About Me

금융 IT 백엔드를 목표로 공부하고 있습니다.

단순한 기능 구현보다 **동시성, 트랜잭션, 데이터 정합성, 성능 병목, 운영 안정성**에 관심이 있습니다.  
실제 사용자가 있는 서비스를 운영하면서 생긴 문제를 `재현 → 계측 → 원인 분리 → 개선 → 재검증`하는 방식으로 프로젝트를 발전시키고 있습니다.

---

## Highlights

| | Evidence |
|---|---|
| **4,000+ Users** | 실제 사용자가 이용한 수강신청 연습 서비스 운영 |
| **0 Oversubscription** | 정원 10명 · 100개 동시 요청 환경에서 정합성 검증 |
| **3 Concurrency Strategies × 3 Runs** | 비관적 락 · 낙관적 락 · Conditional UPDATE 반복 비교 |
| **Hot-row Bottleneck Analysis** | 동일 row 집중 시 Conditional UPDATE p95 약 **10.09×** 증가 구간 분리 |
| **Open Source** | Micrometer 공식 프로젝트 PR **Merged** |

---

# Featured Work

## 1. Course Registration Practice System

> **한정된 좌석에 요청이 동시에 몰릴 때에도 정합성을 지키고, 병목을 근거로 설명할 수 있는가?**

`Java 17` `Spring Boot 3.2` `JPA` `MySQL` `Docker` `k6` `Micrometer` `Prometheus` `Grafana`

실제 사용자 **4,000명 이상**이 이용한 단국대학교 비공식 수강신청 연습 서비스입니다.

### Concurrency — Race Condition 재현과 해결

기존 `조회 → 정원 확인 → 저장` 구조에서 정원 10명인 강의에 100개의 동시 요청을 보내
**13건이 등록되는 Race Condition**과 신청 카운터 불일치를 재현했습니다.

정원 확인과 증가를 하나의 원자적 연산으로 처리하도록 **Conditional UPDATE**를 적용했습니다.

```sql
UPDATE courses
SET applied_count = applied_count + 1
WHERE id = ?
  AND applied_count < limit_count
  AND canceled = false;
```

검증 결과:

`10 Success` · `90 Full Rejected` · **`0 Oversubscription`**

추가로 동일 사용자 동시 중복 신청과 후속 INSERT 실패 상황을 분리해
**UNIQUE Constraint와 Transaction Rollback**까지 검증했습니다.

### Why Conditional UPDATE?

비관적 락 · 낙관적 락 · Conditional UPDATE를 동일한 좌석 선점 조건에서 각각 3회 비교했습니다.

| Strategy | Median elapsed | Notes |
|---|---:|---|
| Pessimistic Lock | **79.83 ms** | 정합성 유지 |
| Optimistic Lock | **196.75 ms** | 충돌·재시도 중앙값 309회 |
| Conditional UPDATE | **63.06 ms** | 정합성 유지, 현재 도메인에 선택 |

9회 모두 `10 success / 90 full rejected / 0 mismatch`를 확인했습니다.  
이 수치는 **로컬 MySQL에서 좌석 선점 핵심 로직을 격리한 비교**이며 운영 HTTP 성능으로 일반화하지 않습니다.

### Performance — 병목을 경로별로 분리

혼합 부하 결과만 보고 원인을 단정하지 않고 처리 경로를 분리했습니다.

`A. DB 없는 요청` → `B. 단건 조회` → `C. 여러 강의 분산 신청` → `D. 동일 강의 집중 신청`

Render + Railway MySQL에서 C/D를 동일한 **20 VU × 3회** 조건으로 비교했습니다.

| Metric | Distributed writes | Same-course hot row |
|---|---:|---:|
| HTTP p95 | **1025.71 ms** | **2519.56 ms** |
| Throughput | **9.29 req/s** | **5.40 req/s** |
| Transaction p95 | **709.97 ms** | **1771.67 ms** |
| Conditional UPDATE p95 | **140.13 ms** | **1413.76 ms** |
| `saveAndFlush()` p95 | **107.70 ms** | **108.18 ms** |
| Connection acquire avg | **23.01 ms** | **564.05 ms** |

동일 강의 집중 시 Conditional UPDATE 구간의 p95가 약 **10.09배** 증가한 반면
`saveAndFlush()`는 거의 변하지 않았습니다.

현재는 이 결과를 근거로 **동일 row 변경 대기가 트랜잭션과 connection 점유시간을 늘리는 가설**을 두고 최소 개선 1개를 적용한 뒤 동일 조건 Before/After 검증을 진행하고 있습니다.

> MySQL lock wait를 직접 관찰한 것은 아니므로, 측정하지 않은 원인을 확정적으로 표현하지 않습니다.

**What I learned**  
`@Transactional`만으로 동시성 정합성이 해결되는 것은 아니며, 성능 문제 역시 CPU나 DB를 막연히 의심하기보다 **통제 실험과 단계별 Timer로 지배 구간을 좁혀야 한다**는 것을 배웠습니다.

→ [Repository](https://github.com/lab412sugang2/sugang)

---

## 2. TOMO — Cultural Email Copilot

> **번역은 맞아도, 관계와 문화에 맞는 표현은 다를 수 있다는 문제에서 시작했습니다.**

`Python` `FastAPI` `PostgreSQL` `SQLAlchemy` `Alembic` `OpenAI Responses API` `Docker`

수신자의 국가 · 언어 · 업무 관계를 고려해 이메일의 문화적 위험을 분석하고 적절한 표현을 추천하는 AI 이메일 서비스입니다.

**Backend contribution ~85% · 6 PRs merged**

- Recipient profile / email analysis REST API 구현
- OpenAI Responses API + Structured Outputs 기반 구조화 응답 처리
- LLM 위험도 과소평가를 보완하는 backend correction logic 구현
- PostgreSQL / SQLAlchemy / Alembic 기반 데이터 계층 및 migration 구성
- 운영 DB와 테스트 DB 분리
- 외부 LLM 실패 및 예외 상황 처리

→ [Repository](https://github.com/tomo-likelion/tomo-backend)

---

## 3. SuperSave — Emergency Room Decision Support

`Java` `Spring Boot` `JPA` `PostgreSQL` `Redis` `Gemini` `Public Data API` `Kakao Map`

실시간 응급실 병상 정보와 이동 정보를 활용해 이송 의사결정을 지원하는 서비스입니다.

**9 PRs merged**

- 구급대원 이송 요청 / 병원 관리자 처리 흐름 구현
- 전국 응급의료기관 및 실시간 가용 병상 공공데이터 연동
- Redis 기반 병원 정보 캐싱
- Kakao Map / Navigation 기반 경로 및 교통정보 연동
- PostgreSQL / Supabase 영속화
- Gemini 호출 실패 시 fallback 처리

→ [Repository](https://github.com/Programming-G1/supersave)

---

# Open Source

## Micrometer

Spring 생태계의 Metrics Facade인 **Micrometer 공식 프로젝트**에 기여했습니다.

**[PR #7241 — docs: add UDS configuration guide for StatsD](https://github.com/micrometer-metrics/micrometer/pull/7241)**

`Issue analysis → Codebase / docs analysis → Documentation → Maintainer review → Revision → Merge`

- StatsD registry의 Unix Domain Socket 설정 방법 문서화
- Java configuration example 추가
- maintainer review를 반영해 Spring Boot 중복 문서 제거
- **Merged into upstream `1.15.x`**

---

# Tech

**Backend**  
`Java` `Spring Boot` `Spring Data JPA` `Spring Security` `Python` `FastAPI`

**Database**  
`MySQL` `PostgreSQL` `Redis`

**Infra / Observability**  
`Docker` `k6` `Micrometer` `Prometheus` `Grafana`

**AI / Data**  
`OpenAI Responses API` `Gemini API` `pgvector`

---

# Current Focus

`Financial IT Backend` · `Transactions & Concurrency` · `Data Consistency`  
`Performance Engineering` · `Trading / Order Systems` · `Algorithms & CS`

---

<div align="center">

### Build → Break → Measure → Improve

**Building backend systems that stay correct under real-world load.**

</div>
