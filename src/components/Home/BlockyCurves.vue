<script setup>
import { onMounted, ref } from 'vue'

const canvas = ref()

const props = defineProps({
  ChangeSize: {
    type: Object
  },
  mobile: {
    type: Number
  }
})

let ifMobile = false
const verticalCount = ref(5)
const horisontalCount = ref(10)

const drawGraph = () => {
  const ctx = canvas.value.getContext('2d')

  let amplitude = 160
  let frequency = 0.01
  let phi = 0
  let frames = 0
  let ampChange = 2

  let width = 25
  let height = 30

  ctx.lineWidth = 2
  ctx.strokeStyle = '#F68D18'

  if (ifMobile) {
    amplitude = 50
    width = 18
    height = 23
    ampChange = 1.5
  }

  const Draw = () => {
    frames++
    phi = frames / 30

    ctx.clearRect(0, 0, canvas.value.width, canvas.value.height)

    for (let i = 0; i < canvas.value.width - 25; i += 40) {
      let y = (Math.sin(i * frequency + phi) * amplitude) / 2 + amplitude / ampChange
      ctx.strokeRect(i + width, y + 15, width, height)
    }

    window.requestAnimationFrame(Draw)
  }

  window.requestAnimationFrame(Draw)
}

const checkIfMobile = () => {
  change.checkScreen()
  ifMobile = change.mobile
  if (ifMobile) {
    verticalCount.value = 3
    horisontalCount.value = 5
  }
  drawGraph()
}

const change = new props.ChangeSize(canvas)

onMounted(() => {
  checkIfMobile()

  change.onScreenResize()

  canvas.value.width = change.canvas.value.width
  canvas.value.height = change.canvas.value.height

  window.addEventListener('resize', () => {
    drawGraph()
    if (window.innerWidth <= props.mobile) {
      ifMobile = true
      verticalCount.value = 3
      horisontalCount.value = 5
    } else {
      ifMobile = false
      verticalCount.value = 5
      horisontalCount.value = 10
    }
  })

  drawGraph()
})
</script>

<template>
  <div class="container">
    <div class="animation">
      <div class="diagram">
        <div class="left">
          <ul>
            <li v-for="n in verticalCount">{{ n }}</li>
          </ul>
        </div>
        <div class="bottom">
          <ul>
            <li v-for="n in horisontalCount">{{ n }}</li>
          </ul>
        </div>
      </div>
      <canvas ref="canvas"> </canvas>
      <div class="diagram-info">
        <ul>
          <li>&#60;&#62;Lorem ipsum dolor sit amet.</li>
          <li>&#60;-Lorem ipsum dolor sit amet consectetur.</li>
          <li>&#60;-Lorem ipsum dolor sit amet consectetur adipisicing.</li>
        </ul>
      </div>
    </div>
    <div class="info">
      <h1>Lorem ipsum dolor sit amet.</h1>
      <p>
        Lorem ipsum, dolor sit amet consectetur adipisicing elit. Ullam temporibus adipisci aliquam
        quia dolore tenetur sint illum doloremque error dolor facere consequatur, cumque saepe ipsa
        ab qui atque at sunt repellendus? Eum, quibusdam aspernatur atque dignissimos sequi dolore
        quia delectus consequatur perferendis voluptas nemo dolor, eius labore dolorem eveniet
        natus.
      </p>
    </div>
  </div>
</template>

<style scoped lang="scss">
.container {
  display: flex;
  flex-direction: row-reverse;
  justify-content: space-between;
  font-family: 'Handjet', sans-serif;

  .animation {
    position: relative;
    font-size: 24px;
    max-width: 510px;

    .diagram {
      margin-left: 12px;

      .left {
        padding-top: 14px;

        ul {
          display: flex;
          flex-direction: column-reverse;
          justify-content: space-between;
          height: 200px;
        }
      }

      .bottom {
        margin-left: 14px;

        ul {
          display: flex;
          justify-content: space-between;
          margin-right: 12px;
        }
      }
    }

    .diagram-info {
      margin-top: 24px;
      padding: 4px 8px;
      border: 3px dotted #f68d18;
      width: 505px;
    }
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
    }
  }
}

ul {
  list-style: none;
}

canvas {
  position: absolute;
  top: 0;
  right: 0;
  border: 3px solid #f68d18;
}

@media (max-width: 762px) {
  .container {
    .animation {
      .diagram {
        margin: auto;
        width: 244px;
        font-size: 18px;
        .left {
          padding-top: 18px;
          ul {
            height: 84px;
          }
        }
      }
    }
    .desk-top {
      display: none;
    }
    .diagram-info {
      max-width: 364px;
      font-size: 18px;
    }
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

  canvas {
    top: 0;
    right: 15%;
  }
}
</style>
