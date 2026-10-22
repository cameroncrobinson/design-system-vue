<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'
import PortfolioSection from './PortfolioSection.vue'
import ProgressBar from './ProgressBar.vue'

const props = defineProps({
  // IDs must be unique on the page and suitable for URL fragments.
  sections: { type: Array, default: () => [
    { id: 'section1', title: 'Section 1', image: 'https://bit.ly/2tS9x51' },
    { id: 'section2', title: 'Section 2', image: 'https://bit.ly/2RbLZA4' },
    { id: 'section3', title: 'Section 3', image: 'https://bit.ly/30gVGkI' },
    { id: 'section4', title: 'Section 4', image: 'https://bit.ly/2QTz5Yx' },
  ] },
})

const root = ref(null)
const progress = ref(0)
let frame = null
let observer

function updateProgress() {
  frame = null
  if (!root.value || !props.sections.length) {
    progress.value = 0
    return
  }
  const { top, height } = root.value.getBoundingClientRect()
  const distance = height - window.innerHeight
  // Progress belongs to this slider, even when other content surrounds it.
  progress.value = distance > 0
    ? Math.min(100, Math.max(0, (-top / distance) * 100))
    : (top <= 0 ? 100 : 0)
}

function scheduleUpdate() {
  if (frame === null) frame = window.requestAnimationFrame(updateProgress)
}

onMounted(() => {
  updateProgress()
  window.addEventListener('scroll', scheduleUpdate, { passive: true })
  window.addEventListener('resize', scheduleUpdate)
  if (typeof ResizeObserver !== 'undefined') {
    observer = new ResizeObserver(scheduleUpdate)
    observer.observe(root.value)
  }
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', scheduleUpdate)
  window.removeEventListener('resize', scheduleUpdate)
  observer?.disconnect()
  if (frame !== null) window.cancelAnimationFrame(frame)
})
</script>

<template>
  <div ref="root" class="portfolio-slider">
    <PortfolioSection
      v-for="(section, index) in sections"
      :key="section.id"
      :id="section.id"
      :title="section.title"
      :image="section.image"
      :previous-id="sections[Math.max(0, index - 1)].id"
      :next-id="sections[Math.min(sections.length - 1, index + 1)].id"
    >
      <slot name="section" :section="section" :index="index">
        <h2>{{ section.title }}</h2>
      </slot>
    </PortfolioSection>
    <ProgressBar :value="progress" />
  </div>
</template>

<style scoped>
.portfolio-slider { color: white; font-family: Montserrat, sans-serif; }
.portfolio-slider :deep(h2) { margin: 15px; }
</style>
