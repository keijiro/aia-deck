<template>
  <div class="slidev-layout cover h-full relative">
    <img src="/unite-title-bg.png" class="absolute inset-0 w-full h-full object-cover" />
    <div class="title-box absolute flex items-center justify-center text-center">
      <slot />
    </div>
  </div>
</template>

<style scoped>
/* Geometry from the Unite template title layout:
   box (1.36, 1.49)in, 7.29 x 2.28in on a 10 x 5.625in slide */
.title-box {
  left: 13.6%;
  top: 26.5%;
  width: 72.9%;
  height: 40.5%;
}

.title-box :deep(h1) {
  font-size: 54px;
  line-height: 1.25;
}
</style>
