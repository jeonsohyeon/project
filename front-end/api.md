---
description: 영화 API 활용하여 일별 박스오피스를 출력해본다.
---

# API 활용

## 1. API 키 발급

[영화진흥위원회](http://www.kobis.or.kr/kobisopenapi/homepg/main/main.do)에서 회원가입 / 키 발급 관리-API 키 발급

## 2. 데이터 요청

 Request URL 구조 : **기본 요청 URL** + **?key=\[API Key\]** + &params=value

```text
ex)
http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?
key=430156241533f1d058c603178cc3ca0e
&targetDt=20120101
```

## 3. 데이터 출력

### 가. 보일러 플레이트 셋팅

[express-generator](https://expressjs.com/ko/starter/generator.html) 로 기본 템플릿을 만든다.

```text
express movieAPI --view=ejs
cd movieAPI
npm i
DEBUG=movieapi:* npm start
http://localhost:3000/ 접속
```

### 나. FETCH 요청

* /view/index.ejs 에 버튼 클릭시 fetch 요청이 발생하여 result 를 출력하도록 설정



