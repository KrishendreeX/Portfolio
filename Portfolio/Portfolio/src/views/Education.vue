<script setup>
import { timeline } from '../data'
</script>

<template>
  <main>
    <section class="education">
      <div class="container">

        <!-- HEADER: eyebrow + serif title + faded background -->
        <div class="section-title">
          <p class="eyebrow">Education &amp; Journey</p>
          <h1 class="main-title">My <em>timeline</em></h1>
          <span class="bg-text">TIMELINE</span>
        </div>

        <!-- TIMELINE WRAPPER -->
        <div class="timeline-wrapper">
          <ul id="timeline">
            <li v-for="(item, index) in timeline" :key="index" class="entry">
              <input
                type="radio"
                name="trigger"
                :id="'t' + index"
                :checked="index === timeline.length - 1"
              >
              <label :for="'t' + index">
                <span>{{ item.title }}</span>
              </label>
              <span class="date">{{ item.label }}</span>
              <span class="circle"></span>
              <div class="content">
                <h3>{{ item.title }}</h3>
                <p v-for="(para, i) in item.text" :key="i">{{ para }}</p>
              </div>
            </li>
          </ul>
        </div>

      </div>
    </section>
  </main>
</template>

<style scoped>
.education {
  padding: 60px 5% 80px 5%;
  scroll-margin-top: 100px;
}

.container {
  width: 90%;
  max-width: 1100px;
  margin: auto;
}

.section-title {
  position: relative;
  text-align: center;
  margin-bottom: 50px;
  padding: 40px 0 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 200px;
}

.eyebrow {
  position: relative;
  z-index: 3;
  color: var(--color-eyebrow);
  font-size: 0.85rem;
  font-weight: 600;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  margin-bottom: 14px;
}

.main-title {
  position: relative;
  z-index: 3;
  font-family: var(--font-serif, 'Fraunces', Georgia, serif);
  font-size: clamp(2.5rem, 6vw, 4.5rem);
  font-weight: 800;
  color: var(--color-dark);
  line-height: 1.05;
  margin: 0;
  letter-spacing: -0.02em;
}

.main-title em {
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

.bg-text {
  position: absolute;
  top: 55%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: clamp(70px, 14vw, 180px);
  font-weight: 800;
  letter-spacing: 6px;
  color: rgba(228, 32, 116, 0.07);
  z-index: 1;
  user-select: none;
  text-transform: uppercase;
  pointer-events: none;
  white-space: nowrap;
  font-family: var(--font-sans);
  line-height: 1;
}

[data-theme="dark"] .bg-text {
  color: rgba(255, 140, 66, 0.08);
}

.timeline-wrapper {
  background: var(--color-card-bg);
  border: 1px solid var(--color-card-border);
  border-radius: 24px;
  padding: 60px 40px 80px 40px;
  box-shadow: 0 8px 40px rgba(34, 22, 56, 0.05);
  transition: background 0.3s ease, border-color 0.3s ease;
}

[data-theme="dark"] .timeline-wrapper {
  box-shadow: 0 8px 40px rgba(0, 0, 0, 0.4);
}

#timeline {
  margin: 0 auto;
  padding: 0;
  list-style: none;
  display: flex;
  justify-content: space-between;
  position: relative;
  border-top: 3px solid var(--color-card-border);
  max-width: 1000px;
}

.entry {
  position: relative;
  flex: 1;
  text-align: center;
  padding-top: 40px;
}

.entry input {
  display: none;
}

.entry label {
  display: inline-block;
  padding: 10px 15px;
  border: 1px solid var(--color-card-border);
  border-radius: 10px;
  cursor: pointer;
  transition: 0.3s;
  color: var(--color-dark);
  font-weight: 500;
  background: var(--color-bg-base);
}

.entry label:hover {
  border-color: var(--color-accent);
  color: var(--color-accent);
}

.date {
  display: block;
  margin-top: 10px;
  font-size: 0.8rem;
  color: var(--color-subtext);
}

.circle {
  width: 12px;
  height: 12px;
  background: var(--color-bg-base);
  border: 3px solid var(--color-accent);
  border-radius: 50%;
  position: absolute;
  top: -7px;
  left: 50%;
  transform: translateX(-50%);
}

.content {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  width: 400px;
  background: var(--color-card-bg);
  padding: 20px;
  border-radius: 12px;
  border: 1px solid var(--color-card-border);
  opacity: 0;
  transition: 0.4s ease;
  pointer-events: none;
  z-index: 10;
  text-align: left;
  box-shadow: 0 8px 30px rgba(34, 22, 56, 0.08);
}

[data-theme="dark"] .content {
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.4);
}

.entry input:checked ~ .content {
  opacity: 1;
  pointer-events: auto;
  transform: translateX(-50%) translateY(10px);
}

.entry input:checked + label {
  color: var(--color-accent);
  border-color: var(--color-accent);
}

.content h3 {
  font-family: var(--font-serif, 'Fraunces', Georgia, serif);
  font-size: 1.15rem;
  color: var(--color-dark);
  margin-bottom: 8px;
}

.content p {
  font-size: 0.9rem;
  color: var(--color-subtext);
  line-height: 1.65;
  margin-bottom: 8px;
}

.content p:last-child {
  margin-bottom: 0;
}

/* --- Mobile --- */
@media (max-width: 768px) {
  .education { padding: 40px 5% 60px 5%; }

  .section-title { padding: 30px 0 40px; min-height: 140px; margin-bottom: 30px; }

  .main-title { font-size: clamp(2rem, 8vw, 3rem); }
  .bg-text { font-size: clamp(48px, 20vw, 100px); letter-spacing: 3px; }

  .timeline-wrapper {
    padding: 40px 24px 50px 24px;
    border-radius: 20px;
  }

  #timeline {
    flex-direction: column;
    gap: 45px;
    border-top: none;
    border-left: 3px solid var(--color-card-border);
    padding-left: 25px;
    margin: 0 auto;
  }

  .entry {
    text-align: left;
    padding-top: 0;
    width: 100%;
  }

  .circle {
    top: 15px;
    left: -31px;
    transform: none;
  }

  .content {
    position: relative;
    left: 0;
    transform: none;
    width: 100%;
    max-width: 100%;
    margin-top: 12px;
    box-sizing: border-box;
    opacity: 1;
    pointer-events: auto;
  }

  .entry input:checked ~ .content {
    transform: translateY(5px);
  }
}
</style>