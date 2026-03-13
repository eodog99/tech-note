# this

자바스크립트에서 `this`는 **함수가 호출되는 방식에 따라 동적으로 결정되는 값**이다.

`this`는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 **자기 참조 변수**이다.

이를 통해 객체의 프로퍼티나 메서드에 접근할 수 있다.

---

# 1. this 키워드

객체는 다음 두 가지 요소로 구성된다.

- 프로퍼티 : 객체의 상태
- 메서드 : 객체의 동작

메서드는 자신이 속한 객체의 프로퍼티를 참조해야 할 때가 많다.

예제

```javascript
const circle = {
  radius: 5,

  getDiameter() {
    return 2 * circle.radius;
  }
};

console.log(circle.getDiameter()); // 10
```

하지만 위 방식에는 문제가 있다.

객체 이름이 변경되면 코드가 깨질 수 있다.

그래서 `this`를 사용한다.

```javascript
const circle = {
  radius: 5,

  getDiameter() {
    return 2 * this.radius;
  }
};

console.log(circle.getDiameter()); // 10
```

여기서 `this`는 **circle 객체를 가리킨다.**

---

# 2. this 바인딩

바인딩이란 **식별자와 값을 연결하는 과정**이다.

예

```
변수 바인딩
변수 이름 → 메모리 주소
```

`this 바인딩`은 다음 의미를 가진다.

```
this → 어떤 객체
```

즉 `this`가 가리킬 객체를 연결하는 것이다.

---

# 3. 함수 호출 방식과 this 바인딩

`this`는 **함수 호출 방식에 따라 동적으로 결정된다.**

중요한 차이

```
렉시컬 스코프 → 함수 정의 시 결정
this 바인딩 → 함수 호출 시 결정
```

---

# 4. 일반 함수 호출

일반 함수에서 `this`는 **전역 객체**를 가리킨다.

브라우저

```
window
```

Node.js

```
global
```

예제

```javascript
function foo() {
  console.log(this);
}

foo();
```

결과

```
window
```

strict mode에서는

```
undefined
```

---

# 5. 메서드 호출

메서드 내부의 `this`는 **메서드를 호출한 객체**를 가리킨다.

예제

```javascript
const person = {
  name: "Lee",

  getName() {
    return this.name;
  }
};

console.log(person.getName());
```

결과

```
Lee
```

여기서

```
this → person 객체
```

중요

```
this는 객체가 아니라
메서드를 호출한 객체를 가리킨다.
```

---

# 6. 생성자 함수 호출

생성자 함수 내부의 `this`는 **생성될 인스턴스**를 가리킨다.

예제

```javascript
function Person(name) {
  this.name = name;
}

const me = new Person("Lee");

console.log(me.name);
```

여기서

```
this → 생성된 인스턴스
```

---

# 7. apply / call / bind 호출

이 메서드들은 **this를 명시적으로 바인딩할 수 있다.**

## call

```javascript
function foo() {
  console.log(this.name);
}

const obj = { name: "Lee" };

foo.call(obj);
```

결과

```
Lee
```

---

## apply

call과 동일하지만 **인수를 배열로 전달한다.**

```javascript
foo.apply(obj);
```

---

## bind

`this`가 바인딩된 **새로운 함수를 반환한다.**

```javascript
const bound = foo.bind(obj);

bound();
```

---

# 8. 화살표 함수와 this

화살표 함수는 **this 바인딩이 없다.**

대신 **상위 스코프의 this를 그대로 사용한다.**

예제

```javascript
const obj = {
  value: 1,

  foo() {
    const bar = () => {
      console.log(this.value);
    };

    bar();
  }
};

obj.foo();
```

결과

```
1
```

화살표 함수의 this는

```
자신이 아닌
상위 함수의 this를 사용한다.
```

---

# 9. this 사용 시 주의점

일반 함수 내부

```
this → 전역 객체
```

객체 메서드

```
this → 메서드 호출 객체
```

생성자 함수

```
this → 생성된 인스턴스
```

화살표 함수

```
this → 상위 스코프 this
```

---

# 정리

this는 **자기 자신을 가리키는 값이 아니라 함수 호출 방식에 따라 결정되는 값**이다.

this 바인딩 규칙

```
일반 함수 호출 → 전역 객체
메서드 호출 → 메서드 호출 객체
생성자 함수 호출 → 생성될 인스턴스
apply / call / bind → 명시적으로 지정된 객체
화살표 함수 → 상위 스코프 this
```

---

# 느낀 점

this는 단순히 객체를 가리키는 키워드라고 생각했지만  
함수 호출 방식에 따라 값이 달라진다.
특히 렉시컬 스코프는 함수 정의 시 결정되지만  
this 바인딩은 함수 호출 시 결정된다는 차이를 이해하는 것이 중요하다고 느꼈다!