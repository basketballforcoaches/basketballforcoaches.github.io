---
layout: default
title: test
permalink: /test
---

# 🏀 *{{ page.title }}*

  {% for video in site.data.videos %}
    {% if video.teachingPoints %}

## Test
<ul>
  {% for video in site.data.videos %}
    {% for point in video.teachingPoints %}
      {% include teaching-point.html
        name=point.name
        description=point.description
        video_id=video.id
        start=point.start
        end=point.end
        duration=point.duration
      %}
    {% endfor %}
  {% endfor %}
</ul>


## Test - no id
<ul>
  {% for video in site.data.videos %}
    {% for point in video.teachingPoints %}
      {% include teaching-point.html
        name=point.name
        description=point.description
        start=point.start
        end=point.end
        duration=point.duration
      %}
    {% endfor %}
  {% endfor %}
</ul>