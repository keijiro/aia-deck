<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  image: {
    type: String,
  },
  class: {
    type: String,
  },
  backgroundSize: {
    type: String,
    default: '85%',
  },
})

function resolveAssetUrl(url: string) {
  if (url.startsWith('/'))
    return import.meta.env.BASE_URL + url.slice(1)
  return url
}

const style = computed(() => ({
  backgroundImage: props.image ? `url("${resolveAssetUrl(props.image)}")` : undefined,
  backgroundRepeat: 'no-repeat',
  backgroundPosition: 'center',
  backgroundSize: props.backgroundSize,
}))
</script>

<template>
  <div class="grid grid-cols-2 w-full h-full auto-rows-fr bg-black">
    <div class="slidev-layout default" :class="props.class">
      <slot />
    </div>
    <div class="w-full h-full" :style="style" />
  </div>
</template>
