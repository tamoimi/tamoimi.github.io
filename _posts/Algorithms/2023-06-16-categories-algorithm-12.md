---
title: "[Algorithm] 대문자로 바꾸기, 문장의 첫 번째 문자만 대문자로 바꾸기"
categories:
  - Algorithms
tags:
  - [Algorithms, JavaScript, charAt, toUpperCase, toLowerCase]
permalink: /Blog/algorithm-12/
toc: true
toc_sticky: true
toc_label: # "ALGORITHM"
date: 2023-06-16
last_modified_at: 2023-06-16
---

## Algorithm 풀기

### 문제 설명

알파벳으로 이루어진 문자열 myString이 주어집니다. 모든 알파벳을 대문자로 변환하여 return 하는 solution 함수를 완성해 주세요.

### 제한사항

- 1 ≤ myString의 길이 ≤ 100,000
  - myString은 알파벳으로 이루어진 문자열입니다.

### 입출력 예

| myString  | result    |
| --------- | --------- |
| "aBcDeFg" | "ABCDEFG" |
| "AAA"     | "AAA"     |

### 나의 풀이 방법

```js
function solution(myString) {
  const answer = myString.toUpperCase();
  return answer;
}
```

> 이번에는 간단한 문제였다. `toUpperCase()`메서드를 문자열을 대문자로 변환해 반환한다.
> 결론은 JavaScript 짱

- 여기서 생긴 질문 하나 🤔
- 예를 들어 "this is a test"에서 문장의 첫 글자만 대문자로 바꾸고 싶다면?

```js
const sentence = "this is a test";
const result = sentence.charAt(0).toUpperCase() + sentence.slice(1);

console.log(result);
// output: "This is a test"
```

- `sentence.charAt(0)`는 문자열 `sentence`의 첫 번째 문자를 반환하는 메서드다. 여기서는 "t"가 반환된다. `.toUpperCase()`는 문자열을 대문자로 변환하는 메서드이다. "t"를 대문자 "T"로 변환한다. 따라서 `sentence.charAt(0).toUpperCase() + sentence.slice(1)`는 첫 번째 문자를 대문자로 변환한 후, 나머지 부분과 합쳐서 "This is a test"라는 결과를 출력한다.

### 🐳 String.prototype.toLowerCase()

- toLowerCase() 메서드는 문자열을 소문자로 변환해 반환한다.

```js
const 대문자문장 = "THIS IS UPPERCASE.";

console.log(대문자문장.toLowerCase());
// output: "this is uppercase."
```
