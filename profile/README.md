# LEONEFERITO

**THE MANLY(더맨리)** 의 기성복(Ready-to-wear) 브랜드.
운동으로 체형이 달라진 남성을 위한 정장 — 일반 기성복이 어깨·가슴·허벅지는 끼고 허리는 남는 문제를 다룬다.

> 현재: **Phase 1 완료** (뼈대·로컬 환경) · 다음은 Phase 2 (상품 도메인)

## 저장소

| 저장소 | 내용 | 스택 |
| --- | --- | --- |
| [BE](https://github.com/LEONEFERITO/BE) | API 서버 | Java 21 · Spring Boot 4.1 · PostgreSQL 18 |
| [FE](https://github.com/LEONEFERITO/FE) | 웹 프론트엔드 | Next.js 16 · React 19 · Tailwind 4 (정적 내보내기) |
| **.github** | 기획·설계 문서 (이 저장소) | — |

## 이 사이트가 다른 쇼핑몰과 다른 점

상품 페이지의 핵심은 사진이 아니라 **"내 몸에 맞는가" 를 판단하게 해주는 정보**다.

1. **핏 구분** — 운동체형 / 일반체형
2. **상세 실측표** — 사이즈별 어깨·가슴·허리·총장·허벅지 (카테고리마다 항목이 다르다)
3. **모델 체형 정보** — 키·몸무게·착용 사이즈

그래서 상품 상세에서 `사이즈 선택 → 실측표 → 핏 설명 → 모델 정보` 가 사진 바로 아래에 온다.
또한 의류는 **사이즈 교환이 CS 의 대부분**이라, 교환 흐름을 부가 기능이 아니라 핵심 흐름으로 만든다.

## 문서

| 문서 | 내용 |
| --- | --- |
| [docs/DECISIONS.md](docs/DECISIONS.md) | 기술 결정 기록(ADR) — 무엇을 왜 골랐고 무엇을 버렸는가 |
| [docs/CLIENT_QUESTIONS.md](docs/CLIENT_QUESTIONS.md) | 고객 확인 질문지 — 답이 없으면 막히는 것까지 명시 |
| [docs/DESIGN_CONCEPT.md](docs/DESIGN_CONCEPT.md) | 색 컨셉과 그 제약 (다크 레드벨벳 + 블랙) |
| [IDEAS.md](IDEAS.md) | 지금은 하지 않는 것들 |

## 확정된 기술 결정

| # | 결정 | 핵심 이유 |
| --- | --- | --- |
| D3 | Next.js + 정적 내보내기 | Node 서버 없이도 상품 SEO·공유 미리보기가 된다. 서버비는 SPA 와 같다 |
| D4 | PostgreSQL 18 | 실측표는 카테고리마다 항목이 달라 고정 컬럼으로 못 짠다 → JSONB |
| D5 | Spring Boot 4.1.1 | 3.5.x 는 2026-06-30 무료 지원 종료. 새 프로젝트를 EOL 로 시작할 이유가 없다 |
| D8 | 비즈니스 로직 직접 타이핑 | 학습 목적. 설정·마이그레이션·테스트·인프라는 자동화 |

미확정: D1(판매 범위) · D2(두 사이트 구조) · D6(AWS 구성) · D7(이미지 저장) —
고객 답변이 필요하다. [docs/CLIENT_QUESTIONS.md](docs/CLIENT_QUESTIONS.md) 참고.

## 로컬 실행

```bash
# DB
cd BE && docker compose up -d

# API (http://localhost:8080)
./gradlew bootRun

# 웹 (http://localhost:3000)
cd ../FE && npm ci && npm run dev
```

`.env.example` 을 `.env`(BE) / `.env.local`(FE) 로 복사해서 쓴다.

## 작업 규칙

- Phase 단위로 진행하고, 각 Phase 끝의 **승인 게이트**를 통과해야 다음으로 넘어간다.
- 확인되지 않은 값(사업자 정보, 치수, 가격, 소재, 연락처)은 `TODO(고객확인)` 으로 비워 두고
  질문지에 모은다. **추측으로 채우지 않는다** — 틀린 값이 나가는 것은 빈칸보다 나쁘다.
- 시크릿은 저장소에 없다. `.env.example` 만 커밋하고, 커밋 훅과 CI 가 같은 스크립트로 검사한다.

## 관련

- **THE MANLY 브랜드 사이트** — LEONEFERITO 오픈 후 착수. 별도 Phase 0 부터 다시 시작한다.
