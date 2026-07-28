# 도구 목록 (10종)

한국일보 공개 홈페이지 데이터를 메타데이터 중심으로 노출합니다. 모든 도구는 **읽기 전용**이며,
기사 본문 전문은 반환하지 않습니다.

| 도구 | 용도 | 필수 입력 | 선택 입력 |
|---|---|---|---|
| `search_news` | 자연어/주제 질의로 관련 기사 검색(AI) | `query` | `limit`(1~20, 기본 5) |
| `list_top_headlines` | 오늘의 주요 뉴스(편집부 머리기사) | 없음 | 없음 |
| `list_timely_news` | 지금 볼만한 뉴스(시간대 추천) | 없음 | 없음 |
| `list_popular_news` | 많이 본 인기 뉴스(분야/전체) | 없음 | `section_cd`(기본 `all`), `page_size`(기본 20), `exclude_section_cd` |
| `list_latest_news` | 최신 기사(최근 발행 순) | 없음 | `page_num`(기본 1), `page_size`(기본 20) |
| `list_most_read_news` | 홈의 '꼼꼼히 본 뉴스' 묶음(+ 많이 본) | 없음 | 없음 |
| `list_recommended_articles` | 분야별 편집부 추천 기사 | `section_cd` | `page_size`(기본 40) |
| `get_daily_horoscope` | 오늘의 운세(제목·링크만) | 없음 | `date`(YYYY-MM-DD, 기본 오늘 KST) |
| `get_mbti_horoscope` | MBTI 오늘의 운세(제목·링크만) | 없음 | `date`(YYYY-MM-DD, 기본 오늘 KST) |
| `list_sections` | 섹션 코드·한글명 목록 | 없음 | 없음 |

## 입력 형식

- `query`: 1~200자 자연어 질의.
- `date`: `YYYY-MM-DD`. 생략 시 한국 시간(Asia/Seoul) 오늘.
- `section_cd`: 소문자 슬러그(`list_sections` 로 확인). `list_popular_news` 만 `all` 허용.
- `page_size`: 1~100 범위로 클램프.
- `limit`(search_news): 1~20 범위로 클램프(기본 5).

## 반환 값

기사 제목, 한국일보 원문 링크, 썸네일, 발행일, 분야, 기자/바이라인, 기사 구분(일반/단독/속보),
원문 접근성 등 **메타데이터**를 반환합니다. 일부 도구는 짧은 발췌(excerpt)를 함께 제공하며,
발췌는 도입부 일부일 뿐 기사 전체 요약이 아닙니다.

- **응답 구조와 필드 구성은 도구마다 다릅니다.** 정확한 스키마는 MCP `tools/list` 응답의
  `outputSchema` 를 참고하세요 — 각 필드 설명이 함께 담겨 있습니다.
- 값이 없는 필드는 응답에서 생략됩니다.

## 운세 도구

`get_daily_horoscope`·`get_mbti_horoscope` 도 다른 기사와 동일하게 제목·발행일·원문 링크 등 메타데이터만
반환하고 운세 내용은 노출하지 않습니다. 원문 링크로 한국일보에서 확인하세요.
