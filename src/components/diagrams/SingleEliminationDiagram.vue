<template>
  <div>
    <button
      class="reset-button"
      @click="resetDiagramData"
    >
      Reset diagram data
    </button>
    {{ participantNames }}
    amountOfParticipants: {{ amountOfParticipants }}
    <div class="single-elimination-diagram-container">
      <template
        v-for="(participants, columnIndex) in columns"
      >
        <div
          class="column"
          :class="['column-' + columnIndex]"
          :key="columnIndex"
        >
          <template v-for="(participantPosiitonInColumn, participantInColumnIndex) in participants">
            <div
              class="participant"
              :class="['participant-' + participantInColumnIndex]"
              :key="participantInColumnIndex"
            >
              <div class="participant__content">
                <input
                  class="participant__content__input"
                  type="text"
                  v-model="participantNames[
                    columnIndex +
                    participantInColumnIndex +
                    participantPosiitonInColumn +
                    participants +
                    participants
                  ]"
                />
              </div>
            </div>
          </template>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
const defaultParticipants = [256, 128, 64, 32, 16, 8, 4, 2, 1];

export default {
  name: 'Single-elimination-diagram',
  data: () => ({
    participantNames: {}
  }),
  props: {
    amountOfParticipants: {
      type: Number,
      default: 0
    }
  },
  computed: {
    columns() {
      return defaultParticipants
        .filter((columns) => columns <= this.$props.amountOfParticipants);
    }
  },
  methods: {
    resetDiagramData() {
      this.$data.participantNames = {};
    }
  },
  watch: {
    amountOfParticipants(value) {
      if (value > 0 || value === 0) {
        this.resetDiagramData();
      }
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

.reset-button {
  -webkit-appearance: none;
  border: 1px solid #FB7943;
  border-radius: 50px;
  background-color: white;
  padding: 10px 12px;
  color: #FB7943;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  outline: none;
  transition: 0.2s ease-in-out;
}

.reset-button:hover {
  background-color: #FB7943;
  color: white;
}

.reset-button:active {
  background-color: #ff5d17;
  color: white;
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

/* .participant::before {
  content: '';
  min-height: 30px;
  border-left: 2px solid var(--connecting-line-active);
  position: absolute;
  left: -10px;
  top: 50%;
  margin-top: -15px;
  margin-left: -2px;
} */

.participant:nth-child(odd)::after {
  content: '';
  border: 2px solid transparent;
  border-color: var(--connecting-line-not-active);
  border-left: 0;
  border-bottom: 0;
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
  border-color: var(--connecting-line-not-active);
  border-left: 0;
  border-top: 0;
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
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  min-width: 60px;
  height: 60px;
  position: relative;
  border-radius: 50px;
  background-color: white;
  -webkit-box-shadow: 0px 3px 15px -4px rgba(0,0,0,0.42);
  -moz-box-shadow: 0px 3px 15px -4px rgba(0,0,0,0.42);
  box-shadow: 0px 3px 15px -4px rgba(0,0,0,0.42);
}

.participant__content__input {
  -webkit-appearance: none;
  width: 100%;
  border: none;
  border-bottom: 1px solid #b6b6b6;
  background-color: transparent;
  padding: 6px 4px;
  margin: 4px 40px;
  font-size: 16px;
  outline: none;
  transition: 0.3s ease-in;
  align-items: center;
}

.participant__content__input:focus {
  border-bottom: 1px solid black;
}
</style>
