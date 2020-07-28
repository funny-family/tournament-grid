<template>
  <div class="home">
    <Grid-setter
      placeholder="Enter an even number"
      type="text"
      v-model="amountOfPlayers"
    />
  </div>
</template>

<script>
import GridSetter from '@/components/inputs/GridSetter.vue';

export default {
  data: () => ({
    amountOfPlayers: ''
  }),
  components: {
    'Grid-setter': GridSetter
  }
};
</script>
