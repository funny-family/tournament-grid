<template>
  <div class="single-elimination-diagram-container">
    <template v-for="(column, columnIndex) in columns">
      <div class="column" :key="columnIndex">
        <template v-for="(participant, participantIndex) in column">
          <div class="participant" :key="participantIndex">
            <div class="participant__content"></div>
          </div>
        </template>
      </div>
    </template>
  </div>
</template>

<script>
const defaultParticipants = [256, 128, 64, 32, 16, 8, 4, 2, 1];

export default {
  name: 'Single-elimination-diagram',
  props: {
    diagramSize: {
      type: Number,
      default: 8
    }
  },
  computed: {
    columns() {
      return defaultParticipants.filter((columns) => columns <= this.$props.diagramSize);
    }
  }
};
</script>

<style scoped>
.single-elimination-diagram-container {
  display: flex;
}

.column {
  display: flex;
  flex-grow: 1;
  flex-direction: column;
}

.participant {
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin: 0 10px;
  padding: 6px 0;
  flex-grow: 1;
  position: relative;
}

.participant__content {
  border: 2px solid green;
  background-color: aquamarine;
  width: 100%;
  min-width: 60px;
  height: 40px;
  position: relative;
}
</style>
