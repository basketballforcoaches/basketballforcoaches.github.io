---
layout: default
title: Offensive Systems -v1 -  Shorts into Pistols
permalink: /systems/v1/short_into_pistols
---

<h2>Teaching Point Videos for *{{ page.title }}*</h2>


## Section 1 - using liquid template
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



## Section 2 - iframe with long id , but no template
  {% for video in site.data.videos %}
    {% if video.teachingPoints %}
      <li>
        <ul>
          {% for point in video.teachingPoints %}
            <li>
              <strong>Teaching Point: {{ point.name }}</strong>: {{ point.description }}. Duration: {{ point.duration }}<br>
              <iframe id="video-{{ video.id }}-{{ point.start }}-{{ point.end }}" width="448" height="252"
                src="https://www.youtube.com/embed/{{ video.id }}?start={{ point.start }}&end={{ point.end }}"
                frameborder="1"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen>
              </iframe>
              <button onclick="resetVideo('video-{{ video.id }}-{{ point.start }}-{{ point.end }}')">🔁 Reset Video</button>
            </li>
            <br>
          {% endfor %}
        </ul>
        <div style="font-size: 0.5em; margin-top: 10px;">
          <p><strong>Video Credit, with Thanks: </strong> {{ video.title }} - Description:{{ video.description }}</p>
        </div>
      </li>
    {% endif %}
  {% endfor %}
</ul>

## Section 3 - iframe, no id, no template

{% for video in site.data.videos %}
  {% if video.teachingPoints %}
    Teaching Points:
        {% for point in video.teachingPoints %}
          {{ point.name }}: {{ point.description }}
            <iframe width="560" height="315" src="https://www.youtube.com/embed/{{ video.id }}?start={{ point.start }}&end={{ point.end }}" title="Basketball For Coaches" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen> </iframe>
        Duration: {{ point.duration }}
        {% endfor %} 
  {% endif %}
{% endfor %} 

## Section 4 - hard coded iframe
Manual code -
<iframe width="560" height="315" src="https://www.youtube.com/embed/wz8sXiNjoSs?start=2477&end=2487" title="Basketball For Coaches" frameborder="15" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Reset Video
Manual code - bk!
<iframe width="560" height="315" src="https://www.youtube.com/embed/wz8sXiNjoSs?si=701MtYzVVNf-lRpJ&start=2477&end=2487" title="Basketball For Coaches" frameborder="15" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Reset Video

🔁 Reset Video - object not page
 <button onclick="resetVideo('video-{{ video.id }}-{{ point.start }}-{{ point.end }}')">🔁 Reset Video</button>


<script>
  function resetVideo(id) {
    const iframe = document.getElementById(id);
    const src = iframe.src;
    iframe.src = src;
  }
</script>