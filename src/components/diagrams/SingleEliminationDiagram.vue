<template>
  <div class="single-elimination-diagram-container">
    <template v-for="(participants, columnIndex) in columns">
      <div
        class="column"
        :class="['column-' + columnIndex]"
        :key="columnIndex"
      >
        columns: {{ columns }}
        <template v-for="(participantPosiitonInColumn, participantIndex) in participants">
          <div
            class="participant"
            :class="['participant-' + participantIndex]"
            :key="participantIndex"
          >
            <div class="participant__content">
              <input
                class="participant__content__input"
                type="text"
                placeholder="Participant name"
                v-if="Math.max(...columns) === participants"
              />
              <br/>
              participantIndex: {{ participantIndex }}
              <br/>
              participantPosiitonInColumn: {{ participantPosiitonInColumn }}
              <br/>
              participants: {{ participants }}
              <br/>
            </div>
          </div>
        </template>
      </div>
    </template>
  </div>
</template>

<script>
const defaultMatches = [256, 128, 64, 32, 16, 8, 4, 2, 1];
const defaultParticipants = [256, 128, 64, 32, 16, 8, 4, 2, 1];

export default {
  name: 'Single-elimination-diagram',
  props: {
    diagramSize: {
      type: Number,
      default: 0
    }
  },
  computed: {
    columns() {
      return defaultParticipants
        .filter((columns) => columns <= this.$props.diagramSize);
    },
    matches() {
      return defaultMatches
        .filter((currentMatches) => currentMatches <= Math.ceil(this.$props.diagramSize / 2));
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
  max-width: 160px;
  border: none;
  border-bottom: 1px solid #b6b6b6;
  background-color: transparent;
  padding: 6px 4px;
  margin: 4px;
  font-size: 16px;
  outline: none;
  transition: 0.3s ease-in;
}

.participant__content__input:focus {
  border-bottom: 1px solid black;
}
</style>
