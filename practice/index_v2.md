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

<p class="mt-4">
  🎯 For video examples, visit the <a href="/basketball-concepts/">Basketball Concepts</a> page and filter by concept name.
</p>

<script>
  // Data from _data/practice-plans.json
  const practicePlans = {{ site.data["practice-plans"] | jsonify }};

  const planSelect = document.getElementById("plan-select");
  const container  = document.getElementById("practicePlan");

  // Small helper to safely show text (prevents accidental HTML rendering)
  const esc = (s) => String(s ?? "").replace(/[&<>"']/g, m => (
    { "&":"&amp;","<":"&lt;",">":"&gt;","\"":"&quot;","'":"&#39;" }[m]
  ));

  function resetVideo(id) {
    const iframe = document.getElementById(id);
    if (iframe) iframe.src = iframe.src;
  }

  function renderPracticePlan(plan) {
    container.innerHTML = "";

    // Sort segments by "order" if present, otherwise keep original
    const segments = [...(plan.segments || [])].sort((a, b) => {
      const ao = a.order ?? 0, bo = b.order ?? 0;
      return ao - bo;
    });

    segments.forEach((segment, index) => {
      const tpList = (segment.teaching_points || []).map(tp => {
        const vidId = `video-${esc(tp.video)}-${esc(tp.startTime)}-${esc(tp.endTime)}`;
        return `
          <div class="row mb-4 align-items-start">
            <div class="col-md-6">
              <div class="ratio ratio-16x9">
                <iframe id="${vidId}"
                        src="${esc(tp.embed_url)}"
                        title="${esc(tp.teachingPoint_name)}"
                        allowfullscreen
                        loading="lazy"
                        referrerpolicy="strict-origin-when-cross-origin"></iframe>
              </div>
            </div>
            <div class="col-md-6">
              <h5>${esc(tp.teachingPoint_id)} – ${esc(tp.teachingPoint_name)}</h5>
              <p class="mb-1">${esc(tp.teachingPoint_short_description)}</p>
              <p class="text-muted small mb-2"><strong>Duration:</strong> ${esc(tp.duration)}</p>
              <button class="btn btn-outline-secondary btn-sm"
                      onclick="resetVideo('${vidId}')">🔁 Reset Video</button>
            </div>
          </div>
        `;
      }).join("");

      const drillsHTML = (segment.drills || []).map(drill => {
        // Steps list (optional)
        const steps = Array.isArray(drill.steps) && drill.steps.length
          ? `
            <div class="mt-3">
              <h6 class="mb-1">Steps</h6>
              <ol class="mb-0">
                ${drill.steps.map(s => `<li>${esc(s.instruction ?? "")}</li>`).join("")}
              </ol>
            </div>
          `
          : "";

        // Setup & Rotations (now shown)
        const setupBlock = drill.setup
          ? `<p class="card-text"><strong>Setup:</strong> ${esc(drill.setup)}</p>` : "";
        const rotationsBlock = drill.rotations
          ? `<p class="card-text"><strong>Rotations:</strong> ${esc(drill.rotations)}</p>` : "";

        const diagram = drill.diagramEmbedUrl_1
          ? `
            <div class="ratio ratio-16x9 mb-3">
              <iframe src="${esc(drill.diagramEmbedUrl_1)}"
                      title="${esc(drill.title)} diagram"
                      allowfullscreen
                      loading="lazy"
                      referrerpolicy="strict-origin-when-cross-origin"></iframe>
            </div>
          `
          : "";

        return `
          <div class="card mb-4 border-success">
            <div class="card-body">
              <h5 class="card-title">🛠️ ${esc(drill.title)}</h5>
              <p class="card-text"><strong>Description:</strong> ${esc(drill.drillDescription ?? "—")}</p>
              <p class="card-text"><strong>Purpose:</strong> ${esc(drill.purpose ?? "—")}</p>
              <p class="card-text"><strong>Coaching Points:</strong> ${esc(drill.coachingPoints ?? "—")}</p>
              ${setupBlock}
              ${rotationsBlock}
              ${diagram}
              ${steps}
            </div>
          </div>
        `;
      }).join("");

      const item = `
        <div class="accordion-item">
          <h2 class="accordion-header" id="heading${index}">
            <button class="accordion-button ${index === 0 ? "" : "collapsed"}" type="button"
                    data-bs-toggle="collapse" data-bs-target="#collapse${index}"
                    aria-expanded="${index === 0}" aria-controls="collapse${index}">
              ${esc(segment.time_range)} – ${esc(segment.title)}
            </button>
          </h2>
          <div id="collapse${index}" class="accordion-collapse collapse ${index === 0 ? "show" : ""}"
               aria-labelledby="heading${index}" data-bs-parent="#practicePlan">
            <div class="accordion-body">
              <p class="mb-2"><strong>Focus:</strong> ${esc(segment.title)}</p>
              <p class="mb-4"><strong>Notes:</strong> ${esc(segment.notes || "—")}</p>
              ${tpList}
              ${drillsHTML}
            </div>
          </div>
        </div>
      `;

      container.insertAdjacentHTML("beforeend", item);
    });
  }

  function init() {
    if (!practicePlans || !practicePlans.length) {
      container.innerHTML = "<p>No practice plans available.</p>";
      return;
    }

    // Sort plans newest first by date (fallback to title)
    const plans = [...practicePlans].sort((a,b) => {
      const ad = new Date(a.date || 0).getTime();
      const bd = new Date(b.date || 0).getTime();
      if (ad && bd && ad !== bd) return bd - ad;
      return String(a.title).localeCompare(String(b.title));
    });

    // Populate dropdown
    planSelect.innerHTML = "";
    plans.forEach((plan, idx) => {
      const opt = document.createElement("option");
      opt.value = idx;
      opt.textContent = `${plan.title} – ${plan.duration_minutes} min`;
      planSelect.appendChild(opt);
    });

    // Render first plan
    renderPracticePlan(plans[0]);

    // Switcher
    planSelect.addEventListener("change", (e) => {
      const selected = plans[parseInt(e.target.value, 10)];
      renderPracticePlan(selected);
    });
  }

  window.addEventListener("load", init);
</script>
