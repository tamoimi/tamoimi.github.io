---
title: "[Algorithm] 배열의 교집합 찾기"
categories:
  - Algorithms
tags:
  - [Algorithms, JavaScript, filter, includes, length]
permalink: /Blog/algorithm-07/
toc: true
toc_sticky: true
toc_label: # "ALGORITHM"
date: 2023-04-03
last_modified_at: 2023-04-03
---

## Algorithm 풀기

### 문제 설명

두 배열이 얼마나 유사한지 확인해보려고 합니다. 문자열 배열 s1과 s2가 주어질 때 같은 원소의 개수를 return하도록 solution 함수를 완성해주세요.

### 제한사항

- 1 ≤ s1, s2의 길이 ≤ 100
- 1 ≤ s1, s2의 원소의 길이 ≤ 10
- s1과 s2의 원소는 알파벳 소문자로만 이루어져 있습니다.
- s1과 s2는 각각 중복된 원소를 갖지 않습니다.

### 입출력 예

| s1              | s2                          | result |
| --------------- | --------------------------- | ------ |
| ["a", "b", "c"] | ["com", "b", "d", "p", "c"] | 2      |
| ["n", "omg"]    | ["m", "dot"]                | 0      |

### 입출력 예 설명

- 입출력 예 #1

  - "b"와 "c"가 같으므로 2를 return합니다.

- 입출력 예 #2

  - 같은 원소가 없으므로 0을 return합니다.

### 나의 풀이 방법

```js
function solution(s1, s2) {
  var answer = s1.filter((i) => s2.includes(i));
  return answer.length;
}
```

> 두 배열의 교집합을 찾는 함수를 작성했다. `filter()`와 `includes()`를 사용하여 배열의 내용을 특정 조건에 따라 걸러주고 배열에서 특정 값을 포함하고 있는 체크한 다음 교집합의 길이를 리턴한다. <br/> > **s1의 요소를 s2에 포함되는지 비교 해서 true인것만 리턴**

### 🐟 `Array.prototype.includes()`

- includes() 메서드는 배열이 특정 요소를 포함하고 있는지 판별합니다.

```js
const array1 = [1, 2, 3];

console.log(array1.includes(2));
//output: true

const pets = ["cat", "dog", "bat"];

console.log(pets.includes("cat"));
//output: true

console.log(pets.includes("at"));
//output: false
```
