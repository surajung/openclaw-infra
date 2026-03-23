# geeknews-summary

## 목적
- GeekNews 기반 기술 뉴스 요약을 생성해 Daily 브리핑에 공급하는 n8n workflow

## 현재 구조
1. `Webhook`
2. `RSS Read`
3. `Aggregate`
4. `Basic LLM Chain`
5. `Code in JavaScript`

Gemini 모델은 `Basic LLM Chain`의 language model로 연결된다.

## 노드별 역할
### Webhook
- 경로: `geeknews-summary`
- 외부에서 호출되는 진입점

### RSS Read
- GeekNews RSS 피드(`https://feeds.feedburner.com/geeknews-feed`)를 읽음

### Aggregate
- 여러 RSS item을 `news_list` 배열로 집계
- 포함 필드: `title`, `link`, `content`

### Basic LLM Chain
- `news_list`를 입력으로 받아 중요도 높은 항목만 골라 JSON 형식으로 요약
- 중복/유사 주제 병합, 오래된 이슈 제외

### Code in JavaScript
- LLM 출력 후처리
- 코드블록 제거
- JSON 느슨한 파싱
- `summaryText` 정리
- `items` 정규화 및 dedupe
- 최종 응답 스키마 래핑

## 출력 스키마
```json
{
  "ok": true,
  "source": "geeknews",
  "generatedAt": "ISO-8601",
  "summaryText": "문단형 요약",
  "items": [
    { "title": "...", "url": "https://..." }
  ]
}
```

## 강점
- 구조가 단순하고 직선적이라 유지보수 쉬움
- 운영용 JSON 응답 스키마가 분명함
- 후처리 노드가 있어 LLM 출력 변동성을 흡수함
- 이후 watchlist-summary workflow의 기준 레퍼런스로 쓰기 좋음

## 개선 포인트
- 실패 시 `ok:false` 응답을 주는 fallback 분기 추가 검토
- RSS 전체가 길어질 경우 최근 N개 제한 필요
- `content` 전체 대신 축약 필드만 LLM에 전달하는 최적화 가능

## watchlist-summary로 재사용 가능한 부분
- `Webhook`
- `Aggregate`
- `Basic LLM Chain` 패턴
- `Code in JavaScript` 후처리 구조

## watchlist-summary에서 바뀔 부분
- 입력 소스 (`RSS Read` 대상 URL)
- 프롬프트 내용
- `source` 값
- 필요 시 출력 스키마 일부 필드
