<script setup>
import { RouterView } from 'vue-router';
</script>

<template>
  <RouterView />
</template>

<style lang="scss">
.noise {
  position: fixed;
  top: 0;
  left: 0;
  // opacity: 0.06;
  mix-blend-mode: overlay;
}
</style>
