---
layout: default
title: Home
---

<h1>Recent Posts</h1>

<ul>
  {% for post in site.posts limit:5 %}
    <li>
      <span class="post-date">{{ post.date | date: "%b %-d, %Y" }}</span>
      <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <!-- <p>{{ post.excerpt | strip_html | truncatewords: 25 }}</p> -->
    </li>
  {% endfor %}
</ul>