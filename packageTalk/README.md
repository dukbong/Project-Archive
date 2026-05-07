# packageTalk — 여행 플랫폼 비교 웹 서비스

여러 여행 플랫폼에 분산된 패키지/항공/숙소 정보를 한 화면에서 비교할 수 있도록 만든 사이드 프로젝트입니다.

**Live**: [https://www.packagetalk.com/](https://www.packagetalk.com/)

![packageTalk 메인 화면](./assets/main.png)

---

## 만든 이유

- 동일한 여행 상품이 플랫폼별로 가격·구성·옵션이 달라 사용자 입장에서 매번 직접 비교해야 하는 불편함이 있었음
- 기존 비교 사이트는 카테고리가 한정적이거나 광고 비중이 높아 객관성이 떨어짐
- 데이터를 직접 수집·정규화해 객관적인 비교 화면을 제공하고자 시작

## 기술 스택

<!-- TODO: 실제 사용 기술로 교체 -->
- **Backend**: Spring Boot, JPA, MariaDB, Redis
- **Infra**: AWS, Docker
- **Frontend**: <!-- 예: Vue / React / Next.js -->
- **Data**: 크롤링 워커, 정규화 파이프라인

## 아키텍처

```mermaid
flowchart LR
    Scheduler[Scheduler] --> Crawler["Crawler Workers<br/>(플랫폼별 분리)"]
    Crawler --> Normalizer[정규화 파이프라인]
    Normalizer --> DB[(MariaDB)]

    User((User)) --> CDN[CloudFront]
    CDN --> Frontend[Frontend]
    Frontend --> API[Spring Boot API]
    API --> DB
    API --> Cache[(Redis)]

    classDef store fill:#FFF4E6,stroke:#D97706,color:#1F2937
    class DB,Cache store
```

| 레이어 | 구성 |
|---|---|
| 수집 | Scheduler가 주기적으로 플랫폼별 Crawler Worker를 실행하여 원천 데이터 수집 |
| 정규화 | 플랫폼별 상이한 스키마를 단일 도메인 모델로 변환 후 MariaDB에 적재 |
| 서빙 | Spring Boot API가 정규화 데이터를 조회·비교, 자주 조회되는 결과는 Redis로 캐싱 |
| 전달 | CloudFront로 정적 자산 전송, Frontend에서 비교 화면 렌더링 |

## 핵심 기술 결정

<!-- TODO: 직접 결정한 내용 1~3개 -->

- **수집 주기 vs 즉시 조회 트레이드오프** — 어떤 기준으로 결정했는가
- **정규화 스키마 설계** — 플랫폼별 상이한 필드를 어떻게 통합했는가
- **캐시 무효화 전략** — 데이터 신선도와 응답 속도 사이에서의 선택

## 화면

| 검색 | 비교 결과 | 상세 보기 |
|---|---|---|
| ![검색](./assets/search.png) | ![비교](./assets/compare.png) | ![상세](./assets/detail.png) |

## 회고

<!-- TODO: 운영하면서 배운 것, 다음에 다르게 할 것 -->
