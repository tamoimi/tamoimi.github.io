---
title: "[Algorithm] 자릿수 더하기"
categories:
  - Algorithms
tags:
  - [Algorithms, JavaScript, reduce, split]
permalink: /Blog/algorithm-10/
toc: true
toc_sticky: true
toc_label: # "ALGORITHM"
date: 2023-04-06
last_modified_at: 2023-04-06
---

## Algorithm 풀기

### 문제 설명

정수 n이 매개변수로 주어질 때 n의 각 자리 숫자의 합을 return하도록 solution 함수를 완성해주세요

### 제한사항

- my_string은 소문자와 공백으로 이루어져 있습니다.
- 1 ≤ my_string의 길이 ≤ 1,000

### 입출력 예

| n      | result |
| ------ | ------ |
| 1234   | 10     |
| 930211 | 16     |

### 입출력 예 설명

- 입출력 예 #1

  - 1 + 2 + 3 + 4 = 10을 return합니다.

- 입출력 예 #2

  - 9 + 3 + 0 + 2 + 1 + 1 = 16을 return합니다.

### 나의 풀이 방법

```js
function solution(n) {
  const answer = String(n)
    .split("")
    .reduce((a, b) => a + b * 1, 0);
  return answer;
}
```

> `n`값을 문자열로 변환 후 하나씩 자른 뒤 `reduce()`함수로 배열 합을 구할 수 있다. <br/>`reduce()`함수 뒤 \* 1을 붙여 다시 숫자로 변환 했다.

### 🐳 Array.prototype.reduce()

- reduce() 메서드는 배열의 각 요소에 대해 주어진 리듀서 (reducer) 함수를 실행하고, 하나의 결과값을 반환한다.

#### 덧셈 등의 사칙 연산

- `reduce()`를 사용해 arr합 구하기

```js
const arr = [1, 20, 45, 23];
const sum = arr.reduce(function (acc, curr, idx) {
  return acc + curr;
});
console.log(sum);
// output: 89
```

- 완전한 함수 대신 화살표 함수를 사용할 수 있다.

```js
// arr의 모든 요소의 합
let arr = [1, 20, 45, 23];
let sum = arr.reduce((acc, curr) => acc + curr, 0);

console.log(sum);
// output: 89
```

- 두번째 인자를 통해 초기값을 설정해 줄 수 있다.

```js
let arr = [1, 20, 45, 23];
let sum = arr.reduce((acc, curr) => acc + curr, 10);

console.log(sum);
// output: 99
```
