---
layout: page
title: Portfolio
excerpt: "An archive of projects sorted by date."
search_omit: true
---

{% for post in site.categories.project %} 
<div class="grid-item">
  <a href="{{ site.url }}{{ post.url }}">
    <img class="img-over" src="../images/{{ post.image.thumb }}" alt="" title="" />
    <div class="after">
      <span><i class="fa fa-search-plus"></i></span>
    </div>
  </a>
  <div class="project-title">
    <p>{{ post.title }}</p>
  </div>
</div>
{% endfor %}