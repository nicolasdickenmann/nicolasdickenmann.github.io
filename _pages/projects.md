---
layout: default
permalink: /projects/
nav: true
title: projects
---

<div class="projects-container" style="text-align: center;">

  <h1 class="projects-title">Projects</h1>
  <h2 class="projects-subtitle">A growing collection of cool projects</h2>

  {% assign projects = site.posts | where: "category", "project" %}
  {% for project in projects %}
  <!-- Debug: Output the title of each project -->
  {{ project.title }}
  {% endfor %}
  <div class="projects-grid">
    {% for project in projects %}
      <div class="project-box">
        <h3 class="project-title">{{ project.title }}</h3>
        <img class="project-image" src="{{ project.image | relative_url }}" alt="{{ project.title }}" style="max-width: 100%; height: auto; margin: 0 auto;">
        <ul class="project-details">
          {% for detail in project.details %}
            <li>{{ detail }}</li>
          {% endfor %}
        </ul>
      </div>
    {% endfor %}
  </div>

</div>

<style>
  .projects-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 50px;
  }
  .projects-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
  }
  .project-box {
    border: 1px solid #121481;
    padding: 20px;
    border-radius: 8px;
    background-color: #121481;
  }
  .project-title {
    margin-bottom: 15px;
  }
  .project-details {
    list-style: none;
    padding: 20;
    text-align: center;
  }
  .project-details li {
    margin-bottom: 5px;
  }
</style>
