---
title: "Practice Project"
layout: archive
permalink: /categories/js-practice
author_profile: true
sidebar_main: true
---

---

## JavaSciprt를 연습하기 위한 프로젝트

- 기간 : 2022-11-15 ~
- 목적 : JavaScript 연습
-

[초보자를 위한 40가지의 자바스크립트 프로젝트](https://www.freecodecamp.org/korean/news/javascript-projects-for-beginners/) 참조

---

## 목록

{% assign posts = site.categories["js practice"] %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
