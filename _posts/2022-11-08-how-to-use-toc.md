---
title: "toc(table of contents) 설정방법"
categories:
  - Blog
tag:
  - Blog
date: 2022-11-08

last_modified_at: 2022-11-08

toc: true
toc_sticky: true
toc_table: "contents"
---

내가 노션을 쓸 때마다 원하는 기능이 있었다.  
하나는 `블록` 이고 하나는 바로 '목차'이다.  
~~최근에 이 기능이 노션에서 업데이트 되긴했다.~~

이것의 이름조차 알지 못해서 방법을 검색 조차도 할 수 없었다.
뭐라고 부르는지 조차 몰랐으니까 ㅋㅋㅋ

[toc 사용 방법](https://devinlife.com/howto%20github%20pages/toc-table)

github blog를 시작하면서 도움을 많이 받은 블로그이다.  
블로그 글에서 toc를 보마자 `유레카`를 외치지 않을 수가 없었다....

---

# toc 사용방법

toc는 h1~h6 목록을 표시해준다고 한다.

```yml
toc: true
```

기본 사용방법

```yml
toc_sticky: true
```

toc_sticky도 같이 추가하면 toc를 사이드 바에 고정시킨다고 한다.
즉, sticky를 주면 스크롤을 내려도 toc가 같이 내려온다 👍

```yml
toc_table: "contents"
```

toc_table을 추가하면 toc에 `labeling`을 할 수 있다.

# 테스트용 헤더

## 두번째 헤더

## 두번째 헤더

### 세번째 헤더
