<template>
  <input
    class="numeric-input-container"
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
  name: 'Numeric-input',
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
input {
  box-sizing: border-box;
}

.numeric-input-container {
  padding: 8px 12px;
  width: 300px;
  height: 40px;
  font-size: 18px;
  border: 1px solid #FB7943;
  border-radius: 8px;
  outline: none;
}
</style>
