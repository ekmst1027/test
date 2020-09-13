---
title: "[Javascript] Javascript 기초 문법 스터디 (8) - 배열 내장함수"
excerpt: "자바스크립트 기초 문법 스터디 - 배열 내장함수편"
toc: true
toc_sticky: true

categories:
  - Javascript
tags:
  - Javascript
---

## Javascript 기초 문법 (8)

### 배열 내장함수

#### forEach

- 배열 안의 원소들을 가지고 어떤 작업을 일괄적으로 할 때 사용
- `for`문을 대체할 수 있음
- `forEach` 함수의 파라미터로 각 원소에 대하여 처리하고 싶은 코드를 함수로 넣어줌
- 함수형태의 파라미터를 전달하는 것을 콜백함수라고 함
- 함수를 등록해주면, forEach가 실행을 하는 개념

forEach 사용 예제

```javascript
const superheros = ["아이언맨", "캡틴 아메리카", "토르", "닥터 스트레인지"];

superheros.forEach((hero) => console.log(hero)); // ["아이언맨", "캡틴 아메리카", "토르", "닥터 스트레인지"]
```

#### map

- 배열 안의 각 원소를 변환할 때 사용
- 리턴값으로 새로운 배열이 만들어짐

map 사용 예제

```javascript
const array = [1, 2, 3, 4, 5, 6, 7, 8];

const squared = array.map((n) => n * n);
console.log(squared); // [1, 4, 9, 16, 25, 36, 49, 64]
```

#### filter

- 배열에서 특정 조건을 만족하는 값들만 따로 추출하여 새로운 배열을 만듦
- 리턴값으로 새로운 배열이 만들어짐

filter 사용 예제

```javascript
const languages = [
  {
    id: 1,
    text: "Java",
    done: true,
  },
  {
    id: 2,
    text: "Python",
    done: true,
  },
  {
    id: 3,
    text: "Javscript",
    done: false,
  },
  {
    id: 4,
    text: "ruby",
    done: false,
  },
];

const tasksNotDone = languages.filter((language) => !language.done);
console.log(tasksNotDone);
//[Object, Object]
// 0: Object
// id: 3
// text: "Javscript"
// done: false
// 1: Object
// id: 4
// text: "ruby"
// done: false
```

#### reduce

- 배열이 주어졌을 때, 배열 안에 있는 모든 원소를 사용하여 어떠한 값을 연산할 때 사용
- reduce 함수는 두개의 파라미터를 전달함, 첫번째 파라미터는 콜백함수, 두번째 파라미터는 reduce 함수에서 사용할 초깃값
- reduce 함수의 첫번째 콜백함수 파라미터는 accumulator와 current 파라미터를 가져와서 결과를 반환하는 함수

reduce 함수를 사용하여 배열 원소의 총합을 구하는 예제

```javascript
const numbers = [1, 2, 3, 4, 5];

const sum = numbers.reduce((accumulator, current) => {
  return accumulator + current;
}, 0);

console.log(sum); // 15
```

reduce 함수를 사용하여 배열의 평균을 구하는 예제

- reduce 함수의 첫번째 파라미터 콜백 함수의 파라미터로 accumulator, current 외에 index, array까지 받아올 수 있음
- index 파라미터는 reduce 함수가 실행중인 현재 원소가 몇 번째 인덱스인지 리턴
- array는 reduce 함수가 실행하는 배열 자기 자신을 뜻함

```javascript
const numbers = [1, 2, 3, 4, 5];

const avg = numbers.reduce((accumulator, current, index, array) => {
  if (index === array.length - 1) {
    return (accumulator + current) / array.length;
  }
  return accumulator + current;
}, 0);

console.log(avg); // 15
```

reduce 함수를 사용하여 배열 내 알파벳의 카운트를 세는 예제

- 위의 예제와는 달리 초깃값으로 빈 객체를 넣어 줌

```javascript
const alphabets = ["a", "a", "a", "b", "c", "c", "c", "d", "e"];

const counts = alphabets.reduce((acc, cur) => {
  if (acc[cur]) {
    acc[cur] += 1;
  } else {
    acc[cur] = 1;
  }
  return acc;
}, {});

console.log(counts); // Object {a: 3, b: 1, c: 3, d: 1, e: 1}
```

#### splice

- 배열에서 특정 항목을 제거할 때 사용
- splice의 첫번째 파라미터로 제거할 인덱스, 두번째 파라미터로 제거할 인덱스부터 몇 개를 지울지 정함(인덱스 번호가 아닌 지울 원소의 개수)
- 새로운 배열을 생성하지 않는 대신 기존의 배열이 수정되며 제거한 인덱스의 값을 리턴

splice 사용 예제

```javascript
const numbers = [10, 20, 30, 40, 50];

const index = numbers.indexOf(30);
const spliced = numbers.splice(index, 1);
console.log(numbers); // [10, 20, 40, 50]
console.log(spliced); // [30]
```

제거할 인덱스부터 2개의 값을 제거

```javascript
const numbers = [10, 20, 30, 40, 50];

const index = numbers.indexOf(30);
const spliced = numbers.splice(index, 2); // 30, 40 총 두 개의 원소를 제거
console.log(numbers); // [10, 20, 50]
console.log(spliced); // [30, 40]
```

#### slice

- 배열을 잘라낼 때 사용
- slice의 첫번째 파라미터로 잘라낼 배열의 시작 인덱스, 두번째 파라미터로 어디까지 자를지를 정함(원소의 개수가 아니라 지정한 인덱스 이전까지 제거)
- `splice`와 비슷하지만 차이점은 기존의 배열을 수정하지 않음

slice 사용 예제

```javascript
const numbers = [10, 20, 30, 40, 50];

const sliced = numbers.slice(1, 4); // 1번 인덱스부터 3번 인덱스(4번 인덱스 전)까지 잘라냄
console.log(sliced); // [20, 30, 40]
console.log(numbers); // [10, 20, 30, 40, 50]
```

#### indexOf

- 원하는 항목이 몇 번째 원소인지 찾아주는 함수
- 일치하는 값이 없을 때 -1을 리턴

indexOf 사용 예제

```javascript
const superheros = ["아이언맨", "캡틴 아메리카", "토르", "닥터 스트레인지"];
const index = superheros.indexOf("토르");
console.log(index); // 2
```

#### findIndex

- 배열 안에 있는 값이 객체이거나 배열일 때, 특정 조건을 이용해서 조건에 해당하는 인덱스를 찾는 함수

findIndex 사용 예제

```javascript
const languages = [
  {
    id: 1,
    text: "Java",
    done: true,
  },
  {
    id: 2,
    text: "Python",
    done: true,
  },
  {
    id: 3,
    text: "Javscript",
    done: true,
  },
  {
    id: 4,
    text: "ruby",
    done: false,
  },
];

const index = languages.findIndex((language) => language.id === 3);
console.log(index); // 2
```

#### find

- `findIndex`와 유사하나 `findIndex`가 조건에 해당하는 인덱스 번호를 리턴하는 반면, `find`는 조건에 해당하는 값 자체를 리턴함

findIndex 사용 예제

```javascript
const languages = [
  {
    id: 1,
    text: "Java",
    done: true,
  },
  {
    id: 2,
    text: "Python",
    done: true,
  },
  {
    id: 3,
    text: "Javscript",
    done: true,
  },
  {
    id: 4,
    text: "ruby",
    done: false,
  },
];

const index = languages.find((language) => language.id === 3);
console.log(index); // Object {id: 3, text: "Javscript", done: true}
```

#### shift

- 첫번째 원소를 배열에서 추출함
- 추출하는 과정에서 배열의 해당 원소는 추출됨

shift 사용 예제

```javascript
const numbers = [10, 20, 30, 40, 50];

const value = numbers.shift();
console.log(value); // 10
console.log(numbers); // [20, 30, 40, 50]
```

#### unshift

- 배열의 맨 앞에 새 원소를 추가함
- `shift`의 반대 개념

unshift 사용 예제

```javascript
const numbers = [10, 20, 30, 40];
numbers.unshift(5);
console.log(numbers); // [5, 10, 20, 30, 40]
```

#### pop

- 마지막 원소를 배열에서 추출함
- 추출하는 과정에서 배열의 해당 원소는 추출됨

pop 사용 예제

```javascript
const numbers = [10, 20, 30, 40, 50];

const value = numbers.pop();
console.log(value); // 50
console.log(numbers); // [10, 20, 30, 40]
```

#### push

- 배열의 맨 마지막에 원소를 추가함
- `pop`의 반대 개념

push 사용 예제

```javascript
const numbers = [10, 20, 30, 40];

numbers.push(50);
console.log(numbers); // [10, 20, 30, 40, 50]
```

#### concat

- 여러개의 배열을 하나의 배열로 합침
- 기존 배열에는 영향이 없음

concat 사용 예제

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

const concated = arr1.concat(arr2);
console.log(concated); // [1, 2, 3, 4, 5, 6];
```

#### join

- 배열 안의 값들을 문자열 형태로 합침

join 사용 예제

```javascript
const array = [1, 2, 3, 4, 5];

console.log(array.join()); // 1,2,3,4,5
console.log(array.join(" ")); // 1 2 3 4 5
console.log(array.join(", ")); // 1, 2, 3, 4, 5
```

**참고자료**

- [벨로퍼트와 함께하는 모던 자바스크립트 패스트캠퍼스 온라인 강의](https://www.fastcampus.co.kr/dev_online_react)
- 모던 자바스크립트 입문 책
