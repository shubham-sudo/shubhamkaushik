---
layout: page
title: Talks
permalink: /talks/
description: Research talks, seminars, and conference presentations.
nav: true
nav_order: 3
---

<div class="talks">
  {% assign sorted_talks = site.talks | sort: "date" | reverse %}
  <div class="row">
    {% for talk in sorted_talks %}

    {% comment %} Resolve card link: video > slides {% endcomment %}
    {% assign card_video = "" %}
    {% assign card_slides = "" %}
    {% for v in talk.venues %}
      {% if v.video and v.video != "" and card_video == "" %}
        {% assign card_video = v.video %}
      {% endif %}
      {% if v.slides and v.slides != "" and card_slides == "" %}
        {% assign card_slides = v.slides %}
      {% endif %}
    {% endfor %}
    {% if card_video != "" %}
      {% assign card_link = card_video %}
    {% elsif card_slides != "" %}
      {% assign card_link = card_slides %}
    {% else %}
      {% assign card_link = "" %}
    {% endif %}

    <div class="col-12 col-sm-6 col-md-4 mb-4">
      <a {% if card_link != "" %}href="{{ card_link }}" target="_blank"{% endif %}
         class="homepage-project-link" style="{% if card_link == "" %}cursor: default; pointer-events: none;{% endif %}">
        <div class="card homepage-project-card h-100">

          {% comment %} Thumbnail {% endcomment %}
          {%- if card_video != "" -%}
            {%- assign video_id = card_video | split: "v=" | last | split: "&" | first -%}
            <img src="https://img.youtube.com/vi/{{ video_id }}/mqdefault.jpg"
                 class="card-img-top" alt="{{ talk.title }}"
                 style="height: 130px; object-fit: cover;">
          {%- elsif card_slides != "" -%}
            <div class="card-img-top" style="height: 130px; overflow: hidden; background: var(--global-card-bg-color); position: relative;">
              <canvas class="pdf-thumb" data-pdf="{{ card_slides }}"
                      style="width: 100%; display: block;"></canvas>
              <span style="position: absolute; top: 6px; right: 8px;
                           background: rgba(0,0,0,0.55); border-radius: 4px;
                           padding: 2px 5px; display: flex; align-items: center; gap: 4px;">
                <i class="fas fa-file-pdf" style="color: #ff6b6b; font-size: 0.7rem;"></i>
                <span style="color: #fff; font-size: 0.6rem; font-weight: 600; letter-spacing: 0.03em;">PDF</span>
              </span>
            </div>
          {%- else -%}
            <div class="card-img-top d-flex align-items-center justify-content-center"
                 style="height: 130px; background: var(--global-divider-color);">
              <i class="fas fa-microphone-alt fa-3x" style="color: var(--global-text-color-light); opacity: 0.5;"></i>
            </div>
          {%- endif -%}

          <div class="card-body" style="padding: 0.75rem 0.9rem 0.6rem;">

            {%- if talk.duration and talk.duration != "" -%}
              <span style="display: inline-block; font-size: 0.65rem; font-weight: 600;
                           color: var(--global-theme-color); margin-bottom: 0.3rem;">
                {{ talk.duration }}''
              </span>
            {%- endif -%}

            <h6 class="card-title" style="font-size: 0.88rem; font-weight: 600;
                color: var(--global-text-color); margin-bottom: 0.5rem; line-height: 1.35;">
              {{ talk.title }}
            </h6>

            <div>
              {%- for v in talk.venues -%}
                <span style="display: inline-block; font-size: 0.65rem; font-weight: 500;
                             border: 1px solid var(--global-theme-color);
                             color: var(--global-theme-color);
                             border-radius: 4px;
                             padding: 2px 6px;
                             margin-right: 4px; margin-bottom: 4px; line-height: 1.4;">
                  {{ v.name }}{%- if v.location and v.location != "" -%}&thinsp;&middot;&thinsp;{{ v.location }}{%- endif -%}
                </span>
              {%- endfor -%}
            </div>

          </div>
        </div>
      </a>
    </div>
    {% endfor %}
  </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script>
  pdfjsLib.GlobalWorkerOptions.workerSrc =
    'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';

  document.querySelectorAll('.pdf-thumb').forEach(function (canvas) {
    var url = canvas.getAttribute('data-pdf');
    pdfjsLib.getDocument(url).promise.then(function (pdf) {
      return pdf.getPage(1);
    }).then(function (page) {
      var w = canvas.parentElement.offsetWidth;
      var viewport = page.getViewport({ scale: 1 });
      var scale = w / viewport.width;
      var scaled = page.getViewport({ scale: scale });
      canvas.width  = scaled.width;
      canvas.height = scaled.height;
      page.render({ canvasContext: canvas.getContext('2d'), viewport: scaled });
    }).catch(function () {
      canvas.parentElement.innerHTML =
        '<div class="d-flex align-items-center justify-content-center h-100">' +
        '<i class="fas fa-file-pdf fa-3x" style="color:#c0392b; opacity:0.7;"></i></div>';
    });
  });
</script>
