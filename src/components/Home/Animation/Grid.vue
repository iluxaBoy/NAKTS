<script setup>
import { onMounted, ref } from "vue";

const canvas = ref()
const width = window.innerWidth - 6;
const height = width / 2.5;

const centerX = width / 2;
const centerY = height / 2;

onMounted(() => {
    let ctx = canvas.value.getContext("2d");

    ctx.strokeStyle = "#F68D18";
    ctx.lineWidth = 3;
    ctx.shadowColor = "#F68D18";
    ctx.shadowBlur = 15;

    let x = 0;
    let y = 0;
    let recWidth = width;
    let recHeight = height;

    for (let i = 0; i < 2; i++) {
        ctx.strokeRect(x += 100, y += 40, recWidth -= 200, recHeight -= 80);
    }

    ctx.beginPath();

    const createLines = (placement, position, amount, change) => {
        if (change) {
            for (let i = 0; i <= position; i += position / amount) {
                ctx.moveTo(placement, i);
                ctx.lineTo(centerX, centerY);
            }
        } else {
            for (let i = 0; i <= position; i += position / amount) {
                ctx.moveTo(i, placement);
                ctx.lineTo(centerX, centerY);
            }
        }
    }

    createLines(width, height, 6, true);
    createLines(0, height, 6, true);
    createLines(0, width, 10, false);
    createLines(height, width, 10, false);

    ctx.stroke();

    ctx.shadowBlur = 0;
    ctx.shadowBlur = 35;
    ctx.fillStyle = "#F68D18"
    ctx.fillRect(x += 84, y += 33, recWidth -= 169, recHeight -= 67);
})
</script>

<template>
    <canvas ref="canvas" :width="width" :height="height">
    </canvas>
    <div :height="height" class="title">
        <h1>NAKTS</h1>
        <div class="box">
            <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Recusandae dolores vel at quaerat</p>
        </div>
    </div>
</template>

<style scoped lang="scss">
.title {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 900px;
    height: 300px;
    margin: 220px auto;
    text-align: center;
    font-family: 'Silkscreen', sans-serif;
    font-size: 1.2rem;
    color: #0E0505;
    font-weight: 600;

    .box {
        padding: 14px 42px;
        border: 4px solid #0E0505;
    }

    h1 {
        font-family: IBM;
        font-size: 9.6rem;
        color: #0E0505;
        font-weight: 600;
        letter-spacing: -12px;
        transition: 0.8s;
    }
}

canvas {
    position: absolute;
    top: 0;
    left: 0;
    border: solid 3px #F68D18;
    box-shadow: inset 0 0 18px #f68e189d,
        0 0 18px #f68e189d;
    z-index: -1;
}
</style>