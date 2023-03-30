---
title: "[JavaScript] padStart()와 padEnd()사용하기"
date: 2023-03-30
categories:
  - JavaScript
tags:
  - [JavaScript, padStart, padEnd, function]
permalink: /Blog/pad/
toc: true
toc_sticky: true
toc_label: "pad function"
last_modified_at: 2023-03-30
---

🪐 **작성자 개발 환경** <br>
**OS** : Windows 10<br>
{: .notice}

## JavaScript pad()

**`String.prototype.padStart()`** <br/>
**`String.prototype.padEnd()`**

**`padStart()` `padEnd()`** 함수는 ES8(ES2017)에 새롭게 추가된 기능이다.

`pad` 는 좌우에 특정한 문자열로 채우는 기능이다. 첫번째 파라미터인 maxLength를 받아 문자열의 길이가 maxLength보다 작을 경우 나머지를 특정한 문자열로 채워주는 기능이다. 이때 두번째 문자열을 넘겨주지 않으면 빈 공백으로 문자열을 채운다.

---

> JavaScript Demo: String.padEnd()

```js
const str1 = "Breaded Mushrooms";

console.log(str1.padEnd(25, "."));
// Expected output: "Breaded Mushrooms........"

const str2 = "200";

console.log(str2.padEnd(5));
// Expected output: "200  "

const str3 = "terence";

console.log(str3.padEnd(20, "1"));
// Expected output: "terence1111111111111"
```

### 구문

`str.padEnd(targetLength [, padString])`

🌞`targetLength`

목표 문자열 길이. 현재 문자열의 길이보다 작다면 채워넣지 않고 그대로 반환.

🌞`padString` (Optional)

현재 문자열에 채워넣을 다른 문자열. 문자열이 너무 길어 목표 문자열 길이를 초과한다면 좌측 일부를 잘라서 넣음. 기본값은 " ". (U+0020)

### 예시

```js
"abc".padEnd(10); // "abc       "
"abc".padEnd(10, "foo"); // "abcfoofoof"
"abc".padEnd(6, "123456"); // "abc123"
"abc".padEnd(1); // "abc"
```

---

> JavaScript Demo: String.padStart()

```js
const str1 = "5";

console.log(str1.padStart(2, "0"));
// Expected output: "05"

const fullNumber = "2034399002125581";
const last4Digits = fullNumber.slice(-4);
const maskedNumber = last4Digits.padStart(fullNumber.length, "*");

console.log(maskedNumber);
// Expected output: "************5581"
```

### 구문

`str.padStart(targetLength [, padString])`

🌞`targetLength`

목표 문자열 길이. 현재 문자열의 길이보다 작다면 채워넣지 않고 그대로 반환.

🌞`padString` (Optional)

현재 문자열에 채워넣을 다른 문자열. 문자열이 너무 길어 목표 문자열 길이를 초과한다면 좌측 일부를 잘라서 넣음. 기본값은 " ". (U+0020)

### 예시

```js
"abc".padStart(10); // "       abc"
"abc".padStart(10, "foo"); // "foofoofabc"
"abc".padStart(6, "123465"); // "123abc"
"abc".padStart(8, "0"); // "00000abc"
"abc".padStart(1); // "abc"
```
