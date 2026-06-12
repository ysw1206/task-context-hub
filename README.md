# task-context-hub

> Trello 카드마다 연결되는 Task Context Document 기반 개발 task 컨텍스트/AI 협업 기록 관리 도구

## Overview

개발팀이 Trello로 작업 상태는 관리하지만 작업 컨텍스트(배경·설계·결정·AI 협업 기록)는 카드에 남지 않는 문제를 해결하기 위해 만들어진 도구입니다. 각 Trello 카드에 1:1로 연결되는 **Task Context Document(TCD)** 를 통해 작업의 배경, 설계 결정, AI 협업 로그를 한 곳에서 관리합니다.

### 핵심 기능

- Trello 카드와 1:1로 매핑되는 Task Context Document 관리
- 작업 배경 · 설계 결정 · 리뷰 코멘트 기록
- Claude API 기반 AI 협업 기록 및 컨텍스트 자동 요약
- 팀 단위 컨텍스트 검색 및 히스토리 추적

### 기술 스택 요약

- **Frontend**: Next.js 15 (App Router), React 19, TypeScript
- **Backend**: NestJS, TypeScript
- **Database**: PostgreSQL 16 + Prisma ORM
- **모노레포**: Turborepo (pnpm workspaces)
- **외부 연동**: Trello REST API, Claude API (Anthropic)

## 프로젝트 구조

Turborepo 기반 모노레포 구조입니다.

```
task-context-hub/
├── apps/
│   ├── web/                # Next.js 15 (App Router) 프론트엔드
│   │   ├── app/
│   │   ├── components/
│   │   └── package.json
│   └── api/                # NestJS 백엔드 API 서버
│       ├── src/
│       ├── prisma/
│       └── package.json
├── packages/               # 공유 패키지 (eslint-config, tsconfig 등)
├── docker-compose.yml      # 로컬 PostgreSQL 등 의존성
├── turbo.json              # Turborepo 파이프라인 설정
├── pnpm-workspace.yaml
├── package.json
└── README.md
```

## Getting Started

### 사전 요구사항

- Node.js 20 LTS 이상
- pnpm 9 이상
- PostgreSQL 16 (로컬은 docker-compose 사용 권장)
- Docker / Docker Compose (로컬 DB 실행용)

### 설치

```bash
git clone https://github.com/ysw1206/task-context-hub.git
cd task-context-hub
pnpm install
```

### 환경변수

루트와 각 앱(`apps/web`, `apps/api`)에 `.env` 파일을 생성합니다. 예시는 `.env.example`을 참고하세요.

```env
# apps/api/.env
DATABASE_URL=postgresql://USER:PASSWORD@localhost:5432/task_context_hub
PORT=4000

TRELLO_API_KEY=<your-trello-api-key>
TRELLO_API_TOKEN=<your-trello-api-token>

ANTHROPIC_API_KEY=<your-claude-api-key>
```

```env
# apps/web/.env
NEXT_PUBLIC_API_BASE_URL=http://localhost:4000
```

> 실제 시크릿 값은 절대 커밋하지 않습니다. `.env`는 `.gitignore`에 포함되어 있어야 합니다.

### 로컬 실행

> ⚠️ 본 커밋은 초기 부트스트랩 단계로 `apps/web`, `apps/api` 구현이 아직 추가되지 않았습니다. 아래 명령은 후속 작업에서 각 앱이 추가된 이후 동작합니다.

```bash
# 로컬 PostgreSQL 실행
docker compose up -d

# (apps/api 추가 이후) API 서버 실행
pnpm --filter @task-context-hub/api dev

# (apps/web 추가 이후) Web 실행
pnpm --filter @task-context-hub/web dev
```

## 인프라

### 로컬 데이터베이스

로컬 PostgreSQL 16은 `docker-compose.yml`로 실행합니다.

```bash
docker compose up -d        # 백그라운드 실행
docker compose ps           # 상태 확인
docker compose down         # 종료
```

### 배포

| 영역 | 플랫폼 | 비고 |
| --- | --- | --- |
| Web (`apps/web`) | Vercel | Next.js 15 App Router 배포 |
| API (`apps/api`) | Railway 또는 Render | NestJS 컨테이너 배포 |
| Database | Railway PostgreSQL 또는 Render PostgreSQL | 운영용 PostgreSQL 16 |

### 외부 API 키 설정

| 키 | 용도 | 발급 위치 |
| --- | --- | --- |
| `TRELLO_API_KEY` / `TRELLO_API_TOKEN` | Trello 카드/보드 동기화 | https://trello.com/power-ups/admin |
| `ANTHROPIC_API_KEY` | Claude API 호출 (AI 협업 기록/요약) | https://console.anthropic.com/ |

각 키는 운영 환경(Vercel / Railway / Render)의 환경변수로 설정합니다.

## 기술 스택

| 영역 | 기술 | 버전 / 비고 |
| --- | --- | --- |
| 모노레포 | Turborepo + pnpm workspaces | - |
| 프론트엔드 | Next.js | 15 (App Router) |
| 프론트엔드 언어 | TypeScript | 5.x |
| 백엔드 | NestJS | 10.x |
| 백엔드 언어 | TypeScript | 5.x |
| 데이터베이스 | PostgreSQL | 16 |
| ORM | Prisma | latest |
| AI | Claude API (Anthropic) | `@anthropic-ai/sdk` |
| 외부 연동 | Trello REST API | - |

## 라이선스

Private — 내부 사용 전용.
