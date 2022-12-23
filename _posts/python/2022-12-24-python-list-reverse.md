---
title: "python 리스트 뒤집기"
excerpt:

categories:
  - python
tag:
  - tip

toc: true
toc_sticky: true
toc_label: "contents"

last_modified_at: 2022-12-24
---

![Untitled](/assets/images/python/list-reverse-1.png)

> python 리스트 또는 numpy를 다룰 때 순서를 앞뒤로 뒤집어야 할때가 생각보다 많다

매번 할 때마다 기억이 안나서 검색하는 나를 발견하고 정리하기로 했다.

>

## 파이썬 리스트 뒤집기

### 슬라이싱 이용

> array[ : : -1 ]

![Untitled](/assets/images/python/list-reverse-2.png)

```python
array = [46250, 46600, 47000, 46500, 45700, 45600, 45500, 45700, 45500, 45350]
reverse_array=array[::-1]
```

### reverse() 메서드 사용

- `reverse()` 메서드 사용
- `원배열` 을 변경시킴 ↔ reversed

![Untitled](/assets/images/python/list-reverse-3.png)

```python
array = [46250, 46600, 47000, 46500, 45700, 45600, 45500, 45700, 45500, 45350]
array.reverse()
```

### 내장함수 reversed() 사용

- `reversed()` 내장함수는 순서가 뒤집어진 `iterator` 객체의 형태로 반환
  → 내장함수 `list()` 이용해서 리스트 자료형으로 변환해줘야함
- 원배열을 변경시키지 않음

![Untitled](/assets/images/python/list-reverse-4.png)

```python
array = [46250, 46600, 47000, 46500, 45700, 45600, 45500, 45700, 45500, 45350]
reversed_array=list(revered(arrary))
```

---

## NumPy arrary 뒤집기

다음 항목은 numpy를 사용할 때 필요하거나 찾아보게 되면 정리해야겠다

---

출처 : [https://codetorial.net/tips_and_examples/reverse_python_list_or_numpy_array.html](https://codetorial.net/tips_and_examples/reverse_python_list_or_numpy_array.html)
