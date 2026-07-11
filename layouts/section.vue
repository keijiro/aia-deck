<template>
  <div class="slidev-layout section h-full relative">
    <img src="/unite-section-bg.jpg" class="absolute inset-0 w-full h-full object-cover" />
    <div class="title-box absolute flex items-center justify-center text-center">
      <slot />
    </div>
  </div>
</template>

<style scoped>
/* Geometry from the Unite template section layout:
   box (1.79, 1.23)in, 6.42 x 3.14in on a 10 x 5.625in slide, title 36pt */
.title-box {
  left: 17.9%;
  top: 21.9%;
  width: 64.2%;
  height: 55.8%;
}

.title-box :deep(h1) {
  font-size: 49px;
  line-height: 1.3;
}
</style>
