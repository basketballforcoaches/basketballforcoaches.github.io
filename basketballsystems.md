---
layout: default
title: Basket Ball Systems
permalink: /systems/
---

<h1>{{ page.title }}</h1>
<p>
This page contains snippets from videos with a description and key teaching points.

Isolating these examples helps coaches break down key teaching points with live video examples, targeting explicit teaching point examples.

You can use this as a resource to hone your craft, customise your own drills or a point of reference.</p>

<ul>
  {% for video in site.data.videos %}
    <li>
        {% if video.teachingPoints %}
        <h2>Basketball Systems</h2>
        <h3>Teaching Points:</h3>
        <ul>
        {% for point in video.teachingPoints %}
        <li>
            <strong>{{ point.name }}</strong>: {{ point.description }}<br>
            <iframe width="560" height="315"
            src="https://www.youtube.com/embed/{{ video.id }}?start={{ point.start }}&end={{ point.end }}" title="Basketball For Coaches" 
            frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen>
            </iframe>
            <p>Duration: {{ point.duration }}</p>
        </li>
        {% endfor %}
        </ul>
      {% endif %}
    </li>
  {% endfor %}
</ul>

<a href="{{ page.url }}">Reset Video</a>

<a href="#" onclick="resetVideo('video-{{ video.id }}-{{ point.start }}-{{ point.end }}')">🔁 Reset Video - object</a>

<script>
  function resetVideo(id) {
    const iframe = document.getElementById(id);
    const src = iframe.src;
    iframe.src = src;
  }
</script>