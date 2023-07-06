---
title: "[React Docs] 3️. 엘리먼트 렌더링"
date: 2023-07-03
categories:
  - React
tags:
  - [React]
permalink: /Blog/react-doc-03/
toc: true
toc_sticky: true
toc_label: "엘리먼트 렌더링"
last_modified_at: 2023-07-03
---

> 본 게시글은 [리액트 공식문서](https://reactjs.org/docs/getting-started.html)를 읽고 정리한 글이다.

## 엘리먼트 렌더링

- 엘리먼트는 React 앱의 **가장 작은 단위**이고 **화면에 표시할 내용**을 기술한다.
- 브라우저 DOM 엘리먼트와 달리 React 엘리먼트는 일반 객체로 쉽게 생성할 수 있고, React DOM은 React 엘리먼트와 일치하도록 DOM을 업데이트한다.

```js
const element = <h1>Hello, world!</h1>;
```

🦥 더 널리 알려진 “컴포넌트”와 엘리먼트를 혼동할 수 있지만, 엘리먼트는 바로 이 컴포넌트의 “구성 요소”라고 할 수 있다.

## DOM에 엘리먼트 렌더링

- React는 일반적으로 `<div id = "root">` 와 같이 특정 id 를 가진 HTML엘리먼트를 생성한다. 이 엘리먼트에 들어가는 모든 엘리먼트를 React DOM에서 관리하기 때문에 최초의 엘리먼트를 “루트(root)”DOM 노드라고 부른다.

```js
<div id="root"></div>
```

- React로 구현된 앱은 일반적으로 하나의 루트DOM 노드가 있지만 React를 기존 앱에 통합하려는 경우 원하는 만큼 많은 수의 독립된 루트 DOM 노드가 있을 수 있다.

- React 엘리먼트를 루트 DOM노드에 렌더링 하기 위해서는 우선 DOM 엘리먼트를 `1.ReactDOM.createRoot()` 에 전달한 다음, React 엘리먼트를 `2.**root.render()**`에 전달해야 한다.

```js
// id가 root인 DOM 요소를 ReactDOM.createRoot()에 전달
const root = ReactDOM.createRoot(document.getElementById("root"));
const element = <h1>Hello, world</h1>;
// React 요소를 root.render()에 전달
root.render(element);

// output: Hello, world
```

## 렌더링 된 엘리먼트 업데이트

- React 엘리먼트는 [불변객체](https://ko.wikipedia.org/wiki/%EB%B6%88%EB%B3%80%EA%B0%9D%EC%B2%B4)로, 엘리먼트를 생성한 이후에는 해당 엘리먼트의 자식이나 속성을 변경할 수 없다.
- 엘리먼트는 하나의 프레임과 같이 특정 시점의 UI를 보여주는데, UI를 업데이트하는 유일한 방법은 새로운 엘리먼트를 생성하고 이를 `root.render()`로 전달하는 것이다.

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

- 위 코드는 초 단위로 업데이트되는 디지털 시계를 구현한 것인데 `setInterval()` 콜백을 이용해 초마다 `root.render()`를 호출한다.
- 하지만 실제 작업에서 대부분의 React 앱은 `ReactDOM.render()`를 한 번만 호출하기 때문에 이와 같은 코드가 상태 컴포넌트에서 **어떻게 캡슐화되는지** 를 이해할 필요가 있다.

## 변경된 부분만 업데이트하기

- 코드를 보면 매 초마다 전체 UI를 다시 그리도록 엘리먼트를 생성했지만 **React DOM은 해당 엘리먼트와 그 자식 엘리먼트를 이전의 엘리먼트와 비교하여 내용이 변경된 텍스트 노드만 업데이트** 했다.

![granular-dom-updates](https://github.com/tamoimi/tamoimi.github.io/assets/100749520/084bbd2b-6332-4a85-afff-dd58023f3f08)

- 이렇게 특정 시점에 UI가 어떻게 보일지 고민하는 접근법은 시간의 변화에 따라 UI가 어떻게 변화할지 고민하는 것보다 더 많은 수의 버그를 없앨 수 있는 방법이 될 수 있다.
