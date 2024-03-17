<script setup>
import { onMounted, ref } from 'vue'

let showBox = ref(false)
let removeBtn = ref(false)

// make availeble to chenge size when for responsivnes
const width = window.innerWidth
const content = ref()
const main = ref()

var startAnimation = null

const createBox = (x, y, z) => {
  const clone = main.value.cloneNode(true)

  clone.className = 'box'
  clone.style.display = 'block'
  clone.style.position = 'absolute'
  clone.style.top = `${x}px`
  clone.style.left = `${y}px`
  clone.style.zIndex = z

  content.value.appendChild(clone)
}

const createAnimation = () => {
  let x = 0
  let y = 0
  let z = 0

  x = Math.floor(Math.random() * (100 - -50) + -50)
  y = Math.floor(Math.random() * width - 1000)
  z--
  createBox(x, y, z)
}

onMounted(() => {
  startAnimation = () => {
    removeBtn.value = true
    window.scrollPosition = 100
    let intervalId = null
    let index = 0

    intervalId = setInterval(() => {
      if (index !== 6) {
        createAnimation()
        index++
      } else {
        clearInterval(intervalId)
        intervalId = null
        showBox.value = true
      }
    }, 200)
  }
})
</script>

<template>
  <div class="container">
    <button v-if="!removeBtn" @click="startAnimation()">Some text</button>
    <div ref="content" class="content">
      <div v-show="showBox" ref="main" class="box main">
        <div class="top">
          <h3>Info</h3>
          <button>X</button>
        </div>
        <div class="mid">
          <h1>Some Main Text</h1>
          <p>
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Culpa quia veritatis vel
            exercitationem dolore aut corrupti ex atque cumque praesentium consectetur quos quam
            delectus voluptatum nobis ducimus numquam nesciunt, cupiditate, dolorem qui deleniti
            eaque fuga! Cum expedita, ipsam nisi voluptate omnis fugiat tenetur sequi minus dolore
            temporibus eos odio reiciendis!
          </p>
          <div class="bottom">
            <button>Continue</button>
            <button>Cancel</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.container {
  display: flex;
  overflow: hidden;
  flex-direction: column;
  align-items: center;
  height: 660px;
  padding: 35px 0 0;
  font-family: 'Handjet', sans-serif;

  .content {
    position: relative;

    .box {
      width: 1000px;
      background-color: var(--secondary-color-home);
      border: 4px solid var(--primary-color-home);

      .top {
        display: flex;
        justify-content: space-between;
        padding: 0 14px;
        align-items: center;
        text-align: center;
        background-color: var(--primary-color-home);
        color: var(--secondary-color-home);

        button {
          border: none;
          background-color: var(--primary-color-home);
          color: var(--secondary-color-home);
        }
      }

      .mid {
        padding: 44px 66px;

        p {
          margin-top: 24px;
        }

        .bottom {
          display: flex;
          justify-content: space-between;
          margin-top: 34px;

          button {
            padding: 12px 22px;
            font-size: 1.7rem;
            border: none;
            background-color: var(--primary-color-home);
            color: var(--secondary-color-home);
          }
        }
      }
    }

    .main {
      margin: auto;
      position: static;
    }
  }

  h1 {
    font-family: 'Silkscreen', sans-serif;
    line-height: 40px;
    font-size: 3.4rem;
    font-weight: 700;
  }

  button {
    padding: 12px 22px;
    background-color: var(--secondary-color-home);
    border: 2px solid var(--primary-color-home);
    color: var(--primary-color-home);
    font-family: 'Silkscreen', sans-serif;
    font-size: 2rem;
  }
}
</style>
