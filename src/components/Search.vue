<template>
  <div class="search-box">
    <input v-if="showInput"
           class="search-box__input"
           ref="searchInput"
           type="search"
           placeholder="filter by name"
           @input="$emit('searching', filterCardsInput)"
           v-model="filterCardsInput">
    <button class="search-box__button" @click="toggleInput">
      <i v-if="showInput" class="material-icons">close</i>
      <i v-else class="material-icons">search</i>
    </button>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        filterCardsInput: '',
        showInput: false
      }
    },
    methods: {
      toggleInput() {
        this.showInput = !this.showInput;

        if (this.showInput) {
          setTimeout(() => {
              this.$refs.searchInput.focus();
          }, 0);
          return;
        }

        this.filterCardsInput = '';
      }
    }
  }
</script>

<style lang="scss">
  .search-box {
    display: flex;
    align-items: center;

    &__input {
      padding: 3px 5px;
      font-size: 18px;
    }

    &__button {
      border-radius: 3px;
    }
  }
</style>
