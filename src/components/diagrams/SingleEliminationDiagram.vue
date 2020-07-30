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
* {
  --picton-blue: #2CA0EC;
  --mercury: #E7E7E7;
  --connecting-line-active: var(--picton-blue);
  --connecting-line-not-active: var(--mercury);
}

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
  border-left: 2px solid var(--connecting-line-not-active);
  position: absolute;
  left: -10px;
  top: 50%;
  margin-top: -15px;
  margin-left: -2px;
}

.participant:nth-child(odd)::after {
  content: '';
  border: 2px solid transparent;
  border-top-color: var(--connecting-line-not-active);
  border-right-color: var(--connecting-line-not-active);
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
  border-bottom-color: var(--connecting-line-not-active);
  border-right-color: var(--connecting-line-not-active);
  height: 50%;
  position: absolute;
  right: -10px;
  width: 12px;
  bottom: 50%;
  z-index: -1;
}

.participant__content::before {
  content: '';
  width: 12px;
  border-bottom: 2px solid var(--connecting-line-not-active);
  margin-left: -2px;
  position: absolute;
  top: 50%;
  left: -10px;
}

.participant__content {
  width: 100%;
  min-width: 60px;
  height: 40px;
  position: relative;
  border-radius: 50px;
  background-color: white;
  -webkit-box-shadow: 0px 3px 15px -4px rgba(0,0,0,0.42);
  -moz-box-shadow: 0px 3px 15px -4px rgba(0,0,0,0.42);
  box-shadow: 0px 3px 15px -4px rgba(0,0,0,0.42);
}
</style>
