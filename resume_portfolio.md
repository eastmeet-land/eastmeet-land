## (주)그리너리에서 한 일 (23.07 ~ 26.01)

```text
- Java 17 + Spring Boot 2.x.x/3.x.x
- JPA, QueryDSL, PostgreSQL, MySQL, Redis
- Kubernetes(NHN Cloud NKS), Docker, Terraform, GitHub Actions
- Nginx, OpenResty + Lua, EFK(Elasticsearch, Fluentd, Kibana)
- Confluence, Slack, Jira
```

### 1. 탄소배출권 인증 센터 및 거래 플랫폼 고도화 (23.07 ~ 23.12)

> 기업 간 탄소배출권 인증과 거래를 지원하는 사내 플랫폼 고도화 및 유지보수<br>
> [Service URL](https://www.pople.kr/)

| 제목 | 요약 |
|------|------|
| Nest.js → Spring Boot 마이그레이션 | - 개발팀 내 기술 스택 통일화를 위해 Nest.js → Java/Spring Boot 마이그레이션 담당<br/>- 기존 API의 any 타입 요청/응답을 실제 데이터 수집 후 DTO 기반 계층 분리로 재설계<br/>- 40건 이상의 API를 Spring Boot 타입 시스템 기반으로 전환<br/>- Google/Kakao OAuth 소셜 로그인 연동 구현 |
| 크레딧 심사 워크플로우 리팩토링 | - 마이그레이션 과정에서 크레딧 발행/이전/상쇄/폐기 4가지 심사 플로우의 상태 관리 로직을 재설계<br/>- 여러 곳에 흩어져 있던 상태 전이 로직을 Enum 내부 메서드로 응집하고, 중첩 분기를 early return + switch 문으로 정리<br/>- 상태(문서)와 행위(액션) 엔티티를 분리하여 심사 단계별 이력 추적이 가능한 구조로 개선 |
| 상쇄 인증서 PDF 생성 파이프라인 | - 크레딧 구매 완료 시 `@Async` 비동기로 상쇄 인증서 PDF 자동 생성 → S3 업로드 → CloudFront URL 제공<br/>- 크레딧 고유번호(Serial Number) 체계 설계: `VRC-{방법론코드}-{프로젝트SEQ}-{모니터링기간}-{일련번호}` 형식<br/>- Slack 알림 연동 및 Stibee 이메일 기반 선물 인증서 발송 |
| API 성능 최적화 | - N+1 쿼리 해결 및 인덱스 최적화로 API 응답속도 40% 개선 (200ms → 120ms)<br/>- Swagger 응답 명세 작성 및 Custom 어노테이션 활용 컨트롤러 코드 간소화 |
| 인프라 고가용성 확보 | - AWS 기반 서버 이중화 및 ALB 트래픽 분산 구성 |

### 2. 가상자산 간편 세금 서비스 개발 (24.01 ~ 24.06)

> 개인 투자자가 가상자산 거래 내역을 정리하고 세금을 산출할 수 있는 서비스<br>
> [Service URL](https://taas.im/)

| 제목 | 요약 |
|------|------|
| Nest.js → Spring Boot 전환 | - 기존 Nest.js 시스템을 Spring Boot로 전환<br/>- 서버 초기 구성(yml, Swagger, Log4j) 및 테스트 환경(H2, Redis) 세팅 |
| 자산·세금·손익 도메인 API 구현 | - 거래소별 자산 조회, 지갑별 토큰 보유량 조회 API 구현<br/>- KRW/USD/JPY 멀티 통화 환율 변환 및 Lang·Base-Currency 헤더 기반 다국어·다통화 대응<br/>- 예상 산출세액 API 및 토큰 평균단가 계산 로직 구현<br/>- 실현/미실현 손익 조회 API 구현 |
| 암호화 아키텍처 개선 | - AWS SDK v1 → v2 전환 및 CryptService 인터페이스 도입으로 암호화 전략 추상화<br/>- 운영(AWS KMS) / 로컬(AES-256-CBC) 환경별 구현체 분리, Spring DI 기반 자동 주입 구조 구축 |
| 어드민 예약 알림 시스템 | - Quartz Scheduler 기반 어드민 예약 알림 CRUD 및 예약 발송 시스템 구현<br/>- 알림 생성/수정/삭제 시 Quartz Job 연동 관리 및 Job 실행 이력 DB 기록 |
| 배포 환경 구축 | - 쉘 스크립트 기반 CI/CD 파이프라인 구축으로 배포 주기 확보<br/>- 프론트엔드 Next.js + PM2 프로세스 관리 및 Nginx 리버스 프록시 기반 배포 환경 구축 |

### 3. 광주 스마트시티 정부과제 수행 (24.07 ~ 24.12)

> RE100 탄소중립을 위한 에너지 자립형 광주 스마트도시 조성 정부 사업

| 제목 | 요약 |
|------|------|
| 인프라 및 백엔드 개발 | - 기존 AWS 기반 탄소배출권 거래 플랫폼을 NCP 환경으로 포팅<br/>- 네이버 클라우드 플랫폼(NCP) 인프라 초기 세팅 및 배포 환경 구성<br/>- JavaScript/React 기반 프론트엔드 추가 기능 구현<br/>- 테이블 정의서 작성 및 데이터베이스 설계 |
| 감리 대응 | - 요구사항 정의서, 기능명세서 및 테스트 문서 작성<br/>- 정부과제 감리 기준에 맞춘 산출물 관리 |

### 4. LCA(전과정평가) 시스템 신규 구축 및 SaaS 플랫폼 전환 (25.01 ~ 25.08)

> 제품의 원료 채취부터 폐기까지 전 생애주기 환경영향을 정량 분석하는 LCA 시스템 신규 구축 및 멀티테넌트 B2B SaaS 전환

| 제목 | 요약 |
|------|------|
| 시스템 설계 및 멀티테넌트 구현 | - 시스템 ERD 및 RESTful API 신규 설계<br/>- 기업별 데이터 격리 및 접근 제어가 가능한 멀티테넌트 구조 구현 |
| 대규모 데이터 정규화 | - ecoinvent 환경영향평가 데이터 76만 건(EcoSpold/XML)을 자사 시스템 스키마에 맞게 재정규화 수행 |
| 도메인 핵심 기능 | - 전과정평가 산정 로직 구현 (원료 투입~공정~수송~폐기 단계별 환경영향 정량 계산)<br/>- QueryDSL 기반 조회 쿼리 최적화로 조회 성능 40% 개선 |
| 모니터링 및 인프라 | - EFK 기반 실시간 로그 모니터링 구축 및 Slack 연동, 로그 분석 소요시간 83% 단축<br/>- HikariCP 커넥션 풀 병목 분석 및 서비스별 유휴 커넥션/타임아웃 최적화<br/>- Terraform 활용 인프라 코드화(IaC)로 프로비저닝 효율 개선 |

### 5. KMAC 디지털 솔루션 포털 개발 (25.06 ~ 25.12) — LCA 프로젝트와 병행 수행

> KMAC(한국능률협회컨설팅) 디지털 솔루션 포털 백엔드 시스템 개발 및 인프라 구축<br>
> [Service URL](https://dts.kmac.co.kr/)

| 제목 | 요약 |
|------|------|
| 시스템 아키텍처 | - Gradle 기반 멀티 모듈 설계로 도메인별 책임 분리 및 공통 모듈 의존성 관리<br/>- 솔루션별 분산 사용자 DB 일원화 및 SSO(Single Sign-On) 적용, 통합 인증 환경 구축 |
| [API Gateway 로그인 프로세스 설계](https://eastmeet.notion.site/API-Gateway-33c1fa500b9880e0b3ece7a070a68d4b?source=copy_link) | - 파이브핑거스(FiveFingers) API Gateway 업체와 협업하여 로그인 프로세스 연동 설계 및 구현<br/>- Spring Security 기반 X-User-Key 헤더를 활용한 사용자 인가 처리 구현<br/>- Gateway 단 비인가 요청 사전 차단 + Spring 2차 인가 검증 이중 체계 확립<br/>- 개발 환경에서 OpenResty + Lua 기반 API Gateway 자체 구축, 운영 환경 사전 검증 수행 |
| 컨테이너 인프라 구축 | - NHN Cloud NKS 환경 Kubernetes 클러스터 구축 및 애플리케이션별 이미지 관리 배포 체계 구성<br/>- Nginx Ingress Controller 활용 TLS 인증서 적용 (HTTP → HTTPS) 및 갱신 스크립트 작성 |
| CI/CD | - GitHub Actions 기반 CI/CD 파이프라인 구성 및 Slack 연동 배포 상태 실시간 공유 |

### 6. 탄소회계 시스템 신규 구축 (25.09 ~ 26.01)

> 기업의 탄소 배출량을 체계적으로 측정·관리할 수 있는 탄소회계 시스템 MVP 구축

| 제목 | 요약 |
|------|------|
| 시스템 설계 | - 탄소 배출량 데이터 모델링 및 확장 가능한 RESTful API 설계 |
| 카테고리별 산출 로직 | - Scope 3 온실가스 15개 카테고리(CAT01~15)별 배출량 산출 로직 설계·구현<br/>- 카테고리마다 배출계수·GWP·단위환산 방식이 상이하여 공통 추상 계층 + 카테고리별 구현체(전략 패턴)로 설계 |
| 성능 최적화 | - N+1 쿼리 문제 진단·해결 및 Redis 기반 사용자 권한 정보 캐싱으로 API 응답시간 55% 단축<br/>- 권한 변경 시 이벤트 발행 → 트랜잭션 커밋 후 비동기로 영향 받는 사용자 캐시만 선택적 무효화<br/>- Nginx HTTP/2 프로토콜 전환 및 Gzip 압축 적용으로 네트워크 전송 효율 개선 |
| 보안 | - Next.js RCE 취약점 긴급 패치 및 QueryDSL 의존성 버전 교체 등 백엔드/프론트엔드 보안 취약점 점검 수행 |

---

## 개인 프로젝트

### OrderTrace - DDD 기반 주문/결제 서비스 (26.02 ~ 26.03)

> 주문-결제 도메인을 DDD 및 Port-Adapter 아키텍처 기반으로 설계한 프로젝트  
> [GitHub Link](https://github.com/eastmeet-land/ordertrace)

```text
- Java 21 + Spring Boot 4.0
- Kafka (KRaft), JPA, PostgreSQL
- Docker Compose, EFK, Slack Alert
```

| 제목 | 요약 |
|------|------|
| 아키텍처 설계 | - DDD 및 Port-Adapter 아키텍처 기반 주문/결제 서비스 설계·구현<br/>- 주문-결제 간 책임 분리, FK 없이 ID 참조로 도메인 간 결합도 감소 |
| Kafka 이벤트 드리븐 | - Kafka 비동기 이벤트 기반 통신으로 서비스 간 결합도 감소<br/>- TransactionSynchronization 활용 DB 커밋 후 이벤트 발행<br/>- Consumer 멱등성 보장으로 메시지 안정성 확보<br/>- Key 기반 파티셔닝으로 동일 주문 이벤트 순서 보장 |
| 동시성 제어 | - 재고 차감 시 비관적 락(PESSIMISTIC_WRITE)으로 Lost Update 방지<br/>- 상품 정보 수정 시 낙관적 락(@Version)으로 충돌 감지<br/>- 결제 실패 시 보상 트랜잭션(재고 복원) 설계 |
| 모니터링 및 테스트 | - Docker Compose 개발 환경 구성 (6개 서비스)<br/>- EFK 스택 연동 이벤트 흐름 로그 기반 추적<br/>- 도메인 단위 테스트 40개 작성<br/>- Slack 에러 알림 연동 (Throttling 적용) |


## 기타 경험

### 비개발 경력에서 얻은 개발자로서의 강점

개발 전 건설 현장 관리(동원건설산업)와 정부 과제 PM(한국수소산업협회) 경험이 있습니다.
이 경험들은 순수 개발 역량 외에, 문제를 구조화하고 이해관계자와 소통하는 능력으로 이어졌습니다.

| 제목 | 요약 |
|------|------|
| 검증 기반 판단 | - 동원건설산업 현장 관리에서 시공 품질 검증을 반복하며 "추측이 아닌 사실 기반 판단" 습관을 형성<br/>- 성능 개선 시 로그·메트릭 기반으로 병목을 분석하고 수치로 검증하는 접근을 유지<br/>- 테스트 코드 작성을 단순 품질 관리가 아닌 "동작하는 사실의 검증"으로 여기며, 비즈니스 로직의 정합성을 코드로 보장하는 것을 중요하게 생각 |
| 구조적 문제 정의 | - 한국수소산업협회 PM으로 14개월간 정부과제를 수행하며 요구사항 정의, 일정 관리, 문서화 역량을 체득<br/>- 그리너리에서 프로젝트 WBS 작성 및 백엔드/프론트엔드 개발 일정 관리에 직접 활용 |
| 주체적 문제 해결 | - 시스템 설계부터 인프라 구축, 운영까지 폭넓게 참여<br/>- 외부 솔루션 업체, 프론트엔드·기획과의 협업에서 기술적 의사결정에 주체적으로 참여 |

### 자기 발전 및 학습

| 제목 | 요약 |
|------|------|
| 지식 관리 | - Obsidian 기반 개인 지식 베이스 운영 (기술 학습, 면접 준비, 트러블슈팅 기록)<br/>- Google Drive 연동으로 어디서든 접근 가능한 학습 환경 구축 |
| AI 도구 활용 | - Claude를 활용한 prompt/context engineering으로 학습 효율화 및 코드 리뷰 보조<br/>- Gemini Code Review를 PR 프로세스에 적용, AI 기반 코드 품질 검증 활용<br/>- AI를 도구로 활용하되 기술 원리 이해를 우선하는 학습 태도 유지 |
| 포트폴리오 프로젝트 | - [OrderTrace](https://github.com/eastmeet-land/ordertrace): DDD, Kafka, EFK 기반 주문/결제 서비스를 설계부터 구현까지 단독 수행<br/>- 실무에서 경험하지 못한 기술(Kafka 이벤트 드리븐, 동시성 제어)을 직접 설계하고 검증 |
| GitHub 조직 운영 | - [eastmeet-land](https://github.com/eastmeet-land): 경력 포트폴리오 및 프로젝트 관리<br/>- [eastmeet-sail](https://github.com/eastmeet-sail) (Organization): 기술 학습 저장소, voyage-[기술명] 네이밍 컨벤션으로 체계적 관리 |
