# Class

## 1. 클래스란?

클래스는 **객체를 생성하기 위한 템플릿(설계도)**이다.

자바스크립트의 클래스는 **생성자 함수와 프로토타입 기반으로 동작하는 문법적 설탕(syntactic sugar)**이다.

예시

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  sayHello() {
    console.log("hello " + this.name);
  }
}

const user = new Person("Mini", 25);

user.sayHello();
```

---

## 2. 클래스 정의

클래스는 `class` 키워드를 사용하여 정의한다.

```javascript
class Person {}
```

특징

O 클래스 이름은 보통 **대문자로 시작**  
O 클래스는 **new 키워드로 인스턴스를 생성**  

```javascript
const user = new Person();
```

---

## 3. constructor

constructor는 **인스턴스를 생성하고 초기화하는 특별한 메서드**이다.

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
}
```

특징

O 클래스 안에 **하나만 정의 가능**  
O 생략 가능  
O 인스턴스 생성 시 자동 실행  

---

## 4. 메서드 정의

클래스 내부에서 정의한 함수는 **프로토타입 메서드가 된다**

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  sayHello() {
    console.log("hello " + this.name);
  }
}
```

```
Person.prototype.sayHello
```

---

## 5. 정적 메서드 (static)

static 키워드를 사용하면 **클래스 자체에서 호출하는 메서드**를 만들 수 있다.

```javascript
class Person {
  static sayHi() {
    console.log("hi");
  }
}

Person.sayHi();
```

특징

O 인스턴스로 호출 불가능  
O 클래스 이름으로 호출  

```
Person.sayHi()
```

---

## 6. 클래스 상속

클래스는 `extends` 키워드를 사용하여 **상속**할 수 있다.

상속은 **기존 클래스를 기반으로 새로운 클래스를 만드는 것**이다.

```javascript
class Animal {
  move() {
    console.log("move");
  }
}

class Dog extends Animal {}

const dog = new Dog();

dog.move();
```

---

## 7. super 키워드

super는 **부모 클래스의 constructor 또는 메서드를 호출할 때 사용한다**

---

### 1. 부모 constructor 호출

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }
}

class Dog extends Animal {
  constructor(name, age) {
    super(name);
    this.age = age;
  }
}
```

설명

```
super(name) → 부모 constructor 실행
```

규칙

O super는 constructor에서 **반드시 먼저 호출해야 한다**

---

### 2. 부모 메서드 호출

```javascript
class Animal {
  speak() {
    console.log("animal sound");
  }
}

class Dog extends Animal {
  speak() {
    super.speak();
    console.log("bark");
  }
}
```

실행 결과

```
animal sound
bark
```

---

## 8. 클래스 특징

O 클래스는 **함수처럼 보이지만 함수가 아니다**

O 클래스는 **호이스팅이 발생하지 않는 것처럼 동작한다**

O 클래스는 **항상 strict mode로 실행된다**

---

# 정리

클래스 핵심 구조

```
class
constructor
method
static
extends
super
```

상속 구조

```
Parent class
↓
Child class
```

자바스크립트 클래스는 **프로토타입 기반 객체지향을 더 쉽게 사용하기 위한 문법이다.**