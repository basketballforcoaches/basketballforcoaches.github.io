---
layout: default
title: Teaching Points
permalink: /teaching-points/
---

<h1>🎥 Teaching Points by Video</h1> 
<p>Source: <code>teachingPoints</code> array in each video</p>

<p>Total videos in data: {{ site.data.teaching_points | size }}</p>

<ul>
  {% for video in site.data.teaching_points %}
    {% assign tps = video.teachingPoints %}
    {% if tps and tps.size > 0 %}
      <div style="margin-bottom: 3em;">

        <ul>
          {% for tp in tps %}
            <li style="margin-bottom: 1em;">
              <strong>{{ tp.teachingPoint_id }} {{ tp.teachingPoint_name }}</strong>: {{ tp.teachingPoint_short_description }}<br>
              <iframe
                id="video-{{ video.videoId }}-{{ tp.startTime }}-{{ tp.endTime }}"
                width="448"
                height="252"
                src="https://www.youtube.com/embed/{{ video.videoId }}?start={{ tp.startTime }}&end={{ tp.endTime }}"
                frameborder="0"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen>
              </iframe>
              <br>
              <button onclick="resetVideo('video-{{ video.videoId }}-{{ tp.startTime }}-{{ tp.endTime }}')">🔁 Reset Video</button>
            </li>
          {% endfor %}
        </ul>
      </div>
    {% endif %}
  {% endfor %}
</ul>

<script>
function resetVideo(id) {
  const iframe = document.getElementById(id);
  if (iframe) {
    const src = iframe.src;
    iframe.src = src;
  }
}
</script>