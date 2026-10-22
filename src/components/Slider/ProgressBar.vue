<script setup>
import { computed } from 'vue'

const props = defineProps({ value: { type: Number, default: 0 } })
const percentage = computed(() => Number.isFinite(props.value)
  ? Math.min(100, Math.max(0, props.value)) : 0)
</script>

<template>
  <div
    class="progress-container"
    role="progressbar"
    aria-label="Portfolio scroll progress"
    :aria-valuenow="Math.round(percentage)"
    :aria-valuemin="0"
    :aria-valuemax="100"
  >
    <div class="progress-bar" :style="{ width: `${percentage}%` }" />
  </div>
</template>

<style scoped>
.progress-container { position: fixed; top: 0; left: 0; z-index: 100; width: 100%; height: 8px; background: #ccc; pointer-events: none; }
.progress-bar { height: 100%; background: #4caf50; }
</style>
