---
description: webpack-simple + sass + vue-router + axios
---

# vue-cli2 webpack-simple project setting

### vue-cli 세팅

#### 설정

* webpack-simple 템플릿으로 기본 개발환경 셋팅\(sass 사용 : Y\)
* 모듈 추가 설치
  * vue-router
  * axios

```text
vue init webpack-simple [project name]
cd [project name]
npm i
npm i --dev vue-router axios
```

* **`main.js`** 에서 vue-router 사용 가능하게 수정 

```text
import Vue from 'vue';
import App from './App';
import router from './router';

Vue.config.productionTip = false;

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  render: h => h(App)
});

```

* **`App.vue`** 에서 router 로 보여질 수 있도록 수정

```text
<template>
  <div id="app">
    <router-view/>
  </div>
</template>
```

* **`/router`** 폴더 생성
* **`/router/index.js`** 파일 생성

```text
import Vue from 'vue';
import Router from 'vue-router';
import IndexPage from '@/components/IndexPage';

export default new Router({
  mode: 'history',
  routes: [
    {
      path: '/',
      name: 'IndexPage',
      component: IndexPage
    }
  ]
});

Vue.use(Router);
```

### import path 길이 단축

#### 설정 : webpack.config.js

```text
module.exports = {
...
 resolve: {
    alias: {
      '@': path.resolve('src')
    }
}
```

#### 사용

```text
import IndexPage from '@/components/IndexPage';
```

### rule 부분 정규식으로 코드 단축

#### 설정 : webpack.config.js &gt; module &gt; rule

before

```text
{
  test: /\.css$/,
  use: ['vue-style-loader', 'css-loader']
},
{
  test: /\.scss$/,
  use: ['vue-style-loader', 'css-loader', 'sass-loader']
},
{
  test: /\.sass$/,
  use: ['vue-style-loader', 'css-loader', 'sass-loader?indentedSyntax']
}
```

after

```text
{
test: /\.(c|sc|sa)ss$/,
use: ['vue-style-loader', 'css-loader', 'sass-loader', 'sass-loader?indentedSyntax']
},
```



