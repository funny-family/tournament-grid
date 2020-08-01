<template>
  <div class="home">
    <Numeric-input
      placeholder="256, 128, 64, 32, 16, 8, 4, 2, 1"
      type="text"
      v-model="stringInputValue"
    />
    <Single-elimination-diagram :amountOfParticipants="numericInputValue" />
  </div>
</template>

<script>
import NumericInput from '@/components/inputs/NumericInput.vue';
import SingleEliminationDiagram from '@/components/diagrams/SingleEliminationDiagram.vue';

const defaultNumbers = [256, 128, 64, 32, 16, 8, 4, 2, 1];

export default {
  data: () => ({
    stringInputValue: '8'
  }),
  components: {
    NumericInput,
    SingleEliminationDiagram
  },
  computed: {
    numericInputValue() {
      return Number.parseInt(this.$data.stringInputValue, 10);
    },
    approximateNumber() {
      return defaultNumbers.find((n) => n <= this.numericInputValue);
    }
  }
};
</script>

<style scoped>

</style>
