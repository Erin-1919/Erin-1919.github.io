---
layout: page
title: Gallery
gallery_path: "assets/img/academic"
poster_pdfs:
  "poster1": "assets/pdf/CanCH4_Poster_May_2025_EL.pdf"
  "poster2": "assets/pdf/ESRI_poster_Li_2022.pdf"
  "poster3": "assets/pdf/ESRI_poster_Li_2019.pdf"
  # Add more poster PDF links as needed
---

<style>
.tab-buttons {
  margin-bottom: 20px;
  text-align: left;
}

.tab-button {
  padding: 10px 20px;
  margin: 0 5px;
  border: none;
  background-color: #f0f0f0;
  cursor: pointer;
}

.tab-button.active {
  background-color: #007bff;
  color: white;
}

.tab-content {
  display: none;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  padding: 20px;
}

.grid-item {
  width: 100%;
  height: auto;
  object-fit: contain; /* Preserves aspect ratio */
}

.tab-content.active {
  display: block;
}
</style>

<div class="tab-buttons">
  <button class="tab-button active" onclick="showTab('posters')">Conference Posters</button>
  <button class="tab-button" onclick="showTab('highlights')">Highlights</button>
</div>

<div id="posters" class="tab-content active">
{% assign poster_files = site.static_files | where_exp: "file", "file.path contains 'posters'" %}
{% for file in poster_files %}
  {% assign poster_index = forloop.index | prepend: 'poster' %}
  <div class="grid-item">
    <img src="{{ file.path | relative_url }}" 
         alt="Poster {{ forloop.index }}" 
         data-pdf="{{ page.poster_pdfs[poster_index] | relative_url }}" 
         onclick="openPosterPDF(this)">
  </div>
{% endfor %}
</div>

<div id="highlights" class="tab-content">
{% include gallery.html gallery_path="assets/img/academic/highlights" disable_links=false %}
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

function openPosterPDF(imgElement) {
  const pdfUrl = imgElement.getAttribute('data-pdf');
  if (pdfUrl) {
    window.open(pdfUrl, '_blank');
  }
}


