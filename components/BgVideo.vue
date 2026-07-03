<script setup lang="ts">
defineProps({
  src: { type: String, required: true },
  blur: { type: String, default: '12px' },
  brightness: { type: Number, default: 0.4 },
  scale: { type: Number, default: 1.1 },
})
</script>

<template>
  <div class="absolute inset-0 -z-1">
    <video
      autoplay muted loop playsinline
      class="w-full h-full object-cover"
      :style="{
        filter: `blur(${blur}) brightness(${brightness})`,
        transform: `scale(${scale})`,
      }"
    >
      <source :src="src" type="video/mp4" />
    </video>
  </div>
</template>
