<script setup>
import { onMounted, ref } from "vue";

const canvas = ref();

const width = 500;
const height = 250;

const drawGraph = () => {
    const ctx = canvas.value.getContext("2d");

    let amplitude = 160;
    let frequency = .01;
    let phi = 0;
    let frames = 0;

    ctx.lineWidth = 2;
    ctx.strokeStyle = "#F68D18";

    const Draw = () => {
        frames++
        phi = frames / 30;

        ctx.clearRect(0, 0, width, height);

        for (let i = 0; i < width - 25; i += 40) {
            let y = Math.sin(i * frequency + phi) * amplitude / 2 + amplitude / 2;
            ctx.strokeRect(i + 25, y + 15, 25, 30);
        }

        window.requestAnimationFrame(Draw);
    }

    window.requestAnimationFrame(Draw);
}

onMounted(() => {
    drawGraph();
});

</script>

<template>
    <div class="container">
        <div class="animation">
            <div class="diagram">
                <div class="left">
                    <ul>
                        <li>1</li>
                        <li>2</li>
                        <li>3</li>
                        <li>4</li>
                    </ul>
                </div>
                <div class="bottom">
                    <ul>
                        <li>1</li>
                        <li>2</li>
                        <li>3</li>
                        <li>4</li>
                        <li>5</li>
                        <li>6</li>
                        <li>7</li>
                        <li>8</li>
                        <li>9</li>
                        <li>10</li>
                    </ul>
                </div>
            </div>
            <canvas ref="canvas" :width="width" :height="height">
            </canvas>
            <div class="diagram-info">
                <ul>
                    <li>
                        &#60;&#62;Lorem ipsum dolor sit amet.
                    </li>
                    <li>&#60;-Lorem ipsum dolor sit amet consectetur.</li>
                    <li>&#60;-Lorem ipsum dolor sit amet consectetur adipisicing.</li>
                </ul>
            </div>
        </div>
        <div class="info">
            <h1>Lorem ipsum dolor sit amet.</h1>
            <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Ullam temporibus adipisci aliquam quia dolore
                tenetur sint illum doloremque error dolor facere consequatur, cumque saepe ipsa ab qui atque at sunt
                repellendus? Eum, quibusdam aspernatur atque dignissimos sequi dolore quia delectus consequatur perferendis
                voluptas nemo dolor, eius labore dolorem eveniet natus.</p>
        </div>
    </div>
</template>

<style scoped lang="scss">
.container {
    position: relative;
    display: flex;
    flex-direction: row-reverse;
    justify-content: space-between;
    margin-top: 134px;
    font-family: 'Handjet', sans-serif;

    margin-bottom: 268px;

    h1 {
        font-family: 'Silkscreen', sans-serif;
        line-height: 40px;
        font-size: 2.4rem;
        font-weight: 700;
    }

    .animation {
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
            border: 3px dotted #F68D18;
            width: 505px;
        }

    }

    .info {
        max-width: 800px;
    }
}

ul {
    list-style: none;
}

canvas {
    position: absolute;
    top: 0;
    right: 0;
    border: 3px solid #F68D18;
}
</style>