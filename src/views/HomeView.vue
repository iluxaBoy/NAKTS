<script setup>
// import Loader from "../components/loader/Loader.vue";
import Grid from '../components/Home/Grid.vue'
import MovingCurves from '../components/Home/MovingCurves.vue'
import BlockyCurves from '../components/Home/BlockyCurves.vue'
import BottomSec from '../components/Home/BottomSec.vue'

let mobile = 762

// class for changeing size of canvas in other components
class ChangeSize {
  constructor(canvas) {
    this.canvas = canvas
    this.mobile = false
  }
  onScreenResize = () => {
    window.addEventListener('resize', () => {
      if (window.innerWidth <= 762) {
        this.updateScreenWidth()
      } else {
        this.defaultScreenWidth()
      }
    })
  }
  updateScreenWidth = () => {
    this.canvas.value.width = 250
    this.canvas.value.height = 125
  }
  defaultScreenWidth = () => {
    this.canvas.value.width = 500
    this.canvas.value.height = 250
  }
  checkScreen = () => {
    if (window.innerWidth <= 762) {
      this.updateScreenWidth()
      this.mobile = true
    } else {
      this.defaultScreenWidth()
      this.mobile = false
    }
  }
}
</script>

<template>
  <main>
    <!-- <Loader /> -->
    <Grid />
    <section>
      <MovingCurves :ChangeSize="ChangeSize" :mobile="mobile" />
      <BlockyCurves :ChangeSize="ChangeSize" :mobile="mobile" />
    </section>
    <BottomSec />
  </main>
</template>

<style scoped>
* {
  color: var(--primary-color-home);
}

section {
  padding: 0 10vw;
  margin-top: 36px;
}

section > * {
  margin-bottom: 172px;
}

main {
  overflow: hidden;
}
</style>
