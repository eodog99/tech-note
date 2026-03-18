# Strict Mode

## 1. Strict Mode란?

Strict Mode는 **자바스크립트 문법을 더 엄격하게 적용하여 오류를 방지하는 기능**이다.

자바스크립트는 설계 초기에 실수를 허용하는 문법이 많았다.  
Strict Mode는 이러한 문제를 방지하고 **안전한 코드를 작성하도록 도와준다.**

---

## 2. Strict Mode 적용 방법

스크립트 또는 함수의 **맨 위에 선언**한다.

```javascript
"use strict";
```

### 스크립트 전체 적용

```javascript
"use strict";

var x = 10;
```

### 함수 단위 적용

```javascript
function foo() {
  "use strict";
  var x = 10;
}
```

---

## 3. Strict Mode 특징

O 선언하지 않은 변수 사용 시 에러 발생

```javascript
"use strict";
x = 10; // ReferenceError
```

O 변수 삭제 금지

```javascript
"use strict";
var x = 10;
delete x; // SyntaxError
```

O 중복 매개변수 금지

```javascript
"use strict";
function foo(a, a) {} // SyntaxError
```

O with 문 사용 금지

with 문은 스코프를 불명확하게 만들기 때문에 사용이 금지된다.

---

## 4. Strict Mode 사용 이유

O 자바스크립트의 잠재적인 오류 방지  
O 더 안전한 코드 작성 가능  
O 코드 가독성 향상  

---

# Built-in Objects

## 1. 자바스크립트 객체 분류

자바스크립트 객체는 크게 **3가지로 분류된다**

```
1 표준 빌트인 객체
2 호스트 객체
3 사용자 정의 객체
```

---

## 2. 표준 빌트인 객체 (Standard Built-in Objects)

자바스크립트에서 **기본적으로 제공하는 객체**이다.

대표적인 객체

```
Object
String
Number
Boolean
Array
Date
Math
RegExp
Function
Promise
```

특징

O ECMAScript 사양에 정의된 객체  
O 모든 자바스크립트 환경에서 사용 가능  

---

## 3. 생성자 함수인 빌트인 객체

대부분의 빌트인 객체는 **생성자 함수로 사용할 수 있다**

```javascript
const str = new String("hello");
const num = new Number(10);
const arr = new Array(1, 2, 3);
```

생성자 함수로 사용할 수 있는 객체

```
String
Number
Boolean
Array
Object
Date
RegExp
Function
Promise
```

---

## 4. 생성자 함수가 아닌 빌트인 객체

생성자 함수로 사용할 수 없는 객체도 존재한다.

예

```
Math
JSON
Reflect
```

이 객체들은 **정적 메서드만 제공한다**

```javascript
Math.random();
JSON.stringify();
```

---

## 5. 래퍼 객체 (Wrapper Object)

문자열, 숫자, 불리언 같은 **원시값도 객체처럼 사용할 수 있다**

예

```javascript
const str = "hello";

console.log(str.length);
console.log(str.toUpperCase());
```

자바스크립트 엔진이 **일시적으로 객체로 변환하여 메서드를 사용할 수 있게 한다**

이를 **래퍼 객체(wrapper object)**라고 한다.

---

## 6. 전역 객체 (Global Object)

전역 객체는 **코드가 실행되기 전에 자바스크립트 엔진에 의해 생성되는 객체**이다.

환경에 따라 이름이 다르다.

```
브라우저 → window
Node.js → global
```

전역 객체 특징

O 전역 변수는 전역 객체의 프로퍼티가 된다  
O 전역 함수는 전역 객체의 메서드가 된다  

예

```javascript
var x = 10;

console.log(window.x);
```

---

## 7. 전역 객체의 주요 프로퍼티

```
Infinity
NaN
undefined
```

---

## 8. 전역 객체의 주요 함수

```
eval()
isFinite()
isNaN()
parseFloat()
parseInt()
encodeURI()
decodeURI()
```

---

# 정리

Strict Mode

```
자바스크립트 문법을 엄격하게 적용하여 오류를 방지하는 기능
```

Built-in Objects

```
자바스크립트에서 기본적으로 제공하는 객체
```

객체 분류

```
1 표준 빌트인 객체
2 호스트 객체
3 사용자 정의 객체
```