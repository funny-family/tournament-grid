<template>
  <div class="home">
    <Numeric-input
      placeholder="Enter an even number"
      type="text"
      v-model="stringInputValue"
    />
    <div v-if="!isNaN(numericInputValue)">{{ numericInputValue }}</div>
    <Single-elimination-diagram :diagramSize="numericInputValue" />
  </div>
</template>

<script>
import NumericInput from '@/components/inputs/NumericInput.vue';
import SingleEliminationDiagram from '@/components/diagrams/SingleEliminationDiagram.vue';

export default {
  data: () => ({
    stringInputValue: ''
  }),
  components: {
    NumericInput,
    SingleEliminationDiagram
  },
  computed: {
    numericInputValue() {
      return Number.parseInt(this.$data.stringInputValue, 10);
    }
  }
};
</script>

<style scoped>

</style>
