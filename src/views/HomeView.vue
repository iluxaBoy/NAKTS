<script setup>
import Loader from "../components/loader/Loader.vue";
import Grid from "../components/Home/Animation/Grid.vue";
</script>

<template>
  <main>
    <!-- <Loader /> -->
    <Grid class="grid" />
  </main>
</template>

<style scoped lang="scss">
.grid {
  position: absolute;
  top: 0;
  left: 0;
}
</style>
