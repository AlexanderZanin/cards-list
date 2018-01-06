<template>
  <div class="cards-list">
    <app-card v-for="card in filteredCard"
              :key="card.cid"
              :card="card"></app-card>
  </div>
</template>

<script>
  import Card from './Card.vue';

  export default {
    props: ['cards', 'filterCardsInput'],
    components: {
      appCard: Card
    },
    computed: {
      filteredCard() {
        if (this.filterCardsInput.length < 3) {
          return this.cards;
        }

        return this.cards.filter((item) => {
          return item.metadata.name.toLowerCase().indexOf(this.filterCardsInput) > -1;
        });
      }
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
