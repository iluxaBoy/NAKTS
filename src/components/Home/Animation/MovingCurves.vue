<script setup>
import { onMounted, ref } from "vue";

const canvas1 = ref();
const width1 = 500;
const height1 = 250;

const canvas2 = ref();
const width2 = 500;
const height2 = 250;

onMounted(() => {
    const drawGraph = () => {
        let ctx = canvas1.value.getContext("2d");
        let ch = 250;
        let h = 200;
        let amplitude = h;
        let frequency = .01;
        let phi = 0;
        let frames = 0;
        let requestId;

        const Draw = () => {
            ctx.lineWidth = 4;
            ctx.strokeStyle = "#0E0505";
            ctx.shadowBlur = "#0E0505";
            frames++
            phi = frames / 30;

            ctx.clearRect(0, 0, width1, ch);
            ctx.beginPath();

            for (let i = 0; i < width1; i++) {
                let y = Math.sin(i * frequency + phi) * amplitude / 2 + amplitude / 2;
                ctx.lineTo(i, y + 40);
                ctx.lineTo(i, y - 200);
            }

            ctx.stroke();
            requestId = window.requestAnimationFrame(Draw);
        }

        requestId = window.requestAnimationFrame(Draw);
    }

    const drawLoader = (y, temp) => {
        let ctx = canvas2.value.getContext("2d");

        let rW = 250;
        let rH = 30;
        let x = 220;
        let tempW = 0;
        let requestId;
        ctx.lineWidth = 2;
        ctx.strokeStyle = "#F68D18";
        ctx.fillStyle = "#F68D18";

        ctx.strokeRect(x, y, rW, rH);

        const Draw = () => {
            requestId = setInterval(() => {
                if (tempW >= rW) {
                    ctx.clearRect(x + 1, y + 1, tempW - 2, rH - 2);
                    tempW = 0;
                }
                ctx.fillRect(x, y, tempW += 1, rH);
            }, temp);
        }

        requestId = window.requestAnimationFrame(Draw);
    }
    // debugger;
    drawGraph();
    drawLoader(25, NaN, 4);
    drawLoader(85, 20, 1);
    drawLoader(125, 90, 1);
});
</script>

<template>
    <div class="container">
        <div>
            <canvas class="draw" ref="canvas1" :width="width1" :height="height1">
            </canvas>
        </div>
        <div>
            <canvas ref="canvas2" :width="width2" :height="height2">
            </canvas>
        </div>
    </div>
</template>

<style scoped lang="scss">
.draw {
    border: 3px solid #F68D18;
    background: #F68D18;
}
</style>