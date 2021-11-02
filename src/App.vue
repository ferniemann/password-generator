<template>
  <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.15.4/css/all.css" integrity="sha384-DyZ88mC6Up2uqS4h/KRgHuoeGwBcD4Ng9SiP4dIRy0EXTlnuz47vAwmeGwVChigm" crossorigin="anonymous">
  <h1 class="title">Password Generator</h1>
  <PasswordGenerator />
</template>

<script>
import PasswordGenerator from './components/PasswordGenerator.vue'

export default {
  name: 'App',
  components: {
    PasswordGenerator
  }
}
</script>

<style>
  @import url(https://fonts.googleapis.com/css?family=Arvo:regular,italic,700,700italic);

  *, *::before, *::after {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
  }

  :root {
    --color-dark: #0F0A0A;
    --color-light: #F5EFED;
    --color-secondary: #2292A4;
    --color-success: #CBE896;
  }

  html {
    font-family: "Arvo";
    font-size: 20px;
  }

  body {
    text-align: center;
    background: var(--color-dark);
    color: var(--color-light);
    padding: .5rem;
  }

  .title {
    font-size: calc(1rem + .5vw);
    text-transform: uppercase;
    letter-spacing: .25rem;
    color: var(--color-secondary);
  }

  h1 {
    padding: 1rem 0;
  }

  button {
    cursor: pointer;
  }

  input[type="range"] {
    -webkit-appearance: none;
    appearance: none;
    background-color: var(--color-light);
    height: .5rem;
    border-radius: .5rem;
  }

  input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 1rem;
    height: 1rem;
    background: var(--color-secondary);
    border-radius: 50%;
  }
</style>
