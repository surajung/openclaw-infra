# n8n Workflow Management

이 디렉토리는 n8n 워크플로우의 JSON export와 관련 문서를 파일 기반으로 관리하기 위한 공간입니다.

## 목적
- GUI에만 의존하지 않고 workflow 원본을 파일로 보관
- 변경 이력을 Git으로 추적
- 가비서가 workflow를 읽고 수정하기 쉽게 구조화

## 구조
- `workflows/` : 운영 반영 기준의 실제 export JSON (source of truth)
- `notes/` : workflow 설명, 입출력 스키마, 설계 메모, 운영 메모
- `archive/` : 참고용 원본 또는 보관본

## 디렉토리 역할 규칙
- `workflows/`에는 **운영 기준본만** 둡니다.
- 설계 문서와 변경 이유, 운영 맥락은 `notes/`에 기록합니다.
- 비교가 끝난 중간 JSON은 남기지 않고, 확정본만 `workflows/`에 유지합니다.

## 권장 흐름
1. n8n에서 workflow를 export
2. 운영 반영본은 `workflows/`에 저장
3. 설계 배경, 입출력, 주의사항은 `notes/`에 정리
4. 필요 시 참고용 원본은 `archive/`에 보관
