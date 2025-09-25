---
layout: default
title: "DefCodex Blog"
subtitle: "High-quality coding tutorials, programming tips & developer insights"
---

<!-- Modern counter badge styles (scoped for this page) -->
<style>
  .counter-wrap { display:flex; justify-content:center; margin:.5rem 0 1rem; }
  .counter-pill {
    display:inline-flex; align-items:center; gap:.4rem;
    padding:.25rem .6rem; border:1px solid var(--border-color, #e5e7eb);
    border-radius:999px; background:var(--pill-bg, rgba(0,0,0,.04));
    font-size:.875rem; line-height:1.25rem;
  }
  .counter-pill svg { width:1rem; height:1rem; opacity:.75; flex:0 0 auto; }
  @media (prefers-color-scheme: dark) {
    .counter-pill { border-color: rgba(255,255,255,.18); background: rgba(255,255,255,.06); }
  }

  .posts-list { list-style:none; padding-left:0; }
  .posts-list li { margin:.5rem 0; display:flex; align-items:center; gap:.5rem; flex-wrap:wrap; }
  .posts-list small { color:var(--muted, #6b7280); }
</style>

<!-- hits.sh-only counter helper (increments via SVG beacon, then reads JSON) -->
<script>
  window.fetchCounter = async function ({ namespace, key }) {
    const fmt = (n) => new Intl.NumberFormat().format(n);

    // Normalize key: trim leading/trailing slashes; root -> 'home'
    const normKey = (key || 'home').replace(/^\/+|\/+$/g, '') || 'home';

    // Build hits.sh path safely: encode each segment, keep slashes between
    const segments = normKey.split('/').filter(Boolean);
    const path = [namespace, ...segments].map(encodeURIComponent).join('/');

    // 1) increment via invisible SVG beacon
    try {
      const img = new Image();
      img.referrerPolicy = 'no-referrer';
      img.decoding = 'async';
      img.src = `https://hits.sh/${path}.svg?style=flat&label=hits&_=${Date.now()}`;
    } catch (_) {}

    // 2) read value via JSON
    try {
      const r = await fetch(`https://hits.sh/${path}.json?secure=1&_=${Date.now()}`, { cache: 'no-store' });
      if (r.ok) {
        const d = await r.json();
        if (typeof d?.hits === 'number') return fmt(d.hits);
      }
    } catch (_) {}

    return '—';
  };
</script>

<p style="text-align:center;">
  <strong>Welcome to DefCodex Blog!</strong>
</p>

<!-- Home page view counter -->
<div class="counter-wrap" aria-live="polite">
  <span class="counter-pill" title="Home views">
    <svg viewBox="0 0 24 24" fill="none" aria-hidden="true">
      <path d="M1.5 12s3.5-7.5 10.5-7.5S22.5 12 22.5 12s-3.5 7.5-10.5 7.5S1.5 12 1.5 12Z" stroke="currentColor"/>
      <circle cx="12" cy="12" r="3.5" stroke="currentColor" />
    </svg>
    <strong id="home-views">—</strong>
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

    <!-- Per-post view badge on the list -->
    <span class="counter-pill" data-key="{{ post.url }}" title="Views" aria-live="polite">
      <svg viewBox="0 0 24 24" fill="none" aria-hidden="true">
        <path d="M1.5 12s3.5-7.5 10.5-7.5S22.5 12 22.5 12s-3.5 7.5-10.5 7.5S1.5 12 1.5 12Z" stroke="currentColor"/>
        <circle cx="12" cy="12" r="3.5" stroke="currentColor" />
      </svg>
      <strong>—</strong>
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

<!-- Counters script (home + per-post list) -->
<script>
  (function () {
    // Namespace from _config.yml (fallback to default if missing)
    const ns  = '{{ site.counter.namespace | default: "defcodex.github.io" }}';

    // Normalize Jekyll URLs to avoid duplicate keys (strip trailing slash; root -> 'home')
    const normalize = (p) => {
      const s = (p || '/').replace(/\/+$/, '');
      return s === '' || s === '/' ? 'home' : s;
    };

    // 1) Home page counter
    (function homeCounter() {
      const el  = document.getElementById('home-views');
      const key = 'home';
      window.fetchCounter({ namespace: ns, key })
        .then(val => { if (el) el.textContent = val; });
    })();

    // 2) Per-post counters shown in the latest list
    (function listCounters() {
      const pills = document.querySelectorAll('.counter-pill[data-key]');
      if (!pills.length) return;

      pills.forEach(pill => {
        const key = normalize(pill.getAttribute('data-key'));
        const strong = pill.querySelector('strong');

        window.fetchCounter({ namespace: ns, key })
          .then(val => { if (strong) strong.textContent = val; });
      });
    })();
  })();
</script>
