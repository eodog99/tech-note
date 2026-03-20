# Promise

## 1. Promise란?

Promise는 **비동기 작업의 결과를 나타내는 객체**이다.

```
비동기 작업 → 성공 or 실패 → 결과 반환
```

기존 방식

```
콜백 함수 → 콜백 지옥 발생
```

Promise 사용

```
.then 체이닝 → 가독성 향상
```

---

## 2. Promise 상태

Promise는 3가지 상태를 가진다.

```
pending → 대기 상태
fulfilled → 성공
rejected → 실패
```

흐름

```
pending → fulfilled
pending → rejected
```

---

## 3. Promise 생성

```javascript
const promise = new Promise((resolve, reject) => {
  // 비동기 작업
});
```

예시

```javascript
const promise = new Promise((resolve, reject) => {
  const success = true;

  if (success) {
    resolve("성공");
  } else {
    reject("실패");
  }
});
```

---

## 4. then / catch / finally

### then (성공 처리)

```javascript
promise.then((result) => {
  console.log(result);
});
```

---

### catch (에러 처리)

```javascript
promise.catch((error) => {
  console.log(error);
});
```

---

### finally (무조건 실행)

```javascript
promise.finally(() => {
  console.log("끝");
});
```

특징

O 성공/실패 관계없이 실행  

---

## 5. Promise 체이닝

then은 **Promise를 반환하므로 계속 연결 가능**

```javascript
Promise.resolve(1)
  .then((num) => num + 1)
  .then((num) => num + 1)
  .then((num) => console.log(num));
```

결과

```
3
```

---

## 6. 에러 핸들링

Promise에서 에러는 **catch로 처리**한다.

```javascript
Promise.reject("에러")
  .then(() => console.log("성공"))
  .catch((err) => console.log(err));
```

---

### then에서 발생한 에러도 catch로 잡힘

```javascript
Promise.resolve()
  .then(() => {
    throw new Error("에러 발생");
  })
  .catch((err) => console.log(err));
```

특징

O 하나의 catch로 여러 에러 처리 가능  

---

## 7. 에러 전파

에러는 **아래로 전파된다**

```javascript
Promise.resolve()
  .then(() => {
    throw new Error("에러");
  })
  .then(() => console.log("실행 안됨"))
  .catch((err) => console.log(err));
```

특징

O 에러 발생 이후 then은 실행되지 않음  
O 가장 가까운 catch로 이동  

---

## 8. Promise 정적 메서드

### Promise.resolve

```javascript
Promise.resolve(10).then(console.log);
```

---

### Promise.reject

```javascript
Promise.reject("에러").catch(console.log);
```

---

### Promise.all

모든 Promise가 성공해야 실행

```javascript
Promise.all([p1, p2, p3])
  .then((result) => console.log(result))
  .catch((err) => console.log(err));
```

특징

O 하나라도 실패하면 전체 실패  

---

### Promise.race

가장 먼저 끝난 Promise 반환

```javascript
Promise.race([p1, p2, p3]).then(console.log);
```

---

## 9. async / await

Promise를 더 쉽게 쓰기 위한 문법

```javascript
async function fetchData() {
  const result = await Promise.resolve("data");
  console.log(result);
}
```

특징

O 동기 코드처럼 작성 가능  
O Promise 기반  

---

## 10. async / await 에러 처리

try...catch 사용

```javascript
async function fetchData() {
  try {
    const result = await Promise.reject("에러");
  } catch (e) {
    console.log(e);
  }
}
```

---

## 11. 실행 순서 (Event Loop 연결)

```javascript
console.log("1");

Promise.resolve().then(() => console.log("2"));

setTimeout(() => console.log("3"), 0);

console.log("4");
```

결과

```
1
4
2
3
```

이유

```
Promise → Microtask Queue
setTimeout → Task Queue
```

---

# 정리

Promise 흐름

```
pending → fulfilled / rejected
```

핵심 메서드

```
then
catch
finally
```

에러 처리

```
catch 하나로 처리 가능
에러는 아래로 전파됨
```

우선순위

```
Promise > setTimeout
```