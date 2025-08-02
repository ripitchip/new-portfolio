---
title: "About"
url: /about/
type: page
---

<style>
  .about-container {
    display: flex;
    align-items: center; /* vertical center */
    gap: 2rem;
    flex-wrap: wrap;
  }

  .about-text {
    flex: 1;
    min-width: 250px;
  }

  @media (max-width: 768px) {
    .about-container {
      flex-direction: column;
      align-items: center;
      text-align: center;
    }
    .about-text {
      min-width: auto;
    }
    img.about-image {
      width: 70vw !important;
      max-width: 250px !important;
      height: 70vw !important;
      max-height: 250px !important;
      margin-bottom: 1rem;
      object-position: center center !important;
    }
  }
</style>

<div class="about-container">
  <img
    src="/images/me.jpg"
    alt="Thomas Derudder"
    class="about-image"
    style="
      width: 250px;
      height: 250px;
      border-radius: 50%;
      object-fit: cover;
      object-position: center center;
      display: block;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    "
  />

  <div class="about-text">
  
  ## Thomas Derudder

  ### Software Developer

  Welcome to my portfolio! I'm Thomas, a passionate learner across various fields. As an SRE intern, I dive into topics like Kubernetes, DevOps, and AI. I love exploring and sharing knowledge.

  My curiosity has led me to Kubernetes, fascinated by its container orchestration, and AI with its incredible applications. As an SRE intern, I ensure the reliability and performance of IT systems, working with development and operations teams.

  I believe in the power of knowledge-sharing. Here, you'll find my projects, thoughts, and discoveries. Hope you enjoy and get inspired!

  </div>
</div>

