<script setup>
import { onMounted, ref } from 'vue'

//two canvas for more easier work with visuals
const canvas1 = ref()
const canvas2 = ref()

const props = defineProps({
  ChangeSize: {
    type: Object
  },
  mobile: {
    type: Number
  }
})

//var for "removing" second canvas
let ifMobile = false

//vars for showing percentage
let pros1 = ref(0)
let pros2 = ref(0)
let pros3 = ref(0)

//fun to draw graf
const drawGraph = () => {
  const ctx = canvas1.value.getContext('2d')

  let amplitude = 200
  let frequency = 0.01
  let phi = 0
  let frames = 0

  ctx.lineWidth = 2
  ctx.strokeStyle = '#0E0505'

  if (ifMobile) amplitude = 50

  const Draw = () => {
    frames++
    phi = frames / 30

    ctx.clearRect(0, 0, canvas1.value.width, canvas1.value.height)
    ctx.beginPath()

    for (let i = 0; i < canvas1.value.width; i++) {
      let y = (Math.sin(i * frequency + phi) * amplitude) / 2 + amplitude / 2
      ctx.lineTo(i, y + 40)
      ctx.lineTo(i, y - canvas1.value.height)
    }

    ctx.stroke()
    window.requestAnimationFrame(Draw)
  }

  window.requestAnimationFrame(Draw)
}

//fun to draw loaders
const drawLoader = (y, frame, pros) => {
  const ctx = canvas2.value.getContext('2d')

  let recWidth = 250
  let recHeight = 30
  let x = canvas2.value.width / 3.5
  let tempW = 0

  ctx.lineWidth = 2
  ctx.strokeStyle = '#F68D18'
  ctx.fillStyle = '#F68D18'

  ctx.strokeRect(x, y, recWidth, recHeight)

  const Draw = () => {
    setInterval(() => {
      if (tempW >= recWidth) {
        ctx.clearRect(x + 1, y + 1, tempW - 2, recHeight - 2)

        tempW = 0
        pros.value = 0
      }

      pros.value += 1

      ctx.fillRect(x, y, (tempW += 1), recHeight)
    }, frame)
  }

  window.requestAnimationFrame(Draw)
}

//fun to check if web was loaded on smaller screen
const checkIfMobile = () => {
  change.checkScreen()
  ifMobile = change.mobile
  drawGraph()
}

const change = new props.ChangeSize(canvas1)

onMounted(() => {
  checkIfMobile()

  change.onScreenResize()

  canvas1.value.width = change.canvas.value.width
  canvas1.value.height = change.canvas.value.height
  //canvas2 has static size because it shows only at certain width
  canvas2.value.width = 500
  canvas2.value.height = 250

  //fun to check on resize and "remove" second canvas
  window.addEventListener('resize', () => {
    if (window.innerWidth <= props.mobile) {
      drawGraph()
      ifMobile = true
    } else {
      drawGraph()
      ifMobile = false
    }
  })

  drawGraph()
  drawLoader(15, 0, pros1)
  drawLoader(65, 20, pros2)
  drawLoader(115, 90, pros3)
})
</script>

<template>
  <div class="container">
    <section class="animation">
      <div class="top">
        <canvas class="draw" ref="canvas1"> </canvas>
      </div>
      <div class="bottom">
        <canvas v-show="!ifMobile" class="loader" ref="canvas2"> </canvas>
        <div class="text">
          <div class="files">
            <div>
              <span>[1] Some File</span>
            </div>
            <div>
              <span>{{ pros1 }}%</span>
            </div>
          </div>
          <div class="files">
            <div>
              <span>[2] Some File</span>
            </div>
            <div>
              <span>{{ pros2 }}%</span>
            </div>
          </div>
          <div class="files">
            <div>
              <span>[3] Some File</span>
            </div>
            <div>
              <span>{{ pros3 }}%</span>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section class="info">
      <h1>Worem ipsum doWor sit amet</h1>
      <h1>Worem ipsum doWor sit amet</h1>
      <h1>Worem ipsum doWor sit amet</h1>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Dicta hic, blanditiis fugiat ad rem
        consequatur omnis aliquid. A iste possimus accusamus explicabo sapiente id laboriosam quasi
        magnam quidem officia consectetur corporis, voluptatibus mollitia voluptas tempore laborum
        eum doloremque, dolor praesentium esse vel. Nihil architecto possimus praesentium quia enim
        dolorum inventore.
      </p>
    </section>
  </div>
</template>

<style scoped lang="scss">
.container {
  display: flex;
  justify-content: space-between;
  font-family: 'Handjet', sans-serif;

  .animation {
    max-width: 510px;
  }

  .info {
    display: flex;
    flex-direction: column;
    padding-left: 24px;
    max-width: 824px;

    h1 {
      font-family: 'Silkscreen', sans-serif;
      line-height: 40px;
      font-size: 2.4rem;
      font-weight: 700;
    }

    p {
      margin-top: 14px;
    }
  }
}

@media (max-width: 1656px) {
  .container {
    .info {
      margin-top: 24px;
      max-width: 624px;

      h1 {
        font-size: 1.8rem;
        line-height: normal;
        text-align: left;
      }

      p {
        font-size: 1.6rem;
      }
    }
  }
}

@media (max-width: 1420px) {
  .container {
    flex-direction: column;
    align-items: center;

    .info {
      padding: 0;
      max-width: 598px;
    }
  }
}

@media (max-width: 762px) {
  .container {
    .info {
      max-width: 462px;
      h1 {
        font-size: 1.4rem;
      }
      p {
        font-size: 1rem;
      }
    }
  }
}

.draw {
  border: 3px solid #f68d18;
  background: #f68d18;
}

.loader {
  position: absolute;
  top: 0;
}

.bottom {
  position: relative;
  max-width: 504px;

  .text {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 140px;
    padding-top: 14px;
    font-size: 24px;

    .files {
      display: flex;
      justify-content: space-between;
      text-align: end;
    }
  }
}

@media (max-width: 762px) {
  .bottom {
    .text {
      height: 100px;
      font-size: 18px;
    }
  }
}
</style>
