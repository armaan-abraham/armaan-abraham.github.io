---
layout: page
title: Writing
---

I'm still getting better about moving my half-formed writing from my personal
notes to something somewhat presentable to the public. Here's what I have so far.

<ul class="post-list">
  {% for post in site.posts %}
    {% if post.path contains '_posts/writing' %}
      <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
        <div class="post-excerpt">
          {{ post.excerpt }}
        </div>
      </li>
    {% endif %}
  {% endfor %}
</ul>