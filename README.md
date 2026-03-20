# Infra Workspace

이 디렉토리는 Docker/인프라 관련 **표준, 템플릿, 스택 초안**을 관리하는 공간입니다.

## 목적
- 새 Docker 스택을 제로베이스로 만들지 않기
- 공통 규칙(네이밍, 포트, env, healthcheck)을 재사용하기
- 운영용 디렉토리(`~/n8n-docker`, `~/rsshub-docker` 등)와 분리된 설계 원본을 유지하기
- GitHub 형상관리 친화적으로 유지하기

## 기본 원칙
- 이 폴더는 **설계 원본/템플릿 저장소**입니다.
- 실제 운영 스택은 기본적으로 workspace 밖(예: `~/n8n-docker`)에 둡니다.
- 민감 정보는 절대 커밋하지 않습니다. 실제 값은 `.env`에 두고, 저장소에는 `.env.example`만 둡니다.
- 이 환경에서는 `docker compose` 대신 `docker-compose` 사용을 우선합니다.

## 디렉토리 구조
```text
infra/
  README.md                # 이 문서
  CONVENTIONS.md           # 운영/구조 규약
  .gitignore               # Git 제외 규칙
  templates/               # 재사용 가능한 compose/env 템플릿
    docker-compose.base.yml
    .env.example
    STACK_README.template.md
  stacks/                  # 서비스별 스택 초안/버전관리 대상
    rsshub/
      README.md
      docker-compose.yml
      .env.example
    n8n/
      README.md
      docker-compose.yml
      .env.example
```

## 권장 워크플로우
1. `templates/` 또는 기존 `stacks/`를 복사해 새 스택 초안을 만든다.
2. `stacks/<service>/README.md`와 `.env.example`를 먼저 정리한다.
3. 로컬 테스트 후 실제 운영 위치(예: `~/rsshub-docker`)로 배포한다.
4. 운영 중 변경이 필요하면 먼저 `infra/`의 원본을 갱신하고, 이후 운영 디렉토리에 반영한다.

## GitHub 업로드 기준
커밋 대상:
- 문서 (`README.md`, `CONVENTIONS.md`)
- 템플릿 (`templates/`)
- 스택 초안 (`stacks/*/docker-compose.yml`)
- 샘플 env (`.env.example`)

커밋 금지:
- `.env`
- 실제 토큰/도메인 비밀값
- 런타임 로그
- 로컬 데이터 볼륨
- 임시 테스트 출력

## 다음 단계 후보
- `rsshub` 스택을 `stacks/rsshub/`로 정리
- `n8n` 스택도 동일 규격으로 초안화
- 배포 스크립트(`scripts/`) 추가
