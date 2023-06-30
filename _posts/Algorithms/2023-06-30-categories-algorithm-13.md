---
title: "[Algorithm] 수 조작하기 1"
categories:
  - Algorithms
tags:
  - [Algorithms, JavaScript, switch, toUpperCase, toLowerCase]
permalink: /Blog/algorithm-13/
toc: true
toc_sticky: true
toc_label: # "ALGORITHM"
date: 2023-06-30
last_modified_at: 2023-06-30
---

## Algorithm 풀기

### 문제 설명

정수 n과 문자열 control이 주어집니다. control은 "w", "a", "s", "d"의 4개의 문자로 이루어져 있으며, control의 앞에서부터 순서대로 문자에 따라 n의 값을 바꿉니다.

- "w" : n이 1 커집니다.
- "s" : n이 1 작아집니다.
- "d" : n이 10 커집니다.
- "a" : n이 10 작아집니다.

위 규칙에 따라 n을 바꿨을 때 가장 마지막에 나오는 n의 값을 return 하는 solution 함수를 완성해 주세요.

### 제한사항

- -100,000 ≤ n ≤ 100,000
- 1 ≤ control의 길이 ≤ 100,000
  - control은 알파벳 소문자 "w", "a", "s", "d"로 이루어진 문자열입니다.

### 입출력 예

| n   | control       | result |
| --- | ------------- | ------ |
| 0   | "wsdawsdassw" | -1     |

### 나의 풀이 방법

```js
function solution(n, control) {
  const newControl = [...control];
  return newControl.reduce((acc, cur) => {
    switch (cur) {
      case "w":
        return acc + 1;
      case "s":
        return acc - 1;
      case "d":
        return acc + 10;
      case "a":
        return acc - 10;
      default:
        return acc;
    }
  }, n);
}
```

> `control`의 문자열을 배열로 변환 했다. 
  - `"wsdawsdassw"` => `["w","s","d","a","w","s","d","a","s","s","w"]`
  그리고 `reduce()`를 사용해 `arr`의 합을 구했다.
   - acc : 이전 함수 호출의 결과
   - n : 초깃값 (optional)
   - newControl : 배열 
  - 함수 최초 호출 시, reduce의 마지막 인수인 `n(0) 초깃값`이 `acc`에 할당된다. `cur`엔 배열의 첫 번째 요소인 `"w" = +1`이 할당된다. 따라서 함수의 결과는 `1`이 된다. (+ 반복)

