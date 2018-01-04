<template>
  <div class="cards-list">
    <app-card v-for="card in cards"
              :key="card.cid"
              :card="card"></app-card>
  </div>
</template>

<script>
  import Card from './Card.vue';

  export default {
    props: ['cards'],
    components: {
      appCard: Card
    }
  }
</script>

<style lang="scss">
  .cards-list {
    display: grid;
    grid-template-columns: repeat(5, 20%);
    grid-gap: 10px;
  }
</style>
