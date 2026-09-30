<script setup>
import { reactive, ref, onMounted, onBeforeUnmount } from 'vue'
import { FORMSPREE_URL, contactInfo } from '../data'

const driven = ref(false)
let driveTimer = null
let statusTimer = null

onMounted(() => {
  driveTimer = setTimeout(() => { driven.value = true }, 350)
})

onBeforeUnmount(() => {
  clearTimeout(driveTimer)
  clearTimeout(statusTimer)
})

const emptyForm = () => ({ name: '', email: '', phone: '', message: '', _gotcha: '' })
const form = reactive(emptyForm())
const status = ref('') // '' | 'sending' | 'sent' | 'error'
const errorMsg = ref('')

function setStatus(value, clearAfterMs = 0) {
  clearTimeout(statusTimer)
  status.value = value
  if (clearAfterMs) statusTimer = setTimeout(() => { status.value = '' }, clearAfterMs)
}

async function send() {
  if (status.value === 'sending') return
  errorMsg.value = ''
  setStatus('sending')

  try {
    const res = await fetch(FORMSPREE_URL, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', Accept: 'application/json' },
      body: JSON.stringify(form),
    })

    if (!res.ok) throw new Error(`Request failed (${res.status})`)

    Object.assign(form, emptyForm())
    setStatus('sent', 6000)
  } catch (err) {
    errorMsg.value = err.message || 'Something went wrong.'
    setStatus('error', 8000)
  }
}
</script>

<template>
  <main>
    <section class="contact">
      <div class="container">

        <!-- BIG ANIMATED TITLE -->
        <h1 class="hero-title">
          Let's make
          <span class="drive" :class="{ go: driven }">something</span>
          happen.
        </h1>

        <h2 class="subtitle">Contact Me</h2>

        <p class="sub-text">
          Have a project in mind, or just want to say hello?
          Send a message and I'll get back to you.
        </p>

        <div class="contact-content">

          <div class="contact-info">
            <h3>Get In Touch</h3>
            <div class="info-item">
              <i class="fas fa-envelope"></i>
              <span>{{ contactInfo.email }}</span>
            </div>
            <div class="info-item">
              <i class="fas fa-location-dot"></i>
              <span>{{ contactInfo.location }}</span>
            </div>
          </div>

          <div class="contact-form">
            <form @submit.prevent="send">
              <input v-model.trim="form.name" type="text" name="name" placeholder="Full Name" required>
              <input v-model.trim="form.email" type="email" name="email" placeholder="Email Address" required>
              <input v-model.trim="form.phone" type="tel" name="phone" placeholder="Phone Number">
              <textarea v-model.trim="form.message" name="message" rows="5" placeholder="Your Message" required></textarea>

              <input
                v-model="form._gotcha"
                type="text"
                name="_gotcha"
                class="honeypot"
                tabindex="-1"
                autocomplete="off"
                aria-hidden="true"
              >

              <button type="submit" :disabled="status === 'sending'">
                {{ status === 'sending' ? 'Sending…' : 'Send Message' }}
              </button>

              <p v-if="status === 'sent'" class="status-msg success" role="status">Message sent!</p>
              <p v-if="status === 'error'" class="status-msg error" role="alert">{{ errorMsg }}</p>
            </form>
          </div>
        </div>

      </div>
    </section>
  </main>
</template>

<style scoped>
/* Layout */
.contact {
  padding: 160px 5% 100px 5%;
  min-height: 100vh;
  overflow-x: hidden;
}

.container {
  width: 90%;
  max-width: 1100px;
  margin: auto;
}

/* title */
.hero-title {
  text-align: center;
  font-size: clamp(2rem, 5vw, 3.8rem);
  font-weight: 500;
  color: var(--color-dark);
  line-height: 1.2;
  margin-bottom: 12px;
  font-family: var(--font-sans);
}

/* animated word slides in from right */
.drive {
  display: inline-block;
  font-style: italic;
  font-weight: 700;
  background: linear-gradient(90deg, #e42074 0%, #eb6b27 100%);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  color: transparent;
  opacity: 0;
  transform: translateX(110vw) skewX(-22deg);
  will-change: transform, opacity;
  padding: 0 4px;
}

.drive.go {
  animation: driveIn 1.3s cubic-bezier(.16, .84, .3, 1) forwards;
}

@keyframes driveIn {
  0%   { opacity: 1; transform: translateX(110vw) skewX(-22deg); filter: blur(10px); }
  65%  { opacity: 1; transform: translateX(-16px) skewX(8deg);   filter: blur(0); }
  82%  { transform: translateX(6px) skewX(-3deg); }
  100% { opacity: 1; transform: none; }
}

.subtitle {
  text-align: center;
  font-size: clamp(1.1rem, 2vw, 1.6rem);
  font-weight: 500;
  color: var(--color-accent);
  text-transform: uppercase;
  letter-spacing: 6px;
  margin-bottom: 24px;
  font-family: var(--font-sans);
}

.sub-text {
  text-align: center;
  max-width: 620px;
  margin: 0 auto 70px auto;
  font-size: 1.05rem;
  color: var(--color-subtext);
  line-height: 1.7;
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1.3fr;
  gap: 60px;
  align-items: start;
}

.contact-info h3 {
  color: var(--color-accent);
  font-size: 1.3rem;
  margin-bottom: 22px;
}

.info-item {
  display: flex;
  align-items: center;
  gap: 14px;
  margin: 18px 0;
  color: var(--color-dark);
  font-size: 0.98rem;
}

.info-item i {
  font-size: 15px;
  color: var(--color-accent);
  border: 1.5px solid var(--color-accent);
  padding: 11px;
  border-radius: 50%;
  width: 42px;
  height: 42px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.contact-form form {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.contact-form input,
.contact-form textarea {
  width: 100%;
  padding: 16px 18px;
  border: 1px solid var(--color-card-border);
  border-radius: 10px;
  background: var(--color-input-bg);
  color: var(--color-dark);
  font-size: 0.98rem;
  font-family: inherit;
  transition: border-color 0.25s ease, box-shadow 0.25s ease;
}

.contact-form input::placeholder,
.contact-form textarea::placeholder {
  color: var(--color-subtext);
  opacity: 0.7;
}

.contact-form input:focus,
.contact-form textarea:focus {
  outline: none;
  border-color: var(--color-accent);
  box-shadow: 0 0 0 3px rgba(228, 32, 116, 0.12);
}

[data-theme="dark"] .contact-form input:focus,
[data-theme="dark"] .contact-form textarea:focus {
  box-shadow: 0 0 0 3px rgba(255, 140, 66, 0.2);
}

.contact-form textarea {
  resize: vertical;
  min-height: 140px;
}

.contact-form input.honeypot {
  position: absolute;
  left: -9999px;
  width: 1px;
  height: 1px;
  padding: 0;
  border: 0;
  opacity: 0;
  pointer-events: none;
}

.contact-form button {
  padding: 16px;
  background: var(--color-accent);
  color: #fff;
  border: none;
  border-radius: 10px;
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: transform 0.2s ease, opacity 0.2s ease, box-shadow 0.3s ease;
  font-family: inherit;
  margin-top: 8px;
}

.contact-form button:hover:not(:disabled) {
  opacity: 0.92;
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(228, 32, 116, 0.3);
}

.contact-form button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.status-msg {
  text-align: center;
  font-weight: 500;
  margin-top: 8px;
}
.status-msg.success { color: var(--color-accent); }
.status-msg.error { color: #e42074; }

/* Reduced motion */
@media (prefers-reduced-motion: reduce) {
  .drive { transform: none; }
  .drive.go { animation: softIn 0.8s ease forwards !important; }
  @keyframes softIn { from { opacity: 0; } to { opacity: 1; } }
}

/* Mobile */
@media (max-width: 768px) {
  .contact { padding: 130px 5% 60px 5%; }

  .subtitle { letter-spacing: 4px; }
  .sub-text { margin-bottom: 50px; }

  .contact-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }
}
</style>