# Fetch API

## 1. Fetch API란?

Fetch API는 **서버와 HTTP 요청/응답을 주고받기 위한 Web API**이다.

```
데이터 요청 → 서버 → 응답(JSON 등)
```

특징

O Promise 기반  
O 비동기 처리  

---

## 2. 기본 사용법

```javascript
fetch("https://api.example.com/data")
  .then((response) => response.json())
  .then((data) => console.log(data));
```

흐름

```
fetch 요청
→ response 객체 반환
→ json()으로 데이터 변환
→ 실제 데이터 사용
```

---

## 3. async / await 사용

```javascript
async function fetchData() {
  const response = await fetch("https://api.example.com/data");
  const data = await response.json();
  console.log(data);
}
```

특징

O 가독성 좋음  
O 동기 코드처럼 작성 가능  

---

## 4. Response 객체

fetch는 **Response 객체를 반환한다**

```javascript
const response = await fetch(url);
```

주요 프로퍼티

```
response.ok → 성공 여부 (true/false)
response.status → HTTP 상태 코드
```

---

## 5. JSON 변환

```javascript
const data = await response.json();
```

특징

O body를 JSON으로 파싱  
O Promise 반환  

주의

X 바로 데이터 아님 → await 필요  

---

## 6. 에러 처리 (중요)

fetch는 **네트워크 에러만 reject 한다**

```javascript
try {
  const response = await fetch(url);
} catch (e) {
  console.log("네트워크 에러");
}
```

---

### HTTP 에러는 직접 처리해야 함

```javascript
const response = await fetch(url);

if (!response.ok) {
  throw new Error("HTTP 에러");
}
```

핵심

```
404 / 500 → catch 안 감
```

---

## 7. GET 요청

```javascript
fetch("https://api.example.com/data");
```

기본값

```
method: GET
```

---

## 8. POST 요청

```javascript
fetch("https://api.example.com/data", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    name: "minini"
  })
});
```

구성

```
method
headers
body
```

---

## 9. 요청 옵션

```javascript
fetch(url, {
  method: "GET",
  headers: {},
  body: null
});
```

주요 옵션

```
method → 요청 방식
headers → 헤더 설정
body → 데이터
```

---

## 10. fetch + async/await 패턴 (중요)

```javascript
async function fetchData() {
  try {
    const response = await fetch(url);

    if (!response.ok) {
      throw new Error("에러 발생");
    }

    const data = await response.json();
    return data;

  } catch (e) {
    console.log(e);
  }
}
```

---

## 11. 여러 요청 처리

### 순차 실행

```javascript
const a = await fetch(url1);
const b = await fetch(url2);
```

---

### 병렬 실행

```javascript
const [res1, res2] = await Promise.all([
  fetch(url1),
  fetch(url2)
]);
```

특징

O 성능 좋음  

---

## 12. fetch vs axios

fetch

```
기본 내장 API
에러 처리 직접 해야 함
```

axios

```
자동 JSON 변환
에러 처리 편함
```

---

## 13. 실행 흐름

```
fetch → Promise 반환
→ Response 객체
→ json() 호출
→ 실제 데이터
```

---

# 정리

핵심 흐름

```
fetch → response → json() → 데이터
```

중요 포인트

```
fetch는 HTTP 에러를 reject 하지 않음
→ response.ok 체크 필수
```

추천 패턴

```
try...catch + response.ok
```

성능

```
여러 요청 → Promise.all
```