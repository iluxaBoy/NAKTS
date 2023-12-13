<script setup>
import { onMounted, ref } from "vue";

const canvas1 = ref();
const canvas2 = ref();

const width = 500;
const height = 250;

let pros1 = ref(0);
let pros2 = ref(0);
let pros3 = ref(0);


const drawGraph = () => {
    const ctx = canvas1.value.getContext("2d");

    let amplitude = 200;
    let frequency = .01;
    let phi = 0;
    let frames = 0;

    ctx.lineWidth = 2;
    ctx.strokeStyle = "#0E0505";

    const Draw = () => {
        frames++
        phi = frames / 30;

        ctx.clearRect(0, 0, width, height);
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

const drawLoader = (y, frame, pros) => {
    const ctx = canvas2.value.getContext("2d");

    let recWidth = 250;
    let recHeight = 30;
    let x = 140;
    let tempW = 0;
    let tempPros = 0;

    ctx.lineWidth = 2;
    ctx.strokeStyle = "#F68D18";
    ctx.fillStyle = "#F68D18";

    ctx.strokeRect(x, y, recWidth, recHeight);

    const Draw = () => {
        setInterval(() => {
            if (tempW >= recWidth) {
                ctx.clearRect(x + 1, y + 1, tempW - 2, recHeight - 2);

                tempW = 0;
                pros.value = 0;
            }
            pros.value += 1;

            ctx.fillRect(x, y, tempW += 1, recHeight);
        }, frame);
    }

    window.requestAnimationFrame(Draw);
}

onMounted(() => {

    drawGraph();
    drawLoader(15, 0, pros1);
    drawLoader(65, 20, pros2);
    drawLoader(115, 90, pros3);

});
</script>

<template>
    <div class="container">
        <div class="animation">
            <div class="top">
                <canvas class="draw" ref="canvas1" :width="width" :height="height">
                </canvas>
            </div>
            <div class="bottom">
                <canvas class="loader" ref="canvas2" :width="width" :height="height">
                </canvas>
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
        </div>
        <div class="info">
            <h1>Worem ipsum doWor sit amet</h1>
            <h1>Worem ipsum doWor sit amet</h1>
            <h1>Worem ipsum doWor sit amet</h1>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Dicta hic, blanditiis fugiat ad rem consequatur
                omnis aliquid. A iste possimus accusamus explicabo sapiente id laboriosam quasi magnam quidem officia
                consectetur corporis, voluptatibus mollitia voluptas tempore laborum eum doloremque, dolor praesentium esse
                vel. Nihil architecto possimus praesentium quia enim dolorum inventore.
            </p>
        </div>
    </div>
</template>

<style scoped lang="scss">
.container {
    display: flex;
    justify-content: space-between;
    font-family: 'Handjet', sans-serif;

    h1 {
        font-family: 'Silkscreen', sans-serif;
        line-height: 40px;
        font-size: 2.4rem;
        font-weight: 700;
    }

    .animation {
        max-width: 510px;
    }

    .info {
        display: flex;
        flex-direction: column;
        max-width: 800px;

        p {
            margin-top: 14px;
        }
    }
}

.draw {
    border: 3px solid #F68D18;
    background: #F68D18;
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
        padding-top: 15px;
        font-size: 24px;

        .files {
            display: flex;
            justify-content: space-between;
            text-align: end;
        }
    }
}
</style>