---
title: "[Javascript] Javascript 기초 문법 스터디 (3) - 조건문"
excerpt: "자바스크립트 기초 문법 스터디"
toc: true
toc_sticky: true

categories:
  - Javascript
tags:
  - Javascript
---

## Javascript 기초 문법 (3)

### 조건문

- **if**
  - 특정 조건인 경우 해당하는 블록문을 수행
  - `let`과 `const`는 블록 범위가 다를 경우 이미 선언된 변수와 같은 이름으로 선언할 수 있음

```javascript
const a = 1;
if (a + 1 === 2) {
  console.log("a + 1 = 2 입니다.");
}
// => a + 1 = 2 입니다. 출력
```

a의 값을 2로 바꿀 경우

```javascript
const a = 2;
if (a + 1 === 2) {
  console.log("a + 1 = 2 입니다.");
}
// 아무것도 출력되지 않음
```

`const` 변수를 if문 블록 안에 동일한 이름으로 선언할 경우

```javascript
const a = 1;
if (a + 1 === 2) {
  const a = 2;
  console.log("if문 안의 a 값은 " + a);
}
console.log("if문 밖의 a 값은 " + a);
// if문 안의 a 값은 2
// if문 안의 a 값은 1
// => 각각 선언된 변수로 출력됨
```

`const`가 아닌 `var`로 선언할 경우

```javascript
var a = 1;
if (a + 1 === 2) {
  var a = 2;
  console.log("if문 안의 a 값은 " + a);
}
console.log("if문 밖의 a 값은 " + a);
// if문 안의 a 값은 2
// if문 안의 a 값은 2
```

의도와 다르게 출력되므로 `var`사용은 주의

- **if/else**

  - 특정 조건인 경우 if 블록문을 수행하고 그렇지 않을 경우 else 블록문을 수행

```javascript
const a = 10;
if (a > 15) {
  console.log("a가 15보다 큼");
} else {
  console.log("a가 15보다 크지 않음");
}
// a가 15보다 크지 않음
```

- **if/else if/else**
  - 여러 조건문에 따라 각각 다른 작업을 수행할 때 사용

```javascript
const a = 8;
if (a < 5) {
  console.log("a가 5보다 작음");
} else if (a < 10) {
  console.log("a가 10보다 작음");
} else {
  console.log("a는 10 이상의 수");
}
// a가 10보다 작음
```

- **switch-case**
  - 여러 조건의 분기를 더 간결하게 표현

```javascript
const device = "iphone";

switch (device) {
  case "iphone":
    console.log("아이폰");
    break;
  case "ipad":
    console.log("아이패드");
    break;
  case "galaxy note":
    console.log("갤럭시 노트!");
    break;
  default:
    console.log("잘 모르겠네요...");
}
```

- break 혹은 return문을 작성하지 않으면 다음 break문, return문, 최악의 경우 switch 블록의 끝까지 발견한 모든 문장을 실행함(fall through)
- default문의 경우 모든 case에 해당하지 않을 때 실행됨

**참고자료**

- [벨로퍼트와 함께하는 모던 자바스크립트 패스트캠퍼스 온라인 강의](https://www.fastcampus.co.kr/dev_online_react)
- 모던 자바스크립트 입문 책

```

```
