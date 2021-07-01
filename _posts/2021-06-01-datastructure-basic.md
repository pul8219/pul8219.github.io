---
layout: single
title: "[JS] 자료구조(Data Structure) 종류"
categories:
  - data-structure
---

자료구조의 개념, 공부방향, 종류

![image](/assets/img/Algorithm_Data_Structure.png)

# 자료구조(Data Structure)

데이터를 메모리에 효율적으로 배치하고 저장하고 관리하는 방법을 의미한다. 데이터 특성에 맞는 자료구조를 선택하는 일은 효율적인 알고리즘을 위해서 필수적인 일이다.

- 목적: 서비스나 어플리케이션에 필요한 데이터를 제공하고 효율적으로 검색(접근), 삽입, 삭제할 수 있으려면 해당 기능에 적합한 자료구조를 쓰는 것이 중요하다.
- 종류: 배열, 단일 연결리스트, 이중 연결리스트, 스택, 해시 테이블 등

# 자료구조 공부방향

- **Order** 자료 구조 안에 있는 데이터들의 순서가 보장되는지
- **Unique** 중복된 데이터가 들어갈 수 있는지
- **Search** 검색할 때 얼마나 효율적인지
- **Modification** 수정할 때 얼마나 효율적인지
- 시간이 없다면 구현방법, 사항을 일일이 공부하는 것 보다는, 해당 자료구조는 어떤 상황에 쓰는 것이 좋고 어떤 API 들이 있는지 위주로 공부하면 좋음.

# 자료구조의 종류

## 1. 선형 자료구조: 데이터가 선처럼 길게 나열된 자료구조

1. 랜덤 접근 가능: 모든 데이터에 O(1)로 접근 가능한 자료구조

- [배열(Array)]()
- [해시(Hash)]()
  - 해시함수에 키값을 넣어 주소값을 얻고 그 주소에 위치한 버킷에 저장된 데이터를 가져오는 방식
  - 항상 O(1)이 보장되는 것은 아니다.

2. 랜덤 접근 불가능: 모든 데이터에 O(1)로 접근이 보장되지 않는 자료구조

- [스택(Stack)]('./Stack_Queue.md')
- [큐(Queue)]('./Stack_Queue.md')
- [데크]()
- [연결 리스트(Linked List)]()

> 선형 자료구조 탐색법
>
> - 순차 탐색
> - 이분 탐색

## 2. 비선형 자료구조: 선형 자료구조가 아닌 모든 자료구조

- [그래프(Graph)]()

> 그래프 순회 알고리즘
>
> - 깊이 우선 탐색(DFS)
> - 너비 우선 탐색(BFS)

- [트리(Tree)]()

> 트리 순회 알고리즘
>
> - 전위 순회
> - 중위 순회
> - 레벨 순서 순회

[이진 검색 트리(Binary Search Tree)]()

## 그 외

- [문자열]()

## 기타

- [Map & Set]()

# References

- [드림코딩 엘리님의 영상](https://www.youtube.com/watch?v=okHGRlgR8ps&feature=youtu.be)
- [javascript datastructure](https://velog.io/@yujo/JS%ED%80%B5-%EC%A0%95%EB%A0%ACQuick-Sort)
- [신입 개발자 전공 지식 & 기술 면접 백과사전](https://github.com/gyoogle/tech-interview-for-developer)
