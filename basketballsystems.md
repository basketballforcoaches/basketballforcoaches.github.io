---
layout: default
title: Offensive Systems - Shorts into Pistols
permalink: /systems/
---

# 🏀 *{{ page.title }}*

This page contains curated video snippets along with descriptions and key teaching points.  
By isolating these examples, coaches can:

- Break down key concepts with real-game footage.
- Target explicit teaching moments for deeper understanding.
- Use this as a reference to refine drills or design your own.

🎯 *Use this page as a tool to sharpen your coaching craft and build intentional practice plans.*

<h2>Teaching Point Videos for *{{ page.title }}*</h2>

<ul>
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

<h1> About "Shorts into Pistols" </h1>

In basketball terminology, especially in the context of modern offenses and coaching lingo, “shorts”, “pistols”, and “shorts into pistols” refer to specific offensive actions or sequences—typically used in youth, high school, or elite coaching programs.

## 1. Shorts
“Shorts” usually refers to a short roll action in a pick-and-roll scenario.
    - Instead of rolling all the way to the rim, the screener pops or stops around elbow area.
    - The ball handler hits them early ("short") to avoid pressure or traps.
    - This is useful when the defense traps or hard-hedges the ball screen.

## 2. Pistols
“Pistols” is a two-player game on one side of the floor that typically includes:
    - A dribble handoff (DHO) or a ball screen, and
    - An off-ball shooter or cutter moving at the same time.
    - Often run early in transition with one guard on the wing and another trailing.

## 3. Shorts into Pistols - combo:
    - The play starts with a short roll or pass to the short roll man (Shorts), and
    - Then immediately flows into a pistol action (DHO or pick-and-roll on the side).

### Example:
    - See teaching point videos above.
    - Guard comes off a ball screen and is blitzed.
    - They pass to the short roller.
    - The short roller quickly hands off to a wing coming up (or sets a screen for a wing), triggering a pistol action.

### Why Use It?
    - It breaks traps and keeps the offense flowing.
    - It creates multiple reads and decisions for the defense.
    - It’s great for ball movement and playing through pressure.

<script>
  function resetVideo(id) {
    const iframe = document.getElementById(id);
    const src = iframe.src;
    iframe.src = src;
  }
</script>