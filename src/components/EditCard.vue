<template>
  <div class="edit-card-control">
    <button class="edit-card" v-click-outside="outsideClick" @click="showMenu">
      <span class="edit-card__circle">Edit</span>
    </button>

    <slot></slot>
  </div>
</template>

<script>
  import EditCardMenu from './EditCardMenu.vue';

  export default {
    data() {
      return {
        menuIsVisible: false
      }
    },
    watch: {
      menuIsVisible() {
        this.$emit('editButtonWasClicked', this.menuIsVisible);
      }
    },
    methods: {
      showMenu() {
        this.menuIsVisible = true;
      },
      outsideClick() {
        this.menuIsVisible = false;
      },
    },
    directives: {
      'click-outside': {
        bind(el, binding, vNode) {
          // Provided expression must evaluate to a function.
          if (typeof binding.value !== 'function') {
            const compName = vNode.context.name;
            let warn = `[Vue-click-outside:] provided expression '${binding.expression}' is not a function, but has to be`;
            if (compName) { warn += `Found in component '${compName}'` }

            console.warn(warn);
          }
          // Define Handler and cache it on the element
          const bubble = binding.modifiers.bubble;
          const handler = (e) => {
            if (bubble || (!el.contains(e.target) && el !== e.target)) {
              binding.value(e)
            }
          };
          el.__vueClickOutside__ = handler;

          // add Event Listeners
          document.addEventListener('click', handler)
        },

        unbind(el, binding) {
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
</style>
