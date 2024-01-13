<script setup>
import { onMounted, ref } from "vue";
import MarqueeText from 'vue-marquee-text-component';

const canvas = ref();

//fun to draw grid
const drawGrid = () => {
    const ctx = canvas.value.getContext("2d");

    //center of canvas so lines know where to go
    const centerX = canvas.value.width / 2;
    const centerY = canvas.value.height / 2;

    //coordinates of rectangle
    let x = 0;
    let y = 0;
    //width and height of rectangle
    let recWidth = canvas.value.width;
    let recHeight = canvas.value.height;

    let amount = 2;

    //canvas styling
    ctx.strokeStyle = "#F68D18";
    ctx.lineWidth = 3;

    //if screen size is small then draw less amount of rect
    if (canvas.value.width <= 1250) {
        amount = 1;
    }

    //draw rectengls
    for (let i = 0; i < amount; i++) {
        ctx.strokeRect(x += 100, y += 40, recWidth -= 200, recHeight -= 80);
    }

    ctx.beginPath();

    //fun to create lines
    const createLines = (placement, position, amount, change) => {
        if (change) {
            createVerticalLines(placement, position, amount);
        } else {
            createHorizontalLines(placement, position, amount);
        }
    }

    //fun to create vertical lines
    const createVerticalLines = (placement, position, amount) => {
        for (let i = 0; i <= position; i += position / amount) {
            ctx.moveTo(placement, i);
            ctx.lineTo(centerX, centerY);
        }
    }

    //fun to create horizontal lines
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

    ctx.fillStyle = "#F68D18";
    ctx.fillRect(x += 84, y += 33, recWidth -= 169, recHeight -= 67);
}

//fun to track if screen changed width and redraw grid
const onScreenResize = () => {
    window.addEventListener("resize", () => {
        updateScreenWidth();
        drawGrid();
    });
}

//fun to change canvas width and height
const updateScreenWidth = () => {
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
                <button>Home</button><button>About</button><button>Info</button><button>Sub</button>
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
    max-width: 900px;
    height: 300px;
    margin: 11.5vw auto 9.5vw;
    text-align: center;
    font-family: 'Silkscreen', sans-serif;
    font-size: 1.2rem;
    color: var(--secondary-color-home);
    font-weight: 600;

    .box {
        display: flex;
        justify-content: space-between;

        button {
            width: 100%;
            height: 100%;
            padding: 18px 24px;
            color: var(--secondary-color-home);
            border: 4px solid var(--secondary-color-home);
            border-right: none;
        }

        button:last-of-type {
            border: 4px solid var(--secondary-color-home);
        }

        button:hover {
            background-color: var(--secondary-color-home);
            color: var(--primary-color-home);
        }
    }

    h1 {
        font-family: IBM;
        font-size: 9.6rem;
        color: var(--secondary-color-home);
        font-weight: 600;
        letter-spacing: -12px;
    }
}

@media (max-width: 1540px) {
    .title {
        max-width: 600px;
        height: 200px;
        margin: 12.5vw auto 10.5vw;

        .box {
            button {
                font-size: 1.1rem;
                padding: 12px 8px;
            }
        }

        h1 {
            font-size: 7.6rem;
        }
    }

}

@media (max-width: 1200px) {
    .title {
        margin: 11.5vw auto 8.5vw;
    }
}

@media (max-width: 1000px) {
    canvas {
        display: none;
    }

    .title {
        margin-bottom: 3.5vw;

        .box {

            button {
                color: var(--primary-color-home);
                border-color: var(--primary-color-home);
            }

            button:last-of-type {
                border-color: var(--primary-color-home);
            }

            button:hover {
                background-color: var(--primary-color-home);
                color: var(--secondary-color-home);
            }
        }

        h1 {
            color: var(--primary-color-home);
        }
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

@media (max-width: 1000px) {
    .moving-text {
        h1 {
            font-size: 3.8rem;
        }
    }
}

button {
    background-color: inherit;
    border: none;
    font-family: 'Silkscreen', sans-serif;
    font-weight: bold;
    font-size: 1.2em;
}
</style>