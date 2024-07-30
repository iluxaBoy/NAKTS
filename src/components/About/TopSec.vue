<script setup>
import { onMounted, ref } from 'vue'

const canvas = ref()

let centerX
let centerY

let circleArr = []

function Circle(startX, startD, stopX, stopD, increaser) {
  this.startX = startX
  this.startD = startD
  this.stopX = stopX
  this.stopD = stopD
  this.increaser = increaser
  this.changeX = this.startX + this.increaser
  this.changeD = this.startD + this.increaser
  this.index = 4

  this.draw = () => {
    const ctx = canvas.value.getContext('2d')
    ctx.beginPath()

    ctx.moveTo(centerX, canvas.value.height)
    ctx.lineTo(centerX, 0)
    ctx.moveTo(canvas.value.width, centerY)
    ctx.lineTo(0, centerY)

    ctx.arc(this.stopX, centerY, this.stopD, 0, 2 * Math.PI)

    ctx.arc(
      (this.changeX += this.index),
      centerY,
      (this.changeD += this.index),
      0,
      2 * Math.PI,
      false
    )

    ctx.stroke()
  }
  this.update = () => {
    this.draw()

    if (this.changeX >= this.stopX) {
      this.changeX = this.startX
      this.changeD = this.startD
      // this.index = 0
      this.draw()
    }
  }
}

const draw = () => {
  const ctx = canvas.value.getContext('2d')

  const bigArcX = 3840
  const bigArcD = 3700
  const smallArcX = 142
  const smallArcD = 2

  let increaser = 0

  ctx.strokeStyle = '#28fe62'
  ctx.lineWidth = 3

  ctx.beginPath()

  ctx.moveTo(centerX, canvas.value.height)
  ctx.lineTo(centerX, 0)
  ctx.moveTo(canvas.value.width, centerY)
  ctx.lineTo(0, centerY)

  ctx.arc(bigArcX, centerY, bigArcD, 0, 2 * Math.PI, false)
  ctx.stroke()

  for (let i = 0; i < 22; i++) {
    circleArr.push(new Circle(smallArcX, smallArcD, bigArcX, bigArcD, increaser))
    increaser += 165
  }

  const anim = () => {
    requestAnimationFrame(anim)
    ctx.clearRect(0, 0, canvas.value.width, canvas.value.height)
    for (let i = 0; i < circleArr.length; i++) {
      circleArr[i].update()
    }
  }
  anim()
}

// const updateScreenWidth = () => {
//   canvas.value.width = window.innerWidth - 500
//   canvas.value.height = canvas.value.width
// }
onMounted(() => {
  //   updateScreenWidth()
  canvas.value.width = window.innerWidth - 500
  canvas.value.height = canvas.value.width / 1.8

  centerX = canvas.value.width / 2
  centerY = canvas.value.height / 2
  draw()
})
</script>

<template>
  <div class="container">
    <section class="animation">
      <canvas ref="canvas"></canvas>
    </section>
    <section class="info">
      <h1>Lorem ipsum dolor sit.</h1>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Quos nobis saepe possimus expedita
        veritatis dolorem nemo aliquam aperiam! Beatae, quas magni voluptates architecto id veniam
        iure dolorum tempore! Ratione provident culpa nam itaque incidunt corporis pariatur
        quibusdam sint excepturi cum, quod omnis? Harum, quos magni maiores voluptatibus repellendus
        illo aspernatur dicta sunt deserunt, obcaecati alias enim accusamus praesentium, error
        assumenda eos veritatis illum? Repellendus deserunt placeat nesciunt distinctio ea magni.
      </p>
      <div>
        <button><RouterLink to="/">Home</RouterLink></button
        ><button><RouterLink to="/about">About</RouterLink></button><button>Info</button
        ><button>Sub</button>
      </div>
    </section>
  </div>
</template>

<style scoped lang="scss">
.container {
  position: relative;
  display: flex;
  justify-content: center;
  margin-top: 64px;
}
.animation {
  position: absolute;
}
.info {
  display: flex;
  flex-direction: column;
  padding: 24px 64px 44px;
  margin: 240px 0 0 730px;
  line-height: 28px;
  text-align: left;
  z-index: 2;
  p {
    width: 700px;
  }
  div {
    display: flex;
    justify-content: space-between;
    button {
      width: 100%;
      height: 100%;
      padding: 18px 24px;
      color: var(--primary-color-about);
      border: 4px solid var(--primary-color-about);
      border-right: none;
    }

    button:last-of-type {
      border: 4px solid var(--primary-color-about);
    }

    button:hover {
      background-color: var(--primary-color-about);
      color: var(--secondary-color-about);
    }
    button {
      background-color: inherit;
      font-family: 'Silkscreen', sans-serif;
      font-weight: bold;
      font-size: 1.2em;
    }
  }
}
canvas {
  background-image: radial-gradient(
    circle at center,
    var(--primary-color-about) 0.08rem,
    transparent 0
  );
  background-size: 5.3rem 5.7rem;
  background-position:
    0 0,
    0.65rem 0.65rem;
  // opacity: 0.7;
}
</style>
