---
title: "[Algorithm] 피자 나눠 먹기"
categories:
  - Algorithms
tags:
  - [Algorithms, JavaScript]
permalink: /Blog/algorithm-01/
toc: true
toc_sticky: true
toc_label: # "ALGORITHM"
date: 2023-03-14
last_modified_at: 2023-03-14
---

## Algorithm 풀기

### 문제 설명

머쓱이네 피자가게는 피자를 일곱 조각으로 잘라 줍니다.
피자를 나눠먹을 사람의 수 n이 주어질 때,
모든 사람이 피자를 한 조각 이상 먹기 위해 필요한 피자의 수를 return 하는 solution 함수를 완성해보세요.

### 제한사항

- 1 ≤ n ≤ 100

### 입출력 예

| n   | result |
| --- | ------ |
| 7   | 1      |
| 1   | 1      |
| 15  | 3      |

### 입출력 예 설명

- 입출력 예 #1
  - 7명이 최소 한 조각씩 먹기 위해서 최소 1판이 필요합니다.
- 입출력 예 #2
  - 1명은 최소 한 조각을 먹기 위해 1판이 필요합니다.
- 입출력 예 #3
  - 15명이 최소 한 조각씩 먹기 위해서 최소 3판이 필요합니다.

### 나의 풀이 방법

```js
function solution(n) {
  let answer = n / 7;
  return Math.ceil(answer);
}
```
**Math.ceil() 함수**:
입력받은 숫자보다 크거나 같은 정수 중 가장 작은 정수를 리턴한다.
즉, 입력받은 숫자를 올림한 정수를 리턴하는 함수

아래와 같이 화살표 함수를 이용해 더 간단하게 작성할 수 있다.
```js
const solution = (n) => Math.ceil(n / 7)
```
