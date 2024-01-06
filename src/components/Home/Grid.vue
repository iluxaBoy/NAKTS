<script setup>
import { onMounted, ref } from "vue";
import MarqueeText from 'vue-marquee-text-component';

const canvas = ref();

const drawGrid = () => {
    const ctx = canvas.value.getContext("2d");

    const centerX = canvas.value.width / 2;
    const centerY = canvas.value.height / 2;

    let x = 0;
    let y = 0;
    let recWidth = canvas.value.width;
    let recHeight = canvas.value.height;

    ctx.strokeStyle = "#F68D18";
    ctx.lineWidth = 3;

    for (let i = 0; i < 2; i++) {
        ctx.strokeRect(x += 100, y += 40, recWidth -= 200, recHeight -= 80);
    }

    ctx.beginPath();

    const createLines = (placement, position, amount, change) => {
        if (change) {
            createVerticalLines(placement, position, amount);
        } else {
            createHorizontalLines(placement, position, amount);
        }
    }

    const createVerticalLines = (placement, position, amount) => {
        for (let i = 0; i <= position; i += position / amount) {
            ctx.moveTo(placement, i);
            ctx.lineTo(centerX, centerY);
        }
    }

    const createHorizontalLines = (placement, position, amount) => {
        for (let i = 0; i <= position; i += position / amount) {
            ctx.moveTo(i, placement);
            ctx.lineTo(centerX, centerY);
        }
    }

    createLines(canvas.value.width, canvas.value.height, 6, true);
    createLines(0, canvas.value.height, 6, true);
    createLines(0, canvas.value.width, 10, false);
    createLines(canvas.value.height, canvas.value.width, 10, false);

    ctx.stroke();

    ctx.fillStyle = "#F68D18"
    ctx.fillRect(x += 84, y += 33, recWidth -= 169, recHeight -= 67);
}

function onScreenResize() {
    window.addEventListener("resize", () => {
        updateScreenWidth();
        drawGrid();
    });
}

function updateScreenWidth() {
    canvas.value.width = window.innerWidth - 16;
    canvas.value.height = canvas.value.width / 2.5;
}

onMounted(() => {
    updateScreenWidth();
    onScreenResize();

    drawGrid();
});
</script>

<template>
    <div class="container">
        <canvas ref="canvas">
        </canvas>
        <div class="title">
            <h1>NAKTS</h1>
            <div class="box">
                <button>Some</button><button>Some</button><button>Some</button><button>Some</button>
            </div>
        </div>
        <marquee-text class="moving-text" :repeat="9" :duration="10">
            <h1>bigbrainMorestufflesspipi</h1>
        </marquee-text>
    </div>
</template>

<style scoped lang="scss">
canvas {
    position: absolute;
    top: 0;
    left: 0;
    border: solid 3px var(--primary-color-home);
    z-index: -1;
}

.title {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 900px;
    height: 300px;
    margin: 11.5vw auto;
    text-align: center;
    font-family: 'Silkscreen', sans-serif;
    font-size: 1.2rem;
    color: var(--secondary-color-home);
    font-weight: 600;

    .box {
        display: flex;
        justify-content: space-between;
        padding: 14px 42px;
        border: 4px solid var(--secondary-color-home);
    }

    h1 {
        font-family: IBM;
        font-size: 9.6rem;
        color: var(--secondary-color-home);
        font-weight: 600;
        letter-spacing: -12px;
        transition: 0.8s;
    }
}

.moving-text {
    height: 180px;
    text-align: center;
    font-family: IBM;
    font-weight: 100;
    color: var(--primary-color-home);
    font-size: 2.6rem;

    h1 {
        margin-top: 50px;
    }
}

button {
    background-color: inherit;
    border: none;
    font-family: 'Silkscreen', sans-serif;
    padding: 14px 24px;
    font-weight: bold;
    font-size: 1.2rem;
}
</style>