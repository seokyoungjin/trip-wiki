# trip-wiki

여행 도시 정보를 **지역별/정렬/검색**으로 탐색하고, 도시 카드를 클릭해 **상세 페이지**를 확인하는 간단한 SPA(바닐라 JS) 프로젝트입니다.

## 실행 방법

### 요구 사항

- Node.js (권장: LTS)

### 설치

```bash
npm install
```

### 서버 실행

이 프로젝트는 Express로 정적 파일을 서빙합니다.

```bash
node server/server.js
```

브라우저에서 아래 주소로 접속합니다.

- `http://localhost:3000`

## 주요 기능

- **지역 선택**: 특정 지역(Region) 기준으로 도시 목록 조회
- **정렬**: 쿼리스트링 `sort` 기준 정렬 (기본값: `total`)
- **검색**: 쿼리스트링 `search`로 도시 검색
- **무한 스크롤 대신 더보기**: `+ 더보기` 버튼으로 추가 로드(40개 단위)
- **도시 상세**: `/city/:id` 경로로 상세 정보 표시

## 데이터/API

도시 데이터는 외부 API를 사용합니다.

- **Base URL**: `https://trip-wiki-api.vercel.app/`
- **도시 목록**: `GET /?start={start}&sort={sort}&search={search}`
    - 지역 필터 사용 시: `GET /{region}?start={start}&sort={sort}&search={search}`
- **도시 상세**: `GET /city/{cityId}`

## 라우팅(클라이언트)

Express는 모든 경로를 `index.html`로 보내고, 화면 전환은 `history.pushState` 기반으로 동작합니다.

- **목록 화면**: `/{region}?sort=...&search=...`
- **상세 화면**: `/city/{id}`

## 폴더 구조(요약)

- `index.html`: 앱 엔트리 HTML
- `src/index.js`: 앱 시작점
- `src/App.js`: 라우팅/상태/렌더링 오케스트레이션
- `src/components/`: UI 컴포넌트 및 API 유틸
    - `api.js`: 외부 API 호출(`request`, `requestCityDetail`)
- `server/server.js`: Express 정적 서버 (기본 포트: 3000)

## 참고

- `package.json`에 실행 스크립트가 정의되어 있지 않아, 현재는 `node server/server.js`로 실행합니다.
