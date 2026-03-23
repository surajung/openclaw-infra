# n8n

## 목적
- n8n 운영 스택의 표준 설계 원본

## 상태
- **Ready**: `~/n8n-docker` 환경을 기준으로 표준화 완료
- 운영 중인 실제 서비스와 동기화된 템플릿입니다.
- `docker-compose.yml` 파일이 추가되어 스택 정의가 명확해졌습니다.

## 노출 포트
- `5678 -> 5678` (내부 및 Cloudflare Tunnel 경유)

## 필수 환경변수
- `N8N_ENCRYPTION_KEY`: n8n 데이터 암호화용 키 (고정 필수)
- `CLOUDFLARED_TOKEN`: Cloudflare Tunnel 인증 토큰
- 기타 `N8N_HOST`, `WEBHOOK_URL` 등
- **`.env` 파일**: 위 환경변수들은 `.env` 파일에 정의되어야 합니다. 예시 (`.env.example`) 파일을 참조하세요.

## 실행
```bash
# 운영 디렉토리로 복사 후 실행 권장
cd ~/n8n-docker
docker-compose up -d
```

## 상태 확인
```bash
docker-compose ps
curl -I https://n8n.surajung.com/healthz
```

## 로그 확인
```bash
docker-compose logs -f n8n
```

## 운영 메모
- **Persistence**: `./data` 폴더가 컨테이너의 `/root/.n8n`에 매핑되어 있습니다.
- **External Storage**: `/Volumes/Data_Server` 볼륨이 `/data/storage`에 연결되어 I/O 작업을 수행합니다.
- **Security**: Cloudflare Tunnel(`cloudflared`) 서비스를 통해 외부 노출을 제어합니다.
