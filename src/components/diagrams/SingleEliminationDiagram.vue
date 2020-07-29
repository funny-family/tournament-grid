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
*,
*::after,
*::before {
  box-sizing: border-box;
}

.single-elimination-diagram-container {
  display: flex;
}

.column {
  display: flex;
  flex-grow: 1;
  flex-direction: column;
}

.column:first-child .participant::before {
  display: none;
}

.column:first-child .participant__content::before {
  display: none;
}

.column:last-child .participant::after {
  display: none;
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

.participant::before {
  content: '';
  min-height: 30px;
  border-left: 2px solid red;
  position: absolute;
  left: -10px;
  top: 50%;
  margin-top: -15px;
  margin-left: -2px;
}

.participant:nth-child(odd)::after {
  content: '';
  border: 2px solid transparent;
  border-top-color: red;
  border-right-color: red;
  height: 50%;
  position: absolute;
  right: -10px;
  width: 12px;
  top: 50%;
  z-index: -1;
}

.participant:nth-child(even)::after {
  content: '';
  border: 2px solid transparent;
  border-bottom-color: red;
  border-right-color: red;
  border-radius: 0%;
  height: 50%;
  position: absolute;
  right: -10px;
  width: 12px;
  bottom: 50%;
  z-index: -1;
}

.participant__content::before {
  content: '';
  width: 10px;
  border-bottom: 2px solid red;
  margin-left: -2px;
  position: absolute;
  top: 50%;
  left: -10px;
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
