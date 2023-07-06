---
title: "[React Docs] 5. State and Lifecycle"
date: 2023-07-06
categories:
  - React
tags:
  - [React]
permalink: /Blog/react-doc-05/
toc: true
toc_sticky: true
toc_label: "스테이트와 라이프사이클"
last_modified_at: 2023-07-06
---

> 본 게시글은 [리액트 공식문서](https://reactjs.org/docs/getting-started.html)를 읽고 정리한 글이다.

: 엘리먼트 렌더링 파트에서 다뤄본 시계 예시를 다시 살펴보자. 렌더링 된 출력값을 변경하기 위해 `root.render()`를 호출했다.

```jsx
const root = ReactDOM.createRoot(document.getElementById("root"));

function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  root.render(element);
}

setInterval(tick, 1000);
```

: 이 섹션에서 `Clock`컴포넌트를 재사용하고 캡슐화하는 방법을 배울 것이다. 그리고 이 컴포넌트는 스스로 타이머를 설정하고 매 초 스스로 업데이트할 것이다.

```jsx
const root = ReactDOM.createRoot(document.getElementById("root"));

function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  root.render(<Clock date={new Date()} />);
}

setInterval(tick, 1000);
```

- 시계를 캡슐화 하기전 여기에는 중요한 조건이 누락되어 있는데, `Clock`이 타이머를 설정하고 매초 UI를 업데이트하는 것은 `Clock`컴포넌트 내부에 있어야 한다.

: 이상적으로 한 번만 코드를 작성하고 `Clock`은 스스로 업데이트하도록 만들어보자.

```jsx
root.render(<Clock />);
```

- 이것을 구현하기 위해서 `Clock`컴포넌트에 “state”를 추가해야 한다.
- State는 Props와 유사하지만, 비공개이며 컴포넌트에 의해 완전히 제어된다.

## 함수를 클래스로 변환

: 다섯 단계로 `Clock` 과 같은 함수형 컴포넌트를 클래스로 변환할 수 있다.

1. `React.Component` 를 확장하는 동일한 이름의 [ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes)를 생성한다.
2. 비어있는 `render()` 메서드를 하나 추가한다.
3. 함수의 내용을 `render()` 메서드 안으로 옮긴다.
4. `render()` 바디 내에서 `props` 를 `this.props` 로 바꾼다.
5. 남아있는 빈 함수 선언문을 제거한다.

```jsx
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

- `Clock` 은 이제 함수가 아닌 클래스로 정의된다.

## Class에 로컬 state 추가하기

: `date`를 props에서 state로 옮기기 위해서 3단계를 진행한다.<br/><br/>

1️⃣ `render()` 메서드 내의 `this.props.date`를 `this.state.date`로 바꾼다.

```jsx
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

2️⃣ `this.state`를 초기화 하는 [클래스 생성자](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes#Constructor) 를 추가한다.

```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

> 클래스 컴포넌트는 항상 `props`로 기본 `constructor`를 호출해야한다.

3️⃣ `<Clock />`요소에서 `date` prop을 삭제한다.

```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(<Clock />, document.getElementById("root"));
```

## 클래스에 라이트사이클 메서드 추가하기

: 많은 컴포넌트가 있는 애플리케이션에서 컴포넌트가 삭제될 때 해당 컴포넌트가 사용 중이던 리소스를 확보하는 것이 중요하다.

- `Clock`이 처음 DOM에 렌더링 될 때마다 **타이머를 설정** 하려고 한다. 이것은 React에서 "**mounting**"이라고 한다.
- `Clock`에 의해 생성된 DOM이 삭제될 때마다 **타이머를 해제**하려고 한다. 이것은 React에서 "**unmounting**"이라고 한다.
- 컴포넌트 클래스에서 특별한 메서드를 선언하여 컴포넌트가 마운트되거나 언마운트 될 때 일부 코드를 작동시킬 수 있게 만드는 메서드들을 **"생명주기 메서드"** 라고 부른다.

**생성 :** `componentDidMount()` 훅은 초기 렌더링 시 실행 하지 않고 DOM이 렌더링 된 이후 동작한다. 이 부분이 타이머를 설정하기 적당하다.

```jsx
componentDidMount() {
  this.timerID = setInterval(
    () => this.tick(),
    1000
  )
}
```

- `this` (`this.timerId`)에서 어떻게 타이머 ID를 제대로 저장하는지 주의하자.

**마운트 해제 :** `componentWillUnmount()` 라이프사이클 훅에서 타이머를 종료한다.

```jsx
componentWillUnmount() {
  clearInterval(this.timerId);
}
```

: `this.setState()`를 사용하여 state 의 값을 변경한다.

```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
```

1️⃣ `<Clock />`이 `ReactDOM.render()`에 전달될 때, React는 `Clock` 컴포넌트의 생성자(constructor) 함수를 호출한다. `Clock`이 현 시간 화면에 보여질 때, 현 시간을 포함하는 `this.state`객체를 초기화한다. 이 state는 나중에 업데이트 한다.

2️⃣ React는 `Clock`컴포넌트의 `render()`메서드를 호출한다. React가 `Clock`컴포넌트의 `render()`메서드를 호출한다. 그다음 React는 `Clock` 의 렌더링 출력과 일치하도록 DOM을 업데이트한다.

3️⃣ `Clock` 출력이 DOM에 주입되었을 때, React는 `componentDidMount()` 라이프 훅을 호출한다. 그안에 `Clock` 컴포넌트는 브라우저에게 컴포넌트의 `tick()` 메서드를 초당 한번 호출하는 타이머를 설정하라고 요구한다.

4️⃣매 초마다 브라우저가`tick()` 메서드를 호출한다. 그 안에서 `Clock` 컴포넌트는 현재 시간을 포함하는 객체로 `setState()` 를 호출하여 UI 업데이트를 예약한다. `setState()` 호출 덕분에, React는 상태가 변경된 걸 알고 있고, `render()` 메서드를 다시 한번 호출해 화면에 무엇이 있어야 하는 지 알 수 있다. 이 때  `render()` 메서드 내의 `this.state.date` 가 달라지고 렌더링 출력값은 업데이트된 시각을 포함한다. React는 그에 따라 DOM을 업데이트한다.

5️⃣만약 `Clock` 컴포넌트가 DOM에서 삭제되었다면, React는 `componentWillUnmount()` 라이프사이클 훅을 호출하고 타이머를 멈춘다.

## State 바르게 사용하기

: `setState()`에 대해 알아야 할 3가지가 있다.<br/>

- **State를 직접 수정하지 말자**

  ```jsx
  // Wrong ❌
  this.state.comment = "Hello";

  // Correct ⭕
  this.setState({ comment: "Hello" });
  ```

  - `this.state`를 지정할 수 있는 유일한 곳은 `constructor`내부이다.

- **State 업데이트는 비동기일 수 있다.**

  - React는 여러 `setState()`호출을 성능을 위해 단일 업데이트로 한꺼번에 처리할 수 있다.
  - `this.props`및 `this.state`가 비동기로 업데이트될 수 있기 때문에, 다음 state를 계산할 때 해당 값을 신뢰해서는 안된다.
  - 예를 들어, 카운터를 업데이트하는 이 코드는 실패할 수 있다.

  ```jsx
  // Wrong ❌
  this.setState({
    counter: this.state.counter + this.props.increment,
  });
  ```

  - 이 문제를 해결하기 위해 객체가 아닌 함수를 인자로 사용하는 다른 형태의 `setState()`를 사용한다. 그 함수는 이전 state를 첫 번째 인자로 받아드릴 것이고, 업데이트가 적용된 시점의 props를 두 번째 인자로 받아들일 것이다.

  ```jsx
  // Correct - 화살표 함수 ⭕
  this.setState((prevState, props) => ({
    counter: prevState.counter + props.increment,
  }));

  // Correct - 일반 함수 ⭕
  this.setState(function (prevState, props) {
    return {
      counter: prevState.counter + props.increment,
    };
  });
  ```

- **State 업데이트는 병합된다.**

  - `setState()`를 호출할 때, React는 현재 state와 제공한 객체를 병합한다. 예를 들어, state는 여러 독립적인 변수를 가질 수 있다.

  ```jsx
  constructor(props) {
    super(props);
    this.state = {
      posts: [],
      comments: []
    };
  }
  ```

  - 개별 `setState()`를 호출하여 아이템을 각 각 업데이트할 수 있다.

  ```jsx
  componentDidMount() {
    fetchPosts().then(response => {
      this.setState({
        posts: response.posts
      });
    });

    fetchComments().then(response => {
      this.setState({
        comments: response.comments
      });
    });
  }
  ```

  - 병합은 얕게 이루어져서 `this.setState({comments})`는 `this.state.posts`에 영향을 주진 않지만 `this.state.comments`는 완전히 대체된다.

## 데이터는 아래로 흐른다.

: 부모 컴포넌트나 자식 컴포넌트는 특정 컴포넌트의 state 유무를 알 수 없으며 해당 컴포넌트가 함수나 클래스로 선언되었는지 알 수 없다.  
이는 state가 로컬이라고 부르거나 캡슐화된 이유이다. 컴포넌트 자신 외에는 접근할 수 없다. **컴포넌트는 자신의 state를 자식 컴포넌트에 props로 전달할 수 있다.**

```jsx
<FormattedDate date={this.state.date} />
```

`FormattedDate` 컴포넌트는 props에서 `date`를 받지만 이 값이 `Clock`의 state인 지, `Clock`의 props인 지, 혹은 수동으로 입력한 건지 알 수 없다.

```jsx
function FormattedDate(props) {
  return <h2>It is {props.date.toLocaleTimeString()}.</h2>;
}
```

- 이런 데이터 흐름을 보통 **“하향식”** 혹은 **“단방향식”** 데이터 흐름이라고 한다. 모든 state는 항상 특정 컴포넌트가 소유하며, 그 state에서 파생된 모든 UI, 데이터는 트리의 컴포넌트 **“아래”**에만 영향을 끼친다.

: 모든 컴포넌트가 완전히 독립적이라는 것을 보여주기 위해 App 을 렌더링하는 세 개의 `<Clock>` 을 생성한다.

```jsx
function App() {
  return (
    <div>
      <Clock />
      <Clock />
      <Clock />
    </div>
  );
}
```

- 각 `<Clock>`은 자신만의 타이머를 설정하고 독립적으로 업데이트 한다.  
  👉🏻 React앱에서 컴포넌트가 상태가 있는 지 없는지에 대한 것은 시간이 지남에 따라 변경될수 있는 구현 세부 사항으로 간주된다. 유상태 컴포넌트 안에서 무상태 컴포넌트를 사용할 수 있고, 그 반대 경우도 마찬가지이다.
