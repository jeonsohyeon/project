# Process

## 기본

* 컨벤션 가이드 확인
  * CSS 방법론\_BEM, SMACSS, OOCSS
  * 대응 범위 설정\(PC, Mobile\) 
  * 최소사이즈 대응 확인\(mobile 320/tablet 768/pc 1024\)
  * 이미지 최적화 or 리소스 최적화 기준 설정
  * 공통 모듈/가이드 컨벤션 확인
  * 레이아웃/서브 페이지 나누기
* 기획서 확인
* 전체적인 일정 확인 및 점검
* 수정 요청 방식\(메일&문자or메신저\)
* 디자인 수급 : PSD / 스케치&제플린
* 웹폰트 수급

```
@font-face {
    font-family: 'kakaoFont-bold';
    font-style: normal;
    font-weight: normal;
    src: url(font/KakaoMoblieBold.eot);/ IE9 호환성 보기 /
    src: local("☺"),/ 웹 브라우저가 지원하지 않는 불필요한 웹 폰트 호출을 막는데 사용 /
    url(경로.eot?#iefix) format('embedded-opentype'),/ IE6-IE8 /
    url(경로.woff2) format('woff2'),/ WOFF의 차기 포맷 /
    url(경로.woff) format('woff'),/ 표준 브라우저 /
    url(경로.ttf) format('truetype'); / Safari, Android, iOS /
}
```

{% hint style="info" %}
 **작업일정버퍼**

* 작업 준비
* 문서화 시간커뮤니케이션 소요 시간
* 이미지 슬라이싱
* 마크업 시간
* 디자인 필터링 및 테스트 시간
{% endhint %}

##  업무환경\_개발 협업 환경

* 버전관리 방법 설정 \(GIT&SVN\) 
* 이슈관리 : 레드마인, 지라
* CI : 허드슨
* 디비 : 몽고디비, mysql
* 서버
* es6 코드 변환을 위한 Babel
* 번들링 패키징 Webpack
* 디플로이 : 트래비스, 젠킨스
* 빌드/배포 : maven, 앤트, grunt, gulp
* 테스트 : Karma, Jasmine, PhantomJS
* 프로젝트 커뮤니케이션 방법 설정 \(jira, trello, slack, 일간or주간회의\)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xBC29;&#xC2DD;</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#xC560;&#xC790;&#xC77C; &#xD504;&#xB85C;&#xC138;&#xC2A4;</td>
      <td style="text-align:left">
        <p>1 &#xC2A4;&#xD504;&#xB9B0;&#xD2B8;(2~4&#xC8FC;) &#xC548;&#xC5D0; &#xBC30;&#xD3EC;&#xAE4C;&#xC9C0;
          &#xB2E4; &#xC9C4;&#xD589;&#xB418;&#xC5B4;&#xC57C;.</p>
        <p>1 &#xC720;&#xC800;&#xC2A4;&#xD1A0;&#xB9AC; : &#xC5D4;&#xB4DC;&#xC720;&#xC800;&#xAC00;
          &#xD6A8;&#xACFC;&#xB97C; &#xBC1B;&#xC744;&#xC218;&#xC788;&#xB294; &#xB2E8;&#xC704;&#xBCC4;.
          &#xBAA8;&#xB4E0; &#xAE30;&#xB2A5;&#xC774; &#xC544;&#xB2C8;&#xB77C;, &#xC791;&#xC740;
          &#xAE30;&#xB2A5; &#xD558;&#xB098;&#xB9CC; &#xC644;&#xB8CC;&#xB418;&#xC5B4;&#xB3C4;
          &#xBC30;&#xD3EC;&#xD574;&#xC11C; &#xD5A5;&#xC0C1;&#xC774; &#xAC00;&#xB2A5;&#xD558;&#xB2E4;.</p>
        <p></p>
        <ul>
          <li>&#xD50C;&#xB798;&#xB2DD; &#xB2E8;&#xACC4;&#xC5D0;&#xC11C; &#xBAA8;&#xB450;
            &#xCC38;&#xC5EC;&#xD574;&#xC11C;, &#xC2A4;&#xD1A0;&#xB9AC; &#xD3EC;&#xC778;&#xD2B8;&#xB97C;
            &#xC0C1;&#xB300;&#xC801;&#xC73C;&#xB85C; &#xC815;&#xD568;</li>
          <li>&#xC2A4;&#xD1A0;&#xB9AC; &#xD3EC;&#xC778;&#xD2B8;&#xB294; &#xC911;&#xC694;&#xB3C4;,
            &#xB9AC;&#xC18C;&#xC2A4;&#xB97C; &#xD310;&#xB2E8;&#xD558;&#xB294; &#xAE30;&#xC900;.
            &#xB9AC;&#xC18C;&#xC2A4;&#xB97C; &#xAC1C;&#xBC1C;&#xC790;&#xAC00; &#xC54C;&#xB824;&#xC90C;.</li>
          <li>&#xC911;&#xC694;&#xB3C4;&#xC5D0; &#xB530;&#xB77C; &#xC9C0;&#xB77C; &#xC774;&#xC288;&#xB97C;
            &#xC0DD;&#xC131;&#xD55C;&#xB2E4;.</li>
          <li>&#xC2A4;&#xD504;&#xB9B0;&#xD2B8; &#xB3D9;&#xC548; &#xD574;&#xB2F9; &#xC774;&#xC288;&#xB97C;
            &#xD574;&#xACB0;&#xD558;&#xB294;&#xB370;. &#xD558;&#xB098;&#xC758; &#xC2A4;&#xD1A0;&#xB9AC;&#xAC00;
            &#xB05D;&#xB0A0;&#xB54C;&#xAE4C;&#xC9C0; &#xB2E4;&#xB978; &#xC2A4;&#xD1A0;&#xB9AC;&#xB97C;
            &#xC548;&#xD55C;&#xB2E4;.</li>
          <li>&#xB2E4;&#xAC19;&#xC774; &#xD55C;&#xB2E4;&#xACE0;&#xD574;&#xB3C4; &#xACB0;&#xAD6D;
            &#xB514;&#xC790;&#xC774;&#xB108;&#xAC00; &#xC8FC;&#xAE30;&#xC804;&#xAE4C;&#xC9C0;
            &#xC548;&#xB418;&#xB294; &#xACBD;&#xC6B0;&#xB3C4; &#xC788;&#xB294;&#xB370;,
            &#xB514;&#xC790;&#xC774;&#xB108;&#xAC00; &#xB300;&#xB7B5; &#xC801;&#xC73C;&#xB85C;
            &#xD504;&#xB85C;&#xD1A0;&#xD0C0;&#xC785;&#xC744; &#xADF8;&#xB824;&#xC8FC;&#xBA74;
            &#xAC1C;&#xBC1C;&#xC790;&#xAC00; &#xB9CC;&#xB4EC;. (&#xC2A4;&#xD0C0;&#xC77C;&#xAC00;&#xC774;&#xB4DC;&#xAC00;
            &#xC788;&#xB294; &#xACBD;&#xC6B0;)</li>
          <li>&#xADF8;&#xB7EC;&#xBA74;&#xC11C; &#xB514;&#xC790;&#xC778;&#xC774; &#xC644;&#xB8CC;&#xB418;&#xBA74;
            &#xAC1C;&#xBC1C;&#xC790;&#xAC00; &#xAC19;&#xC774;&#xD55C;&#xB2E4;.</li>
          <li>&#xC2A4;&#xD504;&#xB9B0;&#xD2B8; &#xD6C4;&#xC5D4; &#xD68C;&#xACE0;&#xB97C;
            &#xD568;.</li>
          <li>&#xC7A5;&#xB2E8;&#xC810;&#xC744; &#xD1B5;&#xD574; &#xB2E4;&#xC74C;&#xC5D0;
            &#xD574;&#xC57C;&#xD558;&#xB294; &#xC561;&#xC158;&#xC544;&#xC774;&#xD15C;&#xC744;
            &#xB9CC;&#xB4E6;.</li>
          <li>&#xB2E4;&#xC74C; &#xC2A4;&#xD504;&#xB9B0;&#xD2B8;&#xB54C; &#xC561;&#xC158;&#xC544;&#xC774;&#xD15C;&#xC744;
            &#xC2E4;&#xD589;&#xD55C;&#xB2E4;.</li>
          <li>&#xAD6C;&#xCCB4;&#xC801;&#xC73C;&#xB85C;. &#xC9C0;&#xD45C; &#xCE21;&#xC815;&#xC744;
            &#xD568;.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>## 개발 체크리스트

* 마크업 : 로딩 / 리사이징 / 분기처리\(os별, 브라우저별\) 확인
* 크로스 브라우징 범위 확인
* 스크립트 이슈 확인
* 디버깅 & 기능 테스트
* 접근성 QA 검수\(웹 접근성\(WCAG/WAI-ARIA\) & SEO\)

{% hint style="info" %}
\[텍스트\]

* 이미지 alt\_크롬 개발자툴로 확인\(기획자 확인 요청\)
* 원페이지일 경우 페이지별 내용에 따라 title 상세변경처리
{% endhint %}

{% hint style="info" %}
\[스크롤/드래그\]

* 드래그인 경우 키보드 좌우버튼으로 조정가능하게 처리
* 스크롤으로 페이지를 조정하는 경우 탭으로 화면 넘어갈 시 깨지는 것 없는지 같이 체크\(스크롤은 막았지만 키보드 이동으로 넘어갈 수 있음\)
{% endhint %}

{% hint style="info" %}
\[키보드\]

* 탭 이동\_포커스&호버 동일동작 해야함
* 엔터 이동\_엔터키 keydown은 click 이벤트를 trigger 하므로 클릭과 엔터의 구분이 필요할 시 keyup 으로 분기처리
* 레이어 : 레이어 안에서만 초점이동 필요
{% endhint %}

{% hint style="info" %}
\[마우스\]

* 연속클릭 시 동작제거
{% endhint %}

{% hint style="info" %}
\[초기화\]

* 로딩
* 리사이징 / 분기처리\(os별, 브라우저별\)
* $\(window\).width\(\) 값으로 분기처리 할 시, 피시-태블릿-모바일 사이의 애매한 사이즈일 때 ie에서 버전별 스크롤바 영역 때문에 틀어지는 경우가 생김. \(제이쿼리 이전버전 이슈로 생각됨.\)$\(document\).width\(\) 를 사용하면 ie11 제외하고 잘 나타나기 때문에 ie11 을 위해 window.innerWidth 를 사용하면 됨. Math.max\(window.innerWidth,$\(document\).width\(\)\) 을 사용
{% endhint %}

{% hint style="info" %}
\[보이스오버\]

* 초점 :  font-size:0 / opacity:0 쓰면 초점 아예 안잡힘.
* text-indent:-9999px 쓰면 초점이 엄청 크게 잡힘.\(브라우저가 -9999px 만큼 영역계산함.\) 
* a, button 요소 안에 span 만들어서`overflow:hidden;position:absolute;clip:rect(0,0,0,0);width:1px;height:1px;margin:-1px;` 적용. ie8 까지 대응 가능.
* tabindex : 사파리/보이스오버에서는 tabindex -1 도 초점이 잡히므로레이어 같은 경우 전체 visibility:hidden 후 html, body, 해당 레이어에 visible 적용하여 처리.
{% endhint %}

* 기기 테스트
* \(후순위\) 디자인 PX 체크 \(디자인 필터링 기준기기 체크\)
* QA 및 검수 일정 확인
* 산출물 전달\(산출물에 대한 템플릿 있으면 확인 필수\) 
*  최종 산출물 전달 일정&실 오픈 일정 확인

