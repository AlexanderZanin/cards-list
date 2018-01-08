<template>
  <button class="button-add" @click="clickButton">+</button>
</template>

<script>
  import { eventBus } from '../main';

  export default {
    methods: {
      clickButton() {
        eventBus.$emit('ButtonAddWasClicked', true);
      }
    }
  }
</script>

<style lang="scss">
  .button-add {
    $buttonBg: #d64423;

    cursor: pointer;
    font-family: 'Avenir', Helvetica;
    border-radius: 50%;
    position: fixed;
    bottom: 5vh;
    left: 50%;
    transform: translateX(-50%);
    background-color: $buttonBg;
    font-size: 50px;
    line-height: 70px;
    width: 70px;
    font-weight: 100;
    height: 70px;
    box-shadow: 0 0 6px 0 rgba(0, 0, 0, .5);
    color: #fff;
    vertical-align: middle;
    &:hover {
      background-color: lighten($buttonBg, 5%);
    }
    &:active {
      background-color: darken($buttonBg, 5%);
    }
  }
</style>
