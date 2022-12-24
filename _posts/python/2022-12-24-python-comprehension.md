---
title: "python list comprehension"
excerpt:

categories:
  - python
tag:
  - concepts

toc: true
toc_sticky: true
toc_label: "contents"

last_modified_at: 2022-12-24
---

> list 안에 `표현식` , `for문` , `if문` 을 이용해서 list를 한줄로 선언함

## 간단한 반복문 comprehension

> [표현식 for 변수명 in list]

```python
>>> [i for i in range(6)]
[0,1,2,3,4,5]
```

## 조건을 사용한 comprehension

> [표현식 for 변수명 in list if 조건]

- 즉, 조건에 해당하는 요소들만 리스트로 만듬
- ~~if, else if로 조건’들’에 따라서 comprehension 하는 방법은 아직 모르겠음~~
  정리하면서 찾아버림

```python
>>> [i for i in range(10) if i%2==0]
[0,2,4,6,8]
```

### if, else를 이용한 comprehension

> [참일때 if 조건 else false일때 for 변수명 in list]

```python
>>> ['even' if i%2 == 0 else 'odd' for i in range(5)]
['even','odd','even','odd']
```

- elif를 사용할 수는 없다고 함

### elif처럼 comprehension

- else 안에 다시 if를 사용해서 `elif` 인 것 처럼 할 수 있음

```python
>>> ['zero' if i==0 else 'even' if i%2==0 else 'odd' for i in range(5)]
['zero','odd','even','odd']
```

## 실제로 사용한 것들

### 2차원 배열을 만들때, comprehension

- 할때마다 찾아봤었는데, 까먹음. 비슷한 상황이 발생하면 다시 적기로

## generator expreession

- 이것도 comprehension을 사용한 기능이라고 함
- generator expression이 뭔지 알아보고 다시 정

referece : [https://doorbw.tistory.com/174](https://doorbw.tistory.com/174)
