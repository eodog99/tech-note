# Async / Await

## 1. async / await란?

async / await는 **Promise를 더 쉽게 사용하기 위한 문법**이다.

```
비동기 코드를 동기 코드처럼 작성 가능
```

기존 방식

```
then 체이닝 → 가독성 떨어짐
```

async / await

```
위에서 아래로 읽히는 코드
```

---

## 2. async 함수

async 키워드를 붙이면 **항상 Promise를 반환한다**

```javascript
async function foo() {
  return 1;
}
```

결과

```
Promise { 1 }
```

특징

O 항상 Promise 반환  
O return 값 → resolve 처리됨  

---

## 3. await

await는 **Promise가 처리될 때까지 기다린다**

```javascript
async function foo() {
  const result = await Promise.resolve(10);
  console.log(result);
}
```

특징

O Promise가 끝날 때까지 대기  
O 결과값 반환  

---

## 4. await 사용 조건

await는 **async 함수 내부에서만 사용 가능**

```javascript
function foo() {
  const result = await Promise.resolve(10); // 에러
}
```

---

## 5. async / await 기본 흐름

```javascript
async function fetchData() {
  const data = await Promise.resolve("data");
  console.log(data);
}
```

흐름

```
Promise 실행
→ 완료될 때까지 대기
→ 결과 반환
```

---

## 6. 에러 처리

async / await에서는 **try...catch 사용**

```javascript
async function fetchData() {
  try {
    const result = await Promise.reject("에러");
  } catch (e) {
    console.log(e);
  }
}
```

특징

O 동기 코드처럼 에러 처리 가능  

---

## 7. Promise vs async/await

### Promise

```javascript
fetchData()
  .then((res) => console.log(res))
  .catch((err) => console.log(err));
```

---

### async / await

```javascript
async function fetchData() {
  try {
    const res = await fetchData();
    console.log(res);
  } catch (err) {
    console.log(err);
  }
}
```

차이

O async/await → 가독성 좋음  
O 흐름 이해 쉬움  

---

## 8. 병렬 처리 (중요)

await를 연속으로 사용하면 **순차 실행된다**

```javascript
const a = await Promise.resolve(1);
const b = await Promise.resolve(2);
```

```
1 → 끝 → 2 실행
```

---

### 병렬 처리 방법

```javascript
const [a, b] = await Promise.all([
  Promise.resolve(1),
  Promise.resolve(2)
]);
```

특징

O 동시에 실행  
O 성능 향상  

---

## 9. 실행 순서 (Event Loop 연결)

```javascript
async function foo() {
  console.log("1");
  await Promise.resolve();
  console.log("2");
}

console.log("3");
foo();
console.log("4");
```

결과

```
3
1
4
2
```

이유

```
await 이후 코드는 Microtask Queue로 이동
```

---

## 10. async / await 주의사항

O await 남용하면 성능 저하  
O 병렬 처리 필요 시 Promise.all 사용  
O 에러 처리 반드시 필요  

---

# 정리

async / await 핵심

```
Promise를 쉽게 사용하는 문법
```

특징

```
async → Promise 반환
await → Promise 완료 대기
```

에러 처리

```
try...catch
```

성능

```
순차 실행 → 느림
병렬 처리 → Promise.all 사용
```