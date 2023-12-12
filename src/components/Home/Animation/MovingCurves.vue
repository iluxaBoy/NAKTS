<script setup>
import { onMounted, ref } from "vue";

const canvas1 = ref();
const width = 500;
const height = 250;

const canvas2 = ref();

onMounted(() => {
    const drawGraph = () => {
        let ctx = canvas1.value.getContext("2d");
        let ch = 250;
        let h = 200;
        let amplitude = h;
        let frequency = .01;
        let phi = 0;
        let frames = 0;

        const Draw = () => {
            ctx.lineWidth = 4;
            ctx.strokeStyle = "#0E0505";
            ctx.shadowBlur = "#0E0505";
            frames++
            phi = frames / 30;

            ctx.clearRect(0, 0, width, ch);
            ctx.beginPath();

            for (let i = 0; i < width; i++) {
                let y = Math.sin(i * frequency + phi) * amplitude / 2 + amplitude / 2;
                ctx.lineTo(i, y + 40);
                ctx.lineTo(i, y - height);
            }

            ctx.stroke();
            window.requestAnimationFrame(Draw);
        }

        window.requestAnimationFrame(Draw);
    }

    const drawLoader = (y, temp) => {
        let ctx = canvas2.value.getContext("2d");

        let rW = 250;
        let rH = 30;
        let x = 210;
        let tempW = 0;

        ctx.lineWidth = 2;
        ctx.strokeStyle = "#F68D18";
        ctx.fillStyle = "#F68D18";

        ctx.strokeRect(x, y, rW, rH);

        const Draw = () => {
            setInterval(() => {
                if (tempW >= rW) {
                    ctx.clearRect(x + 1, y + 1, tempW - 2, rH - 2);
                    tempW = 0;
                }
                ctx.fillRect(x, y, tempW += 1, rH);
            }, temp);
        }

        window.requestAnimationFrame(Draw);
    }

    drawGraph();
    drawLoader(25, 0, 4);
    drawLoader(75, 20, 1);
    drawLoader(125, 90, 1);
});
</script>

<template>
    <div class="container">
        <div class="top">
            <canvas class="draw" ref="canvas1" :width="width" :height="height">
            </canvas>
        </div>
        <div class="bottom">
            <div class="text">
                <div class="files">
                    <div>
                        <span>[1] Some File</span>
                    </div>
                    <div>
                        <span ref="pros">0%</span>
                    </div>
                </div>
                <div class="files">
                    <div>
                        <span>[1] Some File</span>
                    </div>
                    <div>
                        <span ref="pros">0%</span>
                    </div>
                </div>
                <div class="files">
                    <div>
                        <span>[1] Some File</span>
                    </div>
                    <div>
                        <span ref="pros">0%</span>
                    </div>
                </div>
            </div>
            <canvas class="loader" ref="canvas2" :width="width" :height="height">
            </canvas>
        </div>
    </div>
</template>

<style scoped lang="scss">
.bottom {
    position: relative;
    width: 500px;

    .text {
        display: flex;
        flex-direction: column;
        justify-content: space-around;

        .files {
            display: flex;
            justify-content: space-between;
            margin: 18px 0;
        }
    }
}

.text {
    color: #F68D18;
}

.draw {
    border: 3px solid #F68D18;
    background: #F68D18;
}

.loader {
    position: absolute;
    top: 0;
}
</style>