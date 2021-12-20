<template>
  <div class="winner">
    <h2 v-if="winner === 'Tie'" class="heading2">Tie</h2>
    <h2
      v-else-if="winner === 'Player' || winner === 'Computer'"
      class="heading2"
    >
      {{ winner }} won
    </h2>
    <h2 v-else class="heading2">Select your weapon</h2>
  </div>
</template>

<script lang="ts">
export default {
  name: "Winner",
  props: {
    winner: String,
  },
};
</script>

<style scoped lang="scss">
.winner {
  margin: 0 auto;
  background-color: rgba(148, 148, 148, 0.45);
  text-align: center;
  padding: 20px;
  border-radius: 2px;
}
</style>
