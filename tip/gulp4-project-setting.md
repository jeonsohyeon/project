---
description: gulp4 로 프로젝트 세팅.
---

# Gulp4 project setting

## Project Setting

```
$ mkdir [folder-name]
$ cd [folder-name]
$ npm init -y
$ npm i gulp --save-dev
$ touch gulpfile.js
```

이제 편집기에서 `gulpfile.js`를 열고 기본 태스크를 만든다.

### Gulp basic

#### Task

gulp에서는 어떤 일을 하는 하나의 작업을 함수로 묶어서 태스크로 관리한다. exports 를 사용해 태스크를 내보낼 수 있다.

```text
function defaultTask() {
  console.log('default task 실행');
}

exports.default = defaultTask
```

```text
$ gulp //실행결과 : default task 실행
```

#### Series\(\), Parallel\(\)

태스크가 하나 이상인 경우 묶어서 작업을 실행시킬 수 있다.

`series()` 는 순서대로 태스크를 실행시킨다. 앞 작업이 끝나지않으면 다음 작업을 할 수 없다. `parallel()` 은 비동기로 태스크를 실행시킨다. 동시에 할 수 있는 만큼 실행한다.

```text
const { series, parallel } = require('gulp');
function fun1() {}
function fun2() {}
exports.build = series(fun1, fun2...);
exports.build = parallel(fun1, fun2...);
```

#### src, dest

태스크 실행의 시작점, 종착점으로 생각하면 된다.

```text
const { series, parallel, src, dest } = require('gulp');
function copy() {
  return src('/src/*.html')
    .pipe(dest('/dest/'));
}
exports.copy = copy;
```

`/src/` 에 있는 모든 html 파일을 `/dest` 폴더로 옮기라는 뜻.

```text
$gulp copy
```

### Gulp Setting

{% hint style="info" %}
 기본 구조는 다음과 같다.
{% endhint %}

```
const { series, parallel, src, dest } = require('gulp');

function clean(cb) {
  // body omitted
  cb()
}

function cssTranspile(cb) {
  // body omitted
  cb();
}

function cssMinify(cb) {
  // body omitted
  cb();
}

function jsTranspile(cb) {
  // body omitted
  cb();
}

function jsBundle(cb) {
  // body omitted
  cb();
}

function jsMinify(cb) {
  // body omitted
  cb();
}

function publish(cb) {
  // body omitted
  cb();
}

exports.default = series(clean, parallel(cssTranspile, series(jsTranspile, jsBundle)), parallel(cssMinify, jsMinify), publish);

```

* 개발 : scss & js 트랜스파일, 로컬 서버 세팅
* 빌드 : 전체 소스 번들링

## Setting Step.1

### Path

자주 사용하는 리소스 경로를 DIR, PATH 에 담는다.

```text
let DIR = {
  SRC: './src',
  DEST: './dest'
};

let PATH = {
  DIR: DIR,
  SRC: {
    JS: `${DIR.SRC}/js/**/*.js`,
    SCSS: `${DIR.SRC}/scss/**/*.scss`
  },
  DEST: {
    JS: `${DIR.DEST}/js`,
    CSS: `${DIR.DEST}/css`
  }
};
```

### function clean\(\)

* `del` - 폴더 삭제

```text
$npm i del --save-dev
```

```text
const del = require('del');
function clean() {
  return new Promise(resolve => {
    del.sync(PATH.DIR.DEST);
    resolve();
  });
}
```

### function cssTransfile\(\)

* `gulp-concat` — 파일을 하나로 합침
* `gulp-file-cache` — 이미 캐시에 있는 파일 필터링
* `gulp-sass` — SCSS를 CSS로 컴파일
* `gulp-postcss` — CSS 파일에 또 다른 수정을 할 수 있음
  * `autoprefixer` — CSS prefix 추가
  * `cssnano` — CSS 압축
* `gulp-cleancss` — 하위 브라우저 호환\(ie8\)

```text
$npm i gulp-sass gulp-postcss autoprefixer cssnano gulp-clean-css gulp-file-cache --save-dev
```

```text
const sass = require('gulp-sass');
const postcss = require('gulp-postcss');
const autoprefixer = require('autoprefixer');
const cssnano = require('cssnano');
const cleancss = require('gulp-clean-css');
const cache = require('gulp-file-cache');
const fileCache = new cache();

function cssTranspile() {
  return src(PATH.SRC.SCSS, { sourcemaps: true })
    .pipe(fileCache.filter())
    .pipe(sass().on('error', sass.logError))
    .pipe(postcss([autoprefixer(), cssnano()]))
    .pipe(cleancss({ compatibility: 'ie8' }))
    .pipe(fileCache.cache())
    .pipe(dest(PATH.DEST.CSS));
}
```

### function jsTransfile\(\)

* `gulp-file-cache` — 이미 캐시에 있는 파일 필터링
* `gulp-babel` — ES6 트랜스파일링
* `gulp-minify`— 코드 압축

```text
$npm install --save-dev gulp-babel @babel/core @babel/preset-env gulp-minify
```

```text
const babel = require('gulp-babel');
const minify = require('gulp-minify');

function jsTranspile() {
  return src(PATH.SRC.JS, { sourcemaps: true })
    .pipe(fileCache.filter())
    .pipe(
      babel({
        presets: ['@babel/env']
      })
    )
    .pipe(fileCache.cache())
    .pipe(dest(PATH.DEST.JS));
}

```

## 참고 링크

{% embed url="https://coder-coder.com/gulp-4-walk-through/" %}

[https://beomy.tistory.com/42](https://beomy.tistory.com/42)

