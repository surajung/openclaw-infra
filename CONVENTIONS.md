# Infra Conventions

## 1) 저장소 경계
- `infra/`는 형상관리 대상 원본 저장소이다.
- 실제 운영 디렉토리는 기본적으로 workspace 밖에 둔다.
- 운영 디렉토리는 배포 결과물로 취급한다.

## 2) Docker Compose 규칙
- 파일명은 기본적으로 `docker-compose.yml` 사용
- Compose project name은 반드시 명시 권장
  - 예: `name: rsshub-prod`
- 이 환경에서는 `docker compose`보다 `docker-compose`를 우선 사용
- 기본 재시작 정책은 `restart: unless-stopped`
- 시간대는 `TZ: Asia/Seoul`

## 3) 환경변수 규칙
- 실제 비밀값은 `.env`
- 저장소에는 `.env.example`만 커밋
- `.env.example`에는 변수명/설명/예시값만 포함
- 토큰, API 키, 실제 도메인 비밀정보는 금지

## 4) 디렉토리 규칙
- `templates/`: 공통 재사용 템플릿
- `stacks/<service>/`: 서비스별 초안
- 각 stack 디렉토리에는 최소 아래 파일 포함
  - `README.md`
  - `docker-compose.yml`
  - `.env.example`

## 5) README 규칙
각 stack README에는 아래 항목을 포함한다.
- 목적
- 노출 포트
- 필수 환경변수
- 실행 방법
- 상태 확인 방법
- 로그 확인 방법
- 중지 방법
- 운영 메모

## 6) 포트 규칙
- 테스트용 포트와 운영 포트를 구분한다.
- 포트 충돌 시 README에 이유와 변경 이력을 남긴다.
- 외부 공개 여부를 명시한다.

## 7) 볼륨/데이터 규칙
- 런타임 데이터는 Git 관리 대상이 아니다.
- bind mount 경로는 README에 기록한다.
- 서비스별 데이터 경로는 명확한 이름을 사용한다.

## 8) 보안 규칙
- 외부 공개 서비스는 reverse proxy/auth/rate limit 고려
- Cloudflare Tunnel 또는 유사 프록시를 붙이는 경우 연결 구조를 README에 기록
- 테스트용 스택을 외부 공개용으로 바로 승격하지 않는다.

## 9) 변경 절차
1. `infra/` 원본 수정
2. 로컬 테스트
3. 운영 디렉토리 반영
4. README 갱신
5. 필요 시 변경 이유를 커밋 메시지에 명확히 남김
