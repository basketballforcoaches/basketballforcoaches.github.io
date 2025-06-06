---
layout: default
title: Teaching Points
permalink: /teaching-points/
---

<h1>🎥 Teaching Points by Video</h1>
<p>Source: <code>teachingPoints</code> array in each video</p>

<p>Total videos in data: {{ site.data.teaching_points | size }}</p>

<div class="container my-4">
  {% for video in site.data.teaching_points %}
    {% assign tps = video.teachingPoints %}
    {% if tps and tps.size > 0 %}
      {% for tp in tps %}
        <div class="row mb-5 align-items-start">
          <div class="col-md-6">
            <div class="ratio ratio-16x9">
              <iframe
                id="video-{{ video.videoId }}-{{ tp.startTime }}-{{ tp.endTime }}"
                src="https://www.youtube.com/embed/{{ video.videoId }}?start={{ tp.startTime }}&end={{ tp.endTime }}"
                title="{{ tp.teachingPoint_name }}"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen>
              </iframe>
            </div>
          </div>
          <div class="col-md-6">
            <h5>{{ tp.teachingPoint_id }} – {{ tp.teachingPoint_name }}</h5>
            <p>{{ tp.teachingPoint_short_description }}</p>
            <p><strong>Duration:</strong> {{ tp.duration }}</p>
            <button class="btn btn-outline-secondary btn-sm"
                    onclick="resetVideo('video-{{ video.videoId }}-{{ tp.startTime }}-{{ tp.endTime }}')">🔁 Reset Video</button>
          </div>
        </div>
      {% endfor %}
    {% endif %}
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
