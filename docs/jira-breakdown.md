# task-context-hub — Jira 작업 분해 결과 (SCRUM-4836)

> PRD.md / Architecture.md / UX-Design-Spec.md를 입력으로 한 Epic(SCRUM-4829) 하위 Story·Subtask 분해와 Confluence 작업지시서 생성 결과 요약. 결과는 Jira/Confluence에 실제 등록되어 있다.

## 1. 설계 요약

- 5개 분류(인증·기반 / 워크스페이스 / Trello 통합 / TCD 생성·편집·누적 / TCD 탐색 / AI Context Package)의 사용자 가치 흐름을 **10개의 Story**로 펼침
- 각 Story는 단일 Claude 세션에서 완료 가능한 단위의 **Subtask 총 26개**로 분해
- 모든 Subtask는 Confluence 작업지시서 페이지로 1:1 연결, Jira Subtask에 Remote Link 등록 완료
- Story 간 미래 의존성(blocking) 없음 — 자연 순서(인증 → 워크스페이스 → 통합 → TCD → 검색 → AI Context Package)는 허용

## 2. Story 키 목록

| 순번 | Story | 키 |
| --- | --- | --- |
| 1 | 인증 기반 — 회원가입/로그인/세션 | SCRUM-4837 |
| 2 | 워크스페이스 생성 및 멤버 관리 | SCRUM-4838 |
| 3 | Trello 연동 및 보드 조회 | SCRUM-4839 |
| 4 | Task Context Document 생성 및 편집 | SCRUM-4840 |
| 5 | Decision Log 누적 | SCRUM-4841 |
| 6 | AI Work Log 누적 | SCRUM-4842 |
| 7 | 관련 코드/PR/문서 ResourceLink 누적 | SCRUM-4843 |
| 8 | Handoff Summary 작성 | SCRUM-4844 |
| 9 | TCD 검색·목록·필터 | SCRUM-4845 |
| 10 | AI Context Package 생성·복사 | SCRUM-4846 |

## 3. Subtask 키 목록 (26)

| 순번 | Subtask | 키 | 부모 Story |
| --- | --- | --- | --- |
| 1-1 | 모노레포 부트스트랩 (Turborepo + Next.js 15 + NestJS + PostgreSQL) | SCRUM-4847 | SCRUM-4837 |
| 1-2 | Auth 백엔드 — User + bcrypt + JWT + 5회 잠금 | SCRUM-4848 | SCRUM-4837 |
| 1-3 | Auth 프론트엔드 — 회원가입/로그인 페이지 + 토큰 보관 | SCRUM-4849 | SCRUM-4837 |
| 1-4 | 로그아웃 / 세션 만료 + JwtAuthGuard | SCRUM-4850 | SCRUM-4837 |
| 2-1 | Workspace + WorkspaceMember 백엔드 + RBAC 가드 | SCRUM-4851 | SCRUM-4838 |
| 2-2 | 워크스페이스 목록·생성·홈·Switcher 프론트엔드 | SCRUM-4852 | SCRUM-4838 |
| 2-3 | 멤버 관리 화면 — OWNER 초대/제거 | SCRUM-4853 | SCRUM-4838 |
| 3-1 | Integration 모듈 + AES-GCM 토큰 암호화 | SCRUM-4854 | SCRUM-4839 |
| 3-2 | TrelloClient + 카드/보드 캐시 + 백오프 + 보드 목록 API | SCRUM-4855 | SCRUM-4839 |
| 3-3 | Trello 연동 설정 화면 + BoardPicker 프론트엔드 | SCRUM-4856 | SCRUM-4839 |
| 4-1 | TaskContext 백엔드 — 모델 + 자동 생성 + 본문/상태 API + ActivityEvent | SCRUM-4857 | SCRUM-4840 |
| 4-2 | CardLinkInput + 새 TCD 화면 프론트엔드 | SCRUM-4858 | SCRUM-4840 |
| 4-3 | TCD 상세 페이지 + Tabs 구조 + Overview 탭 | SCRUM-4859 | SCRUM-4840 |
| 4-4 | TcdEditor + MarkdownPreview + ContextStatusSwitcher | SCRUM-4860 | SCRUM-4840 |
| 5-1 | DecisionLog 백엔드 — 4필드 필수 + 권한 | SCRUM-4861 | SCRUM-4841 |
| 5-2 | DecisionLogList + Decisions 탭 프론트엔드 | SCRUM-4862 | SCRUM-4841 |
| 6-1 | AIWorkLog 백엔드 — 5필드 + 4000자 + 시크릿 가드 | SCRUM-4863 | SCRUM-4842 |
| 6-2 | AIWorkLogList + AI Worklog 탭 프론트엔드 | SCRUM-4864 | SCRUM-4842 |
| 7-1 | ResourceLink 백엔드 — URL 스킴 검증 + 종류 6 | SCRUM-4865 | SCRUM-4843 |
| 7-2 | LinksPanel + Code/PR 탭 프론트엔드 | SCRUM-4866 | SCRUM-4843 |
| 8-1 | HandoffSummary 백엔드 — 6필드 + 최신 메인 | SCRUM-4867 | SCRUM-4844 |
| 8-2 | HandoffCard + Handoff 탭 프론트엔드 | SCRUM-4868 | SCRUM-4844 |
| 9-1 | TCD 목록·검색·필터 백엔드 + 인덱스 | SCRUM-4869 | SCRUM-4845 |
| 9-2 | TcdListTable + 검색·필터 UI 프론트엔드 | SCRUM-4870 | SCRUM-4845 |
| 10-1 | context-package 백엔드 — Claude SDK + 결과 캐시 + 프롬프트 캐싱 | SCRUM-4871 | SCRUM-4846 |
| 10-2 | ContextPackageButton + ContextPackageResult 프론트엔드 | SCRUM-4872 | SCRUM-4846 |

## 4. FR Coverage Map (PRD §5 → 작업 매핑)

| FR | 내용 | Story | 주요 Subtask |
| --- | --- | --- | --- |
| FR-01 | 회원가입 | SCRUM-4837 | SCRUM-4848, SCRUM-4849 |
| FR-02 | 로그인 (5회 잠금 포함) | SCRUM-4837 | SCRUM-4848, SCRUM-4849 |
| FR-03 | 로그아웃 / 세션 만료 | SCRUM-4837 | SCRUM-4850 |
| FR-04 | 워크스페이스 생성/멤버 관리 | SCRUM-4838 | SCRUM-4851, SCRUM-4852, SCRUM-4853 |
| FR-05 | Trello 연동 등록 | SCRUM-4839 | SCRUM-4854, SCRUM-4856 |
| FR-06 | Trello 보드 목록 조회 | SCRUM-4839 | SCRUM-4855, SCRUM-4856 |
| FR-07 | 카드 URL/ID 입력 | SCRUM-4840 | SCRUM-4857, SCRUM-4858 |
| FR-08 | TCD 자동 생성 | SCRUM-4840 | SCRUM-4857, SCRUM-4858 |
| FR-09 | Task Context Page 편집 | SCRUM-4840 | SCRUM-4857, SCRUM-4860 |
| FR-10 | Decision Log 작성/조회 | SCRUM-4841 | SCRUM-4861, SCRUM-4862 |
| FR-11 | AI Work Log 작성/조회 | SCRUM-4842 | SCRUM-4863, SCRUM-4864 |
| FR-12 | ResourceLink 등록/조회 | SCRUM-4843 | SCRUM-4865, SCRUM-4866 |
| FR-13 | AI Context Package 생성 | SCRUM-4846 | SCRUM-4871, SCRUM-4872 |
| FR-14 | 컨텍스트 상태 관리 | SCRUM-4840 | SCRUM-4857, SCRUM-4860 |
| FR-15 | Handoff Summary 작성 | SCRUM-4844 | SCRUM-4867, SCRUM-4868 |
| FR-16 | TCD 검색/목록 | SCRUM-4845 | SCRUM-4869, SCRUM-4870 |
| FR-17 | 권한 가드 | SCRUM-4837, SCRUM-4838 | SCRUM-4850, SCRUM-4851 |

**Coverage: 17 / 17 = 100% — 누락된 FR 없음.**

## 5. NFR / DR / ADR 반영

- **NFR-02 / NFR-12 / TC-02 / ADR-002 (AI Context Package 결과·프롬프트 캐싱):** Story 10
- **NFR-05 / NFR-06 / TC-03 / TC-05 / ADR-003 (외부 토큰 AES-GCM):** Story 3 (SCRUM-4854)
- **NFR-07 / TC-04 (비밀번호 bcrypt):** Story 1 (SCRUM-4848)
- **NFR-08 (WCAG 2.1 AA):** 모든 프론트엔드 Subtask 검수 기준에 axe-core 위반 0건 포함
- **NFR-13 / TC-01 (Trello rate limit):** Story 3 (SCRUM-4855)
- **NFR-14 / DR-03 (워크스페이스 격리):** Story 2 (SCRUM-4851) + 모든 도메인 모듈
- **NFR-15 / DR-07 (ActivityEvent):** Story 4 (SCRUM-4857)에서 모듈 도입, 이후 모든 도메인 모듈이 emit
- **TC-07 / ADR-004 (고정 ## 헤더):** Story 4 (SCRUM-4857, SCRUM-4860)
- **TC-08~11 (모노레포/Prisma/로컬):** Story 1 (SCRUM-4847)

## 6. Confluence 작업지시서

- 부모 페이지: [Task Context Hub - 구현 (Implementation)](https://team-2026.atlassian.net/wiki/spaces/~5c1214f4a424561a8ea64bc5/pages/110002177)
- 하위 구조: **10 Story 페이지**(`{순번}. {요약} ({Story 키})`) → 각 Story 페이지 하위에 해당 Subtask 작업지시서(`{순번}-{서브}. {요약} ({Subtask 키})`)
- 각 작업지시서 페이지에 포함된 섹션: 개요 / 요구사항(FR·NFR·DR·TC·ADR 인용) / 작업 항목(체크리스트) / 기술 참고사항 / 디자인 참고사항(UX-Design-Spec §2 토큰 인용) / 검수 기준(Given·When·Then)
- 모든 Subtask에 Confluence 작업지시서가 Remote Link로 연결 (26/26)
