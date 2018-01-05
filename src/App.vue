<template>
  <div class="container">
    <app-card-grid :cards="cards"></app-card-grid>
  </div>
</template>

<script>
  import { containers } from '../test.json';
  import CardGrid from './components/CardGrid.vue';

  export default {
    data () {
      return {
        cards: containers
      }
    },
    components: {
      appCardGrid: CardGrid
    }
  }
</script>

<style lang="scss">
  html {
    box-sizing: border-box;
  }

  *, *:before, *:after {
    box-sizing: inherit;
  }

  body {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    background-color: #f1f1f0
  }

  button {
    padding: 0;
    border: none;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .container {
    width: 80%;
    margin: auto;
  }

</style>
