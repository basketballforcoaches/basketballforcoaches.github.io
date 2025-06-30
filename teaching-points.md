---
layout: default
title: Teaching Points
permalink: /teaching-points/
---

<h1>🎥 Teaching Points by Video</h1>
<p>Total teaching points: {{ site.data.teaching-points-by-id | size }}</p>

<div id="teaching-point-list" class="container my-4"></div>
<div id="lazy-sentinel" style="height: 50px;"></div>

<script>
  // Inject all teaching point data into JS
  const allTPs = Object.values({{ site.data["teaching-points-by-id"] | jsonify | safe }});
  const container = document.getElementById("teaching-point-list");
  const sentinel = document.getElementById("lazy-sentinel");

  let currentIndex = 0;
  const batchSize = 10;

  function resetVideo(id) {
  const oldIframe = document.getElementById(id);
  if (oldIframe) {
    const newIframe = oldIframe.cloneNode(true);
    oldIframe.parentNode.replaceChild(newIframe, oldIframe);
   }
  }

  function renderNextBatch() {
    const nextBatch = allTPs.slice(currentIndex, currentIndex + batchSize);
    nextBatch.forEach(tp => {
      const iframeId = `video-${tp.video}-${tp.startTime}-${tp.endTime}`;
      const row = document.createElement("div");
      row.className = "row mb-5 align-items-start";
      row.innerHTML = `
        <div class="col-md-6">
          <div class="ratio ratio-16x9">
            <iframe
              id="${iframeId}"
              src="https://www.youtube.com/embed/${tp.video}?start=${tp.startTime}&end=${tp.endTime}"
              title="${tp.teachingPoint_name}"
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
              allowfullscreen>
            </iframe>
          </div>
        </div>
        <div class="col-md-6">
          <h5>${tp.teachingPoint_id} – ${tp.teachingPoint_name}</h5>
          <p><strong>Duration:</strong> ${tp.duration}</p>
          ${tp.teachingPoint_short_description ? `<p>${tp.teachingPoint_short_description}</p>` : ""}
          <button class="btn btn-outline-secondary btn-sm"
                  onclick="resetVideo('${iframeId}')">🔁 Reset Video</button>
        </div>
      `;
      container.appendChild(row);
    });
    currentIndex += batchSize;
  }

  const observer = new IntersectionObserver(entries => {
    if (entries[0].isIntersecting) {
      renderNextBatch();
    }
  });

  document.addEventListener("DOMContentLoaded", () => {
    renderNextBatch();
    observer.observe(sentinel);
  });
</script>
