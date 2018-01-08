<template>
  <form class="add-new-card" @submit.prevent="submit">
    <div class="add-new-card__row">
      <label for="card-name" class="add-new-card__label">Enter card name:</label>
      <input type="text"
             id="card-name"
             class="add-new-card__input"
             v-model="cardName"
             required>
    </div>
    <div class="add-new-card__row">
      <label for="card-author" class="add-new-card__label">Enter card author:</label>
      <input type="text"
             id="card-author"
             class="add-new-card__input"
             v-model="cardAuthor"
             required>
    </div>
    <div class="add-new-card__row">
      <input type="submit"
             :disabled="!formIsValid"
             class="add-new-card__submit">
    </div>
  </form>
</template>

<script>
  import { eventBus } from '../main';

  export default {
    props: ['cards'],
    data () {
      return {
        cardName: '',
        cardAuthor: ''
      }
    },
    computed: {
      formIsValid() {
        return this.cardName && this.cardAuthor
      }
    },
    methods: {

      submit() {

        this.cards.push({
          created: new Date().getTime(),
          modified: new Date().getTime(),
          metadata: {
            cid: Math.floor(Math.random() * 0x7FFFFFFF) + "." + Math.floor(Date.now() / 1000),
            name: this.cardName,
            owner: this.cardAuthor
          }
        });

        eventBus.$emit('newCardWasAdded');
      }
    }
  }
</script>

<style lang="scss">
  .add-new-card {
    &__row {
      & + & {
        margin-top: 20px;
      }
    }

    &__label {
      display: block;
      margin-bottom: 5px;
    }

    &__input {
      display: block;
      width: 100%;
      border: 1px solid #b2b2b2;
      border-radius: 3px;
      padding: 4px 7px;
      font-size: 20px;
    }

    &__submit {
      font-size: 20px;
    }
  }
</style>
