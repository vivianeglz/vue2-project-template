<template>
  <div class="modal">
    <div class="modal__container" :class="className">
      <div class="modal__header">
        <h3 v-if="title">{{ title }}</h3>
        <button class="modal__btn-close" @click.prevent="$emit('close')">
          <icon-close />
        </button>
      </div>
      <slot />
      <div v-if="thereIsFooter" class="modal__footer">
        <slot name="footer" />
      </div>
    </div>
  </div>
</template>

<script>
import { IconClose } from "@ui/components/globals/icons";

export default {
  name: "Modal",
  components: {
    IconClose
  },
  props: {
    title: {
      type: String,
      default: "Title"
    },
    size: {
      type: String,
      default: "s",
      validator(value) {
        return ["s", "m", "l"].includes(value);
      }
    }
  },
  computed: {
    className() {
      return `modal__container--${this.size}`
    },
    thereIsFooter() {
      return this.$slots.footer ? true : false;
    }
  }
};
</script>
