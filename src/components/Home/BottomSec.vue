<script setup>
import { onMounted, ref } from 'vue'

let showBox = ref(false)
let removeBtn = ref(false)

const content = ref()
const main = ref()

let intervalId = null

var startAnimation = null
var closeAllBox = null

const createBox = (x, y, z) => {
  const clone = main.value.cloneNode(true)

  clone.className = 'box clone'
  clone.style.display = 'block'
  clone.style.position = 'absolute'
  clone.style.top = `${x}px`
  clone.style.left = `${y}px`
  clone.style.zIndex = z

  content.value.appendChild(clone)
}

const createAnimation = () => {
  const width = window.innerWidth

  let x = 0
  let y = main.value.style.width
  let z = 0

  x = Math.floor(Math.random() * (100 - -50) + -50)
  y = Math.floor(Math.random() * width - main.value.style.width - 300)
  z--
  console.log(x, y, z)
  createBox(x, y, z)
}

const loadDOMfun = () => {
  closeAllBox = () => {
    const select = document.querySelectorAll('.clone')

    let index = 0

    intervalId = setInterval(() => {
      if (index !== 6) {
        select[index].remove()
        index++
      } else {
        clearInterval(intervalId)
        intervalId = null

        showBox.value = false
        removeBtn.value = false
      }
    }, 200)
  }
  startAnimation = () => {
    removeBtn.value = true

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
}

onMounted(() => {
  loadDOMfun()
})
</script>

<template>
  <div class="container">
    <button class="activ-btn" v-show="!removeBtn" @click="startAnimation()">Some text</button>
    <div ref="content" class="content">
      <div v-show="showBox" ref="main" class="box main">
        <div class="top">
          <h3>Info</h3>
          <button @click="closeAllBox()">X</button>
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
            <button @click="closeAllBox()">Cancel</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.container {
  display: flex;
  flex-direction: column;
  min-height: 660px;
  padding: 35px 0 0;
  font-family: 'Handjet', sans-serif;
  .activ-btn {
    margin: 0 auto;
  }
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

  @media (max-width: 1100px) {
    .content {
      .box {
        width: 600px;
        .top {
          height: 44px;
          button {
            padding: 0;
          }
        }
        p {
          font-size: 1.2rem;
        }
        h3 {
          font-size: 1.8rem;
        }
        .mid {
          padding: 14px 36px;
          .bottom {
            button {
              font-size: 1rem;
            }
          }
        }
      }
    }
    h1 {
      font-size: 1.9rem;
    }
  }
  @media (max-width: 644px) {
    .content {
      .box {
        width: 300px;
        .mid {
          .bottom {
            flex-direction: column;
            align-items: start;
            button {
              margin: 4px;
              padding: 8px;
              font-size: 0.9rem;
            }
          }
        }
      }
    }
  }
}
</style>
