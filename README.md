# 바로영한

웹을 읽다가 Chrome 사이드패널에서 영어 단어의 한국어 뜻을 바로 찾는 도구입니다. Naver 영한사전 비공식 API를 중계하는 Express 서버와 Chrome 확장프로그램으로 이루어져 있습니다.

![검색 결과: 사전 선택 버튼, 발음기호, 품사별 뜻과 예문](docs/screenshots/result-state.png)

- 품사별 뜻과 영어 예문, 한국어 번역 표시
- Oxford·동아·YBM 사전 전환
- 검색에 성공한 최근 단어를 최대 8개 저장, 추천 단어 표시

## 시작하기

Node.js와 사이드패널을 지원하는 Chrome이 필요합니다. 저장소 루트에서 실행합니다.

```bash
npm install
cp extension/config.example.js extension/config.js
npm start       # http://localhost:3001, /health 가 {"ok":true} 를 반환
```

Chrome에 확장프로그램을 등록합니다.

1. `chrome://extensions`에서 개발자 모드를 켭니다.
2. **압축해제된 확장 프로그램을 로드합니다**에서 `extension/` 폴더를 고릅니다.
3. 툴바 아이콘이나 `Alt+K`로 패널을 엽니다.

포트는 `PORT` 환경변수로 바꿉니다. 바꾸면 `extension/config.js`의 `window.DICT_SERVER`도 맞춥니다.

## API

| 요청 | 동작 |
| --- | --- |
| `GET /api/naver/lookup?word=<word>` | 검색과 항목 조회를 한 번에 (선택: `source=동아`, `source=YBM`) |
| `GET /api/naver/search?query=<word>` | Naver 검색 응답 그대로 반환 |
| `GET /api/naver/entry?entryId=<id>` | 항목의 뜻과 예문을 정리해 반환 |

응답 구조는 [`server/server.js`](server/server.js)에 있습니다.

## 배포

[`docker-compose.yml`](docker-compose.yml)로 띄우면 `http://127.0.0.1:8002`에서 열립니다(포트는 `APP_PORT`). 이때 `extension/config.js`의 `window.DICT_SERVER`도 이 주소로 바꿉니다. Ubuntu/Debian에서 Nginx·Certbot으로 HTTPS를 붙이는 [`setup-server.sh`](setup-server.sh)도 있습니다. 시스템 설정을 바꾸니 실행 전에 내용을 확인하세요.

## 주의

Naver가 공개한 API가 아니어서, 주소나 응답 구조가 바뀌면 조회가 실패할 수 있습니다. 개인 로컬 사용을 전제로 만들었습니다. 여러 사람에게 공개하려면 Naver 이용약관을 먼저 확인하세요. 서버는 조회 결과를 1시간 캐시하고 외부 요청 사이에 지연을 둡니다.

## 라이선스

LICENSE 파일이 없습니다. 라이선스는 확인이 필요합니다. 포함된 Pretendard 글꼴은 [SIL Open Font License 1.1](extension/fonts/LICENSE.txt)을 따릅니다.
