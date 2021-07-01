---
layout: single
title: "[프로그래머스] K번째 수 (JavaScript)"
categories:
  - algorithm-problems
---

알고리즘 문제풀이 [Leetcode] 21. Merge Two Sorted Lists (JavaScript)

![image](/assets/img/Algorithm_Data_Structure.png)

```js
function solution(array, commands) {
    var answer = [];
     let slicing = [];
    commands.forEach(command => {
        slicing = array.slice(command[0]-1, command[1]); // array의 i ~ j번째까지 잘라 새로운 배열에 저장

        slicing.sort((a,b) => a-b); // 정렬

        answer.push(slicing[command[2]-1]);

        slicing = []; // slicing 배열 초기화
    });
    return answer;
```

# References
