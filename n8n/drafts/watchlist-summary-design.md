# watchlist-summary 설계 초안

## 목적
- RSSHub가 제공하는 Threads/X 등 워치리스트 피드를 읽고, Daily 브리핑용 요약 JSON을 반환

## 기본 방향
- `geeknews-summary` workflow를 레퍼런스로 복제/파생
- 차이는 입력 소스와 프롬프트, `source` 값 중심으로 최소화

## 예상 입력 소스
예시:
- `http://127.0.0.1:1200/threads/choi.openai`
- 추후 여러 피드를 합칠 경우 RSS Read 다중 소스 또는 Merge 구조 검토

## 예상 경로
- webhook path: `watchlist-summary`

## 예상 출력 스키마
```json
{
  "ok": true,
  "source": "threads-watchlist",
  "generatedAt": "ISO-8601",
  "summaryText": "문단형 요약",
  "items": [
    { "title": "...", "url": "https://..." }
  ]
}
```

## 예상 노드 구조
1. `Webhook`
2. `RSS Read`
3. `Aggregate`
4. `Basic LLM Chain`
5. `Code in JavaScript`
6. `Google Gemini Chat Model`

## 프롬프트 방향
- 워치리스트 항목 중 의미 있는 주제만 3~5개 선별
- 중복/유사 주제 병합
- 단순 링크 나열보다 '왜 볼 만한지'를 짧게 드러내기
- Daily 브리핑에 넣기 좋은 길이로 제한
- 반드시 JSON 출력

## 추가 고려사항
- 여러 계정을 합칠 경우 source별 구분 필요
- 단일 계정으로 시작 후 다중 계정 확장 권장
- 피드 항목 수가 많으면 최신 N개 제한 필요
- 실패 시 `ok:false` fallback 응답 검토
