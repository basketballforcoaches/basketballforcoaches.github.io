---
layout: default
title: Basket Ball Systems - Shorts into Pistols
permalink: /systems/
---

<h1>{{ page.title }}</h1>
<p>
This page contains snippets from videos with a description and key teaching points.

Isolating these examples helps coaches break down key teaching points with live video examples, targeting explicit teaching point examples.

You can use this as a resource to hone your craft, customise your own drills or a point of reference.</p>

<h1> Offensive System 1 - Shorts into Pistols </h1>

In basketball terminology, especially in the context of modern offenses and coaching lingo, “shorts”, “pistols”, and “shorts into pistols” refer to specific offensive actions or sequences—typically used in youth, high school, or elite coaching programs.

1. Shorts
“Shorts” usually refers to a short roll action in a pick-and-roll scenario.
    - Instead of rolling all the way to the rim, the screener pops or stops around elbow area.
    - The ball handler hits them early ("short") to avoid pressure or traps.
    - This is useful when the defense traps or hard-hedges the ball screen.

2. Pistols
“Pistols” is a two-player game on one side of the floor that typically includes:
    - A dribble handoff (DHO) or a ball screen, and
    - An off-ball shooter or cutter moving at the same time.
    - Often run early in transition with one guard on the wing and another trailing.

3. Shorts into Pistols - combo:
    - The play starts with a short roll or pass to the short roll man (Shorts), and
    - Then immediately flows into a pistol action (DHO or pick-and-roll on the side).

Example:
    - See teaching point video below.
    - Guard comes off a ball screen and is blitzed.
    - They pass to the short roller.
    - The short roller quickly hands off to a wing coming up (or sets a screen for a wing), triggering a pistol action.

Why Use It?
    - It breaks traps and keeps the offense flowing.
    - It creates multiple reads and decisions for the defense.
    - It’s great for ball movement and playing through pressure.

<ul>
  {% for video in site.data.videos %}
    <li>
        {% if video.teachingPoints %}
        <h2>Basketball System - Teaching Points:</h2>
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