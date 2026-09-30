<script setup>
import { technicalSkills, frameworksAndTools } from '../data'

// triple each array for seamless looping
const technicalLoop = [...technicalSkills, ...technicalSkills, ...technicalSkills]
const toolsLoop = [...frameworksAndTools, ...frameworksAndTools, ...frameworksAndTools]
</script>

<template>
  <main>
    <section class="skills">
      <div class="container">

        <div class="section-title">
          <h2>My Skills</h2>
          <span>My Skills</span>
        </div>

        <p class="intro">
          A blend of languages, frameworks, and tools I use to build full-stack web applications — from pixel-perfect interfaces to solid backend APIs.
        </p>

        <!-- TECHNICAL SKILLS — scrolls LEFT -->
        <div class="skill-group">
          <h3 class="group-title">
            <i class="fa-solid fa-code" aria-hidden="true"></i>
            Technical Skills
          </h3>
          <div class="marquee">
            <div class="track track-left">
              <span
                v-for="(s, i) in technicalLoop"
                :key="'t' + i"
                class="skill-pill"
              >
                <i class="icon" :class="s.icon" aria-hidden="true"></i>
                <span class="name">{{ s.name }}</span>
              </span>
            </div>
          </div>
        </div>

        <!-- TOOLS & FRAMEWORKS — scrolls RIGHT -->
        <div class="skill-group">
          <h3 class="group-title">
            <i class="fa-solid fa-screwdriver-wrench" aria-hidden="true"></i>
            Tools &amp; Frameworks
          </h3>
          <div class="marquee">
            <div class="track track-right">
              <span
                v-for="(t, i) in toolsLoop"
                :key="'f' + i"
                class="skill-pill"
              >
                <i class="icon" :class="t.icon" aria-hidden="true"></i>
                <span class="name">{{ t.name }}</span>
              </span>
            </div>
          </div>
        </div>

      </div>
    </section>
  </main>
</template>

<style scoped>
.skills {
  padding: 60px 5% 80px 5%;
}

.container {
  width: 90%;
  max-width: 1100px;
  margin: auto;
}

/* --- Section title with faded background text --- */
.section-title {
  position: relative;
  text-align: center;
  margin-bottom: 40px;
  min-height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.section-title h2 {
  position: relative;
  z-index: 2;
  font-size: clamp(22px, 3vw, 40px);
  color: var(--color-accent);
  text-transform: uppercase;
  letter-spacing: 5px;
  margin: 0;
}

.section-title span {
  width: 100%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: clamp(40px, 8vw, 100px);
  font-weight: 800;
  letter-spacing: 5px;
  color: rgba(255, 140, 66, 0.06);
  z-index: 1;
  user-select: none;
  text-transform: uppercase;
  pointer-events: none;
  white-space: nowrap;
}

[data-theme="light"] .section-title span {
  color: rgba(228, 32, 116, 0.05);
}

/* --- Intro paragraph --- */
.intro {
  text-align: center;
  max-width: 640px;
  margin: 0 auto 60px auto;
  color: var(--color-subtext);
  font-size: 1.02rem;
  line-height: 1.7;
}

/* --- Skill Groups --- */
.skill-group {
  margin-bottom: 55px;
}

.group-title {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  text-align: center;
  color: var(--color-accent);
  font-size: 1.25rem;
  font-weight: 600;
  margin-bottom: 26px;
  letter-spacing: 1px;
}

.group-title i {
  font-size: 1.05rem;
}

/* --- Marquee / Carousel wrapper --- */
.marquee {
  overflow: hidden;
  width: 100%;
  padding: 8px 0;
  /* Fade the edges so pills appear/disappear softly */
  mask-image: linear-gradient(
    90deg,
    transparent 0%,
    #000 8%,
    #000 92%,
    transparent 100%
  );
  -webkit-mask-image: linear-gradient(
    90deg,
    transparent 0%,
    #000 8%,
    #000 92%,
    transparent 100%
  );
}

.track {
  display: flex;
  gap: 16px;
  width: max-content;
  will-change: transform;
}

/* Technical skills → scrolls left */
.track-left {
  animation: scrollLeft 25s linear infinite;
}

/* Tools & frameworks → scrolls right */
.track-right {
  animation: scrollRight 30s linear infinite;
}

/* Pause on hover for both */
.marquee:hover .track {
  animation-play-state: paused;
}

@keyframes scrollLeft {
  from { transform: translateX(0); }
  to   { transform: translateX(-33.333%); }
}

@keyframes scrollRight {
  from { transform: translateX(-33.333%); }
  to   { transform: translateX(0); }
}

/* --- Skill pills --- */
.skill-pill {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 12px 24px;
  border-radius: 999px;
  background: var(--color-card-bg);
  border: 1.5px solid var(--color-accent);
  font-size: 0.95rem;
  font-weight: 500;
  color: var(--color-dark);
  transition: transform 0.25s ease, background 0.25s ease, box-shadow 0.25s ease;
  cursor: default;
  white-space: nowrap;
  flex-shrink: 0;
}

.skill-pill:hover {
  transform: translateY(-3px);
  background: var(--color-accent);
  color: #fff;
  box-shadow: 0 8px 20px rgba(228, 32, 116, 0.2);
}

[data-theme="dark"] .skill-pill:hover {
  color: #0d0d0d;
  box-shadow: 0 8px 20px rgba(255, 140, 66, 0.25);
}

/* Icons use the accent colour, then follow the pill's text colour on hover */
.skill-pill .icon {
  font-size: 1.15rem;
  line-height: 1;
  color: var(--color-accent);
  transition: color 0.25s ease;
}

.skill-pill:hover .icon {
  color: inherit;
}

/* Respect reduced-motion users */
@media (prefers-reduced-motion: reduce) {
  .track-left,
  .track-right {
    animation: none;
    transform: none;
  }
  .marquee {
    overflow-x: auto;
    -webkit-mask-image: none;
    mask-image: none;
  }
}

/* --- Mobile --- */
@media (max-width: 768px) {
  .skills { padding: 40px 5% 60px 5%; }

  .section-title { min-height: 70px; margin-bottom: 20px; }
  .section-title h2 { letter-spacing: 3px; }

  .intro { font-size: 0.95rem; margin-bottom: 40px; }

  .skill-pill { padding: 10px 18px; font-size: 0.88rem; }
}
</style>