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

## 상태\(state\)

React 컴포넌트에 데이터를 저장하고 변경에 따라 자동으로 뷰를 갱신하도록 하는 핵심 개념.

### 초기 상태 설정

#### 조건

* ES6 Class **생성자 안에서** this.state 로 선언
* this.state 는 반드시 객체여야 함
* super\(props\) 로 속성을 전달해야 함

```text
class test extends React.Component{
    constructor(props){
        super(props)
        this.state = {
            stateName = value
        }
    }
    render(){
        return {this.state.stateName}
    }
}
```

### 상태 수정

#### this.setState\(data, callback\)

일반적으로 이벤트 핸들러, 데이터 수신/갱신 콜백 함수에서 호출해서 사용한다. `setState`  는 `render()` 를 실행시킨다.

{% hint style="info" %}
`this.state` : 변경 가능 / 해당 컴포넌트 자체에서 정의

`this.props` : 변경 불가 / 부모 컴포넌트에서 전달 / 정적인 상태로 유지
{% endhint %}

```text
class test extends React.Component{
    constructor(props){
        super(props)
        this.state = {
            stateName = value
        }
        this.init() //valueChange 발생
    }
    init(){
        this.state.stateName = valueChange
    }
    render(){
        return {this.state.stateName}
    }
}
ReactDOM.render(<test/>, document.getElementById('app'))
```

### 상태 비저장\(stateless\)

속성을 전달받아 처리하는 것. 예측가능하므로 많이 사용할 수록 좋다.

함수만으로 작성되는 상태비저장 컴포넌트는 라이프사이클 메소드를 사용할 수 없다.

```text
function link(props){
    return <a href={prop.href}>{prop.text}</a>
}
ReactDOM.render(
    <link text='value' href='http://google.com'/>,
    document.getElementById('app')
)
```

## 이벤트

* mounting : 한번만 실행, 리액트엘리먼트를 DOM 노드에 추가 시 발생
  * `componentWillMount()` : DOM 삽입 전
  * `componentDidMount()` : DOM 삽입/렌더링 완료 후
    * DOM 요소 접근 가
* updating : 여러번 실행, 속성/상태 변경시 리액트엘리먼트 갱신 시 발생
  * `componentWillReceiveProps(nextProps)` : 속성 받기전
  * `shouldComponentUpdate(nextProps, nextState)` : 갱신조건 정의, 재렌더링 최적화
  * `componentWillUpdate(nextProps, nextState)` : 갱신 직전
  * `componentDidUpdate(prevProps, prevState)` : 갱신 후
* unmounting : 한번만 실행, 리액트엘리먼트를 DOM에서 제거 시 발생
  * `componentWillUnmount()` : DOM 제거 전





