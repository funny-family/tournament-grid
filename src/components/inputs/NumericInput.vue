<template>
  <input
    class="numeric-input"
    ref="numericInput"
    :placeholder="placeholder"
    :value="value"
    :type="type"
    @input="updateInputValue($event.target.value)"
    @keypress="onKeyPress"
  />
</template>

<script>
export default {
  props: {
    placeholder: {
      type: String,
      default: ''
    },
    value: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'text',
      Validate: (type) => ['text'].indexOf(type) !== 1,
      required: true
    }
  },
  methods: {
    onKeyPress(event) {
      const char = String.fromCharCode(event.charCode);
      if (!/[0-9]/.test(char)) { // or /^-?\d*$/
        event.preventDefault();
      }
    },
    updateInputValue(value) {
      this.$emit('input', value);
    }
  }
};
</script>

<style scoped>

</style>
