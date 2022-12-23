---
title: "Challenge"
layout: archive
permalink: /categories/challenge
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.challenge %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
