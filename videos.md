---
layout: default
title: Basketball Coaching Videos
permalink: /videos/
---

<h1>{{ page.title }}</h1>

<ul>
  {% for video in site.data.videos %}
    <li>
      <h2><a href="{{ video.url }}">{{ video.title }}</a></h2>
      <p>{{ video.description }}</p>
      <p><strong>Upload Date:</strong> {{ video.uploadDate }}</p>
      {% if video.teachingPoints %}
        <h3>Teaching Points:</h3>
        <ul>
          {% for point in video.teachingPoints %}
            <li>
              <strong>{{ point.name }}</strong>: {{ point.description }}<br>
              <a href="{{ point.startTime }}">Watch from here</a> (Duration: {{ point.duration }})
            </li>
          {% endfor %}
        </ul>
      {% endif %}
    </li>
  {% endfor %}
</ul>
