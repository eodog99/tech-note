# Closure

클로저는 **자바스크립트의 스코프와 실행 컨텍스트를 이해해야 알 수 있는 중요한 개념**이다.

클로저를 이해하면 다음을 이해할 수 있다.

- 렉시컬 스코프
- 함수가 스코프를 기억하는 방식
- 상태 유지
- 캡슐화와 정보 은닉

---

# 1. 렉시컬 스코프 (Lexical Scope)

자바스크립트는 **렉시컬 스코프(정적 스코프)**를 따른다.

> 함수의 상위 스코프는 **함수가 어디서 호출되었는지가 아니라 어디서 정의되었는지에 따라 결정된다.**

예제

```javascript
const x = 1;

function foo() {
  const x = 10;
  bar();
}

function bar() {
  console.log(x);
}

foo(); // 1
bar(); // 1
```

설명

```
bar 함수는 전역에서 정의됨
→ 상위 스코프는 전역 스코프
→ 따라서 x는 1
```

즉

```
호출 위치 x
정의 위치 o
```

이것이 **렉시컬 스코프**이다.

---

# 2. 함수 객체의 내부 슬롯 [[Environment]]

자바스크립트에서 함수는 **자신이 정의된 환경을 기억한다.**

함수가 생성될 때

```
자신이 정의된 스코프
```

를 **내부 슬롯 [[Environment]]** 에 저장한다.

즉 함수는 다음 정보를 기억한다.

```
함수가 정의된 렉시컬 환경
```

예제

```javascript
const x = 1;

function foo() {
  const x = 10;
  bar();
}

function bar() {
  console.log(x);
}
```

`bar` 함수가 생성될 때

```
[[Environment]] → 전역 렉시컬 환경
```

을 저장한다.

그래서 어디서 호출하든 항상 **전역 x**를 참조한다.

---

# 3. 클로저 (Closure)

클로저란

> **외부 함수보다 더 오래 살아있는 중첩 함수가 외부 함수의 변수를 참조하는 것**

이다.

예제

```javascript
function outer() {
  const x = 10;

  function inner() {
    console.log(x);
  }

  return inner;
}

const func = outer();

func(); // 10
```

설명

실행 과정

```
1. outer 실행
2. inner 생성
3. outer 종료
4. func() 호출
```

하지만 `inner` 함수는 **outer의 변수 x를 기억한다.**

왜냐하면

```
inner의 [[Environment]] → outer 렉시컬 환경
```

을 참조하고 있기 때문이다.

이처럼 **외부 함수의 변수에 접근할 수 있는 함수**를 **클로저**라고 한다.

---

# 4. 클로저가 발생하는 이유

자바스크립트 엔진은

**참조되는 변수는 메모리에서 제거하지 않는다.**

예

```
outer 종료
하지만 inner가 x를 참조
→ x 메모리 유지
```

그래서 **outer의 실행 컨텍스트는 사라지지만  
렉시컬 환경은 유지된다.**

---

# 5. 클로저의 활용

클로저는 **상태를 안전하게 유지할 때 사용된다.**

예

```javascript
function counter() {
  let count = 0;

  return function () {
    return ++count;
  };
}

const increase = counter();

console.log(increase()); // 1
console.log(increase()); // 2
console.log(increase()); // 3
```

설명

```
count는 외부에서 접근 불가
하지만 클로저 내부에서는 접근 가능
```

즉

```
상태 유지 가능
```

---

# 6. 캡슐화와 정보 은닉

클로저를 이용하면 **데이터를 보호할 수 있다.**

예

```javascript
function createUser() {
  let password = "1234";

  return {
    checkPassword(input) {
      return input === password;
    },
  };
}

const user = createUser();

user.checkPassword("1234"); // true
```

여기서

```
password 변수
```

는 **외부에서 접근할 수 없다.**

이것을

```
캡슐화
정보 은닉
```

이라고 한다.

---

# 정리

- 자바스크립트는 렉시컬 스코프를 따른다.
- 함수의 상위 스코프는 **정의된 위치**에 따라 결정된다.
- 함수는 내부 슬롯 [[Environment]]에 상위 스코프를 저장한다.
- 외부 함수보다 오래 살아있는 중첩 함수가 외부 변수를 참조하면 클로저가 된다.
- 클로저는 상태 유지와 캡슐화에 활용된다.

---

# 느낀 점

클로저는 단순히 함수 안의 함수가 아니라  
함수가 자신이 정의된 환경을 기억한다는 점이 핵심!  

특히 외부 함수가 종료된 이후에도 내부 함수가 외부 변수를 계속 참조할 수 있다는 점을 알았고  
이 개념이 상태 관리나 데이터 은닉에 활용된다는 것을 이해할 수 있었다.