<template>
  <div id="app">
    <app-header>
      <app-search slot="search"
                  @searching="filterCardsInput = $event"></app-search>
    </app-header>
    <div class="container">

      <!--<p class="app-note">-->
        <!--Cards are sorted by date of modify. If card will be modify it will be set in new cards group (current date).-->
      <!--</p>-->
      <!--<app-card-grid :cards="sortedByDateModify"></app-card-grid>-->

      <div class="cards-group" v-for="group in groupedByDateOfCreate">
        <h3 class="cards-group__title">
          {{ group.date }}
        </h3>
        <app-card-grid :cards="group.cards" :filterCardsInput="filterCardsInput"></app-card-grid>
      </div>

      <app-button-add></app-button-add>

      <app-modal>
        <template slot="header">Add new card.</template>

        <app-add-new-card slot="body" :cards="cards"></app-add-new-card>
      </app-modal>

    </div>
  </div>
</template>

<script>
  import _ from 'lodash';
  import { containers } from '../test.json';
  import { eventBus } from './main';
  import Header from './components/Header.vue';
  import Search from './components/Search.vue';
  import CardGrid from './components/CardGrid.vue';
  import ButtonAdd from './components/ButtonAdd.vue';
  import Modal from './components/Modal.vue';
  import AddNewCard from './components/AddNewCard.vue';



  export default {
    data () {
      return {
        cards: containers,
        filterCardsInput: '',
        showModal: false
      }
    },
    components: {
      appHeader: Header,
      appSearch: Search,
      appCardGrid: CardGrid,
      appButtonAdd: ButtonAdd,
      appModal: Modal,
      appAddNewCard: AddNewCard
    },
    computed: {
      groupedByDateOfCreate() {
        const groups = _.groupBy(this.cards, (card) => {
          let date = new Date(card.created);
          date = new Date(date).toUTCString();
          date = date.split(' ').slice(0, 4).join(' ');

          // returns time string without time and timezone
          return date
        });

        const sortable = [];

        for (let key in groups) {
          sortable.push({
            date: key,
            time: new Date(key).getTime(),
            cards: groups[key]
          });
        }

        return sortable.sort((a, b) => {
          return b.time - a.time;
        });
      }
    },
    created() {
      eventBus.$on('cardWasRemoved', (removedObjId) => {
        this.cards = this.cards.filter((card) => {
          return card.cid !== removedObjId;
        });
      });
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
    font-family: 'Avenir', Arial, Helvetica, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    background-color: #f1f1f0;
    margin: 0;
  }

  button {
    padding: 0;
    border: none;
    background: none;
    -webkit-appearance: none;
    &:focus {
      outline: none;
      box-shadow: 0 0 7px #229fff;
    }
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

  .app-note {
    font-size: 20px;
    text-align: center;
  }


  .cards-group {
    & + & {
      margin-top: 40px;
    }
    &__title {
      margin-top: 0;
      margin-bottom: 20px;
      text-align: center;
    }
  }

</style>
