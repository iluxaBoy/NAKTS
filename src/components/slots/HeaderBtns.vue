<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
  <div>
    <button><RouterLink to="/">Home</RouterLink></button
    ><button><RouterLink to="/about">About</RouterLink></button> <button>Info</button
    ><button>Sub</button>
  </div>
</template>

<style scoped lang="scss">
div {
  display: flex;
  justify-content: space-between;
  button {
    width: 100%;
    height: 100%;
    padding: 18px 24px;
    color: var(--primary-color-about);
    border: 4px solid var(--primary-color-about);
    border-right: none;
  }

  button:last-of-type {
    border: 4px solid var(--primary-color-about);
  }

  button:hover {
    background-color: var(--primary-color-about);
    color: var(--secondary-color-about);
  }
  button {
    background-color: inherit;
    font-family: 'Silkscreen', sans-serif;
    font-weight: bold;
    font-size: 1.2em;
  }
}
</style>
