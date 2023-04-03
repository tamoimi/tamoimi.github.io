---
title: "[Algorithm] 머쓱이보다 키 큰 사람"
categories:
  - Algorithms
tags:
  - [Algorithms, JavaScript]
permalink: /Blog/algorithm-05/
toc: true
toc_sticky: true
toc_label: # "ALGORITHM"
date: 2023-03-17
last_modified_at: 2023-03-17
---

## Algorithm 풀기

### 문제 설명

머쓱이는 학교에서 키 순으로 줄을 설 때 몇 번째로 서야 하는지 궁금해졌습니다.
머쓱이네 반 친구들의 키가 담긴 정수 배열 array와 머쓱이의 키 height가 매개변수로 주어질 때,
머쓱이보다 키 큰 사람 수를 return 하도록 solution 함수를 완성해보세요.

### 제한사항

- 1 ≤ array의 길이 ≤ 100
- 1 ≤ height ≤ 200
- 1 ≤ array의 원소 ≤ 200

### 입출력 예

| array                | height | result |
| -------------------- | ------ | ------ |
| [149, 180, 192, 170] | 167    | 3      |
| [180, 120, 140]      | 190    | 0      |

### 입출력 예 설명

- 입출력 예 #1

  - 149, 180, 192, 170 중 머쓱이보다 키가 큰 사람은 180, 192, 170으로 세 명입니다.

- 입출력 예 #2
  - 180, 120, 140 중 190보다 큰 수는 없으므로 0명입니다.

### 나의 풀이 방법

```js
function solution(array, height) {
  let heights = array.filter((h) => h > height);
  return heights.length;
}
```

> 자바스크립트 filter 함수를 사용해서 배열 내 숫자가 height 보다 큰 경우 새로운 배열의 길이를 리턴한다

### `Array.prototype.filter()`

- filter() 메서드는 주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환한다.


```js
const words = [
  "spray",
  "limit",
  "elite",
  "exuberant",
  "destruction",
  "present",
];

const result = words.filter((word) => word.length > 6);

console.log(result);
// Expected output: Array ["exuberant", "destruction", "present"]
```
