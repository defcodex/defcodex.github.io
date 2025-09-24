---
layout: default
title: "Blog"
permalink: /blog/
---

# Blog

{% if site.posts and site.posts.size > 0 %}
<ul>
  {%- for post in site.posts -%}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <small> — {{ post.date | date: "%b %d, %Y" }}</small>
  </li>
  {%- endfor -%}
</ul>
{% else %}
<p>No posts published yet. Stay tuned!</p>
{% endif %}

---

<p>
  Prefer RSS? <a href="{{ '/rss/' | relative_url }}">Subscribe here</a>.
</p>
