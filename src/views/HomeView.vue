<script setup>
// import Loader from "../components/loader/Loader.vue";
import Grid from "../components/Home/Grid.vue";
import MovingCurves from "../components/Home/movingcurves.vue";
import BlockyCurves from "../components/Home/BlockyCurves.vue";
</script>

<template>
  <main>
    <!-- <Loader /> -->
    <Grid />
    <section>
      <MovingCurves />
      <BlockyCurves />
    </section>
  </main>
</template>

<style scoped lang="scss">
* {
  color: #F68D18;
}

section {
  padding: 0 10vw;
}
</style>
