---
layout: post
title: JavaScript 기초
tags: [NHN, 신입사원, 기술교육, 베이스캠프, 자바스크립트, JavaScript]
color: rgb(229, 64, 54)
excerpt_seperator: <!--more-->

---

아래 내용은 2021-02-04(목) 10:30~17:00 김성호 책임님이 진행한 교육을 요약한 것입니다.

<br>

## DOM

- 자바스크립트로 HTML 문서를 다룰 수 있게 브라우저 환경을 제공하는 API

### JS와 DOM의 상호작용 시점?

- 브라우저는 HTML 문서를 첫줄부터 파싱
- JS는 코드가 평가되는 시점에 Document에 렌더링되어 있는 엘리먼트에만 접근 가능
- `window`의 `load` 이벤트를 이용해 스크립트 실행을 지연 (`EventListener`는 Memory Leak을 발생시키는 주 원인이므로 사용 시 주의!)

<br>

## Document

- 브라우저 상의 HTML 문서를 모델링한 객체
- DOM API의 시작점

```js
document.getElementById("myId");      // returns HTMLElement or null
document.getElementByTagName("div");  // returns HTMLCollection or null
document.getElementByClassName("myClass").getElementsByTagName("div");
```

> HTML Collection?
> 유사 배열로 숫자로 인덱싱 가능하고 length 존재
> Array가 아니라서 Array API(e.g.`forEach()`)를 사용하려면 변환한 뒤 사용
> live한 컬렉션 - ex) 화면에 추가해도 알아서 찾아냄

<br>

## 동적으로 엘리먼트 추가/삭제하기

```js
var newDiv = document.createElement("div");
var newText = document.createTextNode("Hello Rookies");
newDiv.appendChild(newText);
document.body.appendChlid(newDiv);    // 추가 했지만
document.body.removeChild("newDiv");  // 바로 삭제해서 브라우저에 안 보임
```

<br>

## 이벤트 전파

- Bubbling: 아래에서 위로 (`addEventListener` 세번째 인자가 `false`일 때)
- Capturing: 위에서 아래로 (`addEventListener` 세번째 인자가 `true`일 때)
- 해결하려면 이벤트 객체 사용

```js
var useCapturing = true;
elem.addEventListener(
  "click",
  function (eventObject) {
    eventObject.stopPropagation();  // 캡처링이나 버블링 취소 (이벤트 전파 차단)
    eventObject.preventDefault();   // 디폴트 동작을 취소
  },
  useCapturing
);
```

<br>

## CSS 적용

- id는 주로 element를 식별할 때 사용
- 따라서 CSS 스타일을 적용할 때는 보통 class 단위로 적용

<br>

## QuerySelector

jQuery가 너무 신박(?)해서 표준이 됨

```js
document.querySelector(".myClass");     // 처음 찾은 한 개만 리턴
document.querySelectorAll(".myClass");  // 해당되는 모든 엘리먼트를 찾음. NodeList로 not live
```

<br>
