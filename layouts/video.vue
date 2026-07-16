<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  video: {
    type: String,
  },
  // 'contain' で全体表示（見切れなし）、'cover' で枠を充填（見切れあり）
  fit: {
    type: String,
    default: 'contain',
  },
})

// Absolute public paths are not rewritten in component props at build time,
// so prepend the configured base (e.g. --base /aia-deck/) here.
const videoSrc = computed(() => {
  if (props.video?.startsWith('/'))
    return import.meta.env.BASE_URL + props.video.slice(1)
  return props.video
})
</script>

<template>
  <div class="slidev-layout default flex flex-col">
    <slot />
    <SlidevVideo
      autoplay
      loop
      muted
      class="flex-1 min-h-0 w-full mt-4"
      :class="fit === 'cover' ? 'object-cover' : 'object-contain'"
    >
      <source :src="videoSrc" type="video/mp4" />
    </SlidevVideo>
  </div>
</template>
