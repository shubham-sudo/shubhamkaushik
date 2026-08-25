---
layout: page
title: TexBench
description: A Unified Benchmarking Suite for Shifting Workloads
img:
importance: 1
category: Published
related_publications: chanda2026texbench, kaushik2026texbenchllm, ott2025tectonic
---

<div class="texbench-landing">

  <div class="hero hero-row tb-bio-row">
    <div class="hero-left">
      <p class="tb-greeting">
        Thanks for stopping by! If you're here, you're probably looking to <strong>try the live demo</strong>
        or <strong>read the paper</strong> &mdash; pick a side below.
      </p>

      <div class="tb-links">

        <a href="#" class="tb-card tb-card-demo" target="_blank" rel="noopener">
          <span class="tb-card-icon"><i class="fa-solid fa-rocket"></i></span>
          <span class="tb-card-title">Try the Demo</span>
          <span class="tb-card-sub">Spin up TexBench and benchmark key-value stores live, right in your browser.</span>
          <span class="tb-card-cta">Launch demo <i class="fa-solid fa-arrow-right"></i></span>
        </a>

        <div class="tb-card tb-card-papers">
          <span class="tb-card-icon"><i class="fa-solid fa-file-lines"></i></span>
          <span class="tb-card-title">Read the Papers</span>
          <span class="tb-card-sub">Two takes on TexBench &mdash; the full workshop paper and the demo track paper.</span>
          <div class="tb-paper-list">
            <a href="/assets/pdf/TexBenchTPCTC.pdf" class="tb-paper-link" target="_blank" rel="noopener">
              <i class="fa-solid fa-arrow-right"></i> TPCTC Workshop Paper
            </a>
            <a href="/assets/pdf/TexBench.pdf" class="tb-paper-link" target="_blank" rel="noopener">
              <i class="fa-solid fa-arrow-right"></i> VLDB Demo Paper
            </a>
          </div>
        </div>

      </div>
    </div>
    <div class="hero-right">
      <div class="hero-avatar">
        {% include figure.html path="assets/img/prof_pic.jpg" class="img-fluid" alt="Shubham Kaushik" cache_bust=true %}
      </div>
      <h2 class="hero-name">Shubham Kaushik</h2>
      <p class="hero-tagline">PhD Researcher &mdash; Storage &amp; Database Systems</p>
      <div class="hero-social">
        <div class="contact-icons">
          {% include social.html %}
        </div>
      </div>
    </div>
  </div>
</div>

<style>
  .texbench-landing .tb-bio-row {
    align-items: flex-start;
  }

  .tb-greeting {
    font-size: 1.15rem;
    line-height: 1.7;
    color: var(--global-text-color);
    margin: 0;
  }

  .texbench-landing .hero-social .contact-icons {
    justify-content: center;
  }

  .tb-links {
    display: flex;
    flex-wrap: wrap;
    gap: 1.25rem;
    align-items: stretch;
    margin-top: 1.5rem;
  }

  .tb-card {
    flex: 1 1 220px;
    display: flex;
    flex-direction: column;
    padding: 1.15rem 1.25rem;
    border-radius: 16px;
    border: 1px solid var(--global-divider-color);
    background: var(--global-card-bg-color);
    text-decoration: none;
    transition: box-shadow 0.2s ease, transform 0.2s ease, border-color 0.2s ease;
  }

  a.tb-card:hover {
    box-shadow: 0 8px 28px rgba(0, 0, 0, 0.1);
    transform: translateY(-3px);
    border-color: var(--global-theme-color);
  }

  .tb-card-icon {
    font-size: 1.35rem;
    color: var(--global-theme-color);
    margin-bottom: 0.4rem;
  }

  .tb-card-title {
    font-size: 1.15rem;
    font-weight: 700;
    color: var(--global-text-color);
    margin-bottom: 0.3rem;
  }

  .tb-card-sub {
    font-size: 0.95rem;
    color: var(--global-text-color-light);
    line-height: 1.6;
    flex-grow: 1;
  }

  .tb-card-cta {
    margin-top: 0.75rem;
    font-weight: 600;
    color: var(--global-theme-color);
  }

  .tb-card-cta i {
    margin-left: 0.4rem;
    transition: transform 0.2s ease;
  }

  a.tb-card:hover .tb-card-cta i {
    transform: translateX(4px);
  }

  .tb-paper-list {
    margin-top: 0.75rem;
    display: flex;
    flex-direction: column;
    gap: 0.45rem;
  }

  .tb-paper-link {
    font-weight: 600;
    color: var(--global-text-color);
    text-decoration: none;
    padding: 0.5rem 0.8rem;
    border-radius: 10px;
    border: 1px solid var(--global-divider-color);
    transition: background 0.15s ease, color 0.15s ease, border-color 0.15s ease;
  }

  .tb-paper-link i {
    margin-right: 0.5rem;
    color: var(--global-theme-color);
  }

  .tb-paper-link:hover {
    background: var(--global-theme-color);
    color: var(--global-hover-text-color);
    border-color: var(--global-theme-color);
  }

  .tb-paper-link:hover i {
    color: var(--global-hover-text-color);
  }

  @media (max-width: 576px) {
    .tb-links {
      flex-direction: column;
    }
  }
</style>
