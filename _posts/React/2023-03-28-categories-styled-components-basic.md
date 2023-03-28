---
title: "[React] Styled-Components 사용하기"
date: 2023-03-28
categories:
  - React
tags:
  - [React, Styled-Components, css]
permalink: /Blog/styled-components/
toc: true
toc_sticky: true
toc_label: "Styled-Components"
last_modified_at: 2023-03-28
---

🪐 **작성자 개발 환경** <br>
**OS** : Windows 10<br>
{: .notice}

## Styled-Components 시작하기

[💅🏻 Styled-Components 참고 문서는 여기서 확인 가능](https://styled-components.com/){:target="\_blank"} <br/>

styled-components는 인라인으로 CSS를 넣는게 아니라, <스타일> 태그 안에 임의로 생성된 클래스명으로 CSS를 만들고, 그 태그를 가져다 쓰는 방식으로 만들어진다. 클래스명이 유니크하게 생성되기 때문에 클래스 네이밍에 대한 걱정은 안해도 된다.

그리고 Props를 받을 수 있어서 조건부 스타일링을 쉽게 할 수 있고, 쉽게 JavaScript 상수나 변수를 받을 수 있다. 즉 동적 스타일링 기능을 제공한다. 이 동적 스타일링을 제공하느냐 여부에 따라 CSS-in-JS의 세대를 나누기도 한다.

### React 환경 설치

`npx create-react-app 프로젝트 이름`

### Styled Components 설치

터미널에서 아래 명령어를 입력해 설치한다.

`npm i styled-components`

### 컴포넌트에 styled-components import

```jsx
// App.js

import styled from "styled-components";
```

### styled-components를 적용한 방법

> 기본 사용 방법

```js
import styled from "styled-components";

const Father = styled.div`
  display: flex;
`;

const BoxOne = styled.div`
  background-color: teal;
  width: 100px;
  height: 100px;
`;

const BoxTwo = styled.div`
  background-color: tomato;
  width: 100px;
  height: 100px;
`;

function App() {
  return (
    <Father>
      <BoxOne />
      <BoxTwo />
    </Father>
  );
}

export default App;
```

---

> 공통적으로 사용되는 스타일들을 styled-components를 이용해 설정 변경이 가능한 컴포넌트를 만들 수 있다. (props를 통해 컴포넌트를 설정하는 방법)

```js
import styled from "styled-components";

const Father = styled.div`
  display: flex;
`;

const Box = styled.div`
  background-color: ${(props) => props.bgColor};
  width: 100px;
  height: 100px;
`;

function App() {
  return (
    <Father>
      <Box bgColor="teal" />
      <Box bgColor="tomato" />
    </Father>
  );
}
```

---

> 코드 가독성을 높이고 컴포넌트를 확장하는 방법 : 다른 컴포넌트의 스타일을 상속하는 새 컴포넌트를 쉽게 만들려면 styled( ) 생성자에 구성

```js
import styled from "styled-components";

const Father = styled.div`
  display: flex;
`;

const Box = styled.div`
  background-color: ${(props) => props.bgColor};
  width: 100px;
  height: 100px;
`;

const Circle = styled(Box)`
  border-radius: 50px;
`;

function App() {
  return (
    <Father>
      <Box bgColor="teal" />
      <Circle bgColor="tomato" />
    </Father>
  );
}

export default App;
```

---

> 컴포넌트의 태그를 바꾸고 싶은데 스타일을 바꾸고 싶지 않을 때 : as를 사용하여 엘리먼트를 다른 엘리먼트로 교체할 수 있다.

```js
import styled from "styled-components";

const Father = styled.div`
  display: flex;
`;

const Btn = styled.button`
  color: white;
  background-color: tomato;
  border: 0;
  border-radius: 15px;
`;

function App() {
  return (
    <Father>
      <Btn>Log in</Btn>
      <Btn as="a" href="/">
        Log in
      </Btn>
    </Father>
  );
}

export default App;
```

---

> html 태그의 속성을 설정할 수 있다. : styled components가 컴포넌트를 생성할 때, 속성값을 설정할 수 있게 해준다.

```js
import styled from "styled-components";

const Father = styled.div`
  display: flex;
`;

const Input = styled.input.attrs({ required: true })`
  background-color: tomato;
`;

function App() {
  return (
    <Father>
      <Input />
      <Input />
      <Input />
      <Input />
      <Input />
      <Input />
    </Father>
  );
}

export default App;
```
