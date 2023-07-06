---
title: "[React Docs] 4. Components와 Props"
date: 2023-07-04
categories:
  - React
tags:
  - [React]
permalink: /Blog/react-doc-04/
toc: true
toc_sticky: true
toc_label: "컴포넌트와 속성"
last_modified_at: 2023-07-04
---

> 본 게시글은 [리액트 공식문서](https://reactjs.org/docs/getting-started.html)를 읽고 정리한 글이다.

## Components와 Props - 컴포넌트와 속성

: 개념적으로 컴포넌트는 JavaScript 함수와 유사하다. **“props”**라고 하는 임의의 입력을 받은 후, 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환한다.

## 함수 컴포넌트와 클래스 컴포넌트

: 컴포넌트를 정의하는 가장 간단한 방법은 JavaScript 함수를 작성하는 것이다.

- 함수형 컴포넌트

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

: 이 함수는 데이터를 가진 하나의 `"props"` 객체 인자를 받은 후 React 엘리먼트를 반환하므로 유효한 React 컴포넌트이다.  
이러한 컴포넌트는 JavaScript 함수이기 때문에 말 그대로 **“함수 컴포넌트”**라고 호칭한다.

- 클래스형 컴포넌트

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

- React의 관점에서 볼 때 위 두 가지 유형의 컴포넌트는 동일하다.

## 컴포넌트 렌더링

: React는 기존의 DOM 태그 뿐만 아니라 사용자 정의 컴포넌트로도 나타낼 수 있다.

- 기존 DOM 태그

```jsx
const element = <div />;
```

- 사용자 정의 컴포넌트

```jsx
const element = <Welcome name="Sara" />;
```

React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면 **JSX 어트리뷰트`(name=”Sara”)`와 자식을 해당 컴포넌트에 단일 객체로 전달**하게 되는데, 이 때 전달되는 **객체를 “props”** 라고 한다.

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const root = ReactDOM.createRoot(document.getElementById("root"));
const element = <Welcome name="Sara" />;
root.render(element);
```

이 예시에서 어떤 일이 일어났는지 요약하자면

1. `<Welcome name="Sara" />` 엘리먼트로 `root.render()`를 호출
2. React는 `{name: 'Sara'}`를 `props`로 하여 `Welcome` 컴포넌트를 호출
3. `Welcome` 컴포넌트는 `<h1>Hello, Sara</h1>` 엘리먼트를 반환
4. React DOM은 `<h1>Hello, Sara</h1>` 엘리먼트와 일치하도록 DOM을 업데이트

> **🚨 주의 : 컴포넌트의 이름은 항상 대문자로 시작한다.**  
> React는 소문자로 시작하는 컴포넌트를 DOM태그로 인식한다. 예를 들어 `<div />`는 HTML `div` 태그를 나타내지만, `<Welcome />`은 컴포넌트를 나타내기 떄문에 범위 안에 `Welcome`이 정의 되어있어야 한다.

## 컴포넌트 합성

: 컴포넌트는 자신의 출력에 다른 컴포넌트를 참조할 수 있다. 예를 들어 `Welcome`을 여러 번 렌더링하는 `App` 컴포넌트를 만들 수 있다.

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}
```

일반적으로 새 React 앱은 최상위에 단일 `App` 컴포넌트를 가지고 있지만 기존 앱에 React를 통합하는 경우에는 `Button`과 같은 작은 컴포넌트부터 시작해서 뷰 계층의 상단으로 올라가면서 점진적으로 작업해야 할 수 있다.

- 위의 예시에서 `Welcome` 컴포넌트가 어트리뷰트만 다른채 3개가 배치되어 있음을 알 수 있다. : **컴포넌트의 추상화**
- 또 `App` 컴포넌트 안에 `Welcome` 컴포넌트가 배치된 것도 확인할 수 있다. : **컴포넌트의 합성**

## 컴포넌트 추출

: 컴포넌트는 여러 개의 작은 컴포넌트로 나눌 수 있고, 가능한 작은 컴포넌트로 나누는 것이 더 효율적인 작업을 하는데 도움이 될 수 있다.

```jsx
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img
          className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">{props.author.name}</div>
      </div>
      <div className="Comment-text">{props.text}</div>
      <div className="Comment-date">{formatDate(props.date)}</div>
    </div>
  );
}
```

이 컴포넌트는 `author`(객체), `text`(문자열) 및 `date`(날짜)를 props로 받고 있다. `Comment`에 필요한 모든 기능을 제공하고 있지만, 구성요소들이 모두 중첩 구조로 이루어져 있기 때문에 변경이 어렵고, 각 구성요소를 개별적으로 **재사용하기도 힘들다는 단점**이 있다.

🐢**해결**:`Comment` 컴포넌트에서 `Avatar`, `UserInfo`와 같이 몇 가지 컴포넌트를 추출하여 새로운 개별 컴포넌트로 만들면 `Comment` 컴포넌트는 더 단순해지고 효율적인 컴포넌트가 될 수 있다.

1️⃣ 먼저 `Avatar`를 추출한다.

```jsx
function Avatar(props) {
  return (
    <img className="Avatar" src={props.user.avatarUrl} alt={props.user.name} />
  );
}
```

- `Avatar` 는 자신이 `Comment` 내에서 렌더링 된다는 것을 알 필요가 없기 때문에 props의 이름을 `author`에서 더욱 일반화된 `user`로 변경했는데 이렇게 **props의 이름은 사용될 `context`가 아닌 컴포넌트 자체의 관전에서 짓는 것이 권장된다.**

```jsx
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">{props.author.name}</div>
      </div>
      <div className="Comment-text">{props.text}</div>
      <div className="Comment-date">{formatDate(props.date)}</div>
    </div>
  );
}
```

- 💨**결과**: Comment 가 살짝 단순해졌다.

2️⃣ `Avatar` 옆에 사용자의 이름을 렌더링하는 `UserInfo` 컴포넌트를 추출한다.

```jsx
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">{props.user.name}</div>
    </div>
  );
}
```

```jsx
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">{props.text}</div>
      <div className="Comment-date">{formatDate(props.date)}</div>
    </div>
  );
}
```

- 💨**결과**: Comment 가 더욱 단순해졌다.
  : 이런 식으로 재사용 가능한 컴포넌트를 만들어 놓는 것은 큰 규모의 앱에서 작업할 때 두각을 나타낸다. UI의 일부가 여러 번 사용되거나(`Button`, `Panel`, `Avatar`), UI의 일부가 자체적으로 복잡한(`App`, `FeedStory`, `Comment`) 경우에는 개별적인 컴포넌트로 만드는 것이 좋다.

## Props

: 함수 컴포넌트나 클래스 컴포넌트 모두 컴포넌트의 자체 props를 수정해서는 안된다.
: React는 매우 유연하지만 한 가지 엄격한 규칙이 있는데, 바로 **모든 컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수 처럼 동작해야 한다.**

- 순수 함수 ⭕ : 입력값은 바꾸려 하지 않고 항상 동일한 입력값에 대해 동일한 결과를 반환

```jsx
function sum(a, b) {
  return a + b;
}
```

- 순수 함수가 아님 ❌: 자신의 입력값을 변경하기 때문에 순수 함수가 아니다.

```jsx
function withdraw(account, amount) {
  account.total -= amount;
}
```
