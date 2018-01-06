<template>
  <div class="edit-card-control">
    <button class="edit-card" v-click-outside="outsideClick" @click="showMenu">
      <span class="edit-card__circle">Edit</span>
    </button>
    <ul class="edit-card-menu" v-if="menuIsVisible">
      <li class="edit-card-menu__item" @click="renameCard">Rename</li>
      <li class="edit-card-menu__item" @click="deleteCard(card.cid)">Delete</li>
    </ul>
  </div>
</template>

<script>
  import EditCard from './EditCard.vue';
  import { eventBus } from '../main';

  export default {
    props: ['card'],
    data() {
      return {
        menuIsVisible: false
      }
    },
    methods: {
      showMenu() {
        this.menuIsVisible = true;
      },
      outsideClick() {
        this.menuIsVisible = false;
      },
      renameCard() {
        console.log('rename!!!');
      },
      deleteCard(id) {
        console.log('delete!!!', id);
        eventBus.$emit('cardWasRemoved', this.card);
      }
    },
    directives: {
      'click-outside': {
        bind: function(el, binding, vNode) {
          // Provided expression must evaluate to a function.
          if (typeof binding.value !== 'function') {
            const compName = vNode.context.name;
            let warn = `[Vue-click-outside:] provided expression '${binding.expression}' is not a function, but has to be`
            if (compName) { warn += `Found in component '${compName}'` }

            console.warn(warn)
          }
          // Define Handler and cache it on the element
          const bubble = binding.modifiers.bubble;
          const handler = (e) => {
            if (bubble || (!el.contains(e.target) && el !== e.target)) {
              binding.value(e)
            }
          };
          el.__vueClickOutside__ = handler

          // add Event Listeners
          document.addEventListener('click', handler)
        },

        unbind: function(el, binding) {
          // Remove Event Listeners
          document.removeEventListener('click', el.__vueClickOutside__);
          el.__vueClickOutside__ = null

        }
      }
    }
  }
</script>

<style lang="scss">
  .edit-card-control {
    position: relative;
  }


  .edit-card {
    cursor: pointer;
    text-indent: -9999px;
    padding: 12px 3px;

    &__circle {
      display: block;
      position: relative;
      width: 7px;
      height: 7px;
      border-radius: 50%;
      background-color: #a0a0a4;

      &:before, &:after {
        content: '';
        width: inherit;
        height: inherit;
        background-color: inherit;
        border-radius: inherit;
        position: absolute;
        left: 0;
      }

      &:before {
        top: -10px;
      }

      &:after {
        bottom: -10px;
      }

    }

  }


  .edit-card-menu {
    min-width: 160px;
    border-radius: 4px;
    position: absolute;
    left: -25px;
    top: 0;
    background-color: #fff;
    box-shadow: 2px 2px 5px 2px rgba(0, 0, 0, .2);

    &__item {
      cursor: pointer;
      padding: 3px 10px;
      &:hover {
        background-color: #eCeCeC
      }
    }

  }
</style>
