---
layout: default
title: Teaching Points
permalink: /teaching-points/
---
<iframe width="420" height="236" src="https://www.youtube.com/embed/wz8sXiNjoSs?start=2477&end=2487" frameborder="0" allowfullscreen></iframe>
<h1>🎥 Teaching Points by Video</h1> 
<p>Source: <code>teachingPoints</code> array in each video</p>

<p>Total videos in data: {{ site.data.teaching_points | size }}</p>

{% for video in site.data.teaching_points %}
  {% assign tps = video["teachingPoints"] %}
  {% if tps and tps.size > 0 %}
    <div style="margin-bottom: 3em; padding: 1em; border-bottom: 1px solid #ccc;">
      <h2>{{ video.title }}</h2>
      <p>
        <a href="{{ video.url }}" target="_blank">{{ video.url }}</a><br>
        <strong>Upload Date:</strong> {{ video.uploadDate }}
      </p>

      <ul>
        {% for tp in tps %}
          {% include teaching-points.html tp=tp %}
        {% endfor %}
      </ul>
    </div>
  {% endif %}
{% endfor %}

<!-- Debug JSON output at bottom (can be removed) -->
<pre style="font-size: 0.75em; background: #f8f8f8; padding: 1em;">
{{ site.data.teaching_points | jsonify }}
</pre>