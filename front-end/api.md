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

```text
<button class="ajaxsend">AJAX SEND</button>
<div class="result"></div>
<script>
  const apiKey = '430156241533f1d058c603178cc3ca0e';
  const dailyBoxOffice = `http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?key=${apiKey}`;
  document.querySelector('.ajaxsend').addEventListener('click', function() {
    let movieAPI = `${dailyBoxOffice}&targetDt=20190904`;
    fetchURL(movieAPI, findRank);
  });
  function fetchURL(url, callback) {
      fetch(url).then(function(response) {
        response.text().then(function(data) {
          callback(JSON.parse(data));
        });
      });
    }
    
  function findRank(data) {
    let movieList = data.boxOfficeResult.dailyBoxOfficeList;
    let length = movieList.length;
    let ranking = `<ol>`;
    for (let i = 0; i < length; i++) {
      ranking += `<li>
        <div>
          <span>${i + 1}</span>
          ${movieList[i].rankOldAndNew === 'NEW' ? `<em>신규진입</em>` : ''}
          <strong class="tit_movie" data-moviecd="${movieList[i].movieCd}">${movieList[i].movieNm}</strong>
          <p>${movieList[i].openDt} 개봉</p>
          <p>오늘 ${movieList[i].audiCnt} 명 관람</p>
          <p>누적 관객 ${movieList[i].audiAcc} 명</p>
          <p>전일대비 ${movieList[i].rankInten > 0 ? parseInt(movieList[i].rankInten) + ' 상승' : parseInt(movieList[i].rankInten) + ' 하락'}</p>
        </div>
      </li>`;
    }
    ranking += `</ol>`;
    document.querySelector('.result').innerHTML = ranking;
  }
```



