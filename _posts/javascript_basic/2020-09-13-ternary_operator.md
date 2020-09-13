---
title: "[Javascript] Javascript 기초 문법 스터디 (10) - 삼항 연산자"
excerpt: "자바스크립트 기초 문법 스터디 - 삼항 연산자편"
toc: true
toc_sticky: true

categories:
  - Javascript
tags:
  - Javascript
---

## Javascript 기초 문법 (10)

### 삼항 연산자

- 삼항연산자 구문
  - 조건 ? true일때 : false일때

삼항연산자 사용 예제

```javascript
const array = [];

let text =
  array.length === 0 ? "배열이 비어있습니다" : "배열이 비어있지 않습니다";
console.log(text); // 배열이 비어있습니다
```

**참고자료**

- [벨로퍼트와 함께하는 모던 자바스크립트 패스트캠퍼스 온라인 강의](https://www.fastcampus.co.kr/dev_online_react)
- 모던 자바스크립트 입문 책
