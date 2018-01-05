<template>
  <div class="edit-card-control">
    <button class="edit-card">
      <span class="edit-card__circle">Edit</span>
    </button>
    <ul class="edit-card-menu">
      <li class="edit-card-menu__item">Rename</li>
      <li class="edit-card-menu__item">Delete</li>
    </ul>
  </div>
</template>

<script>
  import EditCard from './EditCard.vue';

  export default {
    props: ['card'],
  }
</script>

<style lang="scss">
  .edit-card-control {
    position: relative;
  }


  .edit-card {
    cursor: pointer;
    text-indent: -9999px;
    padding: 12px 3px;

    &__circle {
      display: block;
      position: relative;
      width: 7px;
      height: 7px;
      border-radius: 50%;
      background-color: #a0a0a4;

      &:before, &:after {
        content: '';
        width: inherit;
        height: inherit;
        background-color: inherit;
        border-radius: inherit;
        position: absolute;
        left: 0;
      }

      &:before {
        top: -10px;
      }

      &:after {
        bottom: -10px;
      }

    }

  }


  .edit-card-menu {
    min-width: 160px;
    border-radius: 4px;
    position: absolute;
    left: -25px;
    top: 0;
    background-color: #fff;
    box-shadow: 2px 2px 5px 2px rgba(0, 0, 0, .2);

    &__item {
      cursor: pointer;
      padding: 3px 10px;
      &:hover {
        background-color: #eCeCeC
      }
    }

  }
</style>
