<script setup lang="ts">
import { useNav, useSlideContext } from '@slidev/client'
import { computed } from 'vue'

const props = defineProps({
  src: { type: String, required: true },
  blur: { type: String, default: '12px' },
  brightness: { type: Number, default: 0.4 },
  scale: { type: Number, default: 1.1 },
  printTimestamp: { type: [Number, String], default: 3 },
  printPoster: { type: String, default: null },
})

const { $renderContext } = useSlideContext()
const { isPrintMode } = useNav()

// Absolute public paths are not rewritten in component props at build time,
// so prepend the configured base (e.g. --base /aia-deck/) here.
function resolveAssetUrl(url: string) {
  if (url.startsWith('/'))
    return import.meta.env.BASE_URL + url.slice(1)
  return url
}

const videoSrc = computed(() => resolveAssetUrl(props.src))

// In print/export contexts, show a fixed frame instead of playing.
const noPlay = computed(() => isPrintMode.value || !['slide', 'presenter'].includes($renderContext.value))

// Poster shown in print/export (headless browsers do not paint seeked video
// frames); defaults to a "-print.jpg" image next to the video.
const poster = computed(() => noPlay.value
  ? resolveAssetUrl(props.printPoster ?? props.src.replace(/\.mp4$/, '-print.jpg'))
  : undefined)

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
      :poster="poster"
      :preload="noPlay ? 'none' : 'auto'"
      muted loop playsinline
      class="w-full h-full object-cover"
      :style="{
        filter: `blur(${blur}) brightness(${brightness})`,
        transform: `scale(${scale})`,
      }"
      @loadedmetadata="onLoadedMetadata"
    >
      <source :src="videoSrc" type="video/mp4" />
    </video>
  </div>
</template>
