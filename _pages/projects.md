---
layout: default
permalink: /projects/
nav: true
title: projects
---

<div class="projects-container" style="text-align: center;">

  <h1 class="projects-title">Research, side projects and more</h1>

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
          <a class="project-title" href="{{ project.redirect }}" target="_blank">{{ project.title }}</a>
          </h3>
      {% else %}
        <h3 class="project-title">{{ project.title }}</h3>
      {% endif %}
      {% if project.image %}
          <img class="project-image" src="{{ project.image | relative_url }}" alt="{{ project.title }}">
      {% elsif project.video %}
            <div class="project-video">
            {% include video.liquid path=project.video class="img-fluid rounded z-depth-1" autoplay=true loop=true %}
            </div>
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
    border: 1px solid #711A75;
    padding: 20px;
    border-radius: 12px;
    background-color: #711A75;
    word-wrap: break-word;
    overflow-wrap: break-word;
    box-sizing: border-box;
    min-width: 0;
  }
  .project-title {
    margin-bottom: 15px;
  }
  .project-subtitle {
    margin-bottom: 10px;
  }
  .project-title  {
    color: inherit; /* This makes the link color the same as the surrounding text */
    text-decoration: none; /* This removes the underline from the link */
  }
  .project-title:hover {
    color: #0096D6; /* This changes the link color on hover */
    text-decoration: underline; /* This adds an underline on hover */
  }
  .project-details {
    list-style: none;
    text-align: left;
    margin-top: 20px;
    padding-right: 20px;
    word-wrap: break-word;
    overflow-wrap: break-word;
  }
  ul.project-details li a {
  color: inherit; /* This makes the link color the same as the surrounding text */
  text-decoration: none; /* This removes the underline from the link */
  }
  ul.project-details li a:hover {
  color: #0096D6; /* This changes the link color on hover */
  text-decoration: underline; /* This adds an underline on hover */
  }
  .project-details li {
    margin-bottom: 5px;
  }
  .project-video {
    max-width: 90%;
    height: auto;
    margin: 5% auto;
    border-radius: 12px;
  }
  .project-video video {
    max-width: 100%;
    height: auto;
    border-radius: 12px;
  }
  .project-image {
    max-width: 90%;
    height: auto;
    margin: 5% auto;
    border-radius: 12px;
    display: block;
  }
</style>
