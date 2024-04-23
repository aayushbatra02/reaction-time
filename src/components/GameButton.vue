<template>
  <button
    class="w-60 sm:w-[30rem] lg:w-[40rem] py-4 md:py-6 lg:py-8 xl:py-10 text-white text-4xl md:text-5xl lg:text-6xl rounded-2xl"
    :class="[buttonLabel === 'Stop'  ? 'bg-red' : 'bg-green']"
    @click="$emit(`gameButtonHandler`)"
  >
    {{ buttonLabel }}
  </button>
</template>

<script>
export default {
  props: ["buttonLabel"],
  emits: ["gameButtonHandler"],
};
</script>