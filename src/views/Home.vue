<template>
  <div>
    <div class="home">
      <Numeric-input
        class="numeric-input"
        placeholder="256, 128, 64, 32, 16, 8, 4, 2, 1"
        type="text"
        v-model="stringInputValue"
      />
    </div>
    <Single-elimination-diagram
      class="single-elimination-diagram"
      :amountOfParticipants="approximateNumber"
    />
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
.home {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.single-elimination-diagram {
  margin: 0 12px;
}

.numeric-input {
  margin: 20px 12px;
}
</style>
