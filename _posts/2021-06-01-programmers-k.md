---
layout: single
title: "[프로그래머스] K번째 수 (JavaScript)"
categories:
  - algorithm-problems
---

![image](/assets/img/Algorithm_Data_Structure.png)

# 문제

[프로그래머스 Level1 K번째 수](https://programmers.co.kr/learn/courses/30/lessons/42748)

commands 배열은 \[i, j, k\] 형태의 원소를 가지는 2차원 배열이다. 1차원 배열 array에 대해 commands의 모든 각각의 원소에 대해 다음 연산을 적용한다.

1.  array의 i번째부터 j번째까지 자른다.
2.  1에서 나온 배열을 정렬한다.
3.  2에서 나온 (정렬된) 배열에서 k번째 숫자를 찾는다.

commands의 모든 원소마다 계산된 3에서 나온 숫자를 배열에 담아 return하도록 코드를 작성하는 문제이다.

# 풀이과정 및 어려웠던 점

commands 배열을 순회하도록 반복문을 사용하고 slice 함수를 이용해 1(array를 자르는 과정)을 수행한다. 이를 slicing이라는 미리 정의된 변수에 담은 후 정렬하고 k번째 수를 찾아 answer 배열에 넣는다. (slicing 배열도 사용 후엔 초기화해서 반복마다 다시 사용한다.) 이 과정을 commands 배열의 길이만큼 반복한다.

초기 코드는 제출 때는 통과를 못했는데 배열을 정렬하는 코드를 `slicing.sort()` 이렇게 작성했기 때문이다. JavaScript에서 `sort()`를 사용해 숫자를 오름차순으로 정렬하고 싶을 때는 `sort(a,b => {return a-b;})`처럼 작성해야한다. 안그럼 아스키 문자 순서로 정렬되어 원하는 결과를 얻을 수 없다.(\[100, 1, 4, 13,10\] 을 sort()로 정렬하면 \[1, 10, 100, 13,4\] 이런 순으로 정렬된다. 우리가 원하는 것은 숫자의 크기순으로 정렬되는 것!)

# 코드

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

# 다른 풀이

# References
