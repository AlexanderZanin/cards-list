<template>
  <transition name="modal" v-if="showModal">
    <div class="modal">
      <div class="modal__container">
        <button class="modal__close" @click="close">✕</button>

        <h3 class="modal__header">
          <slot name="header"></slot>
        </h3>

        <div class="modal__body">
          <slot name="body">
            default body
          </slot>
        </div>
      </div>
      <div class="modal__overlay" @click="close" @keypress.esc="close"></div>
    </div>
  </transition>
</template>

<script>
  import { eventBus } from '../main';

  export default {
    data () {
      return {
        showModal: false
      }
    },
    created() {
      eventBus.$on('ButtonAddWasClicked', (isClicked) => {
        this.showModal = isClicked;
      });

      eventBus.$on('newCardWasAdded', () => {
        this.showModal = false;
      });

    },
    watch: {
      showModal() {

        if (this.showModal) {
          window.addEventListener('keydown', this.closeOnEsc);
          return;
        }

        window.removeEventListener('keydown', this.closeOnEsc);

      }
    },
    methods: {
      close() {
        this.showModal = false;
      },
      closeOnEsc(e) {
        const KEY_ESC = 27;

        if (e.keyCode === KEY_ESC) {
          this.close();
        }
      }
    }
  }
</script>

<style lang="scss">
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 9998;
    display: flex;
    align-items: center;
    justify-content: center;

    &__overlay {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, .5);
      transition: opacity .3s ease;
    }

    &__close {
      position: absolute;
      top: 18px;
      right: 18px;
      width: 22px;
      height: 22px;
      line-height: 22px;
      color: #f00;
      font-size: 20px;
      cursor: pointer;
      border-radius: 3px;
      &:hover {
        color: lighten(#f00, 20%);
      }
      &:active {
        transform: scale(.9);
        color: #f00;
      }
    }

    &__container {
      position: relative;
      z-index: 2;
      max-width: 600px;
      width: 100%;
      padding: 40px 30px;
      background-color: #fff;
      border-radius: 2px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
      transition: all .3s ease;
    }
  }




  .modal-enter {
    opacity: 0;
  }

  .modal-leave-active {
    opacity: 0;
  }

  .modal-enter .modal__container,
  .modal-leave-active .modal__container {
    transform: scale(.8);
  }
</style>
