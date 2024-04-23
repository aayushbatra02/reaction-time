<template>
  <div
    @click.self="$emit('hidePopup')"
    class="bg-black/[.7] w-screen h-screen absolute flex justify-center items-center cursor-pointer"
  >
    <div
      class="bg-white cursor-default p-4 md:p-6 lg:p-8 xl:p-10 rounded flex flex-col items-center gap-4 text-lg md:text-xl lg:2xl"
    >
      <h2 class="text-2xl md:text-3xl lg:text-4xl font-bold">Winner!</h2>
      <p v-if="isHighScore" class="flex flex-col gap-2 items-center">
        <span>This is your High Score!!!</span>
        <strong>SCORE: {{ reactionTime }}</strong>
      </p>
      <p v-else>
        Your score is <strong>{{ reactionTime }}</strong>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["reactionTime", "highScoreTime", "isHighScore"],
  emits: ["hidePopup"],
};
</script>