---
layout: single
title: "[js-study-lv1] 2주차: TodoList 리팩토링 + 번들링"
categories:
  - javascript
---

[DKU-STUDY] 2주차: TodoList 리팩토링 + 번들링

- [DKU-STUDY/js-study-lv1](https://github.com/DKU-STUDY/js-study-lv1) 레포지토리의 `step2` 폴더 참고

# 📋 공부한 내용 링크

- [ECMAScript, ES6](https://pul8219.github.io/javascript/js-ecmascript/)
- [Babel 시작하기](https://pul8219.github.io/javascript/js-babel-concept/)
- [Webpack 시작하기](https://pul8219.github.io/javascript/js-webpack-concept/)
- [JS 모듈의 역사와 문법(CommonJS, AMD, ESM 등)](https://pul8219.github.io/javascript/js-module/)
- [브라우저 모듈과 ESM](https://pul8219.github.io/javascript/js-browser-module/)

# 📣 요구사항 체크리스트

- [ ] 리팩토링
  - [ ] ECMAScript에 대한 조사
    - [x] ECMAScript, Javascript 용어 정리
    - [ ] ES5 vs ES6 차이점 정리
  - [ ] 파일을 기능 단위로 분리해본다.
    - [ ] core: 어플리케이션의 베이스 코드
    - [ ] components: 컴포넌트 코드
    - [ ] utils: 유틸리티 성향의 코드
    - [ ] constants: 상수
    - [ ] app.js (entry point)
  - [ ] 다음과 같은 규칙을 지켜가며 코딩한다.
    - [ ] 한 메소드(함수)에 indent(tab)는 최대 2depth로 유지하기
    - [ ] else 예약어(keyword)를 쓰지 않는다.
    - [ ] 상수를 적극적으로 사용한다.
    - [ ] 한 줄에 점을 하나만 찍는다.
    - [ ] 줄여쓰지 않는다 (축약 금지)
- [ ] 번들러 조사 및 적용
  - [ ] 번들러에 대해 알아보기
    - [ ] javascript 번들링
    - [ ] 번들링을 하는 이유, 필요한 이유
    - [ ] 번들러로 할 수 있는 일들
  - [ ] 번들러 종류 알아보기
    - [ ] parcel
    - [x] webpack
    - [ ] rollup
    - [ ] vite
  - [x] 모듈 시스템에 대해 알아보기
    - [x] CommonJS
    - [x] AMD
    - [x] RequireJS
    - [x] ESM
  - [x] 브라우저 모듈에 대해 알아보기
  - [x] 번들러 적용
    - [x] 번들러 설치를 위해 nodejs + npm 설치
    - [x] Parcel, Webpack, Rollup, Vite 중 택 1

# 코드 설명

[2주차: TodoList 리팩토링 + 번들링 PR](https://github.com/DKU-STUDY/js-study-lv1/pull/16)

# 회고

# 고민, 보완할 점

Q. 브라우저 모듈 = ESM 인것인지?

- ESM !== 브라우저모듈 이고, 브라우저 모듈로 ESM의 스펙을 사용하는 거라고 보면 된다. 둘은 다른 점이 많고 완전히 같은 개념이 아니다.
