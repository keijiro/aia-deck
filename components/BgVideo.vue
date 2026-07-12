<script setup lang="ts">
import { useNav, useSlideContext } from '@slidev/client'
import { computed } from 'vue'

const props = defineProps({
  src: { type: String, required: true },
  blur: { type: String, default: '12px' },
  brightness: { type: Number, default: 0.4 },
  scale: { type: Number, default: 1.1 },
  printTimestamp: { type: [Number, String], default: 3 },
})

const { $renderContext } = useSlideContext()
const { isPrintMode } = useNav()

// In print/export contexts, show a fixed frame instead of playing.
const noPlay = computed(() => isPrintMode.value || !['slide', 'presenter'].includes($renderContext.value))

function onLoadedMetadata(ev: Event) {
  const element = ev.target as HTMLMediaElement
  if (noPlay.value)
    element.currentTime = +props.printTimestamp
}
</script>

<template>
  <div class="absolute inset-0 -z-1">
    <video
      :autoplay="!noPlay"
      muted loop playsinline
      class="w-full h-full object-cover"
      :style="{
        filter: `blur(${blur}) brightness(${brightness})`,
        transform: `scale(${scale})`,
      }"
      @loadedmetadata="onLoadedMetadata"
    >
      <source :src="src" type="video/mp4" />
    </video>
  </div>
</template>
