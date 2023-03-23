---
title: "[React] React-To-Print 사용하기"
date: 2023-03-23
categories:
  - React
tags:
  - [React, React-To-Print, pdf]
permalink: /Blog/react-to-print/
toc: true
toc_sticky: true
toc_label: "React-To-Print"
last_modified_at: 2023-03-23
---

🪐 **작성자 개발 환경** <br>
**OS** : Windows 10<br>
{: .notice}

## React-To-Print 시작하기

[🖨 React-To-out 참고 자료는 여기서 확인 가능](https://www.npmjs.com/package/react-to-print/){:target="\_blank"}

🔮터미널에서 아래 명령어로 리액트 훅 폼을 설치한다.

```
npm install --save react-to-print
```

`ReactToPrint`는 컴포넌트 단위로 손쉽게 프린트할 수 있는 기능을 제공한다. <br/>
useRef를 이용해서 ref의 current객체에 프린트 하고자 하는 HTML DOM 요소를 업데이트 시켜, 출력 함수의 content키의 value로 전달할 수 있다.

## 기본 사용 방법

```js
import React, { useRef } from "react";
import { useReactToPrint } from "react-to-print";

const Print = () => {
  const componentRef = useRef();

  const handlePrint = useReactToPrint({
    content: () => componentRef.current,
  });

  return (
    <>
      <div>
        <button onClick={handlePrint}>Print this out!</button>
      </div>
      <div ref={componentRef}>
        <h2>Print this out</h2>
        <p>
          Lorem Ipsum is simply dummy text of the printing and typesetting
          industry. Lorem Ipsum has been the industry's standard dummy text ever
          since the 1500s, when an unknown printer took a galley of type and
          scrambled it to make a type specimen book. It has survived not only
          five centuries, but also the leap into electronic typesetting,
          remaining essentially unchanged. It was popularised in the 1960s with
          the release of Letraset sheets containing Lorem Ipsum passages, and
          more recently with desktop publishing software like Aldus PageMaker
          including versions of Lorem Ipsum.
        </p>
      </div>
    </>
  );
};

export default Print;
```

## 결과 화면

😎 pdf 인쇄 전 미리보기 화면을 확인할 수 있다.

![image](https://user-images.githubusercontent.com/100749520/227086663-a532828d-422a-48cb-83a0-e1a9cc540ff5.png)
