---
title: "[Javascript] Javascript 기초 문법 스터디 (9) - 프로토타입과 클래스"
excerpt: "자바스크립트 기초 문법 스터디 - 프로토타입과 클래스편"
toc: true
toc_sticky: true

categories:
  - Javascript
tags:
  - Javascript
---

## Javascript 기초 문법 (9)

### 프로토타입과 클래스

#### 객체 생성자

- 객체 생성자는 함수를 통해서 새로운 객체를 만들고 그 안에 넣고 싶은 값 혹은 함수를 구현함

객체 생성자 사용 예제

```javascript
function Animal(type, name, sound) {
  this.type = type;
  this.name = name;
  this.sound = sound;
  this.say = function () {
    console.log(this.sound);
  };
}

const cat = new Animal("고양이", "여름이", "야웅");
const dog = new Animal("개", "쿠쿠", "왈왈");

cat.say(); // 야웅
dog.say(); // 왈왈
```

- 생성자 안에서 this 뒤에 함수를 정의하면 그 생성자로 생성한 모든 인스턴스에 똑같은 함수가 추가됨
- 따라서 함수를 포함한 생성자로 인스턴스를 여러 개 생성하면 같은 작업을 하는 함수를 인스턴스 개수만큼 생성하게 되며 결과적으로 그만큼의 메모리를 소비함
- 같은 객체 생성자 함수 또는 값을 사용하는 경우 프로토타입을 통해 재사용할 수 있음

#### 프로토타입

- 프로토타입은 객체 생성자 함수 아래에 `.prototpye.[원하는키] - 코드`를 입력하여 설정할 수 있음

프로토타입 사용 예제

```javascript
function Animal(type, name, sound) {
  this.type = type;
  this.name = name;
  this.sound = sound;
}

Animal.prototype.say = function () {
  console.log(this.sound);
};

Animal.prototype.sharedValue = 1;

const cat = new Animal("고양이", "여름이", "야웅");
const dog = new Animal("개", "쿠쿠", "왈왈");

cat.say();
dog.say();

console.log(dog.sharedValue); // 1
console.log(cat.sharedValue); // 1
```

#### 객체 생성자 상속

- 특정 객체가 다른 객체로부터 기능을 이어받음
- 상속을 통해 기능을 재사용할 수 있음

객체 생성자 상속 예제

```javascript
function Animal(type, name, sound) {
  this.type = type;
  this.name = name;
  this.sound = sound;
}

Animal.prototype.say = function () {
  console.log(this.sound);
};

function Dog(name, sound) {
  Animal.call(this, "개", name, sound);
}

function Cat(name, sound) {
  Animal.call(this, "고양이", name, sound);
}

Dog.prototype = Animal.prototype;
Cat.prototype = Animal.prototype;

const cat = new Cat("여름이", "야웅");
const dog = new Dog("쿠쿠", "왈왈");

cat.say(); // 야웅
dog.say(); // 왈왈
```

- 새로 만든 `Dog`와 `Cat`함수에서 `Animal.call`을 호출하고 있는데, 여기서 첫번째 인자에는 `this`를 넣어주고 그 이후에는 `Animal` 객체 생성자 함수에 필요로 하는 파라미터를 넣어줘야 함
- 추가적으로 `prototype`을 공유해야 하기 때문에 상속받은 객체 생성자 함수를 만들고 나서 `prototype` 값을 `Animal.prototype`으로 설정함

#### 클래스

- ECMAScript 6부터 생성자를 정의하는 새로운 문법인 클래스 구문이 추가됨

```javascript
class Animal {
  constructor(type, name, sound) {
    this.type = type;
    this.name = name;
    this.sound = sound;
  }

  say() {
    console.log(this.sound);
  }
}

const cat = new Animal("고양이", "여름이", "야웅");
const dog = new Animal("개", "쿠쿠", "왈왈");

cat.say(); // 야웅
dog.say(); // 왈왈
```

class 상속 예제

```javascript
class Animal {
  constructor(type, name, sound) {
    this.type = type;
    this.name = name;
    this.sound = sound;
  }

  say() {
    console.log(this.sound);
  }
}

class Dog extends Animal {
  constructor(name, sound) {
    super("개", name, sound);
  }
}

class Cat extends Animal {
  constructor(name, sound) {
    super("고양이", name, sound);
  }
}

const cat = new Cat("여름이", "야웅");
const dog = new Dog("쿠쿠", "왈왈");

cat.say(); // 야웅
dog.say(); // 왈왈
```

**참고자료**

- [벨로퍼트와 함께하는 모던 자바스크립트 패스트캠퍼스 온라인 강의](https://www.fastcampus.co.kr/dev_online_react)
- 모던 자바스크립트 입문 책
