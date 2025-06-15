---
layout: default
title: Teaching Points
permalink: /teaching-points/
---

<h1>🎥 Teaching Points by Video</h1>
<p>Total teaching points: {{ site.data.teaching-points-by-id | size }}</p>

<div class="container my-4">
  {% for pair in site.data.teaching-points-by-id %}
    {% assign tp = pair[1] %}
    
    <div class="row mb-5 align-items-start">
      <div class="col-md-6">
        <div class="ratio ratio-16x9">
          <iframe
            id="video-{{ tp.video }}-{{ tp.startTime }}-{{ tp.endTime }}"
            src="https://www.youtube.com/embed/{{ tp.video }}?start={{ tp.startTime }}&end={{ tp.endTime }}"
            title="{{ tp.teachingPoint_name }}"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen>
          </iframe>
        </div>
      </div>
      <div class="col-md-6">
        <h5>{{ tp.teachingPoint_id }} – {{ tp.teachingPoint_name }}</h5>
        <p><strong>Duration:</strong> {{ tp.duration }}</p>
        {% if tp.teachingPoint_short_description %}
          <p>{{ tp.teachingPoint_short_description }}</p>
        {% endif %}
        <button class="btn btn-outline-secondary btn-sm"
                onclick="resetVideo('video-{{ tp.video }}-{{ tp.startTime }}-{{ tp.endTime }}')">🔁 Reset Video</button>
      </div>
    </div>
  {% endfor %}
</div>

<script>
function resetVideo(id) {
  const iframe = document.getElementById(id);
  if (iframe) {
    const src = iframe.src;
    iframe.src = src;
  }
}
</script>
