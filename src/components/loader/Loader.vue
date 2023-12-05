<script setup>
import { onMounted } from "vue";
onMounted(() => {
    const s = 2;
})
</script>

<template>
    <main>
        <div class="terminal">
            <p class="delay1">Booting up</p>
            <p class="delay2">DONE</p>
            <p class="delay3">Preparing content</p>
            <p class="delay4">DONE</p>
            <p class="delay5">Creating awesomeness</p>
            <p class="delay6">DONE</p>
            <p class="delay7">Ordering pizza</p>
            <p class="delay8">PROCESSING...</p>
        </div>

        <h1>WELCOME</h1>
    </main>
</template>

<style scoped lang="scss">
main {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}

.terminal {
    animation-name: fadeOut;
    animation-duration: 1ms;
    animation-fill-mode: forwards;
    animation-delay: 10000ms;
}

p {
    display: block;
    width: 0px;
    margin: 0;
    font-size: 1.2rem;
    color: #20C20E;
    overflow: hidden;
    font-family: monospace;
    white-space: nowrap;
    animation-name: writeText;
    animation-duration: 1000ms;
    animation-fill-mode: forwards;
}

h1 {
    text-align: center;
    opacity: 0;
    color: white;
    font-family: sans-serif;
    animation-name: fadeIn;
    animation-duration: 1000ms;
    animation-fill-mode: forwards;
    animation-delay: 10500ms;
}

.delay1 {
    animation-delay: 2000ms;
}

.delay2 {
    animation-delay: 3000ms;
}

.delay3 {
    animation-delay: 4000ms;
}

.delay4 {
    animation-delay: 5000ms;
}

.delay5 {
    animation-delay: 6000ms;
}

.delay6 {
    animation-delay: 7000ms;
}

.delay7 {
    animation-delay: 8000ms;
}

.delay8 {
    animation-delay: 9000ms;
}

/* Standard syntax */
@keyframes writeText {
    from {
        width: 0;
    }

    to {
        width: 200px;
    }
}

@keyframes fadeOut {
    from {
        opacity: 1;
    }

    to {
        opacity: 0;
    }
}

@keyframes fadeIn {
    from {
        opacity: 0;
    }

    to {
        opacity: 1;
    }
}
</style>