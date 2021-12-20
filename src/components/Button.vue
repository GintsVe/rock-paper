<template>
  <button class="button">{{ title }}</button>
</template>

<script lang="ts">
export default {
  name: "Button",
  props: {
    title: String,
  },
};
</script>

<style scoped lang="scss">
.button {
  max-width: 400px;
  width: 100%;
  border: none;
  border-radius: 20px;
  background-color: rgba(68, 68, 68, 0.6);
  color: white;
  font-family: "Inter", sans-serif;
  font-size: 24px;
  padding: 20px;

  &:hover {
    cursor: pointer;
    background-color: rgba(68, 68, 68, 0.9);
  }
}
</style>
