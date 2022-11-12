<template>
  <button type="button" :class="classes" @click="onClick" :style="style">{{ label }}</button>
</template>

<script>
import { reactive, computed } from 'vue';

export default {
  name: 'my-button',

  props: {
    label: {
      type: String,
      required: true,
    },
    size: {
      type: String,
      validator: function (value) {
        return ['sm', 'md', 'lg'].indexOf(value) !== -1;
      },
    },
    backgroundColor: {
        type: String,
    },
    textColor: {
        type: String,
    },
  },

  emits: ['click'],

  setup(props, { emit }) {
    props = reactive(props);
    return {
      classes: computed(() => ({
        'btn': true,
        [`btn-${props.size || 'md'}`]: true,
      })),
      style: computed(() => ({
        backgroundColor: props.backgroundColor,
        color: props.textColor,
      })),
      onClick() {
        emit('click');
      }
    }
  },
};
</script>
