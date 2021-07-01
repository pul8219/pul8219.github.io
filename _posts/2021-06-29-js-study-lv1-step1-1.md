---
layout: single
title: "[js-study-lv1] 1주차: Todo List 만들기"
categories:
  - javascript
---

# [DKU-STUDY] 1주차: Todo List 만들기

[DKU-STUDY/js-study-lv1](https://github.com/DKU-STUDY/js-study-lv1) 레포지토리의 `step1` 폴더 참고

# 📣 요구사항 체크리스트

- [x] 아이템 추가
  - [x] 아이템 추가 `input`에 텍스트를 입력 후 `Enter`를 누르거나 `생성 버튼`을 클릭하여 아이템을 추가할 수 있다.
  - [x] 입력한 내용이 없을 때 아이템 추가를 시도할 경우 `아이템 이름을 입력해주세요` 라고 경고창을 띄워야 한다.
- [x] 아이템이 추가 성공 시 TodoList에 반영된다.
- [x] 아이템 수정
  - [x] 아이템 내용 옆에 `수정` 버튼이 존재한다.
  - [x] `수정` 버튼을 클릭할 경우 아이템의 내용이 포함된 `input`으로 `DOM`이 변경된다.
  - [x] 수정 `input`에 내용을 입력 후 `Enter`를 누르거나 `완료 버튼`을 클릭하면 아이템의 내용이 수정된다.
  - [x] 수정 `input`에서 `esc`를 누르거나 `취소 버튼`을 클릭할 경우 수정이 취소된다.
- [x] 아이템 삭제
  - [x] 아이템 내용 옆에 `삭제` 버튼이 존재한다.
  - [x] `삭제` 버튼을 클릭할 경우 아이템이 삭제된다.
- [x] Todo 아이템 Toggle
  - [x] 아이템 내용 왼쪽에 체크박스가 존재한다.
  - [x] 체크박스를 클릭할 경우 아이템의 색상이 파란색으로 변경된다.

# 코드 설명

[1주차: Todo List 만들기 pr](https://github.com/DKU-STUDY/js-study-lv1/pull/9)

- 투두리스트의 내용이 담긴 데이터(상태)를 일관성 있게 관리하기 위해 컴포넌트로 구현
- 구현에 다음 문서를 참고 [Vanilla Javascript로 웹 컴포넌트 만들기](https://junilhwang.github.io/TIL/Javascript/Design/Vanilla-JS-Component) (투두리스트 리팩토링과 컴포넌트 구현에 도움됨)

```plaintext
│  index.html
│  README.md
│
└─src
        Component.js
        main.js
        TodoApp.js
        TodoAppender.js
        TodoList.js
```

- 투두리스트 데이터(`$state`)를 관리하는 역할은 `TodoApp.js`라는 컴포넌트가 담당
- `TodoApp.js`의 하위 구조로 `TodoList.js`, `TodoAppender.js` 컴포넌트가 있고 컴포넌트들이 상속하고 있는 `Component.js`는 구현의 코어이며 모든 컴포넌트들의 틀임. (재사용성 증대)
- `render()`이후에 실행되는 `mounted()`를 통해 `TodoApp.js`과 같은 컴포넌트(부모 컴포넌트)가 `TodoItem.js`, `TodoAppender.js` 컴포넌트(자식 컴포넌트)에게 상태나 메소드를 전달할 수 있게 작성함.
- 투두리스트의 데이터를 변경할 때는 꼭 `setState()` 메소드를 사용하도록 구현함.
- `main.js`는 컴포넌트 구조 없이 처음에 작성했던 코드로 실행되지 않음(참고용으로 업로드만)

- 기존 코드에서 추가된 내용
  - 투두리스트 입력 form을 `<div class="todo-appender"></div>` 코드로 감쌈.
  - 투두리스트 기본 구조에서 `완료`버튼을 checkbox로 대체하고 삭제.

# 회고

이전에 공부했던 준일님의 Vanilla JS로 웹 컴포넌트 만들기 문서를 활용해 컴포넌트로 투두리스트를 구현했다.
DOM만 제어할 때보다 확실히 데이터 관리가 쉬워졌고 데이터 변경시에도 setState를 통해 여러곳에서 데이터를 중구난방으로 변경하지 않도록 했기 때문에 좋아진 것 같다. setEvent 내부 코드가 좀 지저분한데 이를 고치고 싶다. 더불어 너무 긴 함수를 쪼개고, 반복적인 유틸 작업을 따로 빼는 것 등 좀 더 개선해나가고싶다.

# 고민, 보완할 점

- `<script type="module" src="./src/main.js" defer></script>`와 같이 `defer`를 써서 스크립트를 로드하는 부분이 `<head>`에 있는 것과 `<body>` 맨끝에 있는 것의 차이점은?(defer는 HTML를 파싱하면서 js파일을 fetching 하다가 HTML이 모두 파싱되고 페이지가 준비되면 js 파일을 실행하는 방식)
  - 별로 차이 없음
  - 만약 `<body>` 하단에 작성한다면 그건 브라우저 폴리필(구형 브라우저에서도 지원하기 위함)하기 위해서임.
  - `type="module"`을 작성하면 `defer`를 쓰지 않았더라도 내부적으로 `defer`방식으로 스크립트가 로드된다.
- `TodoList.js` 파일의 `setEvent()` 코드에서 `수정`, `삭제`같은 버튼들의 DOM요소를 선택하고 이벤트를 등록하는 과정이 효율적으로 작성되었는지 잘 모르겠음. 이벤트 등록 과정을 메소드를 추가해 일반화 시키고, 렌더링 과정도 효율적으로 보완 필요.
- 투두리스트 아이템에 고유한 id를 부여하는 util함수 추가 필요
- render가 실행될 때 TodoApp 컴포넌트의 mounted가 실행되는 경우가 많은데 이때마다 하위 컴포넌트들의 setEvent()에 정의된 이벤트들이 자주 등록되는 것 같음. render와 분리시켰지만 이벤트 등록을 반복하는 똑같은 현상을 가지게 된건가?
