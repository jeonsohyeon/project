---
description: 개발환경 셋팅 중에 환경 변수 오류로 인해 발생할 수 있는 이슈 해결 모음.
---

# window 10 path issue

## npm package global install error

npm 패키지 글로벌 설치 후 오류가 발생하는 경우 해결법.

```text
$ npm i express -g
$ express -h //command not found 오류 발생
```

1. 우선 터미널에서 해당 패키지가 글로벌 설치 되어있는지 확인하고
2. 현재 npm 설치 경로를 확인해서 이 경로를 환경변수에 넣어준다.

```text
$ npm list -g --depth=0 //현재 global 설치 되어있는 패키지 확인
$ npm bin -g //현재 npm 이 어디에 설치 되어있는지 확인
```

{% hint style="warning" %}
시스템 환경변수 편집 &gt; 환경변수로 들어가서 Path 설정을 해준다.

* **사용자 변수, 시스템 변수** 모두 추가
{% endhint %}

1. cmd 창을 열고 set 명령어로 새로운 환경 변수를 적용해준다.

```text
$ cmd
```

그 후에 다시 원래 하려고 했던 명령어를 적용한다.

[출처](https://medium.com/@jagatjyoti.1si13cs040/npm-g-install-npm-package-not-working-as-desired-why-why-why-19795abf0b59)

