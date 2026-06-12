# project-context.md — task-context-hub

> Trello 카드 단위로 연결되는 Task Context Document(TCD)를 통해 작업 맥락 · 설계 결정 · AI 협업 기록을 한 곳에 모아 사람과 AI가 작업을 끊김 없이 이어갈 수 있도록 돕는 개발팀용 컨텍스트 레이어 도구.

본 문서는 후속 산출물(PRD, 아키텍처 설계, 도메인 모델, 화면 설계 등)의 입력이 되는 프로젝트 정의 문서다. 이 문서가 변경되면 PRD와 후속 산출물도 함께 갱신한다.

---

## 1. 프로젝트 개요

### 1.1 비전

> "Trello가 작업 카드/상태 관리라면, Task Context Hub는 작업 맥락/지식/AI 협업 기록 관리."

개발팀이 Trello로 "무엇을 / 어떤 상태인가"는 관리하지만, 작업의 **배경 · 설계 · 결정 · 진행상황 · AI 협업 기록** 같은 '작업 컨텍스트'는 카드 안에 잘 남지 않는 문제를 해결한다. Trello 카드 하나마다 1:1로 연결되는 **Task Context Document(TCD)** 를 두어, 사람과 AI가 작업을 끊김 없이 이어갈 수 있게 한다.

### 1.2 목적

- 작업의 **왜(Why)** 와 **어떻게(How)** 가 사라지지 않도록 task 단위로 구조화된 컨텍스트를 누적한다.
- 여러 AI 도구(Claude / Cursor / ChatGPT / Codex)에 흩어지는 AI 작업 기록을 task 기준으로 통합한다.
- 인수인계 · 리뷰 · AI에게 작업 이어시키기에 필요한 컨텍스트를 **한 번의 복사**로 전달할 수 있게 한다.

### 1.3 차별점

| 비교 대상 | 차별점 |
| --- | --- |
| **Trello** | Trello는 task 정의·상태 도구. 본 도구는 그 위에 얹는 **컨텍스트 레이어**이며 Trello를 대체하지 않음. |
| **Confluence** | Confluence는 주제 중심 범용 문서도구. 본 도구는 **개발 task 단위**의 구조화된 컨텍스트 관리에 특화. |
| **Jira Issue Detail** | Jira는 이슈 트래킹 중심. 본 도구는 AI 협업 기록과 인수인계 흐름까지 task 단위로 결합. |
| **AI 도구별 메모리** | 도구별로 흩어진 AI 작업 기록을 task 기준으로 모으고, **AI Context Package** 한 번의 복사로 어떤 AI에도 컨텍스트 이식 가능. |

핵심 가치는 *"Confluence + Jira Issue Detail + AI 작업 메모리 + 개발 인수인계 문서를 개발 task 단위로 합친, task 중심 구조화 문서도구"* 다.

---

## 2. 타겟 사용자

### 2.1 페르소나

| 페르소나 | 설명 |
| --- | --- |
| **소규모~중규모 개발팀(2~15명) 개발자** | Trello로 작업을 관리하며 Claude Code / Cursor / ChatGPT / Codex 등 AI 도구를 일상적으로 사용. 작업 맥락이 여러 도구에 흩어져 있음. |
| **팀 리드 / 시니어 개발자** | 다른 사람의 작업을 자주 이어받거나 인수인계해야 함. 컨텍스트 부실한 작업을 식별·보완해야 함. |
| **코드 리뷰어** | 작업 의도와 설계 결정을 빠르게 파악한 뒤 코드를 봐야 함. PR 본문만으로는 맥락이 부족할 때가 많음. |

### 2.2 사용자 문제

1. Trello 카드에는 작업 목록/상태만 있고 **왜 이 작업을 하는지 · 어떤 설계 논의가 있었는지 · 왜 그렇게 결정했는지**가 남지 않는다.
2. AI로 한 작업이 Claude / Cursor / ChatGPT 등에 **흩어져** 있어, 같은 task에 대한 AI 작업 맥락이 한 곳에 모이지 않는다.
3. 작업을 이어받는 개발자가 **현재 어디까지 진행됐는지 · 어떤 파일/PR과 연결되는지** 파악하는 데 시간이 오래 걸린다.
4. AI에게 작업을 이어서 시키려면 매번 현재 컨텍스트를 **처음부터 다시 설명**해야 한다.
5. 리뷰어가 **작업 의도를 이해하지 못한 채 코드만 보게 되어** 리뷰 품질/속도가 떨어진다.
6. Confluence는 **주제 중심 범용 문서도구**라 개발 task 단위의 구조화된 컨텍스트 관리에는 맞지 않는다.

### 2.3 성공 지표

| 지표 | 목표 |
| --- | --- |
| 인수인계 파악 시간 단축 | Handoff Summary 사용 시 다른 개발자가 작업을 파악하는 시간 **50% 이상** 단축 |
| AI 재설명 시간 단축 | AI Context Package 생성 후 AI에 작업 컨텍스트를 재설명하는 시간 **70% 이상** 단축 |
| 컨텍스트 작성률 | MVP 사용 팀의 **70% 이상**이 task당 최소 1개 이상의 Decision Log 또는 AI Work Log를 작성 |
| 리뷰 전 참조율 | 리뷰어가 PR 리뷰 전 Task Context Document를 참조하는 비율 **60% 이상** |

---

## 3. 핵심 기능 목록

각 기능은 우선순위(MVP / Phase2 / Phase3)와 함께 정의된다. MVP는 출시 범위이며, Phase2/3은 후속 단계의 확장이다.

### 3.1 MVP 기능

| # | 기능명 | 설명 |
| --- | --- | --- |
| F-01 | **회원가입 및 워크스페이스/Trello 연동** | 이메일 기반 회원가입/로그인(JWT). 팀 단위 워크스페이스. Trello 계정(OAuth 또는 API Key/Token) 연결 후 보드/카드 접근. 이후 카드 ↔ Context 연결의 기반. |
| F-02 | **Trello 카드 연결 및 Task Context 자동 생성** | Trello 카드 URL/ID 입력 시 카드 메타데이터(제목/담당자/상태/라벨/마감일)를 가져와 연결된 Task Context Document를 자동 생성. 카드 1개당 컨텍스트 문서 1개. 작업 상태와 컨텍스트 상태는 별도 관리. |
| F-03 | **Task Context Page (작업 컨텍스트 본문)** | 작업 개요 / 목적 / 배경 / 요구사항 / 관련 도메인 · 모듈 / 관련 파일 / 진행 상태 / 남은 작업 / 이슈 · 주의사항을 구조화 섹션으로 작성. 사람 + AI 모두 읽기 좋은 마크다운. 초기에는 필수 항목만 우선 강제. |
| F-04 | **Decision Log (의사결정 기록)** | "무엇을"이 아니라 "왜"를 기록. 결정 내용 / 검토 대안 / 선택 이유 / 영향 범위. task별 누적 · 시간순 표시. 설계 변경 시 작성하는 운영 규칙. |
| F-05 | **관련 코드 / PR / 문서 링크** | Repository / Branch / Commit / PR / 변경 파일 / 설계 문서 / API 문서를 링크로 연결. MVP는 수동 링크 등록(제목 + URL + 종류). 깊은 Git/PR 자동 동기화는 Phase 2. |
| F-06 | **AI Work Log (AI 작업 로그)** | AI 개발 기록을 요약 중심으로 저장. 사용 도구 / 목적 / 입력 요청 요약 / 결과 요약 / 적용 여부 / 관련 파일 / 후속 작업. 여러 AI 도구에 흩어진 맥락을 task 기준으로 모음. |
| F-07 | **AI Context Package 생성** | **핵심 기능.** 버튼 하나로 현재 task 컨텍스트를 AI에게 넘길 패키지(텍스트/마크다운) 생성. 작업명 / 목적 / 진행 상태 / 요구사항 / 설계 결정 / 관련 파일 / 완료·남은 작업 / 주의사항 / 다음 요청. 복사 후 어떤 AI에든 붙여넣어 이어가기. |
| F-08 | **Handoff Summary (인수인계 요약)** | 현재 상태 / 완료 / 미완료 / 주의사항 / 먼저 봐야 할 파일 / 다음 추천 작업. 작업 중단 · 담당자 변경 시 작성하는 운영 규칙. |
| F-09 | **컨텍스트 상태 관리 (작업 상태와 분리)** | 작업 상태(TODO / DOING / REVIEW / DONE, Trello)와 별개로 컨텍스트 상태(미작성 / 요구사항 정리됨 / 설계 확정됨 / 구현 진행 중 / 인수인계 가능 / 완료 요약됨)를 관리. 컨텍스트가 부실한 task를 식별. |

### 3.2 Phase 2 기능

| # | 기능명 | 설명 |
| --- | --- | --- |
| F-10 | **Timeline / Activity History** | task별 변경 이력을 시간순으로 표시(생성 / 요구사항 정리 / 설계 결정 / AI 로그 / PR 연결 / 리뷰 반영 / 인수인계 / 완료). |
| F-11 | **Context Quality Score** | task 컨텍스트 충실도를 점수화하고 부족 항목을 표시. 컨텍스트 부실 작업을 팀 전체에서 식별. |
| F-12 | **Git / PR 자동 연동** | GitHub/GitLab 연동으로 Repo / Branch / Commit / PR / 변경 파일 / 리뷰 코멘트 / 배포 이력 자동 연결. PR 생성 시 리뷰 포인트 자동 수집. |
| F-13 | **Slack / 회의록 / 문서 링크 연동** | Slack 스레드 / 회의록 / 설계 문서 / API 문서 / 장애 리포트 / 운영 가이드 연결. |

### 3.3 Phase 3 기능

| # | 기능명 | 설명 |
| --- | --- | --- |
| F-14 | **과거 유사 작업 추천** | 축적된 task context를 기반으로 유사 과거 작업을 추천. 임베딩 기반 유사도 검색. 데이터가 축적된 뒤 의미를 가짐. |

---

## 4. 기술 아키텍처

### 4.1 기술 스택 요약

| 영역 | 기술 | 버전 / 비고 |
| --- | --- | --- |
| 모노레포 | Turborepo + pnpm workspaces | - |
| 프론트엔드 | Next.js (App Router) | 15 |
| 프론트엔드 언어 | TypeScript | 5.x |
| 백엔드 | NestJS | 10.x |
| 백엔드 언어 | TypeScript | 5.x |
| 데이터베이스 | PostgreSQL | 16 |
| ORM | Prisma | latest |
| UI | TailwindCSS + shadcn/ui | - |
| AI 보조 | Claude API (Anthropic) | `@anthropic-ai/sdk` |
| 외부 연동(MVP) | Trello REST API | - |

### 4.2 시스템 구성 (논리적 뷰)

```
[Browser]
    │ HTTPS
    ▼
[Next.js 15 (apps/web)]  ── SSR/CSR, Auth UI, TCD 편집기, AI Context Package UI
    │ REST / fetch
    ▼
[NestJS API (apps/api)]
    ├─ Auth Module      (회원가입/로그인, JWT 발급/검증)
    ├─ Workspace Module (워크스페이스 · 멤버 관리)
    ├─ Integration      (Trello/GitHub/Slack 토큰 암호화 저장)
    ├─ TaskContext      (TCD CRUD, 컨텍스트 상태)
    ├─ DecisionLog
    ├─ AIWorkLog
    ├─ ResourceLink
    ├─ Handoff
    ├─ ContextPackage   (AI Context Package 생성, Claude API 호출)
    └─ ActivityEvent    (이벤트 기록)
            │
            ├──► [Trello REST API]   (카드 메타데이터)
            └──► [Claude API]        (Context Package 생성/요약)
    │
    ▼
[PostgreSQL 16 + Prisma]
```

### 4.3 배포 / 인프라

| 영역 | 플랫폼 | 비고 |
| --- | --- | --- |
| Web (`apps/web`) | Vercel | Next.js 15 App Router 배포 |
| API (`apps/api`) | Railway 또는 Render (대체: AWS ECS) | NestJS 컨테이너 배포 |
| Database | Railway PostgreSQL 또는 Render PostgreSQL | 운영용 PostgreSQL 16 |
| 로컬 DB | docker-compose의 PostgreSQL 16 | 개발 환경 |

- **단일 서버에서 시작**, 트래픽 증가 시 web/api 분리. 무거운 통합 동기화(Trello/GitHub 폴링 등)는 별도 **워커/큐**로 분리하여 확장한다.
- 외부 연동 토큰(Trello/GitHub/Slack)은 **암호화 저장 필수**.

---

## 5. 디렉토리 구조 제안 (Turborepo)

```
task-context-hub/
├── apps/
│   ├── web/                    # Next.js 15 (App Router) 프론트엔드
│   │   ├── app/                # 라우트 및 페이지
│   │   ├── components/         # UI 컴포넌트 (shadcn/ui 기반)
│   │   ├── lib/                # API 클라이언트, 유틸
│   │   ├── styles/             # Tailwind 등 글로벌 스타일
│   │   ├── public/
│   │   └── package.json
│   └── api/                    # NestJS 백엔드 API 서버
│       ├── src/
│       │   ├── auth/           # 회원가입/로그인, JWT
│       │   ├── workspace/      # 워크스페이스/멤버
│       │   ├── integration/    # Trello/GitHub/Slack 연동
│       │   ├── task-context/   # TCD CRUD, 컨텍스트 상태
│       │   ├── decision-log/
│       │   ├── ai-work-log/
│       │   ├── resource-link/
│       │   ├── handoff/
│       │   ├── context-package/ # AI Context Package 생성
│       │   ├── activity-event/
│       │   ├── common/         # 가드/인터셉터/필터/DTO 베이스
│       │   └── main.ts
│       ├── prisma/             # schema.prisma, migrations/
│       ├── test/
│       └── package.json
├── packages/                   # 공유 패키지
│   ├── eslint-config/
│   ├── tsconfig/
│   ├── ui/                     # (선택) 공통 UI 컴포넌트
│   └── types/                  # (선택) 도메인/공통 타입
├── docker-compose.yml          # 로컬 PostgreSQL 등 의존성
├── turbo.json                  # Turborepo 파이프라인 설정
├── pnpm-workspace.yaml
├── package.json
├── project-context.md          # 본 문서
├── PRD.md                      # 제품 요구사항 문서
└── README.md
```

- `apps/web`, `apps/api`는 각자 독립적으로 빌드/배포되며, 공통 설정은 `packages/` 하위에 둔다.
- Prisma 스키마는 `apps/api/prisma/`에 위치하고, 마이그레이션은 API 서버 단일 출처로 관리한다.

---

## 6. 외부 연동 서비스

| 서비스 | 단계 | 용도 | 인증 방식 |
| --- | --- | --- | --- |
| **Trello REST API** | MVP | 카드 메타데이터(제목/담당자/상태/라벨/마감일) 조회, 카드↔TCD 매핑 | OAuth 또는 API Key/Token |
| **Claude API (Anthropic)** | MVP | AI Context Package 텍스트 생성/요약 보조 | API Key |
| **GitHub / GitLab API** | Phase 2 | Repo/Branch/Commit/PR/변경 파일/리뷰 코멘트 자동 동기화 | OAuth App + Personal/App Token |
| **Slack API** | Phase 2 | 논의 스레드/메시지/회의록 링크 동기화 | OAuth (Bot Token) |
| **OpenAI Embeddings 또는 pgvector** | Phase 3 | 과거 유사 작업 추천(임베딩 기반 검색) | API Key / 내장 |

- 모든 외부 토큰은 **암호화 저장**이 필수이며, 노출 가능한 평문 로그/응답은 남기지 않는다.
- 외부 API 호출은 워크스페이스 단위로 격리되며, 한 워크스페이스의 토큰이 다른 워크스페이스에 사용되지 않도록 가드한다.

---

## 7. 기술적 제약사항

1. **Trello API rate limit**: 카드 메타데이터 캐싱 및 폴링 주기 관리 필수. 동일 카드를 짧은 시간 내 반복 조회하지 않는다.
2. **외부 연동 토큰 암호화 저장**: Trello/GitHub/Slack 등 모든 외부 연동 토큰은 DB에 평문 저장 금지. 애플리케이션 레벨 암호화(예: KMS 또는 환경 키 기반 AES) 필수.
3. **AI Work Log 민감 데이터 가드**: AI Work Log는 전체 대화가 아니라 **요약 저장**. 시크릿/내부 코드 노출을 줄이기 위한 입력 가드 및 사용자 검수 단계 필요.
4. **Claude API 비용 관리**: AI Context Package 생성 시 LLM 호출 비용을 통제. 컨텍스트 길이 제한, 프롬프트 캐싱, 동일 입력에 대한 결과 캐싱 등을 적용한다.
5. **문서 구조 일관성**: Task Context Document는 사람이 읽기 좋으면서 AI가 파싱 가능한 구조(마크다운 ## Level 2 헤더 기반)로 유지한다. 임의의 자유 형식 본문은 핵심 섹션 밖에서만 허용한다.
6. **데스크톱 우선**: MVP는 웹 데스크톱 우선 반응형이며, 네이티브 모바일 앱은 범위 밖이다.
7. **접근성 기준**: 색대비/키보드 내비게이션 등 WCAG 2.1 AA 기준을 만족한다.

---

## 부록 A. 도메인 모델 초안

| 모델 | 주요 필드(요약) |
| --- | --- |
| **User** | id, email, passwordHash, name, createdAt |
| **Workspace** | id, name, ownerId, trelloIntegrationId, createdAt |
| **WorkspaceMember** | id, workspaceId, userId, role(OWNER/MEMBER) |
| **Integration** | id, workspaceId, type(TRELLO/GITHUB/SLACK), encryptedToken, status |
| **TaskContext** | id, workspaceId, trelloCardId, trelloCardUrl, title, purpose, background, requirements, workStatus, contextStatus, createdBy, createdAt, updatedAt |
| **DecisionLog** | id, taskContextId, decision, alternatives, rationale, impactScope, createdBy, createdAt |
| **AIWorkLog** | id, taskContextId, tool, goal, requestSummary, resultSummary, applied, relatedFiles, followUp, createdBy, createdAt |
| **ResourceLink** | id, taskContextId, kind(REPO/BRANCH/COMMIT/PR/DOC/API), title, url, createdAt |
| **HandoffSummary** | id, taskContextId, currentState, doneItems, todoItems, cautions, filesToReadFirst, nextRecommended, createdBy, createdAt |
| **ActivityEvent** | id, taskContextId, type, payload, actorId, createdAt |
| **AIContextPackage** | id, taskContextId, content, generatedAt, generatedBy |

상세 스키마(컬럼 타입, 인덱스, 관계)는 후속 작업의 `apps/api/prisma/schema.prisma`에서 확정한다.

---

## 부록 B. 디자인 가이드 요약

- **톤**: 전문적이고 신뢰감 있는, 정보 밀도 높은 개발자 도구 톤. 미니멀 모던.
- **디자인 시스템**: shadcn/ui
- **Primary Color**: `#2563EB`
- **참조 앱**: Linear(빠르고 정돈된 개발자 UX, 키보드 중심), Notion(구조화된 문서 편집), Confluence(페이지/문서 계층 구조 — task 중심으로 단순화)
- **반응형**: 데스크톱 우선
- **접근성**: WCAG 2.1 AA

---

## 부록 C. 범위 정리 (MVP / Out of Scope)

### MVP

- 회원가입/로그인(이메일 + JWT)
- 워크스페이스 + Trello 연동
- 카드 URL/ID → Task Context Document 자동 생성
- Task Context Page 작성, Decision Log, 수동 ResourceLink
- AI Work Log 요약 저장
- AI Context Package 생성(복사)
- Handoff Summary
- 작업 상태와 분리된 컨텍스트 상태 관리

### Out of Scope

- Trello 대체(카드/상태/칸반) — Trello는 task 정의/상태 도구로 계속 사용
- Git/PR 자동 동기화(Phase 2)
- Slack/회의록 자동 연동(Phase 2)
- 과거 유사 작업 추천(Phase 3)
- Timeline/Activity History, Context Quality Score(Phase 2)
- AI 도구 직접 API 통합(자동 AI Work Log) — 후순위
- 네이티브 모바일 앱
