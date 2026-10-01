<script setup>
import TypeWriter from '../components/TypeWriter.vue'
import { roles } from '../data'
</script>

<template>
  <main>
    <section class="hero">
      <div class="hero-copy">
        <p class="eyebrow">Hello, I'm</p>

        <h1 class="hero-title">
          <span class="name-line1">Krishendree</span>
          <span class="name-line2">Kistensamy</span>
        </h1>

        <TypeWriter :words="roles" />

        <div class="hero-cta">
          <RouterLink class="btn btn-primary" to="/projects">See my work</RouterLink>
          <RouterLink class="btn btn-secondary" to="/contact">Let's talk</RouterLink>
        </div>
      </div>

      <div class="hero-image">
        <img
          class="bounce-float"
          src="https://i.ibb.co/CKqGMVhr/cartoon.png"
          alt="portrait of Krishendree Kistensamy"
        >
      </div>
    </section>
  </main>
</template>

<style scoped>
.hero {
  min-height: calc(100vh - 70px);
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  gap: 48px;
  flex-wrap: wrap;
  padding: 40px 5% 60px 5%;
}

.hero-copy {
  flex: 1 1 420px;
  text-align: left;
  max-width: 600px;
}

.eyebrow {
  color: var(--color-eyebrow);
  font-size: 0.85rem;
  font-weight: 600;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  margin-bottom: 12px;
}

.hero-title {
  font-family: var(--font-serif, 'Fraunces', Georgia, serif);
  line-height: 1.02;
  margin-bottom: 20px;
}

.name-line1 {
  display: block;
  font-size: clamp(2.8rem, 6.5vw, 5rem);
  font-weight: 800;
  color: var(--color-dark);
  letter-spacing: -0.02em;
}

.name-line2 {
  display: inline-block;
  font-size: clamp(2.8rem, 6.5vw, 5rem);
  font-weight: 700;
  font-style: italic;
  background: linear-gradient(90deg, #e42074 0%, #eb6b27 100%);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  color: transparent;
  letter-spacing: -0.01em;
}

/* TypeWriter comes with its own centered styling, so pull it left to match everything else here */
:deep(.hero-subtitle) {
  justify-content: flex-start !important;
  text-align: left !important;
  font-size: clamp(1.3rem, 2.6vw, 1.9rem) !important;
  color: var(--color-subtext) !important;
  min-height: 2.2em !important;
  margin-bottom: 8px !important;
  padding-left: 0 !important;
}

:deep(.role-highlight) {
  font-size: 1em;
  font-weight: 700;
}

:deep(.typing-cursor) {
  font-size: 1em;
}

.hero-cta {
  display: flex;
  gap: 16px;
  margin-top: 28px;
  flex-wrap: wrap;
}

.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 13px 32px;
  border-radius: 999px;
  font-size: 0.95rem;
  font-weight: 600;
  text-decoration: none;
  cursor: pointer;
  transition: transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1),
              box-shadow 0.3s ease,
              background 0.25s ease;
  border: none;
  font-family: var(--font-sans);
}

.btn-primary {
  background: linear-gradient(135deg, #e42074 0%, #ee6b22 100%);
  color: #fff;
  box-shadow: 0 8px 24px rgba(228, 32, 116, 0.25);
}

.btn-primary:hover {
  transform: translateY(-4px) scale(1.03);
  box-shadow: 0 14px 32px rgba(228, 32, 116, 0.4);
}

.btn-secondary {
  background: rgba(255, 255, 255, 0.7);
  border: 1px solid rgba(34, 22, 56, 0.15);
  color: var(--color-dark);
}

.btn-secondary:hover {
  transform: translateY(-4px) scale(1.03);
  background: #ffffff;
  border-color: var(--color-dark);
  box-shadow: 0 10px 24px rgba(34, 22, 56, 0.1);
}

[data-theme="dark"] .btn-secondary {
  background: rgba(255, 255, 255, 0.05);
  border-color: rgba(255, 255, 255, 0.2);
  color: var(--color-dark);
}

.hero-image {
  position: relative;
  flex: 1 1 320px;
  max-width: 420px;
  display: flex;
  justify-content: center;
  margin: 0 auto;
}

.hero-image img {
  width: 100%;
  max-width: 360px;
  border-radius: 28px;
  filter: drop-shadow(0 25px 45px rgba(34, 22, 56, 0.25));
}

@keyframes bounceIdle {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-7px); }
}

.bounce-float {
  animation: bounceIdle 4s ease-in-out infinite;
}

/* small screens */
@media (max-width: 700px) {
  .hero {
    flex-direction: column;
    text-align: center;
    padding: 30px 5% 40px 5%;
    gap: 32px;
  }

  .hero-copy { text-align: center; }

  :deep(.hero-subtitle) {
    justify-content: center !important;
    text-align: center !important;
  }

  .hero-cta { justify-content: center; }
  .hero-image img { max-width: 280px; }
}

@media (prefers-reduced-motion: reduce) {
  .bounce-float { animation: none; }
}
</style>