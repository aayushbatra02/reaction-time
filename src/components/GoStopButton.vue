<template>
  <button
    :style="[buttonType === 'Stop' ? { backgroundColor: '#C86A67' } : null]"
    @click="$emit(`changeButton`)"
  >
    {{ buttonType }}
  </button>
</template>

<script>
export default {
  props: ["buttonType"],
  emits:["changeButton"],
};
</script>

<style scoped>
button {
  background-color: #68ae64;
  color: white;
  border: none;
  font-size: 4rem;
  width: 50rem;
  height: 10rem;
  border-radius: 1rem;
  cursor: pointer;
}
</style>