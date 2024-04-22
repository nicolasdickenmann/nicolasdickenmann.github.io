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
  <!--{% for project in projects %}
   Debug: Output the title of each project 
  {{ project.title }}
  {% endfor %} -->
  <div class="projects-grid">
    {% for project in projects %}
      <div class="project-box">
      {% if project.redirect contains '://' %}
          <h3> 
          <a class="project-title" href="{{ project.redirect }}" target="_blank">{{ post.title }}</a>
          <svg width="2rem" height="2rem" viewBox="0 0 40 40" xmlns="http://www.w3.org/2000/svg">
            <path d="M17 13.5v6H5v-12h6m3-3h6v6m0-6-9 9" class="icon_svg-stroke" stroke="#999" stroke-width="1.5" fill="none" fill-rule="evenodd" stroke-linecap="round" stroke-linejoin="round"></path>
          </svg>
          </h3>
      {% else %}
        <h3 class="project-title">{{ project.title }}</h3>
      {% endif %}
      {% if project.image %}
          <img class="project-image" src="{{ project.image | relative_url }}" alt="{{ project.title }}" style="max-width: 90%; height: auto; margin: 0 auto;border-radius: 12px;">
        {% endif %}
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
    border: 1px solid #AE75F9;
    padding: 20px;
    border-radius: 12px;
    background-color: #AE75F9;
  }
  .project-title {
    margin-bottom: 15px;
  }
  .project-details {
    list-style: none;
    padding: 25;
    text-align: left;
    margin-top: 20px;
  }
  .project-details li {
    margin-bottom: 5px;
  }
</style>
