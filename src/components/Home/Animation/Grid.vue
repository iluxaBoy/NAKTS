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

    for (let i = 0; i < 3; i++) {
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
    ctx.fillStyle = "#0E0505"
    ctx.fillRect(x + 1, y + 1, recWidth - 2, recHeight - 2);

    ctx.shadowBlur = 35;
    ctx.strokeRect(x, y, recWidth, recHeight);
})
</script>

<template>
    <canvas ref="canvas" :width="width" :height="height">
    </canvas>
    <div>
        <h1>Some Text</h1>
    </div>
</template>

<style scoped lang="scss">
canvas {
    position: absolute;
    top: 0;
    left: 0;
    border: solid 3px #F68D18;
    box-shadow: inset 0 0 15px #f68e189d,
        0 0 15px #f68e189d;
    z-index: -1;
}
</style>