# rsshub

## 목적
- Threads 등 소셜/웹 소스를 RSS 피드로 변환하기 위한 RSSHub 스택 초안

## 노출 포트
- 기본 테스트 포트: `127.0.0.1:1200 -> 1200`

## 필수 환경변수
- 현재 최소 테스트 버전은 필수 `.env` 없음
- 운영 전환 시 캐시/프록시 관련 변수 추가 예정

## 실행
```bash
cd /Users/surajung/.openclaw/workspace/infra/stacks/rsshub
docker-compose up -d
```

## 상태 확인
```bash
docker-compose ps
curl http://127.0.0.1:1200/healthz
```

## 로그 확인
```bash
docker-compose logs -f rsshub
```

## 중지
```bash
docker-compose down
```

## 운영 메모
- 현재는 테스트용 최소 구성
- 예시 route: `http://127.0.0.1:1200/threads/choi.openai`
- 운영용 전환 시 Redis/프록시 분리 검토
