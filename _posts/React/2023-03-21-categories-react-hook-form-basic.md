---
title: "[React] React-Hook-Form 시작하기"
date: 2023-03-21
categories:
  - React
tags:
  - [React, React-Hook-Form]
permalink: /Blog/react-hook-form-basic/
toc: true
toc_sticky: true
toc_label: "React-Hook-Form"
last_modified_at: 2023-03-21
---

🪐 **작성자 개발 환경** <br>
**OS** : Windows 10<br>
{: .notice}

## React-Hook-Form 시작하기

React는 사용자 인터페이스를 구축하기 위한 자바스크립트 라이브러리이며, React Hook Form은 React 애플리케이션에서 폼을 관리하기 위한 라이브러리다.

React는 재사용 가능한 UI 컴포넌트를 정의하고 useState 및 useEffect 훅과 클래스 컴포넌트 및 라이프사이클 메소드를 사용하여 상태를 관리하는 방법을 제공한다. 그러나 React만으로 폼 상태 및 유효성 검사를 처리하는 것은 복잡한 폼의 경우 도전적일 수 있다.

React Hook Form은 폼 상태를 관리하고 유효성 검사를 수행하며 폼 제출을 처리하기 쉽게 만드는 useForm, useField, useController 등의 훅 세트를 제공한다. 기존의 React 기능 위에 구축되었으며, 다른 React 라이브러리 및 컴포넌트와 함께 사용할 수 있다.

---

🔮터미널에서 아래 명령어로 리액트 훅 폼을 설치한다.

```js
npm install react-hook-form
```

## 기존 방법

```js
import React, { useState } from "react";

function MyForm() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");

  const handleSubmit = (event) => {
    event.preventDefault();
    // Form submission logic here
  };

  const handleNameChange = (event) => {
    setName(event.target.value);
  };

  const handleEmailChange = (event) => {
    setEmail(event.target.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>Name:</label>
      <input type="text" name="name" value={name} onChange={handleNameChange} />

      <label>Email:</label>
      <input
        type="email"
        name="email"
        value={email}
        onChange={handleEmailChange}
      />

      <button type="submit">Submit</button>
    </form>
  );
}
```

이 예시에서는 React에서 useState와 onChange 이벤트를 사용하여 폼 상태를 관리하고
입력 필드에 사용자가 타이핑할 때 상태를 업데이트한다.
또한 폼 제출을 처리하기 위해 handleSubmit 함수를 제공한다.

## React-Hook-Form을 이용한 방법

```js
import React from "react";
import { useForm } from "react-hook-form";

function MyForm() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm();

  const onSubmit = (data) => {
    // Form submission logic here
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <label>Name:</label>
      <input
        type="text"
        name="name"
        {...register("name", { required: true })}
      />
      {errors.name && <span>This field is required</span>}

      <label>Email:</label>
      <input
        type="email"
        name="email"
        {...register("email", { required: true })}
      />
      {errors.email && <span>This field is required</span>}

      <button type="submit">Submit</button>
    </form>
  );
}
```

React Hook Form으로 작성된 동일한 폼에서는 useForm 훅을 사용하여 폼을 초기화하고 폼 제출 로직을 제공한다.

register 함수를 사용하여 각 폼 필드를 등록하고 인자로 유효성 검사 규칙을 제공한다. 또한 errors 객체를 사용하여 유효성 검사 오류를 표시할 수 있다.

이 방법은 React 애플리케이션에서 폼 상태 및 유효성 검사를 처리하는 더욱 깔끔하고 선언적인 방법을 제공한다.
