---
layout: post
title: "Blog"
---

<style>
.tab-buttons {
  margin-bottom: 20px;
  text-align: left;
  flex-wrap: wrap;
  display: flex;
  gap: 5px;
}
.tab-buttons button {
  padding: 10px 20px;
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

{% comment %}Collect unique years and counts from posts{% endcomment %}
{% assign years = "" %}
{% for post in site.posts %}
  {% assign post_year = post.date | date: '%Y' %}
  {% unless years contains post_year %}
    {% if years == "" %}
      {% assign years = post_year %}
    {% else %}
      {% assign years = years | append: "," | append: post_year %}
    {% endif %}
  {% endunless %}
{% endfor %}
{% assign year_list = years | split: "," %}

<div class="tab-buttons">
  {% for year in year_list %}
    {% assign count = 0 %}
    {% for post in site.posts %}
      {% assign post_year = post.date | date: '%Y' %}
      {% if post_year == year %}
        {% assign count = count | plus: 1 %}
      {% endif %}
    {% endfor %}
    <button class="tab-button" onclick="showTab('blog-{{ year }}')">{{ year }} ({{ count }})</button>
  {% endfor %}
</div>

{% for year in year_list %}
<div id="blog-{{ year }}" class="tab-content">
  <h2>{{ year }}</h2>
  {% for post in site.posts %}
    {% assign post_year = post.date | date: '%Y' %}
    {% if post_year == year %}
      <article class="post">
        <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
        <time>{{ post.date | date: '%B %-d, %Y' }}</time>
      </article>
    {% endif %}
  {% endfor %}
</div>
{% endfor %}

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
  var firstButton = document.querySelector('.tab-button');
  if (firstButton) firstButton.click();
});
</script>
