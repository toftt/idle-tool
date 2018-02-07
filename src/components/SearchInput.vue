<template>
    <input
        class="input"
        placeholder="Enter name here"
        ref="input"
        :value="value"
        @input="updateValue($event.target.value)"
    >
</template>

<script>
import trimStart from 'lodash/trimStart';

export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      default: '',
    },
  },
  methods: {
    updateValue(value) {
      const formattedValue = trimStart(value);

      if (formattedValue !== value) {
        this.$refs.input.value = formattedValue;
      }

      this.$emit('input', formattedValue);
    },
  },
};
</script>
