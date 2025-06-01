---
layout: default
title: test
permalink: /test
---

# 🏀 *{{ page.title }}*

<ul>
  {% for video in site.data.videos %}
    {% if video.teachingPoints %}
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
    {% endif %}
  {% endfor %}
</ul>


## Test - no id
<ul>
  {% for video in site.data.videos %}
    {% if video.teachingPoints %}
      {% for point in video.teachingPoints %}
        {% include teaching-point.html
          name=point.name
          description=point.description
          start=point.start
          end=point.end
          duration=point.duration
        %}
      {% endfor %}
    {% endif %}
  {% endfor %}
</ul>