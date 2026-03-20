# <stack-name>

## 목적
- 이 스택이 무엇을 하는지 한 줄 설명

## 노출 포트
- 예: `127.0.0.1:9999 -> 9999`

## 필수 환경변수
- `EXAMPLE_VAR`: 설명

## 실행
```bash
cd <stack-directory>
docker-compose up -d
```

## 상태 확인
```bash
docker-compose ps
curl http://127.0.0.1:9999/healthz
```

## 로그 확인
```bash
docker-compose logs -f
```

## 중지
```bash
docker-compose down
```

## 운영 메모
- reverse proxy 여부
- 데이터 저장 위치
- 외부 공개 여부
