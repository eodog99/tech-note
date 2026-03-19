# Browser Rendering

## 1. 브라우저 렌더링 과정

브라우저는 HTML, CSS, JavaScript를 받아 **화면에 그리는 과정(렌더링)**을 수행한다.

전체 흐름

```
1 HTML 파싱 → DOM 생성
2 CSS 파싱 → CSSOM 생성
3 DOM + CSSOM → Render Tree 생성
4 Layout (Reflow)
5 Paint
```

---

## 2. HTML 파싱과 DOM 생성

브라우저는 HTML을 읽어 **DOM(Document Object Model)**을 생성한다.

```html
<div>
  <p>Hello</p>
</div>
```

↓

```
Document
 └─ div
     └─ p
```

특징

O HTML을 위에서 아래로 순차적으로 파싱  
O 요소를 객체 형태로 변환  

---

## 3. CSS 파싱과 CSSOM 생성

CSS도 HTML과 동일하게 파싱되어 **CSSOM**을 생성한다.

```css
p {
  color: red;
}
```

↓

```
CSSOM Tree 생성
```

특징

O 스타일 정보를 객체 형태로 변환  
O 렌더링에 필요한 스타일 정보 제공  

---

## 4. Render Tree 생성

DOM과 CSSOM을 결합하여 **Render Tree**를 만든다.

```
DOM + CSSOM → Render Tree
```

특징

O 화면에 표시되는 요소만 포함  
X display: none 요소는 제외  

---

## 5. Layout (Reflow)

Render Tree를 기반으로 **각 요소의 위치와 크기를 계산**한다.

```
width
height
position
```

특징

O 요소의 위치와 크기 계산  
O 화면 배치 결정  

---

## 6. Paint

Layout이 끝나면 실제 화면에 픽셀을 그린다.

```
색상
텍스트
이미지
```

특징

O 요소를 화면에 표시  
O 스타일 적용  

---

## 7. Reflow와 Repaint

### Reflow (Layout 다시 계산)

레이아웃이 변경될 때 발생

예

```
width 변경
height 변경
요소 추가/삭제
```

특징

X 비용이 큼  
X 성능에 큰 영향  

---

### Repaint (다시 그리기)

색상 등 스타일만 변경될 때 발생

예

```
color 변경
background 변경
```

특징

O Reflow보다 가벼움  
O 하지만 자주 발생하면 성능 저하  

---

## 8. JavaScript와 렌더링

JavaScript는 **DOM과 CSSOM 생성을 중단시킬 수 있다**

```html
<script>
  console.log("stop");
</script>
```

특징

X HTML 파싱 중단  
X 렌더링 지연 발생  

---

## 9. script 위치

### head에 script

```html
<head>
  <script src="app.js"></script>
</head>
```

문제

X HTML 파싱 중단  
X 렌더링 느려짐  

---

### body 끝에 script

```html
<body>
  ...
  <script src="app.js"></script>
</body>
```

장점

O HTML 파싱 완료 후 실행  
O 렌더링 빠름  

---

## 10. async / defer

### async

```html
<script async src="app.js"></script>
```

특징

O 다운로드와 실행이 비동기  
X 실행 순서 보장 안됨  

---

### defer

```html
<script defer src="app.js"></script>
```

특징

O HTML 파싱 후 실행  
O 실행 순서 보장  

---

## 11. 렌더링 최적화

O Reflow 최소화  
O DOM 조작 최소화  
O CSS 변경 최소화  
O script는 body 아래 또는 defer 사용  

---

# 정리

브라우저 렌더링 흐름

```
HTML → DOM
CSS → CSSOM
DOM + CSSOM → Render Tree
→ Layout
→ Paint
```

성능 핵심

```
Reflow 줄이기
Repaint 줄이기
JS 실행 타이밍 관리
```