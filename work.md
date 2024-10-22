---
layout: default
title: Work
---

# Work

## Papers

[Multivalent binding model quantifies antibody species from systems
serology](https://www.biorxiv.org/content/10.1101/2024.07.05.602296v1)
*<span class="font-small">__Armaan A.
Abraham__, Zhixin Cyrillus Tan, Priyanka Shrestha, Emily R. Bozich, Aaron S.
Meyer (2024). Submitted to PLOS Computational Biology.
</span>*

[Integrative, high-resolution analysis of single cells across experimental
conditions with
PARAFAC2](https://www.biorxiv.org/content/10.1101/2024.07.29.605698v1)
*<span class="font-small">Andrew
Ramirez, Brian T. Orcutt-Jahns, Sean Pascoe, __Armaan A. Abraham__, Breanna Remigio,
Nathaniel Thomas, Aaron S. Meyer (2024). Preprint.</span>*

## Projects

<ul class="post-list">
  {% assign sorted_posts = site.posts | where_exp: "post", "post.path contains '_posts/work'" | sort: "importance" | reverse %}
  {% for post in sorted_posts %}
      <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
        {% if post.github %}
          (<a href="{{ post.github }}">github</a>)
        {% endif %}
        <div class="post-excerpt">
          {{ post.excerpt }}
        </div>
      </li>
  {% endfor %}
</ul>
