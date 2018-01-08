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
    grid-template-columns: repeat(5, 1fr);
    grid-gap: 10px;

    @media all and (max-width: 1100px) {
      grid-template-columns: repeat(3, 1fr);
    }

    @media all and (max-width: 768px) {
      grid-template-columns: 1fr 1fr;
    }

    @media all and (max-width: 640px) {
      grid-template-columns: 1fr;
    }
  }
</style>
