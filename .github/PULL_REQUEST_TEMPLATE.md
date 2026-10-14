## 관련 이슈

Closes #

## 변경 내용

## 영향 범위

- [ ] backend (`backend/src/modules/…`)
- [ ] frontend (`frontend/src/views/…`)
- [ ] model-server
- [ ] db/migrations
- [ ] design/ 도면 · 문서

## 체크리스트

- [ ] 브랜치 이름이 규칙을 따른다
- [ ] 커밋 메시지가 규칙을 따른다
- [ ] 리뷰어를 지정했다
- [ ] `lint` · `secrets:scan` · `typecheck` 통과
- [ ] 관련 테스트(`backend`/`frontend`/`model-server`/`db:ddl-tests`) 통과
- [ ] 비식별화 전 텍스트를 DB·로그·모델 API 로 보내지 않았다(`DeidentifiedText`)
- [ ] `design/crd_ddl.sql` 을 수정하지 않았고, 유도 판정은 `v_*` 뷰를 쓴다
- [ ] 게이트 응답은 `gates` 모듈의 `GateError` 로만 만들었다
- [ ] 비밀번호·API 키를 코드·로그·문서에 넣지 않았다
- [ ] 구현 변경을 `design/` 도면(`/sad`)에 반영했거나, 반영 불필요함을 확인했다

## 리뷰어에게
