# Array Methods

## 1. 배열 메서드란?

배열 메서드는 **배열을 쉽게 조작하기 위한 함수**이다.

```
조회 / 변환 / 추가 / 삭제 / 순회
```

---

## 2. forEach

배열을 순회한다

```javascript
const arr = [1, 2, 3];

arr.forEach((item) => {
  console.log(item);
});
```

특징

O 반환값 없음  
O 단순 반복  

---

## 3. map

배열을 변환하여 **새로운 배열 반환**

```javascript
const arr = [1, 2, 3];

const result = arr.map((item) => item * 2);
```

결과

```
[2, 4, 6]
```

특징

O 새로운 배열 반환  
O 원본 변경 X  

---

## 4. filter

조건에 맞는 요소만 **새 배열로 반환**

```javascript
const arr = [1, 2, 3, 4];

const result = arr.filter((item) => item % 2 === 0);
```

결과

```
[2, 4]
```

특징

O 조건 기반 필터링  
O 원본 변경 X  

---

## 5. find

조건에 맞는 **첫 번째 요소 반환**

```javascript
const arr = [1, 2, 3];

const result = arr.find((item) => item === 2);
```

결과

```
2
```

특징

O 하나만 반환  
O 없으면 undefined  

---

## 6. some / every

### some

하나라도 조건 만족하면 true

```javascript
arr.some((item) => item > 2);
```

---

### every

모두 만족하면 true

```javascript
arr.every((item) => item > 0);
```

---

## 7. reduce (중요)

배열을 하나의 값으로 줄인다

```javascript
const arr = [1, 2, 3];

const sum = arr.reduce((acc, cur) => acc + cur, 0);
```

결과

```
6
```

구조

```
acc → 누적값
cur → 현재값
```

---

## 8. push / pop

### push

```javascript
arr.push(4);
```

O 뒤에 추가  
O 원본 변경  

---

### pop

```javascript
arr.pop();
```

O 마지막 요소 제거  

---

## 9. shift / unshift

### shift

```javascript
arr.shift();
```

O 앞 요소 제거  

---

### unshift

```javascript
arr.unshift(0);
```

O 앞에 추가  

---

## 10. slice / splice

### slice

```javascript
arr.slice(0, 2);
```

O 일부 복사  
O 원본 변경 X  

---

### splice

```javascript
arr.splice(1, 1);
```

O 요소 삭제/추가  
X 원본 변경 O  

---

## 11. includes / indexOf

```javascript
arr.includes(2);
```

O 포함 여부 확인  

```javascript
arr.indexOf(2);
```

O 인덱스 반환  

---

## 12. sort

```javascript
arr.sort((a, b) => a - b);
```

특징

O 정렬  
X 원본 변경 O  

주의

```
기본은 문자열 기준 정렬
```

---

## 13. flat

```javascript
[1, [2, 3]].flat();
```

결과

```
[1, 2, 3]
```

---

## 14. join

```javascript
arr.join(",");
```

결과

```
"1,2,3"
```

---

## 15. 핵심 정리

반환 vs 원본 변경

```
원본 변경 X
map
filter
slice

원본 변경 O
push
pop
splice
sort
```

---

# 정리

핵심 메서드

```
forEach → 반복
map → 변환
filter → 조건
reduce → 누적
find → 하나 찾기
```

실무 핵심

```
map / filter / reduce 많이 사용
```