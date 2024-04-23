<template>
  <button
    class="bg-green w-60 sm:w-[30rem] lg:w-[40rem] py-4 md:py-6 lg:py-8 xl:py-10 text-white text-4xl md:text-5xl lg:text-6xl rounded-2xl"
    :style="[buttonType === 'Stop' ? { backgroundColor: '#C86A67' } : null]"
    @click="$emit(`gameButtonHandler`)"
  >
    {{ buttonType }}
  </button>
</template>

<script>
export default {
  props: ["buttonType"],
  emits: ["gameButtonHandler"],
};
</script>

normal 
w-[10rem] h-[2rem] 