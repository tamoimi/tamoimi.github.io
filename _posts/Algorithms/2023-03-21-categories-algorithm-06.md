---
title: "[Algorithm] 문자 반복 출력하기"
categories:
  - Algorithms
tags:
  - [Algorithms, JavaScript, repeat, join, Destructuring assignment]
permalink: /Blog/algorithm-06/
toc: true
toc_sticky: true
toc_label: # "GITHUB BLOG START"
date: 2023-03-21
last_modified_at: 2023-03-21
---

## Algorithm 풀기

### 문제 설명

문자열 `my_string`과 정수 `n`이 매개변수로 주어질 때, `my_string`에 들어있는 각 문자를 `n`만큼 반복한 문자열을 return 하도록 solution 함수를 완성해보세요.

### 제한사항

- 2 ≤ my_string 길이 ≤ 5
- 2 ≤ n ≤ 10
- "my_string"은 영어 대소문자로 이루어져 있습니다.

### 입출력 예

| my_string | n   | result            |
| --------- | --- | ----------------- |
| "hello"   | 3   | "hhheeellllllooo" |

### 입출력 예 설명

- 입출력 예 #1

  - "hello"의 각 문자를 세 번씩 반복한 "hhheeellllllooo"를 return 합니다.

### 나의 풀이 방법

```js
function solution(my_string, n) {
  let answer = [...my_string].map((l) => l.repeat(n)).join("");
  return answer;
}
```

> 스프레드 연산자를 활용하여 `my_string`에 들어간 문자를 배열로 변환하고, 그 배열을 map으로 하나씩 풀어 `n`번씩 반복한다. 배열의 요소를 연결해 다시 문자열로 변환한다.

### 🐟 `스프레드 연산자 / Spread Operator`

- 스프레드 연산자를 이용하여 문자열을 배열로 변환할 수 있다. 문자열을 구성하는 문자들이 분리되어 요소로 배열에 추가된다.

```js
const apple = "apple";

const result = [...apple];
console.log(result); // output: (5) ["a", "p", "p", "l", "e"]
```

### 🐟 `Array.prototype.join()`

- join() 메서드는 배열의 모든 요소를 연결해 하나의 문자열로 만든다.

```js
let a = ["mango", "apple", "banana"];
let myResult1 = a.join(); // output: mango,apple,banana
let myResult2 = a.join(", "); // output: mango, apple, banana
let myResult3 = a.join(" + "); // output: mango + apple + banana
let myResult4 = a.join(""); // output: mangoapplebanana
```

### 🐟 `String.prototype.repeat()`

- repeat() 메서드는 문자열을 주어진 횟수만큼 반복해 붙인 새로운 문자열을 반환한다.

- `RangeError`
  - 반복 횟수는 양의 정수여야 함.
  - 반복 횟수는 무한대보다 작아야 하며, 최대 문자열 크기를 넘어선 안됨.

```js
"abc".repeat(-1); // RangeError
"abc".repeat(0); // ''
"abc".repeat(1); // 'abc'
"abc".repeat(2); // 'abcabc'
"abc".repeat(3.5); // 'abcabcabc' (count will be converted to integer)
"abc".repeat(1 / 0); // RangeError

({ toString: () => "abc", repeat: String.prototype.repeat }.repeat(2));
// 'abcabc' (repeat() is a generic method)
```
