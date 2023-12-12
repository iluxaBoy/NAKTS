<script setup>
// import Loader from "../components/loader/Loader.vue";
import Grid from "../components/Home/Animation/Grid.vue";
import MovingCurves from "../components/Home/Animation/MovingCurves.vue";
</script>

<template>
  <main>
    <!-- <Loader /> -->
    <Grid />
    <section>
      <MovingCurves />
    </section>
  </main>
</template>

<style scoped lang="scss">
section {
  padding: 0 10vw;
}
</style>
