---
title: "[Algorithm] 중앙값 구하기"
categories:
  - Algorithms
tags:
  - [Algorithms, JavaScript, sort, Math.floor, length]
permalink: /Blog/algorithm-08/
toc: true
toc_sticky: true
toc_label: # "ALGORITHM"
date: 2023-04-04
last_modified_at: 2023-04-04
---

## Algorithm 풀기

### 문제 설명

중앙값은 어떤 주어진 값들을 크기의 순서대로 정렬했을 때 가장 중앙에 위치하는 값을 의미합니다.
예를 들어 1, 2, 7, 10, 11의 중앙값은 7입니다.
정수 배열 array가 매개변수로 주어질 때, 중앙값을 return 하도록 solution 함수를 완성해보세요.

### 제한사항

- array의 길이는 홀수입니다.
- 0 < array의 길이 < 100
- -1,000 < array의 원소 < 1,000

### 입출력 예

| array             | result |
| ----------------- | ------ |
| [1, 2, 7, 10, 11] | 7      |
| [9, -1, 0]        | 0      |

### 입출력 예 설명

- 입출력 예 #1

  - 본문과 동일합니다.

- 입출력 예 #2

  - 9, -1, 0을 오름차순 정렬하면 -1, 0, 9이고 가장 중앙에 위치하는 값은 0입니다.

### 나의 풀이 방법

```js
function solution(array) {
  const asc_array = array.sort((a, b) => a - b);
  const answer = Math.floor(array.length / 2);
  return asc_array[answer];
}
```

> 배열의 길이가 홀수인 경우 해당 배열을 2로 나눈 후 소수점 값에서 정숫값을 얻는다. 주어진 값들을 크기의 순서대로 정렬해야 하므로 `sort()`함수를 사용할 수 있다. 마지막으로 오름차순 된 새로운 배열 중 중간 index 값을 반환한다.
