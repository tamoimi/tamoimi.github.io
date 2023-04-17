---
title: "[html] form 기본 유효성 검사 비활성화 하기 / Disable validation of HTML5"
date: 2023-04-17
categories:
  - Html
tags:
  - [Html, form, validate]
permalink: /Blog/disable-form-validate/
toc: true
toc_sticky: true
toc_label: "Disable form validate"
last_modified_at: 2023-04-17
---

🪐 **작성자 개발 환경** <br>
**OS** : Windows 10<br>
{: .notice}

## 문제

`form`을 생성해 만들어 둔 에러 메시지를 보여주려고 했지만, `form` 제출 시에 아래 이미지와 같이 html의 경고창이 띄워졌다. <br/>
![image](https://user-images.githubusercontent.com/129496536/232424666-3a66b997-30d3-456f-ae62-9476fe1dffe9.png)

## 문제 해결

`<form>` 태그에 `noValidate`를 추가한다.
![image](https://user-images.githubusercontent.com/129496536/232426269-7f3aab72-8a57-439d-9d08-e7411e7aaa3c.png)

### <form> 태그의 novalidate 속성

`<form>` 태그의 novalidate 속성은 폼 데이터(form data)를 서버로 제출할 때 해당 데이터의 유효성을 검사하지 않음을 명시한다.
novalidate 속성은 불리언(boolean) 속성이다. 불리언 속성은 해당 속성을 명시하지 않으면 속성값이 자동으로 false 값을 가지게 되며, 명시하면 자동으로 true 값을 가지게 된다.

### 예제

```js
<form novalidate>
    이메일 주소 : <input type="email" name="user-email">
    <input type="submit">
</form>
```
