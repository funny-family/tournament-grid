<template>
  <input
    class="grid-setter"
    ref="gridSetter"
    :placeholder="placeholder"
    :value="value"
    :type="type"
    @input="updateInputValue($event.target.value)"
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
    updateInputValue(value) {
      this.$emit('input', value);
    }
  }
};
</script>

<style scoped>

</style>
