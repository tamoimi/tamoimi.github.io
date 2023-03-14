---
title: "[JavaScript] 배열 오름차순, 내림차순 정렬 sort()"
excerpt: "JavaScript sort() function"

categories:
  - JavaScript
tags:
  - [HTML, JavaScript, sort, array]

permalink: /Blog/sort/

toc: true
toc_sticky: true

date: 2023-03-13
last_modified_at: 2023-03-13
---
## arr.sort()

arr.sort()는 배열의 요소를 정렬하며 배열 자체가 변경된다.

```js
let arr = [1, 2, 15];

arr.sort();

alert( arr );

//output: 1, 15, 2
```

하지만 재정렬 후 배열 요소가 `1, 2, 15`가 아니라 `1, 15, 2`가 되었다. 

**요소는 문자열로 취급되어 재 정렬되기 때문이다.**  
  모든 요소는 문자형으로 변환된 이후에 재 정렬된다. 
문자열 비교는 사전편집 순으로 진행되기 때문에 2는 15보다 큰 값으로 취급된다.

원하는대로 정렬을 하고 싶다면, 값을 비교해줄 수 있는 함수를 넣어야 한다.

## arr.sort()로 숫자 오름차순 정렬하기

**오름차순으로 정렬**
```js
let arr = [1, 2, 15];

arr.sort(function(a, b) { return a - b });

alert(arr); 

//output: 1, 2, 15
```
>**여기서 화살표 함수를 사용하면 정렬 함수를 더 깔끔하게 만들 수 있다.**
```js
arr.sort((a, b) => a - b) 
```

## arr.sort()로 숫자 내림차순 정렬하기  

```js
arr.sort((a, b) => b - a) 
```

