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
.tournament-grid {
  background-color: #ebebeb;
}

/*           test           */
.table {
  position: relative;
  width: 200px;
  padding-right: 9px;
  height: 100%;
}

.box {
  width: 100%;
  height: 40px;
  background-color: aquamarine;
  margin: 10px 0;
}

.box:not(:last-child) { /* set botton marign for all box classes but not for last! */
  /* margin-bottom: 100px; */
}

.aft::after { /* link line between first and second player */
  display: block;
  width: 7px;
  background-size: contain;
  content: '';
  position: absolute;
  right: 0;
  top: 20px;
  bottom: 20px;
  border: 2px solid #005050;
  border-left: none;
}
/*           test           */
</style>
