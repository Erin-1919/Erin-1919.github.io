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

{% assign years = "" %}
{% for post in site.posts %}
  {% assign y = post.date | date: "%Y" %}
  {% assign years = years | append: y | append: "," %}
{% endfor %}

{% assign years = years | split: "," | uniq | sort %}
{% assign years_desc = years | reverse %}

{% assign max_year = years_desc[0] | plus: 0 %}
{% assign latest_start = max_year | divided_by: 5 | times: 5 %}

{% assign groups = "" %}

{% for y in years_desc %}
  {% assign year_num = y | plus: 0 %}
  {% assign start_year = year_num | divided_by: 5 | times: 5 %}
  {% assign end_year = start_year | plus: 4 %}

  {% if start_year == latest_start %}
    {% assign label = start_year | append: "-Present" %}
  {% else %}
    {% assign label = start_year | append: "-" | append: end_year %}
  {% endif %}

  {% assign groups = groups | append: label | append: "," %}
{% endfor %}

{% assign groups = groups | split: "," | uniq %}
{% assign default_group = groups[0] %}

<div class="tab-buttons">
  {% for g in groups %}
    {% assign tab_id = "blog-" | append: g %}
    <button class="tab-button" onclick="showTab('{{ tab_id }}')">{{ g }}</button>
  {% endfor %}
</div>

{% for g in groups %}
  {% assign tab_id = "blog-" | append: g %}

  {% if g contains "Present" %}
    {% assign start_year_str = g | replace: "-Present", "" %}
    {% assign start_year = start_year_str | plus: 0 %}

    <div id="{{ tab_id }}" class="tab-content">
      <h2>{{ start_year }}–Present</h2>

      {% for post in site.posts %}
        {% assign post_year = post.date | date: "%Y" | plus: 0 %}
        {% if post_year >= start_year %}
          <article class="post">
            <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
            <time>{{ post.date | date: "%B %-d, %Y" }}</time>
          </article>
        {% endif %}
      {% endfor %}
    </div>

  {% else %}
    {% assign parts = g | split: "-" %}
    {% assign start_year = parts[0] | plus: 0 %}
    {% assign end_year = parts[1] | plus: 0 %}

    <div id="{{ tab_id }}" class="tab-content">
      <h2>{{ start_year }}–{{ end_year }}</h2>

      {% for post in site.posts %}
        {% assign post_year = post.date | date: "%Y" | plus: 0 %}
        {% if post_year >= start_year and post_year <= end_year %}
          <article class="post">
            <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
            <time>{{ post.date | date: "%B %-d, %Y" }}</time>
          </article>
        {% endif %}
      {% endfor %}
    </div>
  {% endif %}
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
  showTab("blog-{{ default_group }}");
});
</script>
