---
layout: post
title: "Blog"
---

<style>
.tab-buttons {
  margin-bottom: 20px;
  text-align: left;
}
.tab-buttons button {
  padding: 10px 20px;
  margin-right: 5px;
  border: none;
  background-color: #f0f0f0;
  cursor: pointer;
}
.tab-buttons button.active {
  background-color: #007bff;
  color: white;
}
.tab-content {
  display: none;
  max-width: 800px;
  margin: 0 auto;
  padding: 0 20px;
}
.tab-content.active {
  display: block;
}
.post {
  margin-bottom: 20px;
}
h2 {
  text-align: left; 
}
</style>

<div class="tab-buttons">
  <button class="tab-button" onclick="showTab('blog-2026-present')">2026-Present</button>
  <button class="tab-button" onclick="showTab('blog-2021-2025')">2021-2025</button>
  <button class="tab-button" onclick="showTab('blog-2016-2020')">2016-2020</button>
</div>

<div id="blog-2026-present" class="tab-content">
  <h2>2026–Present</h2>
  {% for post in site.posts %}
    {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
    {% if year >= '2026' %}
      <article class="post">
        <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
        <time>{{ post.date | date: '%B %-d, %Y' }}</time>
      </article>
    {% endif %}
  {% endfor %}
</div>

<div id="blog-2021-2025" class="tab-content">
  <h2>2021–2025</h2>
  {% for post in site.posts %}
    {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
    {% if year >= '2021' and year <= '2025' %}
      <article class="post">
        <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
        <time>{{ post.date | date: '%B %-d, %Y' }}</time>
      </article>
    {% endif %}
  {% endfor %}
</div>

<div id="blog-2016-2020" class="tab-content">
  <h2>2016–2020</h2>
  {% for post in site.posts %}
    {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
    {% if year >= '2016' and year <= '2020' %}
      <article class="post">
        <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
        <time>{{ post.date | date: '%B %-d, %Y' }}</time>
      </article>
    {% endif %}
  {% endfor %}
</div>

<script>
function showTab(tabId) {
  document.querySelectorAll('.tab-content').forEach(content => {
    content.style.display = 'none';
  });

  document.querySelectorAll('.tab-button').forEach(button => {
    button.classList.remove('active');
  });

  document.getElementById(tabId).style.display = 'block';
  document.querySelector(`button[onclick="showTab('${tabId}')"]`).classList.add('active');
}

document.addEventListener('DOMContentLoaded', function () {
  showTab('blog-2026-present');
});
</script>
