---
layout: single
title: "코드스피츠 CSS Rendering 4회차 정리(2) (STEP 44)"
categories:
  - frontend-study
---

JS로 3D 드럼통 그리기

> **STEP 44**
>
> - 작성자: Wol-dan (@pul8219)
> - 스터디 주제: FrontEnd 면접 스터디 <https://gitlab.com/siots-study/topics/-/wikis/%EC%8B%AC%ED%99%941>
> - 공부 범위: STEP 43 [코드스피츠76 CSS Rendering - 4회차](https://www.youtube.com/watch?v=Tf5KvpYNNv8c) `2/3`
> - 기한: 07/03(토) ~ 07/06(화) (STEP 44)
> - [📋 스터디 문서 목록 바로가기](https://github.com/pul8219/TIL/blob/master/Documents/FrontEnd-Study/README.md)

# 드럼통 그리기

CSS로 회전하는 드럼통을 그려보자. 트럼통은 수많은 직사각형으로 이루어진 옆면과 원형인 상하판으로 만들어야한다.

## 방법1. JS Mix

<img src="https://images.velog.io/images/pul8219/post/aaab4f7c-c637-41f5-b26a-cc42211e126e/ezgif.com-gif-maker.gif" width="40%">

먼저 자바스크립트로 드럼통을 만들어보자.

![](https://images.velog.io/images/pul8219/post/d1744b53-1641-4fd1-be4b-c93a695e5c54/image.png)

드럼통은 위와 같은 이미지 한개를 이용해 CSS split으로 잘라서 사용할 것이다.(여러개의 이미지를 로드하지 않아도 된다는 장점이 있다.)

> `3D` 용어
>
> - 아틀라스: `3D`에서는 이미지 소스를 `텍스쳐`라고 하는데, 하나의 텍스쳐가 여러가지 텍스쳐(드럼통 예에선 옆면, 뚜껑 등)를 대신하는 경우 `3D`에선 그 텍스쳐를 `아틀라스`라고 부른다.(CSS에선 split) 정육면체는 6개의 사각형 면(face)을 잘 합치면 정육면체가 된다. 이런 것처럼 face에 필요한 데이터를 아틀라스로 공급받아서 이를 잘 변형하면 하나의 드럼통, 사람, 정육면체를 만들 수 있다.
> - 매쉬(Mesh): 이렇게 면(face)이 모인 것은 하나의 입체가 되고 이를 매쉬라고 부른다.

![](https://images.velog.io/images/pul8219/post/ac9b7f14-cd1b-45e6-81d6-fa2850f801a9/image.png)

- 면(face)들을 나누기 위해서는 `x, y, z`, `height, width`값이 필요하다.
- 아틀라스 안에서의 영역을 인식하기 위해 `tx, ty`값이 필요하다.
- 회전하기 위해서 `rx, ry, rz` 값이 필요하다.

```html
<style>
  @keyframes spin {
    to {
      transform: rotateY(360deg) rotateZ(360deg) rotateX(720deg);
    }
  }
  html,
  body {
    height: 100%;
  }
  body {
    perspective: 600px;
    background: #404040;
  }
  .ani {
    animation: spin 4s linear infinite;
  }
  .drum {
    background: url("http://keithclark.co.uk/labs/css-fps/drum2.png");
  }
</style>
```

```js
// div를 만들어주는 El 클래스
const El = class {
  constructor() {
    this.el = document.createElement("div");
  }
  set class(v) {
    this.el.className = v;
  }
};

// El을 상속받는 Face 클래스
const Face = class extends El {
  constructor(w, h, x, y, z, rx, ry, rz, tx, ty) {
    super();
    this.el.style.cssText = `
      position: absolute;
      width: ${w}px;
      height: ${h}px;
      margin: -${h / 2}px 0 0 -${w / 2}px;
      transform: translate3d(${x}px, ${y}px, ${z}px)
        rotateX(${rx}rad) rotateY(${ry}rad) rotateZ(${rz}rad);
      background-position: -${tx}px ${ty}px;
      backface-visibility: hidden; //⭐
    `;
  }
};
```

![](https://images.velog.io/images/pul8219/post/2dd98101-5283-4d4b-84c4-14c80ae24d02/image.png)

- 그림이 생기면 이렇게 좌상단 점이 기준이 된다. 그림을 옮겨 정중앙점을 기준으로 하도록 margin에 코드처럼 값을 준다.

> 중앙 정렬
>
> - 요소가 absolute가 아닐 때, margin의 left, right에 auto를 주면 된다.
> - 요소가 absolute일 때, margin의 top에 height의 `1/2`을 배고, left에 width의 `1/2`을 뺀다.

> margin은 top, right, bottom, left순 (반시계 방향)

```js
// Face를 모아 하나의 Mesh(드럼통)를 만드는 클래스
const Mesh = class extends El {
  constructor(l, t) {
    super();
    this.el.style.cssText = `
      position: absolute;
      left: ${l}; top: ${t};
      transform-style: preserve-3d;
    `;
  }

  add(face) {
    if (!(face instanceof Face)) throw "invalid face";
    this.el.appendChild(face.el);
    return face;
  }
};
```

- Mesh도 div로 여러 div들을 가두는 역할을 한다. (그래서 El을 상속받았다.)
- 자식들도 자신과 같은 속성을 이어받을 수 있도록 `transform-style: preserve-3d`로 설정한다. ([STEP 43](https://pul8219.github.io/frontend-study/fe-study-step43/#transform-style) 참고)
- Mesh가 위치할 값을 `left`, `top`로 준다.
- `add`메소드: 나의 div에 Face element(자식)을 추가

```js
// 본격적으로 드럼통을 만들어보자
const mesh = new Mesh("50%", "50%");

const r = 100,
  height = 196,
  sides = 20;
const sideAngle = (Math.PI / sides) * 2;
const sideLen = r * Math.tan(Math.PI / sides);

for (let c = 0; c < sides; c++) {
  const x = (Math.sin(sideAngle * c) * r) / 2;
  const z = (Math.cos(sideAngle * c) * r) / 2;
  const ry = Math.atan2(x, z);
  const face = new Face(sideLen + 1, height, x, 0, z, 0, ry, 0, sideLen * c, 0);
  face.class = "drum";
  mesh.add(face);
}

const tface = new Face(100, 100, 0, -98, 0, Math.PI / 2, 0, 0, 0, 100);
const bface = new Face(100, 100, 0, 98, 0, -Math.PI / 2, 0, 0, 0, 100);
tface.class = "drum";
bface.class = "drum";
mesh.add(tface);
mesh.add(bface);
mesh.class = "ani";
document.body.appendChild(mesh.el);
```

- `r(반지름)`, `height(원통의 높이)`
- `sides`: 옆면을 얼마나 등분할 건지에 대한 변수이다. 여기선 20등분 했다는 것
- `sideAnle`: 각 side에서 원의 중심점을 향하게 했`을 때 각도이다. (라디안 기준에서 PI는 180도이기 때문에 360도로 만들기 위해 2를 곱해줬다.)
- `sideLen`: 나뉜 면이 원에서 차지하는 길이 (여기서 `tan`을 사용하지 않고 `sin`을 사용하면 나누는 면 개수가 적으면 사이 공간이 빌 수 있다)

- `for문`: for문을 돌면서 side가 20개면 20개의 Face를 만들어야한다.

  - `x, z` 를 주는 이유는 누워있는 원을 x,y,z로 이루어진 평면의 x,z에 그려야하기 때문이다.
  - 원주에 닿는 접점을 그리기 위해 `sin`, `cos`을 사용한다.(원에서 원주에 특정 각도에 위치한 점을 구하려면, 라디안값을 알고 있을 때 sin,cos를 이용해 x,z를 구할 수 있다.)
  - x,z로 `arc tan`을 이용하면 빗면들을 얼마만큼 휘게 할지 정할 수 있다. (즉 몇도를 돌려야 하는지 알 수 있다.)
  - `ry`는 y축을 기준으로 회전하며 옆면을 구성하기 때문에 정의한 것이다.
  - `new Face` 라인: `sideLen+1` 틈 벌어지지 말라고 1을 더해줬다. / x,z 원주에서의 위치 / 각도는 ry만 회전시키면 되니까 이렇게 설정 / `sideLen*c` 해당 face가 몇번째 위치인지 알 수 있게 준 값
  - `face.class = 'drum';`: 이미지를 가리키도록 한다.
  - Mesh에 지금 만든 Face를 추가한다.

**`backface-visibility` 적용**

- Face에 `backface-visibility: hidden`을 주고(⭐표시 코드라인 참고하기) 위아래 뚜껑을 주석으로 잠깐 없애보자.
- 뒷면이 보일 때마다 투명해지는 것을 볼 수 있다. 뚜껑을 다시 씌우면 잘 작동되는 것을 볼 수 있다.
- 이렇게 안 보이는 곳을 그리지 않게 `hidden`시킴으로써 자원을 절약할 수 있다. ([STEP 43](https://pul8219.github.io/frontend-study/fe-study-step43/#transform-style) 참고)

방법2는 다음 포스팅에 계속

# Comment

# References

# 팀원들 결과물‍
