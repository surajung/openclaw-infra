# n8n Workflow Management

이 디렉토리는 n8n 워크플로우의 JSON export와 관련 문서를 파일 기반으로 관리하기 위한 공간입니다.

## 목적
- GUI에만 의존하지 않고 workflow 원본을 파일로 보관
- 변경 이력을 Git으로 추적
- 가비서가 workflow를 읽고 수정하기 쉽게 구조화

## 구조
- `workflows/` : 운영 반영 기준의 실제 export JSON (source of truth)
- `notes/` : workflow 설명, 입출력 스키마, 운영 메모
- `experiments/` : 실험안, 튜닝본, 설계 초안

## 디렉토리 역할 규칙
- `workflows/`에는 **운영 기준본만** 둡니다.
- `experiments/`에는 아직 확정되지 않은 설계안/튜닝본/비교본을 둡니다.
- 같은 "draft"라는 표현이 `posts/`의 게시용 초안과 혼동되므로, n8n 쪽은 `drafts/` 대신 `experiments/`를 사용합니다.

## 권장 흐름
1. n8n에서 workflow를 export
2. 운영 반영본은 `workflows/`에 저장
3. 실험/수정 중간본은 `experiments/`에서 작업
4. 필요 시 `notes/`에 입력/출력/운영 메모 정리
5. 검토 완료 후 `experiments/` 내용을 `workflows/`에 반영
