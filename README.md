# 바로영한

웹을 읽다가 Chrome 사이드패널에서 영어 단어의 한국어 뜻을 바로 찾는 도구입니다. Naver 영한사전 비공식 API를 중계하는 Express 서버와 Chrome 확장프로그램으로 이루어져 있습니다.

Naver가 공개한 API가 아니어서 주소나 응답 구조가 바뀌면 조회가 실패할 수 있습니다. 개인 로컬 사용을 전제로 만들었으며, 여러 사람에게 공개하려면 Naver 이용약관을 먼저 확인하세요.

![검색 결과: 사전 선택 버튼, 발음기호, 품사별 뜻과 예문](docs/screenshots/result-state.png)

## 시작하기

Node.js 20과 npm, 사이드패널을 지원하는 Chrome이 필요합니다. 단어를 조회하려면 Naver 사전에 접속할 수 있어야 합니다. 저장소 루트에서 실행합니다.

```bash
npm install
cp extension/config.example.js extension/config.js
npm start
```

서버 주소는 `http://localhost:3001`입니다. `/health`의 정상 응답은 `{"ok":true}`입니다.

1. `chrome://extensions`에서 개발자 모드를 켭니다.
2. **압축해제된 확장 프로그램을 로드합니다**에서 `extension/` 폴더를 고릅니다.
3. 툴바 아이콘이나 `Alt+K`로 패널을 열고 `resilient`를 검색합니다.

## 관련 문서

- [작업 기록과 보류 항목](TODO.md)

## 라이선스

프로젝트의 LICENSE 파일이 없어 라이선스는 확인이 필요합니다. 포함된 Pretendard 글꼴은 [SIL Open Font License 1.1](extension/fonts/LICENSE.txt)을 따릅니다.
