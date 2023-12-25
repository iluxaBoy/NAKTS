<script setup>
import { RouterView } from 'vue-router'
</script>

<template>
  <!-- <div class="noise"><img src="src\assets\img\шум.png" alt=""></div> -->
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
