# penguin-math keep-warm

펭귄수학 API(Vercel 서버리스 + Neon)를 깨워 두는 스케줄 워크플로. 5분마다 실행.

- 항상: `GET /api/v1/health` — Vercel 함수 인스턴스를 살려 둔다 (DB 안 건드림)
- 한국 시간 16:00–23:59: `GET /api/v1/health?deep=1` — `SELECT 1` 로 Neon 컴퓨트도 깨워 둔다
  (Neon 무료 한도 월 100 CU시간 → 하루 7시간만 깨워서 약 50시간 사용)
- DB 응답이 실패(503)하면 워크플로가 실패해 GitHub 가 메일 알림을 보낸다
- 하루 한 번 `last-ping.txt` 를 갱신해 커밋 → 60일 비활성으로 스케줄이 꺼지는 것 방지

공개 저장소인 이유: 공개 저장소는 Actions 분수가 무료·무제한. 담긴 건 공개 health 주소뿐이다.
본 프로젝트 문서: penguin_math 저장소 `docs/deployment.md` "콜드 스타트 방지".
