---
layout: page
title: Projects
permalink: /projects/
description: Building brilliance, bit by bit.
nav: true
nav_order: 1
display_categories: [Ongoing, Published, Academics]
horizontal: false
---

<!-- pages/projects.md -->
<div class="projects">
{%- if site.enable_project_categories and page.display_categories %}
  {%- for category in page.display_categories %}
  {%- assign categorized_projects = site.projects | where: "category", category -%}
  {%- assign sorted_projects = categorized_projects | sort: "importance" %}
  {%- if sorted_projects.size > 0 %}
  <h2 class="category">{{ category }}</h2>
  <div class="row row-cols-1 row-cols-md-2">
    {%- for project in sorted_projects -%}
    <div class="col mb-4">
      <a href="{{ project.url | relative_url }}" class="homepage-project-link">
        <div class="card homepage-project-card h-100">
          {%- if project.img -%}
          <img src="{{ project.img | relative_url }}" class="card-img-top" alt="{{ project.title }}">
          {%- endif -%}
          <div class="card-body">
            <span class="project-category-badge">{{ project.category }}</span>
            <h3 class="card-title">{{ project.title }}</h3>
            <p class="card-text">{{ project.description }}</p>
          </div>
        </div>
      </a>
    </div>
    {%- endfor %}
  </div>
  {%- endif -%}
  {% endfor %}
{%- else -%}
  {%- assign sorted_projects = site.projects | sort: "importance" -%}
  <div class="row row-cols-1 row-cols-md-2">
    {%- for project in sorted_projects -%}
    <div class="col mb-4">
      <a href="{{ project.url | relative_url }}" class="homepage-project-link">
        <div class="card homepage-project-card h-100">
          {%- if project.img -%}
          <img src="{{ project.img | relative_url }}" class="card-img-top" alt="{{ project.title }}">
          {%- endif -%}
          <div class="card-body">
            <span class="project-category-badge">{{ project.category }}</span>
            <h3 class="card-title">{{ project.title }}</h3>
            <p class="card-text">{{ project.description }}</p>
          </div>
        </div>
      </a>
    </div>
    {%- endfor %}
  </div>
{%- endif -%}
</div>
