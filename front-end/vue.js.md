# Vue.js

## 리스트 렌더링

### v-for

* 데이터가 여러개인 경우 v-for 를 사용해 리스트를 렌더링한다.
* 2.2.0 이상에서 v-for는 key 가 필수. \(:key=""\)

```text
<template>
<div v-for="(nickname(임시 별칭), index) in item(프로퍼티명)" :key="index">
  {{ nickname.title }}
  {{ nickname.description }}
</div>
</template>
```

#### v-for + v-if : 단일 엘리먼트의 조건부 렌더링

* 단일 엘리먼트\(ex:페이징에서 버튼 태그 렌더링 등\)에서 v-for를 사용해서 렌더링 하면서 v-if 를 함께 사용해야 할 경우 `<template>` 를 사용하면 좋다.
* 최종 렌더링 결과에는  엘리먼트가 포함되지 않는다.
* `<template>` 태그에 :key 를 설정할 수는 없다.

```text
<template>
  ~~~~
  <template v-for="(nickname, index) in item">
    <button :key="index" v-if="paging.active" class="active-paging">{{ index+1 }}</button> //paging.active 가 true 일 경우
    <button :key="index" v-else>{{ index+1 }}</button>
  </template>
</template>
```

#### v-for + v-if : 조건부 렌더링

* 일부만 렌더링 하려는 경우.

```text
<li v-for="todo in todos" v-if="todo.isComplete">
  {{ todo }}
</li>
```

### v-if

#### 여러개의 엘리먼트를 한꺼번에 v-if

* `<template>` 에 v-if 를 사용할 수 있다.
* v-else 는 v-if 또는 v-else-if 바로 뒤에 있어야 인식할 수 있다.

```text
<template>
  ~~~~
  <template v-if="paging.active">
    if 일 경우 html
  </template>
  <template v-else>
    else 일 경우 html
  </template>
</template>
```

### v-show

* v-show는  구문을 지원하지 않는다.

## 컴포넌트

### 컴포넌트 만들기

기본이 될 컴포넌트 만들기.

```text
<template>
html
</template>
<script>
export default {
 name: '컴포넌트명'
}
</script>
<style lang="scss" scoped>
style
</style>
```

### 컴포넌트 불러오기

상위 컴포넌트에서 하위 컴포넌트 불러오기.

```text
<script>
import 컴포넌트명 from '컴포넌트 위치'

export default {
  components: {
   컴포넌트명
  }
}
</script>
```

## 상위-하위 컴포넌트로 데이터 전달

### 하위 컴포넌트에서

* `props`를 사용해서 데이터를 받을 프로퍼티명을 설정\(item\)한다.
* `<template>`에 해당 프로퍼티명\(item\)을 넣어준다.

  ```text
  <template>
  <div>{{ item(프로퍼티명) }}</div>
  </template>
  <script>
  export default {
  props: ['item(프로퍼티명)']
  }
  </script>
  ```

> `props` 옵션
>
> ```text
>   propA: (Number | Array | String | Object | Boolean | Function | Symbol),
>   propB: [String, Number], //여러개 가능
>   propC: { // 문자열이며 꼭 필요합니다
>       type: String,
>       required: true
>   },
>   propD: { // 숫자이며 기본 값을 가집니다
>       type: Number,
>       default: 100
>   },
>   propE: { // 객체/배열의 기본값은 팩토리 함수에서 반환 되어야 합니다.
>       type: Object,
>       default: function () {
>         return { message: 'hello' }
>       }
>   },
>   propF: { // 사용자 정의 유효성 검사 가능
>       validator: function (value) {
>         return value > 10
>       }
>   }
> ```

### 상위 컴포넌트에서

* 해당 컴포넌트를 import
* v-bind 를 이용해 해당 프로퍼티\(item\)에 전달할 데이터 값\(listItem\)을 넣는다. \(v-bind:item="listItem"\)
* 객체의 모든 속성을 props로 전달하려면, 인자없이 v-bind를 쓸 수 있다. \(v-bind="listItem"\)
* v-bind 를 빼고 표현해도 된다. \(:item="listItem"\)

```text
<template>
<h1>부모 컴포넌트</h1>
<child-component v-bind:item(자식이 가지고 있던 프로퍼티명)="listItem(전달할 데이터 값)"/>
</template>
<script>
import childComponent from '../url'
export default {
  components: {
    childComponent
  },
  data: function(){
    return {
      listItem(전달할 데이터 값) : [
        {'title': 'title', 'desc': 'description' }
        {'title': 'title2', 'desc': 'description2' }
      ]
    }
  }
}
</script>
```

### 다시 하위 컴포넌트에서

* 데이터가 여러개인 경우 `v-for` 를 사용해 리스트를 렌더링한다.
* 2.2.0 이상에서 v-for는 key 가 필수. \(v-bind:key=""\)

```text
<template>
<div v-for="(nickname(임시 별칭), index) in item(프로퍼티명)" :key="index">
  {{ nickname.title }}
  {{ nickname.description }}
</div>
</template>
<script>
export default {
  props: {
    item(프로퍼티명): {
      type: Array
    }
  }
}
</script>
```

## 상위-하위-하위 컴포넌트로 데이터 전달

### 상위 컴포넌트에서

* 해당 컴포넌트를 import
* v-bind 를 이용해 데이터 값 전달\(v-bind:todos="todos"\)

```text
<template>
  <h1>부모 컴포넌트</h1>
  <Todos v-bind:todos="todos"/>
</template>

<script>
import Todos from './components/Todos.vue'

export default {
  name: 'app',
  components: {
    Todos
  },
  data () {
    return {
      todos : [
        {
          id: 1,
          title: '1',
          completed: false
        },
        {
          id: 2,
          title: '2',
          completed: true
        }
      ]
    }
  }
}
</script>
```

### 하위 컴포넌트에서

* `props`를 사용해서 데이터를 받을 프로퍼티명을 설정\(props: \['todos'\]\)한다.
* `<template>`에서 v-for로 리스트 렌더링을 한다.
* 리스트 렌더링을 받을 컴포넌트를 새롭게 하나 생성\(TodoItem.vue\)하고 v-bind 로 데이터값\(todo\) 을 다시 건넨다.

```text
<template>
  <div v-for="todo in todos" v-bind:key="todo.id">
    <TodoItem v-bind:todo="todo"/>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
  name: 'Todos',
  components : {
    TodoItem
  },
  props: ['todos']
}
</script>
```

### 하위2 컴포넌트에서

* `props`를 사용해서 데이터를 받을 프로퍼티명을 설정\(props: \['todo'\]\)한다.
* `<template>`에서 v-for로 받은 데이터를 사용한다. `{{ todo.title }}`

```text
<template>
  <div class="todo-item" v-bind:class="{'is-completed':todo.completed}">
    <input type="checkbox" v-on:change="markComplete" name="" id="">
    <p>{{ todo.title }}</p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete () {
      this.todo.completed = !this.todo.completed;
    }
  }
}
</script>
```



## 이벤트 핸들링

### 이벤트 핸들링

* `v-on:eventName="MethodName"`을 기본으로 사용
* 파라미터 전달 시에는 `v-on:eventName="MethodName(paramsName)"`
* 만약 기본 이벤트를 제어해야 할 시에는 `v-on:eventName="MethodName(paramsName, $event)"` 를 사용하고 메소드 안에 event.preventDefault\(\); 를 넣는다.

```text
<script>
export default {
  methods : {
    eventName(paramsName, event){
      if (event) event.preventDefault();
      alert(message)
    }
  }
}
</script>
```

**하지만 이렇게 쓰는 대신 v-on 이벤트 수식어를 사용하면 좀 더 편하다.** [수식어\_상세](https://kr.vuejs.org/v2/guide/events.html)

### 이벤트 트리거 $emit

### 하위 컴포넌트에서 상위 컴포넌트로 이벤트 전달하기

#### 하위 컴포넌트에서

* `@이벤트명="$emit('상위 컴포넌트의 이벤트명', 전달할 데이터 값);`

```text
<template>
   <button @click="$emit('test', data)"></button>
</template>
```

#### 상위 컴포넌트에서\(최종 상위 컴포넌트\)

* `v-on:전달받은 이벤트명="메소드명"`
* methods 에 해당 메소드\(testData\)를 만든다.

```text
<template>
  <div v-on:testData="testData"/>
  </div>
</template>
<script>
export default {
  methods: {
    testData(data){
      console.log(data);
    }
  }
}
</script>
```

### 하위 컴포넌트에서 상위 컴포넌트로 이벤트 전달하기2

#### 하위 컴포넌트에서

* 메소드에서 `this.$emit('상위 컴포넌트의 이벤트명', 전달할 데이터 값);`

```text
<template>
   <button @click="test(data)"></button>
</template>
<script>
export default {
  methods: {
    test(data){
      this.$emit('testData', data)
    }
  }
}
</script>
```

#### 상위 컴포넌트에서

* `v-on:전달받은 이벤트명="메소드명"`
* methods 에 해당 메소드\(testData\)를 만든다.

```text
<template>
  <div v-on:testData="testData"/>
  </div>
</template>
<script>
export default {
  methods: {
    testData(data){
      console.log(data);
    }
  }
}
</script>
```

### 주의점

* 해당 컴포넌트만 가지고 있는 데이터\(this.property\)를 $emit 으로 보낼 때는 임시 변수에 담아 보낸다.

  데이터는 해당 컴포넌트 안에서만 스코프를 갖기 때문. \(확실치않음..아마도?\)

```text
data: function () {
  return {
    pageNum: 0,
    pageLength: this.pagingLength - 1
  }
},
methods: {
  nextBtn () {
    this.pageNum++;
    if (this.pageNum > this.pageLength) { this.pageNum = 0 }
    let activeNum = this.pageNum;
    this.$emit('changeNumber', activeNum);
  }
}
```



