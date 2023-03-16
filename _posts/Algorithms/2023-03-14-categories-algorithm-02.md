---
title: "[Algorithm] 배열 두 배 만들기"
categories:
  - Algorithms
tags:
  - [Algorithms, JavaScript]
permalink: /Blog/algorithm-02/
toc: true
toc_sticky: true
toc_label: # "GITHUB BLOG START"
date: 2023-03-14
last_modified_at: 2023-03-14
---

## Algorithm 풀기

### 문제 설명

정수 배열 numbers가 매개변수로 주어집니다.
numbers의 각 원소에 두배한 원소를 가진 배열을 return하도록 solution 함수를 완성해주세요.

### 제한사항

- -10,000 ≤ numbers의 원소 ≤ 10,000
- 1 ≤ numbers의 길이 ≤ 1,000

### 입출력 예

| numbers                   | result                     |
| ------------------------- | -------------------------- |
| [1, 2, 3, 4, 5]           | [2, 4, 6, 8, 10]           |
| [1, 2, 100, -99, 1, 2, 3] | [2, 4, 200, -198, 2, 4, 6] |

### 입출력 예 설명

- 입출력 예 #1
  - [1, 2, 3, 4, 5]의 각 원소에 두배를 한 배열 [2, 4, 6, 8, 10]을 return합니다.
- 입출력 예 #2
  - [1, 2, 100, -99, 1, 2, 3]의 각 원소에 두배를 한 배열 [2, 4, 200, -198, 2, 4, 6]을 return합니다.

### 나의 풀이 방법

```js
function solution(numbers) {
  let answer = numbers.map((n) => n * 2);
  return answer;
}
```
>`map()` 메서드는 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환한다.


numbers는 정수 배열로 받고 있기 때문에 map으로 각 정수를 풀어서 `n`이라는 각 값에 곱하기 2를 하고 새로운 배열을 반환했다.

