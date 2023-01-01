---
title: "color flipper"
excerpt:

categories:
  - js practice
tag:
  - js
  - toy project

toc: true
toc_sticky: true
toc_label: "contents"

last_modified_at: 2022-11-13
---

![Untitled](/assets/images/js-practice/color-flipper.png)

[https://vannilla-js-basic-project-1-background-color.netlify.app](https://vannilla-js-basic-project-1-background-color.netlify.app/)

## 개요

> button을 누르면 배경색깔이 랜덤해서 바뀌는 페이지를 만들어보려고 한다.

어떻게 색깔을 랜덤으로 할 수 있는지 의문이였다.

rgb 표현, 단어 표현, hex 표현이 랜덤으로 나와서 알고보니 배열에 넣고 랜덤으로 돌니는 것이였다.

`const colors = ["green", "red", "rgba(133,122,200)", "#f15025"];`

어이가 없네

## 과정

- single : 배열에 값 저장하고 배열 길이만큼 랜덤 값 뽑아서 바꿈
- hex : 0~16\*\*6 만큼 랜덤 돌림 → 해당 값을 16진수로 바꿈

## 배운 것들

### document.body

document 가장 상단 tag는 프로퍼티로 접근가능

- `<html>` : document.documentElement
- `<body>` : document.body
- `<head>` : document.head

### js 에서 16진수 변환

js 에서의 16진수

- 좀 거지 같은듯
- 10진수를 2진수, 16진수로 `문자열` 로 바꿔줌
- `toString( n )`

```jsx
var a = 16;
var a1 = a.toString(16); //a1="10"
```

### css shadow

- `box-shadow` 사용
- box-shadwow : x-position y-position blur color 등

```css
nav {
  bax-shadow: 0 5px 15px rgb(0, 0, 0, 0.2);
}
```

### js 에서 문자열 붙이는 방법

1. 그냥 + 하기
2. concat( string1, string2,…);
3. join([배열])

### a 링크의 기본적인 효과 제거

```css
a {
  text-decoration: none;
}
```

### element 배경 투명하게

1. `background-image` : none
2. `background-color` : transparant

### addEventListener

`addEventListener` : html element에 이벤트 등록하는듯

```jsx
btn.addEventListener("click", function () {});
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
    <nav>
      <span id="title">Color Flipper</span>
      <span>
        <a href="#">Simple</a>
        <a href="./hex.html">Hex</a>
      </span>
    </nav>

    <main>
      <div class="colorbar">
        Background Color :&nbsp<span class="color">Red</span>
      </div>
      <button id="btn">CLICK ME</button>
    </main>
    <script src="app.js"></script>
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
  margin: 0;
  letter-spacing: 5px;
}
nav {
  width: 100%;
  background-color: whitesmoke;
  height: 7%;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  font-weight: 700;
  box-shadow: 0 5px 15px rgb(0, 0, 0, 0.2);
}
a {
  text-decoration: none;
  color: black;
}
a :hover {
  color: skyblue;
}
#title {
  color: skyblue;
}

body {
  background-color: red;
  height: 100vh;
}
main {
  height: 93%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.colorbar {
  background-color: rgb(37, 37, 37);
  color: white;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 40px;
  font-weight: 700;
  padding: 10px 15px;
  margin: 30px;
}
button {
  background: transparent;
  padding: 15px;
  font-size: 15px;
  font-weight: 600;
  border-color: rgb(37, 37, 37);
  border-radius: 10px;
  letter-spacing: 5px;
}
button:hover {
  background-color: rgb(37, 37, 37);
  color: white;
  transition: all 0.5s linear;
}
.color {
  color: blue;
}
```

</div>
</details>

<details>
  <summary>js</summary>
  <div markdown="1">
  
```jsx
const colors = ["green", "red", "rgba(133,122,200)", "#f15025"];

var btn = document.getElementById("btn");
var color = document.getElementsByClassName("color");

btn.addEventListener("click", function () {
var randomNum = Math.floor(Math.random() \* colors.length);
color[0].innerHTML = colors[randomNum].toUpperCase();
document.body.style.backgroundColor = colors[randomNum];
});

```

</div>
</details>
```
