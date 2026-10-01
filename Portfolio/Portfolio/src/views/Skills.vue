<script setup>
import { technicalSkills, frameworksAndTools } from '../data'

// Repeat each list twice so the scroll never runs out
const technicalLoop = [...technicalSkills, ...technicalSkills]
const toolsLoop = [...frameworksAndTools, ...frameworksAndTools]
</script>

<template>
  <main>
    <section class="skills">
      <div class="container">

        <h2>My Skills</h2>

        <p class="intro">
          These are the languages, frameworks and tools I use to build web apps,
          from the pages you see to the servers behind them.
        </p>

        <!-- Scrolls left -->
        <h3>Technical Skills</h3>
        <div class="marquee">
          <div class="track scroll-left">
            <span v-for="(skill, i) in technicalLoop" :key="i" class="pill">
              <i :class="skill.icon"></i>
              {{ skill.name }}
            </span>
          </div>
        </div>

        <!-- Scrolls right -->
        <h3>Tools &amp; Frameworks</h3>
        <div class="marquee">
          <div class="track scroll-right">
            <span v-for="(tool, i) in toolsLoop" :key="i" class="pill">
              <i :class="tool.icon"></i>
              {{ tool.name }}
            </span>
          </div>
        </div>

      </div>
    </section>
  </main>
</template>

<style scoped>
.skills {
  padding: 60px 5% 80px;
}

.container {
  max-width: 1100px;
  margin: auto;
}

h2 {
  text-align: center;
  font-size: 2rem;
  color: var(--color-accent);
  margin-bottom: 16px;
}

.intro {
  text-align: center;
  max-width: 600px;
  margin: 0 auto 50px;
  color: var(--color-subtext);
  line-height: 1.7;
}

h3 {
  text-align: center;
  font-size: 1.2rem;
  color: var(--color-dark);
  margin-bottom: 20px;
}

/* Hides the part of the track that is off screen */
.marquee {
  overflow: hidden;
  margin-bottom: 50px;
}

/* One long row of pills */
.track {
  display: flex;
  gap: 16px;
  width: max-content;
}

.scroll-left {
  animation: scrollLeft 25s linear infinite;
}

.scroll-right {
  animation: scrollRight 30s linear infinite;
}

/* Pause when the mouse is over it */
.marquee:hover .track {
  animation-play-state: paused;
}

/* The track holds two copies, so moving 50% loops it smoothly */
@keyframes scrollLeft {
  from { transform: translateX(0); }
  to   { transform: translateX(-50%); }
}

@keyframes scrollRight {
  from { transform: translateX(-50%); }
  to   { transform: translateX(0); }
}

.pill {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 12px 22px;
  border: 1px solid var(--color-accent);
  border-radius: 999px;
  background: var(--color-card-bg);
  color: var(--color-dark);
  white-space: nowrap;
}

.pill i {
  color: var(--color-accent);
  font-size: 1.1rem;
}

/* Turn off the scrolling for people who prefer less motion */
@media (prefers-reduced-motion: reduce) {
  .track {
    animation: none;
  }
  .marquee {
    overflow-x: auto;
  }
}

@media (max-width: 768px) {
  .skills { padding: 40px 5% 60px; }
  .pill { padding: 10px 16px; font-size: 0.9rem; }
}
</style>