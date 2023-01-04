---
title: "review carousel"
excerpt: "js 연습 프로젝트 No.3 리뷰 캐러셀 만들기"

categories:
  - js practice
tag:
  - js
  - toy project

toc: true
toc_sticky: true
toc_label: "contents"

last_modified_at: 2023-01-04
---

## 개요

![Untitled](/assets/images/js-practice/review-carousel.png)

> 버튼으로 이전, 다음 혹은 랜덤해서 리뷰들을 보여주는 리뷰 캐러셀

## 과정

### 디자인

- 이미지 뒤에 파란부분은 야매로 `box-shadow` 로 구현

### 작동

- 각각의 리뷰들을 객체로 배열에 저장
- 버튼들을 select 한 다음 forEach로 각각 이벤트 등록
- 버튼 누르면 리뷰 저장된 배열에서 가져와서 요소들의 innerText 바꿔줌
- ❓ 이미지 옆에 따옴표 못만들겠음..

## 배운것들

### html 꺽쇠 표현

- 꺽쇠 쓰려고하니까 태그 기호로 인식해서 안됨 ㅜ
- `&lt;` , `&gt;` 로 표시할 수 있다.

### Element의 자식,부모형제 노드 선택

childNode

- `ele.childNodes` : 모든 자식 찾기
- `ele.firstChild` : 첫번째 자식
- `ele.lastChild` : 막내 자식

parentNode

- `ele.parentNode` : 부모찾기
- `ele.parentNode.parentNode` : 할머니 찾기

sibling

- `ele.nextSibling` : 동생 찾기
- `ele.previoussSilbling` : 형찾기

### childNodes 했더니 안됨

```jsx
let contents = document.getElementById("container");
function change(newContents) {
  let child = contents.childNodes;
  console.log(child);
  child[1].innerText = newContents.name;
  child[2].innerText = newContents.job;
  child[3].innerText = newContents.explanation;
}
```

- 이렇게 childNodes 써서 컨텐츠들을 하나씩 선택하려했는데 중간에 이상한 것들이 껴있음
  ⇒ `childNodes` 와 `children` 의 차이
- `childNodes` : 자식 노드가 포함된 NodeList를 반환하는데, 주석 노드 같은 비요소 노드를 포함함
- `children` : 현재 요소의 자식 요소가 포함된 HTMLCollection을 반환, 비요소 노드 제외

### 템플릿 리터럴

> ` ` (백틱) 과 ${} 사이에 변수 사용

맨날 이름을 까먹어서 검색하기 힘듦

```jsx
child[0].src = `carousel${now + 1}.jpg`;
```

### html 텍스트 정렬

```css
p {
  text-align: center / right / left;
}
```

## 코드

<details>
  <summary>html</summary>
  <div markdown="1">
```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Document</title>
      <link rel="stylesheet" href="index.css" />
    </head>
    <body>
      <div id="title">Our Reviews</div>
      <div id="container">
        <img src="carousel1.jpg" alt="" />
        <div id="name">Anna Johnson</div>
        <div id="job">WEB DESIGNER</div>
        <div id="explanation">
          Helvetica artisan kinfolk thundercats lumbersexual blue bottle.
          Disrupt glossier gastropub deep v vice franzen hell of brooklyn twee
          enamel pin fashion axe.photo booth jean shorts artisan narwhal.
        </div>
        <div id="page">
          <button id="previous">&lt;</button>
          <button id="next">&gt;</button>
        </div>
        <button id="random">Suprise Me</button>
      </div>
      <script src="carousel.js"></script>
    </body>
  </html>
```
  </div>
</details>

<details>
  <summary>css</summary>
  <div markdown="1">
```css
  body {
    height: 100vh;
    background-color: hsl(206, 33%, 96%);
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    flex-direction: column;
  }
  #title {
    color: rgb(48, 54, 75);
    font-size: 40px;
    font-weight: 600;
    letter-spacing: 4px;
  }
  #container {
    width: 45%;
    height: 60%;
    background-color: white;
    box-shadow: 5px 5px 15px rgb(0, 0, 0, 0.1);
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    padding: 10px 30px;
  }
  #explanation {
    padding: 0 10px;
    text-align: center;
  }
  #name {
    font-size: 15px;
    font-weight: 600;
    letter-spacing: 3px;
  }
  #job {
    color: rgb(118, 182, 255);
  }
  #page button {
    border: none;
    background-color: white;
    cursor: pointer;
    font-size: large;
    color: rgb(118, 182, 255);
    font-weight: 600;
  }
  #random {
    padding: 3px 7px;
    color: rgb(118, 182, 255);
    background-color: rgb(244, 249, 255);
    cursor: pointer;
    border-radius: 5px;
    border: solid 1px rgb(118, 182, 255);
    box-shadow: 2px 2px rgb(32, 67, 107);
    transition: 0.5s linear;
  }
  #random:hover {
    background-color: rgb(26, 108, 202);
    color: black;
    box-shadow: 1px 1px rgb(32, 67, 107);
  }
  img {
    width: 150px;
    height: 150px;
    object-fit: cover;
    border-radius: 50% 50% 50% 50%;
    box-shadow: 7px -7px rgb(118, 182, 255);
    position: relative;
  }
```
  </div>
</details>
<details>
  <summary>js</summary>
  <div markdown="1">
```jsx
let data = [
    {
      id: 1,
      name: "Anna Johnson",
      job: "WEB DESIGNER",
      explanation:
        "Helvetica artisan kinfolk thundercats lumbersexual blue bottle. Disrupt glossier gastropub deep v vice franzen hell of brooklyn twee enamel pin fashion axe.photo booth jean shorts artisan narwhal.",
    },
    {
      id: 2,
      name: "Peter Jones",
      job: "INTERN",
      explanation:
        "Sriracha literally flexitarian irony, vape marfa unicorn. Glossier tattooed 8-bit, fixie waistcoat offal activated charcoal slow-carb marfa hell of pabst raclette post-ironic jianbing swag.",
    },
    {
      id: 3,
      name: "Bill Anderson",
      job: "THE BOSS",
      explanation:
        "Edison bulb put a bird on it humblebrag, marfa pok pok heirloom fashion axe cray stumptown venmo actually seitan. VHS farm-to-table schlitz, edison bulb pop-up 3 wolf moon tote bag street art shabby chic.",
    },
    {
      id: 4,
      name: "Susan Smith",
      job: "WEB DEVELOPER",
      explanation:
        "I'm baby meggings twee health goth +1. Bicycle rights tumeric chartreuse before they sold out chambray pop-up. Shaman humblebrag pickled coloring book salvia hoodie, cold-pressed four dollar toast everyday carry",
    },
  ];

let now = 0;
let contents = document.getElementById("container");
let btns = document.querySelectorAll("button");

btns.forEach(function (btn) {
btn.addEventListener("click", function (e) {
if (e.currentTarget.id == "previous") now--;
else if (e.currentTarget.id == "next") now++;
else now = Math.floor(Math.random() \* data.length);
now = (4 + now) % 4;
change(data[now]);
});
});

function change(newContents) {
let child = contents.children;
child[0].src = `carousel${now + 1}.jpg`;
child[1].innerText = newContents.name;
child[2].innerText = newContents.job;
child[3].innerText = newContents.explanation;
}

```
  </div>
</details>

```
