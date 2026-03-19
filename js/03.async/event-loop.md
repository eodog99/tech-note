# Event Loop

## 1. 자바스크립트의 특징

자바스크립트는 **싱글 스레드(single thread)** 언어이다.

```
한 번에 하나의 작업만 실행 가능
```

하지만 실제로는 **비동기 처리가 가능하다**

이유

```
Event Loop + Web API + Queue 구조 때문
```

---

## 2. 실행 환경 구조

자바스크립트 실행 환경은 다음과 같이 구성된다.

```
Call Stack
Web API
Task Queue (Callback Queue)
Microtask Queue
Event Loop
```

---

## 3. Call Stack

Call Stack은 **실행 중인 함수가 쌓이는 공간**이다.

```javascript
function a() {
  b();
}

function b() {
  console.log("b");
}

a();
```

실행 순서

```
a() → push
b() → push
console.log 실행
b() → pop
a() → pop
```

특징

O LIFO 구조 (Last In First Out)  
O 현재 실행 중인 코드 관리  

---

## 4. Web API

Web API는 **브라우저가 제공하는 비동기 기능**이다.

예

```
setTimeout
setInterval
DOM 이벤트
fetch
```

특징

O 자바스크립트 엔진이 아닌 브라우저 영역  
O 비동기 작업 처리 담당  

---

## 5. Task Queue (Callback Queue)

비동기 작업이 완료되면 **콜백 함수가 Task Queue로 이동한다**

```javascript
setTimeout(() => {
  console.log("hello");
}, 1000);
```

흐름

```
setTimeout → Web API
→ 1초 후 → Task Queue 이동
```

특징

O FIFO 구조 (먼저 들어온 순서대로 실행)  

---

## 6. Microtask Queue

Microtask Queue는 **우선순위가 높은 큐**이다.

예

```
Promise.then
catch
finally
MutationObserver
```

```javascript
Promise.resolve().then(() => {
  console.log("microtask");
});
```

특징

O Task Queue보다 먼저 실행됨  
O 비동기 처리 우선순위 높음  

---

## 7. Event Loop

Event Loop는 **Call Stack과 Queue를 감시하는 역할**을 한다.

동작 방식

```
1 Call Stack이 비어있는지 확인
2 비어있으면
   Microtask Queue 먼저 실행
3 그 다음 Task Queue 실행
```

---

## 8. 실행 순서 핵심

```javascript
console.log("1");

setTimeout(() => {
  console.log("2");
}, 0);

Promise.resolve().then(() => {
  console.log("3");
});

console.log("4");
```

실행 결과

```
1
4
3
2
```

이유

```
1 → 동기 실행
4 → 동기 실행
3 → Microtask Queue
2 → Task Queue
```

---

## 9. 전체 흐름 정리

```
1 코드 실행 → Call Stack
2 비동기 작업 → Web API
3 작업 완료 → Queue 이동
4 Event Loop가 확인
5 Call Stack 비면 실행
```

---

## 10. 핵심 정리

우선순위

```
1 Call Stack (동기)
2 Microtask Queue (Promise)
3 Task Queue (setTimeout 등)
```

---

# 정리

자바스크립트는 싱글 스레드지만

```
Event Loop + Queue 구조로 비동기 처리 가능
```

실행 흐름

```
Call Stack
→ Microtask Queue
→ Task Queue
```

핵심

```
Promise가 setTimeout보다 먼저 실행된다
```