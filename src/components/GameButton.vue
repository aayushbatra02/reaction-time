<template>
  <button
    class="bg-green text-white w-[50rem] h-[10rem] text-6xl rounded-2xl"
    :style="[buttonType === 'Stop' ? { backgroundColor: '#C86A67' } : null]"
    @click="$emit(`buttonHandler`)"
  >
    {{ buttonType }}
  </button>
</template>

<script>
export default {
  props: ["buttonType"],
  emits: ["buttonHandler"],
};
</script>
