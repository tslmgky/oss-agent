# tools.py 함수 정리 (수정 전)

대상 파일: `week09/oss-week7-copy/tools.py`

## 파일 개요

KOBIS(영화진흥위원회) 오픈 API를 이용해 박스오피스 정보를 가져오는 도구 모음입니다.

- 사용하는 라이브러리: `requests`
- API 키: `secret.py`의 `API_KEY`를 가져와 사용
- 상수 `BASE_URL`: 일별 박스오피스 조회 API 주소
  (`https://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json`)

## 함수 목록

파일에 들어 있는 함수는 **1개**입니다.

### `get_boxoffice_rank_1(date)`

그 날짜의 박스오피스 1위 영화 제목을 알려줍니다.

| 구분 | 내용 |
| --- | --- |
| 받는 것 | `date` (문자열) — 8자리 날짜. 예: `"20260824"` |
| 돌려주는 것 | (문자열) 1위 영화 제목. 예: `"오디세이"` |

동작 순서:

1. API 키(`key`)와 날짜(`targetDt`)를 요청 파라미터로 만든다.
2. `BASE_URL`로 GET 요청을 보낸다 (타임아웃 10초).
3. 응답 JSON에서 `boxOfficeResult` → `dailyBoxOfficeList` 목록을 꺼낸다.
4. 목록의 첫 번째 영화(1위)의 `movieNm`(영화 제목)을 돌려준다.

## 참고: 눈에 띄는 점

- 응답 상태 코드나 API 오류를 확인하지 않습니다. 키가 잘못됐거나 날짜 형식이 틀리면 `KeyError` 등으로 바로 실패합니다.
- 해당 날짜의 목록이 비어 있으면 `movies[0]`에서 `IndexError`가 납니다.
- 1위 제목만 돌려주므로, 다른 순위나 관객 수 등의 정보는 얻을 수 없습니다.
