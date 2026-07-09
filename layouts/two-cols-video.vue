<script setup lang="ts">
const props = defineProps({
  class: {
    type: String,
  },
  layoutClass: {
    type: String,
  },
})
</script>

<template>
  <div class="slidev-layout two-columns w-full h-full grid grid-cols-2 auto-rows-fr gap-x-8" :class="props.layoutClass">
    <div class="col-left min-h-0" :class="props.class">
      <slot />
      <slot name="left" />
    </div>
    <div
      class="col-right min-h-0 overflow-hidden flex items-center justify-center
             [&_video]:w-full [&_video]:h-full [&_video]:object-contain
             [&_img]:w-full [&_img]:h-full [&_img]:object-contain"
      :class="props.class"
    >
      <slot name="right" />
    </div>
  </div>
</template>
