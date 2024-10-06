---
layout: page
title: Writing
---

I'm still getting better about moving my half-formed writing from my personal
notes to something somewhat presentable to the public. So far, it's not going
that well. But, here's what I have so far.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
