---
title: "markdown toggle"
excerpt:

categories:
  - blog
tag:
  - markdown

toc: true
toc_sticky: true
toc_label: "contents"

last_modified_at: 2022-12-30
---

### 개요

노션의 `toggle` 기능을 정말 열심히 쓰는 입장에서 `markdown` 에서 `toggle` 을 지원하지 않는 것은 조금 슬프다 ㅜ

다행히 html 을 사용해서 `toggle` 을 사용할 수 있다.

이 기능을 이용해서 vlog 의 시리즈 기능을 제현해 놓고 싶다.

---

### markdown toggle

- `detail` : toggle을 지원해주는 tag
- ~~`div markdown="1"` : jekyll에서 markdwon 사이에서 html을 인식하는 코드~~
- ~~업데이트 됐는지 그냥 해야함~~
- `div markdown="1"` : 정정. html 사이에서 markdown을 인식하는 코드이다.

```html
<details>
  <summary>토글 접기/펼치기</summary>
  <div markdown="1">안녕</div>
</details>
```

<details>
<summary>토글 접기/펼치기</summary>
<div markdown="1">

안녕

</div>
</details>

### toggle head

시리즈같은 느낌을 주려면 h1,h2 등도 같이 사용됐으면 좋겠다.

- style로 `inline`을 설정해줘야 잘 나온다

```html
<details>
<summary><h3 style="display:inline">토글 접기/펼치기<h3></summary>
안녕
</details>
```

<details>
<summary><h3 style="display:inline">토글 접기/펼치기</h3></summary>
안녕
</details>

### reference:

- [https://computer-science-student.tistory.com/388](https://computer-science-student.tistory.com/388)
