<script setup>
import { RouterView, useRoute } from 'vue-router'
import { watch } from 'vue'

const router = useRoute()

const homePageColor = () => {
  document.body.style.backgroundColor = '#0e0505'
}

const aboutPageColor = () => {
  document.body.style.backgroundColor = '#000800'
  // console.log(document.body.style.scrollbarFaceColor)
}

watch(
  () => router.path,
  (newPath) => {
    if (newPath === '/about') {
      aboutPageColor()
    } else {
      homePageColor()
    }
  }
)
</script>

<template>
  <img src="./assets/img/noise.png" alt="" />
  <RouterView />
</template>

<style scoped>
img {
  position: absolute;
  top: 0;
  left: 0;
  opacity: 0.09;
}
</style>
