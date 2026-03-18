# Prototype

## 1. 객체지향 프로그래밍

객체지향 프로그래밍(OOP)은 **프로그램을 객체 단위로 나누어 설계하는 프로그래밍 패러다임**이다.

객체는 **상태와 동작을 하나의 단위로 묶은 것**이다.

```
상태 → property
동작 → method
```

예시

```javascript
const person = {
  name: "Mini",
  age: 25,
  getName() {
    return this.name;
  }
};
```

---

## 2. 상속과 프로토타입

자바스크립트는 **프로토타입 기반 상속(prototypal inheritance)**을 사용한다.

상속이란 **어떤 객체의 프로퍼티나 메서드를 다른 객체가 사용할 수 있도록 하는 것**이다.

### 문제 상황

객체를 여러 개 생성하면 **메서드가 중복 생성될 수 있다**

```javascript
function Circle(radius) {
  this.radius = radius;
  this.getArea = function () {
    return Math.PI * this.radius ** 2;
  };
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);
```

위 코드에서는 `getArea` 함수가 **객체마다 새로 생성된다**

X 메모리 낭비 발생

---

### 해결 방법 → Prototype

```javascript
function Circle(radius) {
  this.radius = radius;
}

Circle.prototype.getArea = function () {
  return Math.PI * this.radius ** 2;
};
```

O 메서드를 공유  
O 메모리 절약  
O 상속 구조 형성  

---

## 3. 프로토타입 객체

프로토타입은 **객체가 상속받는 메서드와 프로퍼티를 저장하는 객체**이다.

모든 객체는 **하나의 프로토타입을 가진다**

특징

O 객체는 프로토타입을 상속받는다  
O 프로토타입을 통해 메서드를 공유한다  

예시

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function () {
  console.log("hello " + this.name);
};

const user = new Person("Mini");

user.sayHello();
```

---

## 4. [[Prototype]] 내부 슬롯

모든 객체는 **[[Prototype]]이라는 내부 슬롯을 가진다**

이 값은 **자신의 프로토타입 객체를 가리킨다**

하지만 `[[Prototype]]`은 직접 접근할 수 없다.

대신 다음 방법을 사용한다.

```
__proto__
Object.getPrototypeOf()
Object.setPrototypeOf()
```

예

```javascript
const obj = {};

console.log(obj.__proto__);
```

---

## 5. 프로토타입 체인

객체에서 프로퍼티를 찾을 때

```
1 객체 내부에서 검색
2 프로토타입에서 검색
3 상위 프로토타입에서 검색
```

이 과정을 **프로토타입 체인**이라고 한다.

예시

```javascript
const arr = [1, 2, 3];

arr.hasOwnProperty("length");
```

검색 과정

```
arr 객체
→ Array.prototype
→ Object.prototype
→ null
```

---

## 6. 프로토타입의 constructor 프로퍼티

모든 프로토타입은 **constructor 프로퍼티를 가진다**

이 프로퍼티는 **생성자 함수를 가리킨다**

예

```javascript
function Person(name) {
  this.name = name;
}

const user = new Person("Mini");

console.log(user.constructor === Person);
```

결과

```
true
```

---

## 7. 프로토타입 생성 시점

프로토타입은 **생성자 함수가 생성되는 시점에 함께 생성된다**

구분

```
사용자 정의 생성자 함수 → 함수 정의 시 생성
빌트인 생성자 함수 → 자바스크립트 엔진 시작 시 생성
```

---

## 8. 객체 생성 방식과 프로토타입

객체 생성 방식에 따라 프로토타입이 다르게 연결된다.

객체 리터럴

```javascript
const obj = {};
```

```
obj → Object.prototype
```

배열

```javascript
const arr = [];
```

```
arr → Array.prototype
```

함수

```javascript
function foo() {}
```

```
foo → Function.prototype
```

---

## 9. 프로토타입 교체

프로토타입은 **동적으로 변경할 수 있다**

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype = {
  sayHello() {
    console.log("hello");
  }
};
```

하지만 이 경우 **constructor가 사라질 수 있다**

따라서 보통 다음처럼 작성한다.

```javascript
Person.prototype = {
  constructor: Person,
  sayHello() {
    console.log("hello");
  }
};
```

---

# 정리

프로토타입이 필요한 이유

```
1 메서드 공유
2 메모리 절약
3 상속 구조 구현
```

프로토타입 체인

```
객체
→ Prototype
→ 상위 Prototype
→ Object.prototype
→ null
```

자바스크립트는 **프로토타입 기반 객체지향 언어**이다.