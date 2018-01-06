<template>
  <div class="container">
    <div>
      <input type="search" v-model="filterCardsInput">
    </div>
    <!--<app-card-grid :cards="sortedByDateModify"></app-card-grid>-->
    <div class="cards-group" v-for="(groupValue, groupKey) in groupedByDateOfModify">
      <h3 class="cards-group__title">
        {{ groupKey }}
      </h3>
      <app-card-grid :cards="groupValue" :filterCardsInput="filterCardsInput"></app-card-grid>
    </div>
  </div>
</template>

<script>
  import _ from 'lodash';
  import { containers } from '../test.json';
  import { eventBus } from './main';
  import CardGrid from './components/CardGrid.vue';


  export default {
    data () {
      return {
        cards: containers,
        filterCardsInput: ''
      }
    },
    computed: {
      sortedByDateOfModify() {
//        return this.cards.sort((a, b) => {
//            return a.modified - b.modified;
//        });
      },
      groupedByDateOfModify() {
        return _.groupBy(this.cards, (card) => {
          let dateOfModify = new Date(card.modified);
          dateOfModify = new Date(dateOfModify).toUTCString();
          dateOfModify = dateOfModify.split(' ').slice(0, 4).join(' ');

          // returns time string without time and timezone
          console.log('dateOfModify', dateOfModify);
          return dateOfModify
        });
      }
    },
    components: {
      appCardGrid: CardGrid
    },
    created() {
      eventBus.$on('cardWasRemoved', (removedObj) => {
        this.cards = this.cards.filter((card) => {
          return card.cid !== removedObj.cid;
        });
      })
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


  .cards-group {
    &__title {
      text-align: center;
    }
  }

</style>
