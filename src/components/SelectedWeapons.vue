<template>
  <div>
    <div v-if="!player.selected.weapon" class="selected-weapons">
      <div class="weapon">
        <h2 class="heading2">Select weapon</h2>
      </div>
      <div class="weapon">
        <h2 class="heading2">Select weapon</h2>
      </div>
    </div>
    <div v-else class="selected-weapons">
      <div class="weapon">
        <img
          class="image"
          :src="player.selected.img"
          :alt="player.selected.weapon"
        />
      </div>
      <div class="weapon">
        <img class="image" :src="cpu.selected.img" :alt="cpu.selected.weapon" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: "SelectedWeapons",
  props: {
    player: {},
    cpu: {},
  },
};
</script>

<style scoped lang="scss">
.weapon {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: white;
}

.selected-weapons {
  display: flex;
  justify-content: space-around;
}
</style>
