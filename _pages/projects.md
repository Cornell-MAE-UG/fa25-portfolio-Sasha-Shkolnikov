---
layout: default
title: Sasha Shkolnikov - Portfolio
permalink: /projects/
---

<style>
  .gallery-container {
    max-width: 1500px;
    margin: 0 auto;
    padding: 2rem 1rem;
  }

  .project-gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
  }

  .gallery-item {
    position: relative;
    overflow: hidden;
    border-radius: 12px;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    cursor: pointer;
  }

  .gallery-item img {
    width: 100%;
    height: auto;
    display: block;
    border-radius: 12px;
    transition: transform 0.4s ease;
  }

  /* Always show title below the image */
  .gallery-item p {
    margin-top: 0.75rem;
    font-weight: 600;
    font-size: 1.05rem;
    text-align: center;
    color: #222;
  }

  /* Hover effect: subtle lift and image scale */
  .gallery-item:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 30px rgba(0,0,0,0.2);
  }

  .gallery-item:hover img {
    transform: scale(1.05);
  }

  /* Responsive adjustments */
  @media (max-width: 900px) {
    .project-gallery {
      gap: 1.5rem;
    }
  }

  @media (max-width: 550px) {
    .project-gallery {
      gap: 1rem;
    }
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
