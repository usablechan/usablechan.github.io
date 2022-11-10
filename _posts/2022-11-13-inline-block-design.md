---
title: "github blog 인라인 코드블록 설정방법"
excerpt: "inline block css 설정방법"

categories:
  - Blog

toc: true
toc_sticky: true
toc_label: "contents"

last_modified_at: 2022-11-13
---

### 인라인 코드 블록

```c
print(hello)
```

이런 코드블록의 인라인 버전이라고 보면된다

`바로 이런거` `요런거` `히히릿`

github blog 만들면서 기대 만빵이였는데  
minimal-mistake의 인라인 코드 블록이 너무 못생겼다. ㅜ  
나는 인라인 블록을 약간 강조의 표시로 사용하고 싶었기 때문인다.

그래서 찾았다 나는 방법을  
바로 고고

파일 위치 : /\_sass/minimal-mitaeks/\_pages.scss
{: .notice--warning}

`:not(pre) > code` 의 css를 입맛에 맞게 요리조리 해주면 된다.

```css
:not(pre) > code {
  padding-top: 0.1rem;
  padding-bottom: 0.1rem;
  font-size: 0.9em;
  background: $code-background-color;
  border-radius: $border-radius;

  color: #4b89dc;
  font-weight: bold;
  background-color: #dde9f9;

  &::before,
  &::after {
    letter-spacing: -0.2em;
    content: "\00a0"; /* non-breaking space*/
  }
}
```

---

\+ `잡설`
인라인 코드 블록 디자인을 새롭게 하면서  
색깔을 엄청 고민했다.  
더 나아가서 블로그의 블스널 컬러도 정해보았다. ㅋㅋㅋ
파란색이 좋아서 대략 푸르댕댕한 색깔로 설정해보았다.
