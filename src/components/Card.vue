<template>
  <div class="card">
    <strong class="card__name">
      {{ card.metadata.name }}
    </strong>
    <div class="card__bar">
      <span class="card__author">
        By {{ card.metadata.owner }}
      </span>

      <app-edit-card></app-edit-card>
    </div>
  </div>
</template>

<script>
  import EditCard from './EditCard.vue';

  export default {
    props: ['card'],
    components: {
      appEditCard: EditCard
    }
  }
</script>

<style lang="scss">
  .card {
    padding: 20px 30px 20px 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex-basis: 200px;
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 2px 0 5px rgba(0, 0, 0, .1);
    min-height: 150px;

    &__name {
      text-transform: uppercase;
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
