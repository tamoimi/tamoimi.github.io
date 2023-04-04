---
title: "[Algorithm] 모음 제거"
categories:
  - Algorithms
tags:
  - [Algorithms, JavaScript, replace, 정규표현식]
permalink: /Blog/algorithm-09/
toc: true
toc_sticky: true
toc_label: # "ALGORITHM"
date: 2023-04-04
last_modified_at: 2023-04-04
---

## Algorithm 풀기

### 문제 설명

영어에선 a, e, i, o, u 다섯 가지 알파벳을 모음으로 분류합니다.
문자열 my_string이 매개변수로 주어질 때 모음을 제거한 문자열을 return하도록 solution 함수를 완성해주세요.

### 제한사항

- my_string은 소문자와 공백으로 이루어져 있습니다.
- 1 ≤ my_string의 길이 ≤ 1,000

### 입출력 예

| my_string          | result      |
| ------------------ | ----------- |
| "bus"              | "bs"        |
| "nice to meet you" | "nc t mt y" |

### 입출력 예 설명

- 입출력 예 #1

  - "bus"에서 모음 u를 제거한 "bs"를 return합니다.

- 입출력 예 #2

  - "nice to meet you"에서 모음 i, o, e, u를 모두 제거한 "nc t mt y"를 return합니다.

### 나의 풀이 방법

```js
function solution(my_string) {
  const newStr = my_string.replace(/a|e|i|o|u/g, "");
  return newStr;
}
```

> `replace()`메서드와 정규식을 이용하여 작성했다.

### 🐳 String.prototype.replace()

#### 구문

```js
var newStr = str.replace(regexp|substr, newSubstr|function)
```

- `replace()` 메서드는 어떤 패턴에 일치하는 일부 또는 모든 부분이 교체된 새로운 문자열을 반환한다.
  그 패턴은 문자열이나 정규식(RegExp)이 될 수 있으며, 교체 문자열은 문자열이나 모든 매치에 대해서 호출된 함수일 수 있다.

* pattern이 문자열 인 경우, 첫 번째 문자열만 치환이 되며 원래 문자열은 변경되지 않는다.

```js
const text = "나는 바나나 입니다.";

console.log(text.replace("바나나", "딸기"));
// output: "나는 딸기 입니다."

const regex = /바나나/i;
console.log(text.replace(regex, "수박"));
// output: "나는 수박 입니다."

const text = "I am a monkey.";
console.log(text.replace(/[am]/, "y"));
// Expected output: "I ym a monkey."

const p = "i am a monkey";
// 정규식으로 replaceAll을 호출할 때 필요한 전역 플래그
const regex = /a|m/gi;
console.log(p.replaceAll(regex, ""));
// Expected output: "i   onkey"
```
