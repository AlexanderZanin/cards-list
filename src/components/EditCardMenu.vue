<template>
  <ul class="edit-card-menu" v-if="menuIsVisible">
    <li class="edit-card-menu__item" @click="renameCard(card)">Rename</li>
    <li class="edit-card-menu__item" @click="deleteCard(card.cid)">Delete</li>
  </ul>
</template>


<script>
  import EditCard from './EditCard.vue';
  import { eventBus } from '../main';

  export default {
    props: ['card', 'menuIsVisible'],
    methods: {
      renameCard(card) {
        this.$emit('cardRename', card);
      },
      deleteCard(id) {
        eventBus.$emit('cardWasRemoved', id);
      }
    },
    created() {
    }
  }
//  console.log('from bottom ', eventBus);
</script>


<style lang="scss">
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
        background-color: #ececec
      }
    }
  }
</style>
