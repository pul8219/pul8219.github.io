---
layout: single
title: "[Leetcode] Merge Two Sorted Lists (JavaScript)"
categories:
  - algorithm-problems
---

알고리즘 문제풀이 [Leetcode] 21. Merge Two Sorted Lists (JavaScript)

![image](/assets/img/Algorithm_Data_Structure.png)

# 문제 설명

- 문제 분류: `?`
- 문제 출처: [LeetCode - 21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
- 라벨: `Easy`, `JavaScript`

> Merge two sorted linked lists and return it as a sorted list. The list should be made by splicing together the nodes of the first two lists.
>
> **Example**
>
> ```
> Input: l1 = [1,2,4], l2 = [1,3,4]
> Output: [1,1,2,3,4,4]
> ```

# 풀이과정 및 어려웠던 점

- 입력값으로 들어오는 인자도 `ListNode`로 이루어진 연결리스트이며 이미 정렬되어있다.
- 내부적으로 `ListNode`가 선언되어있다. 반환값도 마찬가지로 `ListNode`로 구성된 연결리스트로 반환해야한다.
- 반복문을 돌며 l1, l2에 대한 포인터 값을 바꿔가면서 list에 노드를 담도록 구현했다.

# 코드

## 풀이1

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var mergeTwoLists = function (l1, l2) {
  let list = new ListNode();
  let head = list;

  while (l1 !== null && l2 !== null) {
    // l1, l2 모두 null이 아닐 때까지 반복
    if (l1.val < l2.val) {
      list.next = new ListNode(l1.val);
      l1 = l1.next;
    } else {
      list.next = new ListNode(l2.val);
      l2 = l2.next;
    }
    list = list.next;
  }

  list.next = l1 || l2; // l1, l2 중에 값이 비교되지 않은 노드가 남아있을 수 있다. 따라서 현재 null을 가리키고 있는 리스트(모두 검사 완료)말고 다른 리스트의 노드를 이어주어야한다.

  return head.next;
};
```

## 풀이2

풀이1의 실행속도가 느린편이라 Leetcode Dicussion에서 다른 풀이를 찾아봤는데 재귀적인 방식으로 문제를 푼 코드가 있었다. 실행시켜보니까 풀이1보다 훨씬 빠르다. 코드는 이해했지만 처음부터 이렇게 짜보라고 하면 짤 수 있을까 싶다..ㅎ

```js
var mergeTwoLists = function (l1, l2) {
  // l1, l2중 하나가 null이라면 둘 중 null이 아닌 것을 반환. 물론 둘다 null일 경우는 null을 리턴할 것이다.
  if (!l1 || !l2) return l1 || l2;
  if (l1.val < l2.val) {
    l1.next = mergeTwoLists(l1.next, l2);
    return l1;
  }
  l2.next = mergeTwoLists(l1, l2.next);
  return l2;
};
```

# References
