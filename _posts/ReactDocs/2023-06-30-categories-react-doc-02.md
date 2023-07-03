---
title: "[React Docs] 2️. JSX 소개"
date: 2023-06-30
categories:
  - React
tags:
  - [React]
permalink: /Blog/react-doc-02/
toc: true
toc_sticky: true
toc_label: "JSX 소개"
last_modified_at: 2023-06-30
---

> 리액트 공식문서 주요개념 부분의 JSX 소개를 읽고 정리한 글이다.

## JSX란?

```js
const element = <h1>Hello, world!</h1>;
```

- 위의 태그 문법은 문자열도, HTML도 아니다. 이 태그 문법은 **JSX**라 하며 **JavaScript에 XML을 추가하여 확장한 문법**이다.  
  브라우저에서 실행되기 전에 **바벨을 통해 일반적인 자바스크립트 코드로 변환**되며 공식적인 자바스크립트 문법은 아니다.

- React는 본질적으로 **렌더링 로직이 UI로직과 연결**되는데, 별도의 파일에 마크업과 로직을 넣어 기술을 인위적으로 분리하는 대신, 마크업과 로직을 모두 포함하는 **컴포넌트 형태**로 구성할 수 있다.

- 여기서 UI로직이란, **이벤트가 처리되는 방식, 시간에 따라 state가 변하는 방식, 화면에 표시하기 위해 데이터가 준비되는 방식** 등을 말하는데, React에서는 JSX가 필수는 아니지만 자바스크립트 코드 안에서 UI관련 작업을 할 때 도움이 될 수 있고 React가 더욱 도움이 되는 에러 및 경고 메시지를 표시할 수 있게 해준다. **<u>라고 공식 문서에 나와있지만 무슨 말인지 이해 하기 어렵다. 쉽게 말해 React에서 Virural DOM을 만들 때 편하게 코딩할 수 있게 HTML처럼 작성 할 수 있게 도와주는 템플릿 언어 비슷한 것 이라고 이해 하면 쉬울 것 같다.</u>**

### 🤔XML(Extensible Markup Language) 이란?

: 데이터를 정의하는 규칙을 제공하는 마크업 언어이다. 다른 프로그래밍 언어와 달리 XML은 자체적으로 작업을 수행할 수 없지만 구조적 데이터 관리를 위해 모든 프로그래밍 언어 또는 소프트웨어를 구현할 수 있다.

## JSX에 표현식 포함하기

```js
const name = "Tami Kim";
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(element, document.getElementById("root"));
```

- 위 예시는 `name`이라는 변수를 선언한 후 중괄호로 감싸 JSX 안에 사용하는 예로, JSX의 중괄호 안에는 유효한 모든 [JavaScript 표현식](<https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Expressions_and_Operators#%ED%91%9C%ED%98%84(%EC%8B%9D)>)을 넣을 수 있다. **문이 아닌 표현식이라는 점에 유의하자.**

```js
function formatName(user) {
  return user.firstName + " " + user.lastName;
}

const user = {
  firstName: "Tami",
  lastName: "Kim",
};

const element = <h1>Hello, {formatName(user)}!</h1>;

ReactDOM.render(element, document.getElementById("root"));
```

- 위 예시에서는 JS함수 호출의 결과인 `formatName(user)`을 `<h1>` 엘리먼트에 포함한다. 위와 같이 element의 JSX를 여러 줄로 나눌때, 자동 세미콜론 삽입을 피하기 위해 괄호로 묶는 것을 권장한다.

## JSX도 표현식이다

컴파일이 끝나면 JSX 표현식이 정규 JavaScript 함수가 호출되고 JavaScript 객체로 인식한다.
즉, JSX를 `if`구문 및 `for` loop안에 사용하고, 변수에 할당하고, 인자로서 받아들이고, 함수로 부터 반환할 수 있다

```js
const getGreeting = (user) => {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
};
```

## JSX 속성 정의와 자식 정의

### 속성 정의

```js
const element = <a href="https://www.reactjs.org"> link </a>;
```

- JSX는 위 코드와 같이 속성에 따옴표“”를 이용해 문자열 리터럴을 정의할 수 있는데, 다음과 같이 중괄호{}를 사용하여 속성에 자바스크립트 표현식을 삽입할 수도 있다.

```js
const element = <img src={user.avatarUrl}></img>;
```

- JSX의 속성에 자바스크립트 표현식을 삽입하는 경우에는 중괄호를 따옴표“”로 감싸면 안되는데, 홈페이지의 관련 문서에는 따옴표 또는 중괄호 중 하나만 사용해야 한다고 안내되어 있다.
- 참고로 속성을 사용할 때 JSX는 HTML보다는 JavaScript에 가깝기 때문에, React DOM은 HTML 속성의 이름 대신 카멜케이스 프로퍼티 명명 규칙을 사용한다. 예를 들어, JSX에서 `class`는 `className` 으로, `tabindex`는 `tabIndex`와 같이 사용할 수 있다.

### 자식 정의

```js
const element = <img src={user.avatarUrl} />;
```

- 위 코드와 같이 JSX 문법에서 태그가 비어있는 경우에 XML처럼 `/>`를 이용해 바로 닫아주어야 한다. 만약 자식 요소가 있다면 다음 코드와 같이 자식을 포함시킬 수 있다.

```js
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

## JSX의 특징

### 주입 공격 방지

- JSX에서 사용자 입력을 받아 코드에 삽입하는 것은 안전하다. 기본적으로 React DOM은 JSX에 삽입된 모든 값을 렌더링 하기 전에 이스케이프 처리를 하기 때문에, 앱에서 명시적으로 작성되지 않은 내용은 주입되지 않고, 모든 항목은 렌더링 되기 전에 문자열로 변환되는데, JSX는 이런 특성으로 인해 [XSS (cross-site-scripting)](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9D%B4%ED%8A%B8_%EA%B0%84_%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8C%85)공격을 방지할 수 있다.

```js
const title = response.potentiallyMaliciousInput;
const element = <h1>{title}</h1>; // 안전한 코드
```

### 객체 표현

- Babel은 JSX를 `React.createElement()`호출로 컴파일하는데, 다음의 두 예제는 동일한 결과를 보여준다.

```js
const element = <h1 className="greeting">Hello, world!</h1>;
```

```js
const element = React.createElement(
  "h1",
  { className: "greeting" },
  "Hello, world!"
);
```

- `React.createElement()`는 버그가 없는 코드를 작성하는데 도움이 되도록 몇 가지 검사를 수행하는데, 기본적으로 다음과 같은 객체를 생성한다.

```js
const element = {
  type: "h1",
  props: {
    className: "greeting",
    children: "Hello, world!",
  },
};
```

- 이렇게 생성된 객체는 “React 엘리먼트”라고 하는데, 화면의 UI를 나타내는 표현 객체라고 할 수 있다. React는 이 객체를 읽어서 DOM을 구성하고 최신 상태로 유지하는데 사용한다.
