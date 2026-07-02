<script setup lang="ts">
defineProps({
  video: {
    type: String,
  },
  // 'contain' で全体表示（見切れなし）、'cover' で枠を充填（見切れあり）
  fit: {
    type: String,
    default: 'contain',
  },
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
      <source :src="video" type="video/mp4" />
    </SlidevVideo>
  </div>
</template>
