---
description: by React Quickly
---

# React.js

## 엘리먼트 생성 : createElement

`React.createElement(태그명/사용자정의 컴포넌트 클래스명, 속성/상위 컴포넌트 데이터값, 자식 엘리먼트or텍스트)`

* HTML Tag 생성하는 경우

```text
let h1 = React.createElement('h1', null, 'Hello world!')
let link = React.createElement('a', {href:'http://google.com'}, 'link google');
```

* 사용자 정의의 컴포넌트 클래스\(=컴포넌트\)를 생성하는 경우
  * 재사용 가능한 UI를 만들기 위해서 사

{% hint style="danger" %}
컴포넌트 클래스를 구현할 때는 render\(\) 메서드가 반드시 필요하고, React 엘리먼트를 반환 해야 한다.
{% endhint %}

`class 컴포넌트이름(대문자로 시작해야 함) extends React.Component {render(){return 컴포넌트 or 엘리먼트}}`

```text
class HelloWorld extends React.Component {
  render() {
    return React.createElement('div', null, 'div 생성')
  }
}
React.createElement(HelloWorld, null);
```

### ex\) 엘리먼트 중첩

* `createElement` 의 세번째 인자로 계속해서 전달

```text
React.createElement(h1, null, link, link);
```

## 엘리먼트 렌더링 : render

`ReactDOM.render(요소, 들어갈 위치)`

* HTML Tag 렌더링하는 경우

```text
ReactDOM.render(h1, document.getElemnentById('app')); 
```

```text
ReactDOM.render(
    React.createElement('div', null, h1, h1),
    document.getElementById('content')
)
```

* 컴포넌트 렌더링

```text
ReactDOM.render(HelloWorld, document.getElemnentById('app'));
```

```text
ReactDOM.render(
    React.createElement('div', null, 
        React.createElement(HelloWorld),
        React.createElement(HelloWorld)
    ),
    document.getElementById('app')
)
```

## 엘리먼트 속성

컴포넌트 내부에서는 변경할 수 없는 값.

* 표준 속성

```text
let link = React.createElement('a', {href:'http://google.com'}, 'link google');
```

* 커스텀 속성
  * 소문자로 작성해야 함
  * 컴포넌트 재사용성을 높
  * `this.props.프로퍼티명` 으로 컴포넌트 프로퍼티 값을 불러올 수 있음

    \(예제에서는 `this.props.frameworkName`\)

```text
class HelloWorld extends React.Component {
  render() {
    return React.createElement(
      'div',
      this.props,
      'Hello ' + this.props.frameworkName + ' world!'
    )
  }
}

ReactDOM.render(
  React.createElement(HelloWorld, {frameworkName: 'Ember.js'}),
  document.getElementById('app')
)
```

## JSX : &lt;/&gt;

* 함수 호출, 객체 생성을 위한 문법적 편의를 제공하는 자바스크립트의 확장.
* `React.createElement()` 반복해야 하는 불편을 해소.
* 컴포넌트 생성의 방법
* **생산성 향상 / 코드량 감소**
* 컴파일 or 트랜스파일 필

```text
React.createElement(HelloWorld, null) => <HelloWorld/>
```

#### React.DOM

* JSX 를 쓰지 않고 `React.createElement()` 를 줄일 수 있는 방법

`React.DOM.*`

```text
React.createElement('h1', null, 'hello') => React.DOM.h1(null, 'hello');
```

### 엘리먼트 렌더링

* HTML Tag 렌더링

```text
//Before
let link = React.createElement('a', {href:'http://google.com'}, 'link google');
ReactDOM.render(link, document.getElementById('app');

//After
let link = <a href="http://google.com">link google</a>
ReactDOM.render(link, document.getElementById('app');
```

* 컴포넌트 렌더

```text
class HelloWorld extends React.Component {
  render() {
    return <div>Hello world!</div>
    )
  }
}

ReactDOM.render(
  React.createElement(<HelloWorld/>),
  document.getElementById('app')
)
```

### 변수 : {}

```text
class HelloWorld extends React.Component {
  render() {
    let h1 = <h1>{this.props.titleData}</h1>
    return <div>{h1}</div>
    )
  }
}

ReactDOM.render(
  React.createElement(<HelloWorld/>, {titleData : 'title'}),
  document.getElementById('app')
)
```

### 속성 : key=value

```text
class HelloWorld extends React.Component {
  render() {
    let h1 = <h1 {...this.props}>{this.props.titleData}</h1>
    return <div>{h1}</div>
    )
  }
}

ReactDOM.render(
  React.createElement(<HelloWorld/>, {titleData : 'title', data-test: 'test'}),
  document.getElementById('app')
)
```

### 메소드

```text
class HelloWorld extends React.Component {
  getUrl() {
    return 'http://google.com'
  }
  render() {
    return <div>{this.getUrl()}</div>
    )
  }
}
```

### if/else

* 중괄호{ } 안에서 return 문을 사용하는 건 유효치 않다.

```text
class HelloWorld extends React.Component {
  getUrl() {
    return 'http://google.com'
  }
  render() {
    let flag = this.props.flag;
    return <a href="{flag ? '/login':'/logout'}">{flag ? 'login':'logout'}</a>
    )
  }
}
```

### 주석

```text
{/* comments */}
/*
 line comments
*/
```

### Style / ClassName / htmlFor

* `htmlFor` : `label for`
* `className` : `class`

```text
<input id="inpComm" className="hidden" style="{{border:'1px solid red'}}"/>
<label htmlFor="inpComm">text</label>
```

### Attribute Boolean

* `disabled, required, checked, autofocus, readOnly` 같은 boolean 을 가지는 속성값은 반드시 **{} 안에.**

```text
<input type="checkbox" checked="{true}"/>
<input type="checkbox" checked/> //생략 시 true 로 간주
```



