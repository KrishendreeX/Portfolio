<script setup>
import ProjectCard from '../components/ProjectCard.vue'
import { projects } from '../data'
</script>

<template>
  <main>
    <section class="projects">
      <div class="container">

        <!-- TITLE: eyebrow + serif "Things I've built" -->
        <p class="eyebrow">Projects</p>
        <h1 class="page-title">Things I've <em>built</em></h1>

        <!-- PROJECT GRID -->
        <div class="projects-grid">
          <ProjectCard v-for="p in projects" :key="p.title" :project="p" />
        </div>

      </div>
    </section>
  </main>
</template>

<style scoped>
.projects {
  padding: 60px 5% 80px 5%;
  scroll-margin-top: 100px;
}

.container {
  width: 90%;
  max-width: 1100px;
  margin: auto;
}

/* Eyebrow */
.eyebrow {
  color: var(--color-eyebrow);
  font-size: 0.85rem;
  font-weight: 600;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  margin-bottom: 12px;
}

/* Big serif title */
.page-title {
  font-family: var(--font-serif, 'Fraunces', Georgia, serif);
  font-size: clamp(2.5rem, 6vw, 4.5rem);
  font-weight: 800;
  color: var(--color-dark);
  line-height: 1.05;
  letter-spacing: -0.02em;
  margin-bottom: 60px;
}

.page-title em {
  display: inline-block;
  font-style: italic;
  font-weight: 700;
  background: linear-gradient(90deg, #e42074 0%, #eb6b27 100%);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  color: transparent;
  letter-spacing: -0.01em;
}

/* Projects grid */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 28px;
  align-items: stretch;
}

/* Mobile */
@media (max-width: 600px) {
  .projects { padding: 40px 5% 60px 5%; }
  .page-title { font-size: clamp(2rem, 8vw, 3rem); margin-bottom: 40px; }
}
</style>