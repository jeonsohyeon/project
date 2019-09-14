---
description: webpack-simple + sass + vue-router + axios
---

# vue-cli2 webpack-simple project setting

### vue-cli 세팅

#### 설정

* webpack-simple 템플릿으로 기본 개발환경 셋팅\(sass 사용 : Y\)
* npm audit fix 로 보안취약점을 가진 모듈 업데이트
* 모듈 추가 설치
  * vue-router
  * axios

```text
vue init webpack-simple [project name]
cd [project name]
npm i
npm i --dev vue-router axios
npm audit fix --force
```

* **`/src/main.js`** 에서 vue-router 사용 가능하게 수정 

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

* **`/src/App.vue`** 에서 router 로 보여질 수 있도록 수정

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

### axios 통신

#### 사용

```text
<template>
<div>
  <img src="@/assets/logo.png" alt="logo">
  <p>{{ msg }} </p>
  <button @click="getAxiosData()">Axios Test</button>
  <br/>
  <br/>
  <div class="result">{{ result }}</div>
</div>
</template>
<script>
const axios = require('axios');
export default {
  name: 'IndexPage',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      result: ['axios test']
    }
  },
  methods: {
    getAxiosData() {
      axios.get('https://jsonplaceholder.typicode.com/todos/1')
      .then((response) => {
        this.result = response.data;
      }, (error) => {
        this.result = error;
      });
    }
  }
}
</script>
```

### Result

[link](https://github.com/jeonsohyeon/setting/tree/master/project-ws)

