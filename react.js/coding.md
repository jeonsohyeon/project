---
description: 리액트 코드 작성 시에 고려해야 할 점
---

# Coding

## 컴포넌트 작성 : 관심사의 분리

### Presentational Component : 상태 비저장 컴포넌트

상태가 없는 상태 비저장 컴포넌트/함수형 컴포넌트 내부에 이벤트 핸들러를 주지 말고, 부모 컴포넌트가 이벤트 핸들러를 전달하여 this.props 로 받아서 사용한다.

* Button 과 같은 컴포넌트는 여러 군데에서 사용하므로 이 방법을 사용하면 **다른 UI에서 재사용성이 높아진다.**
* 부모 컴포넌트에 이벤트 핸들러를 두면 자식과 데이터를 교환할 수 있다.

```text
//부모 컴포넌
class Content extends React.Component {
  constructor(props){
    super(props)
    this.state = {text : "클릭 전"};
    this.btnClick = this.btnClick.bind(this); //컨텍스트 연결하여 this.setState() 를 쓸 수 있게 함
  }
  btnClick(){
    this.setState({text : "클릭했음"});
  }
  render () {
    return (
      <main>
        <h1>Content</h1>
        <Button text={this.state.text} handler={this.btnClick}/>
      </main>
    )
  }
}

//Button 컴포넌트
class Button extends React.Component {
  render() {
    return (
      <button onClick={this.props.handler} className="btn-comm">{this.props.text}</button>
    )
  }
}
```

### Naming

* 자식에게 속성을 전달할 때 같은 이름을 사용하면 서로 다른 컴포넌트에서 데이터가 관련되어 있다고 유추할 수 있다.



