<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  n: { type: Number, default: 4 },
  color: { type: String, default: 'currentColor' },
  palette: { type: Array as () => string[], default: null },
  // When given, dot colors are deterministic — tiles sharing a seed (and the
  // same n / palette) render an identical pattern.
  seed: { type: Number, default: null },
})

// Deterministic PRNG (mulberry32) so a seeded tile reproduces the same pattern.
function makeRandom(seed: number) {
  let s = seed >>> 0
  return () => {
    s |= 0
    s = (s + 0x6d2b79f5) | 0
    let t = Math.imul(s ^ (s >>> 15), 1 | s)
    t = (t + Math.imul(t ^ (t >>> 7), 61 | t)) ^ t
    return ((t ^ (t >>> 14)) >>> 0) / 4294967296
  }
}

// Assign each dot a color: random pick from palette when given, otherwise the
// single uniform color.
const dots = computed(() => {
  const rand = props.seed != null ? makeRandom(props.seed) : Math.random
  return Array.from({ length: props.n * props.n }, () =>
    props.palette && props.palette.length
      ? props.palette[Math.floor(rand() * props.palette.length)]
      : props.color
  )
})
</script>

<template>
  <div class="density-tile" :style="{ '--n': n }">
    <div
      v-for="(c, i) in dots"
      :key="i"
      class="dot"
      :style="{ background: c }"
    />
  </div>
</template>

<style scoped>
.density-tile {
  display: grid;
  grid-template-columns: repeat(var(--n), 1fr);
  gap: 0.12rem;
  place-items: center;
  width: 6rem;
  height: 6rem;
  padding: 0.4rem;
  border: 1px solid rgba(128, 128, 128, 0.5);
  border-radius: 0.5rem;
  box-sizing: border-box;
  transition: all 0.4s ease;
}
.dot {
  width: 100%;
  aspect-ratio: 1;
  border-radius: 50%;
}
</style>
