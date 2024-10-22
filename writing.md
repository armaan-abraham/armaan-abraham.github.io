---
layout: page
title: Writing
---

I'm still getting better about moving my half-formed writing from my personal
notes to something somewhat presentable to the public. Here's what I have so far.

<ul class="post-list">
  {% assign sorted_posts = site.posts | where_exp: "post", "post.path contains '_posts/writing'" | sort: "date" | reverse %}
  {% for post in sorted_posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <div class="post-excerpt">
        {{ post.excerpt }}
      </div>
    </li>
  {% endfor %}
</ul>