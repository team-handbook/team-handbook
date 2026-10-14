# 기여 가이드 — 계약위험탐지서비스

## 브랜치 이름

`<type>/<이슈번호>-<kebab-case 요약>` 예: `feat/42-deid-pipeline`, `fix/57-gate-g4-message`

| type | 쓰임 |
| --- | --- |
| feat | 기능 추가 |
| fix | 버그 수정 |
| refactor | 동작 변화 없는 구조 개선 |
| perf | 성능 개선 |
| test | 테스트 추가·수정 |
| docs | 문서·설계 도면(design/) 수정 |
| chore | 빌드·설정·의존성 등 |
| hotfix | 운영(main) 긴급 수정 |

## 커밋 메시지

`<type>(#이슈번호): 요약` 예: `feat(#42): 비식별화 파이프라인 추가`

type: feat, fix, refactor, perf, test, docs, chore, revert

## 작업 전 확인

- Node 20 LTS(`.nvmrc`), 루트·`backend`·`frontend`·`tools/model-api-stub` 각각 `npm ci`
- 모델 호출은 개발·CI 에서 `tools/model-api-stub`(:9542). 게이트웨이와 둘 중 하나만 띄운다

## 꼭 지키는 규칙 (CLAUDE.md)

- 비식별화 전 텍스트를 DB·로그·모델 API 로 보내지 않는다(`DeidentifiedText` 타입만 허용)
- `design/crd_ddl.sql` 은 수정하지 않는다. 유도 판정은 DB 뷰(`v_*`)를 단일 지점으로 쓴다
- 게이트 G0~G14 응답은 `gates` 모듈의 `GateError` 로만 만든다(문구 = SD_02 §14-2)
- DB 비밀번호·모델 API 키를 코드·로그·문서에 쓰지 않는다(`backend/.env`, `model-server/.env` 만)
- 공유 Ollama 에는 `pull`·`create`·`rm`·`stop`·`serve` 를 런타임에서 부르지 않는다(상태 조회는 60초 캐시)
- 구현을 바꿨으면 `/sad` 로 `design/` 도면에 반영한다

## 머지 전 확인

- `npm run lint`, `npm run secrets:scan`
- `npm run typecheck --prefix backend`
- `npm test --prefix backend|frontend`, `npm run db:ddl-tests --prefix backend`
- 모델 서버 변경 시 `cd model-server && uv run pytest -q`
- CI(lint → test → build → deploy)가 초록인지 확인. `deploy` 는 `main` 에서만 돈다

## PR 규칙

- PR 템플릿을 모두 채운다. 제목은 이슈 제목과 맞춘다.
- 리뷰어 1명이 승인한 뒤 작성자가 머지한다.
- 머지 후 원격과 로컬의 작업 브랜치를 삭제한다.
