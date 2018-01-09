<template>
  <div class="card">
    <div v-if="showEditName" class="card__rename">
      <input type="text"
             class="card__rename-input"
             ref="nameInput"
             v-model="card.metadata.name"
             @blur="finishEditing" @keydown.enter="finishEditing">
      <p class="card__rename-note">
        Press enter for finish redacting or blur input
      </p>
    </div>
    <strong v-else class="card__name">
      {{ card.metadata.name }}
    </strong>

    <div class="card__bar">
      <span class="card__author">
        By {{ card.metadata.owner }}
      </span>

      <app-edit-card :card="card" @editButtonWasClicked="menuIsVisible = $event">
        <app-edit-card-menu :card="card"
                            :menuIsVisible="menuIsVisible" @cardRename="cardRename"></app-edit-card-menu>
      </app-edit-card>
    </div>
  </div>
</template>

<script>
  import EditCard from './EditCard.vue';
  import EditCardMenu from './EditCardMenu.vue';

  export default {
    props: ['card'],
    data() {
      return {
        menuIsVisible: false,
        showEditName: false
      }
    },
    components: {
      appEditCard: EditCard,
      appEditCardMenu: EditCardMenu
    },
    methods: {
      cardRename() {
        this.showEditName = true;

        setTimeout(() => {
          let input = this.$refs.nameInput;

          input.focus();
          input.select();
        }, 0);
      },

      finishEditing() {
        this.showEditName = false;
      }
    }
  }
</script>

<style lang="scss">
  .card {
    min-width: 0;
    padding: 20px 30px 20px 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex-basis: 200px;
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 2px 0 5px rgba(0, 0, 0, .1);
    min-height: 150px;

    &__rename-input {
      font-size: 18px;
      width: 100%;
    }

    &__rename-note {
      color: #959595;
      font-size: 12px;
      margin-top: 10px;
      margin-bottom: 0;
    }

    &__name {
      text-overflow: ellipsis;
      overflow: hidden;

    }

    &__bar {
      display: flex;
      align-items: center;
      justify-content: space-between;

    }

    &__author {
      flex-basis: 70%;
      font-size: 14px;
      text-overflow: ellipsis;
      white-space: nowrap;
      overflow: hidden;
    }

  }
</style>
