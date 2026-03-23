# n8n Workflow Management

이 디렉토리는 n8n 워크플로우의 JSON export와 관련 문서를 파일 기반으로 관리하기 위한 공간입니다.

## 목적
- GUI에만 의존하지 않고 workflow 원본을 파일로 보관
- 변경 이력을 Git으로 추적
- 가비서가 workflow를 읽고 수정하기 쉽게 구조화

## 구조
- `workflows/` : 실제 export JSON
- `notes/` : workflow 설명, 입출력 스키마, 주의사항
- `drafts/` : 실험/수정 초안

## 권장 흐름
1. n8n에서 workflow를 export
2. `workflows/`에 저장
3. 필요 시 `notes/`에 입력/출력/운영 메모 정리
4. 수정 작업은 초안 또는 새 버전으로 만든 뒤 검토 후 반영
