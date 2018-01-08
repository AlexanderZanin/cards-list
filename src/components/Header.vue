<template>
    <header class="header">
      <a href="#" class="header__admin">
        <i class="material-icons">account_box</i>
      </a>
      <h2 class="header__title">My Folias</h2>

      <div class="header__tools">
        <slot name="search"></slot>
      </div>
    </header>
</template>


<style lang="scss">
  .header {
    position: relative;
    padding: 10px 40px;
    background-color: #fff;
    text-align: center;
    box-shadow: 0 2px 8px rgba(0, 0, 0, .1);
    margin-bottom: 50px;

    &__admin {
      color: #000;
    }

    &__admin, &__tools {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
    }

    &__admin {
      left: 20px;
    }

    &__tools {
      right: 20px;
    }

    &__title {
      margin: 0;
    }
  }
</style>
