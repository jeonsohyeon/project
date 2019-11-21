# learning react

## Settings

[https://github.com/basarat/typescript-react/tree/master/01 bootstrap](https://github.com/basarat/typescript-react/tree/master/01%20bootstrap)

### Issue

책 내용을 따라가는 도중 버전이 달라서 생기는 오류나 해결 방안 수록.

### 6장 프로퍼티, 상태, 컴포넌트 트리

#### propTypes 문법 오류

react 15.5 이후 부터는 React.PropTypes 가 별도의 패키지로 분리되어 있어서 패키지를 설치해야 하고, 웹팩+바벨 설정을 해놓았을 경우 webpack.config.js 에서 플러그인을 추가해줘야 한다.

설치해야 할 패키지

* prop-types
* @babel/plugin-proposal-class-properties

```text
//설치
npm i --save prop-types

//설정 webpack.config.js : rules
{
    test: /\.js|jsx$/,
    exclude: /(node_modules)/,
    loader: 'babel-loader',
    query: {
        cacheDirectory: true,
        presets: ['@babel/preset-env', '@babel/preset-react'],
        plugins: ['@babel/plugin-proposal-class-properties']
    }
},

//사용
import PropTypes from 'prop-types'

static propTypes = {
    title: PropTypes.string
}
```

또 책에서는 `createClass` 를 사용하여 클래스를 만들었지만, `class` 문법으로 변환하여 작업 시에는 아래와 같이 만들어야 작동된다.

```text
class Summary extends React.Component {
    static propTypes = {
        ingredients: PropTypes.number,
        steps: PropTypes.number,
        title: (props, propName) => {
            (typeof props[propName] !== 'string') ? new Error("제목은 문자열이어야 합니다.") : (props[propName].length > 20) ? new Error("제목은 20자 이내여야 합니다.") : null;
        }
    }
    static defaultProps = {
        ingredients: 0,
        steps : 0,
        title : "[무제]"
    }
}
```

[https://ko.reactjs.org/docs/typechecking-with-proptypes.html](https://ko.reactjs.org/docs/typechecking-with-proptypes.html)

ref 필드 ref 는 DOM 엘리먼트를 참조할 때 사용하는 식별자. 콜백함수를 받고 컴포넌트가 마운트 되거나 언마운트 된 이후에 즉시 실행된다. `this.refs.[refName]`으로 접근할 수 있다.

ref : 해당 DOM 엘리먼트 this : 컴포넌트

사용하는 곳 포커스 제어, 텍스트 선택, 미디어 재생을 관리할 때 특정 DOM 의 스크롤 위치를 가져오거나 설정을 해야 할 때 명령형 애니메이션을 발생시킬 때 서드파티 DOM 라이브러리를 사용 할 때

주의사항 리액트 16 부터는 문자열이 아닌 함수를 사용해야 한다.

* 렌더링 요소를 추적해서 느려진다.

```text
<input ref={ref => this.input = ref}/>
```

인라인 함수로 정의하지 말고 클래스의 메서드를 ref 콜백으로 정의한다.

* 렌더링 될 때마다 인라인 함수가 생성되기 때문에 항상 새 ref 를 지정해야 한다.

리액트 16 부터는 React.createRef\(\) 로도 사용 가능하다.

```text
//생성
this.a = React.createRef()

//접근
this.a.current;

//사용
render(){
    return (
        <button ref={this.a}></button>
    )
}

/*
예를 들어 버튼은 disabled 속성을 가지고 있으니
this.a.current.disabled 라고 접근이 가능하다.

input[type="text"]인 경우는 this.a.current.focus() 등으로도 사용 가능
*/
```

함수형 컴포넌트\(function name\(\){ return }\) 에 사용하면 안된다. 인스턴스가 없어서. [https://medium.com/@enro2414\_40667/react-refs-%EA%B7%B8%EB%A6%AC%EA%B3%A0-dom-8900c72e7ab1](https://medium.com/@enro2414_40667/react-refs-%EA%B7%B8%EB%A6%AC%EA%B3%A0-dom-8900c72e7ab1)

라이브러리 사용 시, 적용 DOM 에 ref 설정 

생성 : componentDidMount 에서 인스턴스 생성 

수정 : componentDidUpdate 에서 기존 인스턴스 제거, 새 인스턴스 생성\(변경 비교\) 

삭제 : componentWillUnmount 에서 제거

```text
componentDidUpdate(prevProps, prevState){ if(prevProps.[data] !== this.props.[data]){ //내용 변경 } }
```



