# Object Creation

## 객체 리터럴

### 1 객체란?

객체(object)는 **프로퍼티와 메서드로 구성된 복합 자료구조**이다.

- 프로퍼티 : 객체의 상태(state)
- 메서드 : 상태를 참조하거나 조작하는 동작(behavior)

객체는 **0개 이상의 프로퍼티로 구성된 집합**이며 자바스크립트에서 가장 중요한 데이터 타입이다.

예시

```javascript
const person = {
  name: "Mini",
  age: 25,
  sayHello() {
    console.log("Hello");
  }
};
```

---

### 2 객체 리터럴에 의한 객체 생성

객체 리터럴은 **중괄호 `{}`를 사용하여 객체를 생성하는 방법**이다.

```javascript
const person = {
  name: "Mini",
  age: 25
};
```

특징

O 가장 일반적인 객체 생성 방식  
O 런타임에 객체 생성 가능  
O 프로퍼티와 메서드를 함께 정의 가능  

---

### 3 프로퍼티 (Property)

프로퍼티는 **객체의 상태를 나타내는 값**이다.

구조

```
key : value
```

예시

```javascript
const person = {
  name: "Mini",
  age: 25
};
```

구성

```
name → 프로퍼티 키
Mini → 프로퍼티 값
```

특징

O 프로퍼티 키는 문자열 또는 심볼  
O 프로퍼티 값은 모든 값이 가능  

예

```
숫자
문자열
배열
객체
함수
```

---

### 4 메서드 (Method)

메서드는 **객체에 포함된 함수**이다.

```javascript
const circle = {
  radius: 5,
  getDiameter() {
    return 2 * this.radius;
  }
};
```

```
getDiameter → 메서드
```

메서드는 객체 내부에서 **this를 통해 자신의 프로퍼티를 참조할 수 있다.**

---

### 5 프로퍼티 접근

객체 프로퍼티 접근 방법

1. 마침표 표기법

```javascript
person.name
```

2. 대괄호 표기법

```javascript
person["name"]
```

특징

O 대괄호 표기법은 문자열 형태의 키 사용  
O 동적으로 키 접근 가능  

---

### 6 프로퍼티 값 갱신

이미 존재하는 프로퍼티에 값을 다시 할당하면 **값이 갱신된다**

```javascript
person.age = 30;
```

---

### 7 프로퍼티 동적 생성

존재하지 않는 프로퍼티에 값을 할당하면 **프로퍼티가 동적으로 생성된다**

```javascript
person.job = "developer";
```

---

### 8 프로퍼티 삭제

delete 연산자를 사용하여 프로퍼티를 삭제할 수 있다

```javascript
delete person.age;
```

---

## 생성자 함수에 의한 객체 생성

객체는 **생성자 함수(constructor)**를 사용하여 생성할 수도 있다.

---

### 1 Object 생성자 함수

자바스크립트는 **Object 생성자 함수**를 제공한다.

```javascript
const person = new Object();

person.name = "Mini";
person.age = 25;
```

하지만 이 방식은 **실무에서 거의 사용되지 않는다**

보통 다음 방식을 사용한다

```
객체 리터럴
생성자 함수
class
```

---

### 2. 생성자 함수

생성자 함수는 **동일한 구조의 객체를 여러 개 만들 때 사용하는 함수**이다.

예시

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const user1 = new Person("Mini", 25);
const user2 = new Person("Tom", 30);
```

객체 생성 과정

```
1 new 키워드로 생성자 함수 호출
2 빈 객체 생성
3 this가 새 객체를 가리킴
4 프로퍼티 할당
5 객체 반환
```

---

### 생성자 함수 네이밍 규칙

생성자 함수는 **첫 글자를 대문자로 작성한다**

예

```
Person
User
Car
```

이유

O 일반 함수와 구분하기 위한 관례

---

### new 없이 호출하면?

```javascript
const user = Person("Mini", 25);
```

이 경우

X 객체 생성되지 않음  
X 일반 함수로 실행됨  

---

### 생성자 함수 장점

O 동일한 구조의 객체 여러 개 생성 가능  
O 코드 재사용성 증가  
O 객체 생성 패턴을 명확하게 표현 가능  

---

# 객체 생성 방식 정리

자바스크립트에서 객체를 생성하는 방법

```
1 객체 리터럴
2 Object 생성자 함수
3 생성자 함수
4 class
```

