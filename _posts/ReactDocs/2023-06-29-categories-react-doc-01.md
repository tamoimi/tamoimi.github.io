---
title: "[React Docs] 1. Hello World"
date: 2023-06-29
categories:
  - React
tags:
  - [React]
permalink: /Blog/react-doc-01/
toc: true
toc_sticky: true
toc_label: "Hello World"
last_modified_at: 2023-06-29
---

## Hello World!

> 본 게시글은 [리액트 공식문서](https://reactjs.org/docs/getting-started.html)를 읽고 정리한 글이다.

오늘 부터 리액트 문서를 읽고 요약할 것이다.  
이 문서는 오래되어 업데이트 되지 않을 것이기 때문에 [react.dev](https://react.dev)에서 업데이트 된 내용을 확인 할 수 있다.

- 가장 단순한 React 예시는 다음과 같이 생겼다.

```js
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<h1>Hello, world!</h1>);
```

![image](https://github.com/tamoimi/tami-portfolio/assets/100749520/6dea3f3c-5dc7-4d64-a7fa-9f055e9e2637)

- 위 코드는 페이지에 “Hello, world!”라는 제목을 보여준다.

> React는 JavaScript의 라이브러리이며, 따라서 JavaScript 언어에 대한 기본적인 이해가 필요하다. 아직 자신이 없다면, [JavaScript 튜토리얼 살펴보기](https://developer.mozilla.org/ko/docs/A_re-introduction_to_JavaScript)를 통해 자신의 지식수준을 확인하길 권장한다.
