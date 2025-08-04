---
layout: default
title: Practice Plans
permalink: /practice/
---

<h1>🏀 Practice Plans</h1>
<p>Select a plan from the dropdown to view the full session breakdown.</p>

<label for="plan-select" class="form-label">Choose a Practice Plan:</label>
<select id="plan-select" class="form-select mb-4" style="max-width: 400px;"></select>

<div class="accordion" id="practicePlan"></div>

<p class="mt-4">🎯 For video examples, visit the <a href="/basketball-concepts/">Basketball Concepts</a> page and filter by concept name.</p>

<script>
  const practicePlans = {{ site.data["practice-plans"] | jsonify }};
  const planSelect = document.getElementById("plan-select");
  const container = document.getElementById("practicePlan");

  function resetVideo(id) {
    const iframe = document.getElementById(id);
    if (iframe) iframe.src = iframe.src;
  }

  function renderPracticePlan(plan) {
    container.innerHTML = "";

    plan.segments.forEach((segment, index) => {
      const teachingPointsHTML = (segment.teaching_points || []).map(tp => `
        <div class="row mb-4 align-items-start">
          <div class="col-md-6">
            <div class="ratio ratio-16x9">
              <iframe id="video-${tp.video}-${tp.startTime}-${tp.endTime}" src="${tp.embed_url}" title="${tp.teachingPoint_name}" allowfullscreen></iframe>
            </div>
          </div>
          <div class="col-md-6">
            <h5>${tp.teachingPoint_id} – ${tp.teachingPoint_name}</h5>
            <p>${tp.teachingPoint_short_description}</p>
            <p><strong>Duration:</strong> ${tp.duration}</p>
            <button class="btn btn-outline-secondary btn-sm" onclick="resetVideo('video-${tp.video}-${tp.startTime}-${tp.endTime}')">🔁 Reset Video</button>
          </div>
        </div>
      `).join("");

      const drillsHTML = (segment.drills || []).map(drill => `
        <div class="card mb-4 border-success">
          <div class="card-body">
            <h5 class="card-title">🛠️ ${drill.title}</h5>
            <p class="card-text"><strong>Description:</strong> ${drill.drillDescription}</p>
            <p class="card-text"><strong>Purpose:</strong> ${drill.purpose || "—"}</p>
            <p class="card-text"><strong>Coaching Points:</strong> ${drill.coachingPoints || "—"}</p>
            ${drill.diagramEmbedUrl_1 ? `
              <div class="ratio ratio-16x9 mb-3">
                <iframe src="${drill.diagramEmbedUrl_1}" title="${drill.title} diagram" allowfullscreen></iframe>
              </div>
            ` : ''}
          </div>
        </div>
      `).join("");

      container.innerHTML += `
        <div class="accordion-item">
          <h2 class="accordion-header" id="heading${index}">
            <button class="accordion-button ${index === 0 ? '' : 'collapsed'}" type="button" data-bs-toggle="collapse" data-bs-target="#collapse${index}" aria-expanded="${index === 0}" aria-controls="collapse${index}">
              ${segment.time_range} – ${segment.title}
            </button>
          </h2>
          <div id="collapse${index}" class="accordion-collapse collapse ${index === 0 ? 'show' : ''}" aria-labelledby="heading${index}" data-bs-parent="#practicePlan">
            <div class="accordion-body">
              <strong>Focus:</strong> ${segment.title}<br>
              <strong>Notes:</strong> ${segment.notes || "—"}<br><br>
              ${teachingPointsHTML}
              ${drillsHTML}
            </div>
          </div>
        </div>
      `;
    });
  }

  function init() {
    if (!practicePlans.length) {
      container.innerHTML = "<p>No practice plans available.</p>";
      return;
    }

    // Populate dropdown
    practicePlans.forEach((plan, index) => {
      const option = document.createElement("option");
      option.value = index;
      option.textContent = `${plan.title} – ${plan.duration_minutes} min`;
      planSelect.appendChild(option);
    });

    renderPracticePlan(practicePlans[0]);

    planSelect.addEventListener("change", (e) => {
      const selected = practicePlans[parseInt(e.target.value)];
      renderPracticePlan(selected);
    });
  }

  window.onload = init;
</script>
