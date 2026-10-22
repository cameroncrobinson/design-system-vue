<script setup>
defineProps({
  id: { type: String, required: true },
  title: { type: String, required: true },
  image: { type: String, default: '' },
  previousId: { type: String, required: true },
  nextId: { type: String, required: true },
})

function navigate(event, targetId) {
  const target = document.getElementById(targetId)
  if (!target) return
  event.preventDefault()
  target.scrollIntoView({
    behavior: window.matchMedia('(prefers-reduced-motion: reduce)').matches ? 'instant' : 'smooth',
    block: 'start',
  })
  target.focus({ preventScroll: true })
}
</script>

<template>
  <section
    :id="id"
    class="portfolio-section"
    :aria-label="title"
    tabindex="-1"
    :style="{ backgroundImage: image ? `url(${JSON.stringify(image)})` : undefined }"
  >
    <a :href="`#${previousId}`" class="arrow arrow-up" aria-label="Previous section" @click="navigate($event, previousId)">
      <svg aria-hidden="true" viewBox="0 0 24 24"><path d="M12 20V4M5 11l7-7 7 7" /></svg>
    </a>
    <div class="section-content"><slot><h2>{{ title }}</h2></slot></div>
    <a :href="`#${nextId}`" class="arrow arrow-down" aria-label="Next section" @click="navigate($event, nextId)">
      <svg aria-hidden="true" viewBox="0 0 24 24"><path d="M12 4v16M5 13l7 7 7-7" /></svg>
    </a>
  </section>
</template>

<style scoped>
.portfolio-section {
  box-sizing: border-box;
  min-height: 100vh;
  min-height: 100svh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #263238;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  background-attachment: fixed;
  padding: 24px 12px;
}
.section-content { min-width: 0; overflow-wrap: anywhere; }
h2 { margin: 15px; }
.arrow { display: inline-flex; align-items: center; justify-content: center; flex-shrink: 0; width: 44px; height: 44px; color: inherit; }
.arrow svg { width: 20px; height: 20px; fill: none; stroke: currentColor; stroke-width: 2; }
.arrow:focus-visible { outline: 2px solid currentColor; outline-offset: 3px; }
.arrow-up:hover svg { animation: bounce-up 1s infinite; }
.arrow-down:hover svg { animation: bounce-down 1s infinite; }
@keyframes bounce-up { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }
@keyframes bounce-down { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(10px); } }
@media (hover: none) { .portfolio-section { background-attachment: scroll; } }
@media (prefers-reduced-motion: reduce) { .arrow svg { animation: none !important; } }
</style>
