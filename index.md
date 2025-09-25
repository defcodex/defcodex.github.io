---
layout: default
title: "DefCodex Blog"
subtitle: "High-quality coding tutorials, programming tips & developer insights"
---

<style>
  .counter-wrap { display:flex; justify-content:center; margin:.5rem 0 1rem; }
  .counter-pill {
    display:inline-flex; align-items:center; gap:.4rem;
    padding:.25rem .6rem; border:1px solid var(--border-color, #e5e7eb);
    border-radius:999px; background:var(--pill-bg, rgba(0,0,0,.04));
    font-size:.875rem; line-height:1.25rem;
  }
  .counter-pill svg { width:1rem; height:1rem; opacity:.75; flex:0 0 auto; }
  .hit-badge { height:20px; vertical-align:middle; }
  @media (prefers-color-scheme: dark) {
    .counter-pill { border-color: rgba(255,255,255,.18); background: rgba(255,255,255,.06); }
  }
  .posts-list { list-style:none; padding-left:0; }
  .posts-list li { margin:.5rem 0; display:flex; align-items:center; gap:.5rem; flex-wrap:wrap; }
  .posts-list small { color:var(--muted, #6b7280); }
</style>

<p style="text-align:center;">
  <strong>Welcome to DefCodex Blog!</strong>
</p>

<!-- Home page view counter (root key 'home') -->
<div class="counter-wrap" aria-live="polite">
  <span class="counter-pill" title="Home views">
    <svg viewBox="0 0 24 24" fill="none" aria-hidden="true">
      <path d="M1.5 12s3.5-7.5 10.5-7.5S22.5 12 22.5 12s-3.5 7.5-10.5 7.5S1.5 12 1.5 12Z" stroke="currentColor"/>
      <circle cx="12" cy="12" r="3.5" stroke="currentColor" />
    </svg>
    <img
      class="hit-badge"
      src="https://hits.sh/{{ site.counter.namespace }}/home.svg?style=flat&label=home"
      alt="home views counter" loading="eager" decoding="async">
  </span>
</div>

<p>
  This is your go-to destination for high-quality coding tutorials, programming tips,
  software development best practices, and technology news covering Python, JavaScript,
  Java, Go, and frameworks like React, Django, and .NET. Whether you're a beginner
  or an experienced engineer, you'll find valuable resources to improve your skills
  and stay ahead in the ever-evolving tech world.
</p>

## Latest Posts

{% if site.posts and site.posts.size > 0 %}
<ul class="posts-list">
  {%- for post in site.posts limit:5 -%}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <small> — {{ post.date | date: "%b %d, %Y" }}</small>
    <!-- Per-post view badge (path = namespace + post.url) -->
    <span class="counter-pill" title="Views" aria-live="polite">
      <svg viewBox="0 0 24 24" fill="none" aria-hidden="true">
        <path d="M1.5 12s3.5-7.5 10.5-7.5S22.5 12 22.5 12s-3.5 7.5-10.5 7.5S1.5 12 1.5 12Z" stroke="currentColor"/>
        <circle cx="12" cy="12" r="3.5" stroke="currentColor" />
      </svg>
      <img
        class="hit-badge"
        src="https://hits.sh/{{ site.counter.namespace }}{{ post.url }}.svg?style=flat&label=views"
        alt="post views counter" loading="eager" decoding="async">
    </span>
  </li>
  {%- endfor -%}
</ul>
<p><a href="{{ '/blog/' | relative_url }}">View all posts →</a></p>
{% else %}
<p>No posts published yet. Stay tuned!</p>
{% endif %}

## About DefCodex

<p>
  DefCodex is run by passionate developers who love sharing knowledge. Our mission is to provide clear, practical
  tutorials and insights to help developers of all levels grow.
</p>

<hr />

<p>
  Prefer RSS? <a href="{{ '/rss/' | relative_url }}">Subscribe to the feed</a>.
</p>
