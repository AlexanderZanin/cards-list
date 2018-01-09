<template>
  <div class="search-box">
    <transition name="expand">
      <input v-if="showInput"
             class="search-box__input"
             ref="searchInput"
             type="search"
             placeholder="filter by name"
             @input="$emit('searching', filterCardsInput)"
             v-model="filterCardsInput">
    </transition>
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
    updated() {
      if (this.showInput) {
        this.$refs.searchInput.focus();
        return;
      }

      this.filterCardsInput = '';
      this.$emit('searching', this.filterCardsInput)
    },
    methods: {
      toggleInput() {
        this.showInput = !this.showInput;
      }
    }
  }
</script>

<style lang="scss">
  .search-box {
    display: flex;
    align-items: center;

    &__input {
      padding: 3px 7px;
      font-size: 18px;
      background-color: #fff;
      border: 1px solid #b2b2b2;
      border-radius: 5px;
    }

    &__button {
      border-radius: 3px;
      height: 24px;
      width: 24px;
      cursor: pointer;
    }
  }


  .expand-enter-active, .expand-leave-active {
    transition: all .25s;
  }
  .expand-enter, .expand-leave-to {
    opacity: 0;
    transform: translateX(40px);
  }
</style>
