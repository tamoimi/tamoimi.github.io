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

터미널에서 아래 명령어로 리액트 훅 폼을 설치한다.

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

