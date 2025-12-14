---
layout: default
title: Sasha Shkolnikov - Portfolio
permalink: /projects/
---

<style>
  .gallery-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem 1rem;
  }

  .project-gallery {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2.5rem; /* vertical + horizontal spacing */
  }

  /* Tablet */
  @media (max-width: 900px) {
    .project-gallery {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  /* Mobile */
  @media (max-width: 550px) {
    .project-gallery {
      grid-template-columns: 1fr;
    }
  }

  .gallery-item {
    text-align: center;
  }

  .gallery-item img {
    width: 100%;
    height: auto;
    border-radius: 8px;
    display: block;
  }

  .gallery-item p {
    margin-top: 0.75rem;
    font-weight: 500;
  }

  .gallery-item a {
    text-decoration: none;
    color: inherit;
    display: block;
  }
</style>

<div class="gallery-container">
  <div class="project-gallery">
    {% for project in site.projects %}
      <div class="gallery-item">
        <a href="{{ project.url | relative_url }}">
          <img src="{{ project.image | relative_url }}" alt="{{ project.title | default: 'Project image' }}">
          <p>{{ project.title | default: project.slug }}</p>
        </a>
      </div>
    {% endfor %}
  </div>
</div>
