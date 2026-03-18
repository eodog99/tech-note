# Function

자바스크립트에서 함수의 개념과 함수가 일급 객체라는 특징에 대해 정리한다.

---

# 1. 함수란 무엇인가

함수는 **일련의 과정을 코드 블록으로 묶어 하나의 실행 단위로 정의한 것**이다.

함수는 입력을 받아 처리한 후 결과를 반환한다.

구성 요소

- 입력: 인수(argument)
- 입력을 받는 변수: 매개변수(parameter)
- 출력: 반환값(return value)

```javascript
function add(x, y) {
  return x + y;
}
```

함수 정의만으로는 실행되지 않는다.  
함수를 실행하려면 **함수 호출**을 해야 한다.

```javascript
var result = add(2, 5);

console.log(result); // 7
```

함수를 호출하면 코드 블록에 담긴 문이 실행되고 결과값이 반환된다.

---

# 2. 함수를 사용하는 이유

### 코드 재사용

같은 코드를 여러 번 작성할 필요가 없다.

### 코드 신뢰성

중복 코드가 줄어들어 실수 가능성이 줄어든다.

### 코드 가독성

프로그램의 구조를 이해하기 쉬워진다.

---

# 3. 함수 리터럴

자바스크립트에서 함수는 **객체 타입의 값**이다.

따라서 함수도 **리터럴로 생성할 수 있다.**

함수 리터럴 구성 요소

- function 키워드
- 함수 이름
- 매개변수 목록
- 함수 몸체

```javascript
var f = function add(x, y) {
  return x + y;
};
```

---

## 함수 리터럴 구성 요소

### 함수 이름

함수 이름은 식별자이므로 **식별자 네이밍 규칙을 따라야 한다.**

함수 이름은 **함수 내부에서만 참조 가능하다.**

- 이름이 있는 함수 → 기명 함수
- 이름이 없는 함수 → 익명 함수

---

### 매개변수 목록

매개변수는 0개 이상 사용할 수 있다.

```javascript
function add(x, y) {
  return x + y;
}
```

함수 호출 시 전달된 인수가 순서대로 매개변수에 할당된다.

---

### 함수 몸체

함수가 호출되었을 때 실행되는 코드 블록이다.

```javascript
function add(x, y) {
  return x + y;
}
```

---

# 4. 함수 선언문과 함수 표현식

## 함수 선언문

```javascript
function add(x, y) {
  return x + y;
}
```

특징

- 함수 이름을 생략할 수 없다
- 함수 호이스팅이 발생한다

---

## 함수 표현식

자바스크립트의 함수는 **값처럼 사용할 수 있다.**

따라서 변수에 할당할 수 있다.

```javascript
var add = function (x, y) {
  return x + y;
};
```

또는 기명 함수 표현식도 가능하다.

```javascript
var add = function add(x, y) {
  return x + y;
};
```

---

# 5. 함수 생성 시점과 함수 호이스팅

함수 선언문과 함수 표현식은 생성 시점이 다르다.

## 함수 선언문

```javascript
add(2, 5);

function add(x, y) {
  return x + y;
}
```

함수 선언문은 **런타임 이전에 먼저 생성된다.**

이처럼 **함수가 코드의 선두로 끌어올려진 것처럼 동작하는 현상**을  
**함수 호이스팅**이라고 한다.

---

## 함수 표현식

```javascript
add(2, 5); // 오류

var add = function (x, y) {
  return x + y;
};
```

함수 표현식은 **변수 호이스팅만 발생한다.**

즉, 함수 객체는 **런타임에 생성된다.**

---

# 6. 다양한 함수 생성 방법

## Function 생성자 함수

```javascript
var add = new Function('x', 'y', 'return x + y');
```

일반적으로 잘 사용하지 않는다.

---

## 화살표 함수 (Arrow Function)

ES6에서 도입된 함수 표현 방식이다.

```javascript
const add = (x, y) => x + y;
```

특징

- this 바인딩 방식이 다르다
- 코드가 간결하다

---

# 7. 매개변수와 인수

매개변수는 함수 내부에서 변수처럼 사용된다.

```javascript
function add(x, y) {
  return x + y;
}
```

함수 호출 시 전달된 값이 인수다.

```javascript
add(2, 5);
```

---

# 8. 반환문 (return)

함수는 `return` 키워드를 사용해 값을 반환할 수 있다.

```javascript
function add(x, y) {
  return x + y;
}
```

return 이후의 코드는 실행되지 않는다.

---

# 9. 다양한 함수 형태

## 중첩 함수

함수 내부에 정의된 함수

```javascript
function outer() {
  function inner() {
    console.log("inner");
  }

  inner();
}
```

---

## 콜백 함수

다른 함수에 **인수로 전달되는 함수**

```javascript
function repeat(n, callback) {
  for (let i = 0; i < n; i++) {
    callback(i);
  }
}

repeat(3, console.log);
```

---

## 고차 함수

함수를 **인수로 전달받거나 반환하는 함수**

대표적인 예

- map
- filter
- reduce

---

# 10. 함수와 일급 객체

자바스크립트에서 함수는 **일급 객체**다.

일급 객체란 다음 조건을 만족하는 객체를 말한다.

1. 무명의 리터럴로 생성 가능하다
2. 변수나 자료구조에 저장할 수 있다
3. 함수의 매개변수로 전달할 수 있다
4. 함수의 반환값으로 사용할 수 있다

---

## 예제

```javascript
const increase = function (num) {
  return ++num;
};

const decrease = function (num) {
  return --num;
};

const auxs = { increase, decrease };
```

함수는 객체에 저장할 수도 있다.

---

# 11. 함수 객체의 프로퍼티

함수는 객체이기 때문에 여러 프로퍼티를 가진다.

대표적인 프로퍼티

- arguments
- length
- name
- prototype
- __proto__

이 프로퍼티들은 **일반 객체에는 없는 함수 객체 고유의 프로퍼티**이다.

---

## arguments 프로퍼티

함수 호출 시 전달된 인수 정보를 담고 있는 객체

---

## length 프로퍼티

함수 정의 시 선언한 매개변수 개수를 나타낸다.

---

## name 프로퍼티

함수 이름을 나타낸다.

---

## prototype 프로퍼티

생성자 함수가 생성할 **인스턴스의 프로토타입 객체**를 가리킨다.

---

# 정리

- 함수는 일련의 작업을 수행하는 코드 블록이다.
- 함수는 호출을 통해 실행된다.
- 자바스크립트의 함수는 객체이며 일급 객체다.
- 함수 선언문은 함수 호이스팅이 발생한다.
- 함수 표현식은 변수 호이스팅이 발생한다.
- 함수는 변수에 할당하거나 다른 함수의 인수로 전달할 수 있다.