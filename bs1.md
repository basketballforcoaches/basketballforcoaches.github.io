---
layout: default
title: Basketball Systems - Shorts into Pistols - v1
permalink: /systems - v1/
---

<h1>{{ page.title }}</h1>

<p>
  This page contains snippets from videos with a description and key teaching points.
  Isolating these examples helps coaches break down critical moments with live footage, targeting explicit teaching examples.
</p>

<p>
  Use this as a resource to hone your craft, customise drills, or refer back when planning or teaching.
</p>

<h2>Offensive System 1: Shorts into Pistols</h2>

<p>
  In modern basketball terminology, especially in youth, high school, or elite coaching contexts, “shorts”, “pistols”, and “shorts into pistols” describe specific offensive sequences designed to break down defenses and maintain fluid offense.
</p>

<h3>1. Shorts</h3>
<ul>
  <li>The screener performs a short roll — stopping near the elbow instead of rolling to the rim.</li>
  <li>The ball handler passes early to avoid pressure or traps.</li>
  <li>This is effective against hard hedges or traps on the pick-and-roll.</li>
</ul>

<h3>2. Pistols</h3>
<ul>
  <li>A two-player game on one side of the floor (wing and trail guard).</li>
  <li>Involves a dribble handoff (DHO) or ball screen.</li>
  <li>Often used in early transition to create quick offense.</li>
</ul>

<h3>3. Shorts into Pistols (Combo Action)</h3>
<ul>
  <li>Starts with a pass to the short roller.</li>
  <li>Then flows into a pistol action — either a DHO or quick screen for a wing.</li>
</ul>

<h4>Example</h4>
<ul>
  <li>See video clip below.</li>
  <li>Guard comes off a ball screen and is blitzed.</li>
  <li>Pass goes to the short roller.</li>
  <li>Short roller executes a handoff or sets a screen for a trailing wing — triggering the pistol action.</li>
</ul>

<h4>Why Use It?</h4>
<ul>
  <li>Disrupts traps and maintains offensive flow.</li>
  <li>Creates multiple options and reads for the offense.</li>
  <li>Improves ball movement and decision-making under pressure.</li>
</ul>

<h2>Teaching Point Videos</h2>

<ul>
  {% for video in site.data.videos %}
    {% if video.teachingPoints %}
      <li>
        <ul>
          {% for point in video.teachingPoints %}
            <li>
              <strong>{{ point.name }}</strong>: {{ point.description }}<br>
              <iframe id="video-{{ video.id }}-{{ point.start }}-{{ point.end }}" width="560" height="315"
                src="https://www.youtube.com/embed/{{ video.id }}?start={{ point.start }}&end={{ point.end }}"
                title="Basketball For Coaches"
                frameborder="0"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen>
              </iframe>
              <p>Duration: {{ point.duration }}</p>
              <button onclick="resetVideo('video-{{ video.id }}-{{ point.start }}-{{ point.end }}')">🔁 Reset Video</button>
            </li>
          {% endfor %}
        </ul>
        <div style="font-size: 0.8em; margin-top: 10px;">
          <h3>Video Credit - with Thanks!</h3>
          <h3>Thnks{{ video.title }}</h3>
          <p><strong>Description:</strong> {{ video.description }}</p>
        </div>
      </li>
    {% endif %}
  {% endfor %}
</ul>

<script>
  function resetVideo(id) {
    const iframe = document.getElementById(id);
    const src = iframe.src;
    iframe.src = src;
  }
</script>