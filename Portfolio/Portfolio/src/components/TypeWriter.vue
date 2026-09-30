<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// Words to type, passed in from the parent
const props = defineProps({
  words: { type: Array, required: true },
})

// Text shown on screen
const text = ref('')

// Speeds in milliseconds
const TYPING_SPEED = 85
const DELETING_SPEED = 40
const PAUSE_AFTER_TYPING = 1400
const PAUSE_AFTER_DELETING = 350

// Set to false to stop the loop
let isRunning = true

// Wait for a number of milliseconds
function sleep(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms))
}

// Add one letter at a time
async function typeWord(word) {
  for (let i = 1; i <= word.length; i++) {
    if (!isRunning) return
    text.value = word.slice(0, i)
    await sleep(TYPING_SPEED)
  }
}

// Remove one letter at a time
async function deleteWord(word) {
  for (let i = word.length - 1; i >= 0; i--) {
    if (!isRunning) return
    text.value = word.slice(0, i)
    await sleep(DELETING_SPEED)
  }
}

// Type, wait, delete, next word, repeat
async function runTypewriter() {
  let wordIndex = 0

  while (isRunning) {
    const word = props.words[wordIndex]

    await typeWord(word)
    await sleep(PAUSE_AFTER_TYPING)
    await deleteWord(word)
    await sleep(PAUSE_AFTER_DELETING)

    // Go back to the first word after the last
    wordIndex = (wordIndex + 1) % props.words.length
  }
}

onMounted(runTypewriter)

// Stop when the component is removed
onUnmounted(() => {
  isRunning = false
})
</script>

<template>
  <p class="hero-subtitle">
    I'm a
    <span class="role-highlight">{{ text }}</span>
    <span class="typing-cursor">|</span>
  </p>
</template>

<style scoped>
.hero-subtitle {
  font-size: clamp(1.2rem, 3.2vw, 1.8rem);
  color: var(--color-subtext);
  font-weight: 400;
  min-height: 2.2em; /* stops the layout jumping */
  display: flex;
  align-items: center;
  justify-content: center;
}

.role-highlight {
  color: var(--color-accent);
  font-weight: 600;
  margin-left: 0.3em;
}

/* Blinking cursor */
.typing-cursor {
  display: inline-block;
  color: var(--color-accent);
  font-weight: 300;
  margin-left: 2px;
  animation: blinkCursor 0.8s step-end infinite;
}

@keyframes blinkCursor {
  0%, 100% { opacity: 1; }
  50%      { opacity: 0; }
}
</style>