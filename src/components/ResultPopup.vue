<template>
  <div
    @click.self="$emit('hidePopup')"
    class="bg-black/[.7] w-screen h-screen absolute flex justify-center items-center cursor-pointer"
  >
    <div
      class="bg-white cursor-default p-8 rounded flex flex-col items-center gap-4 text-2xl"
    >
      <h2 class="text-4xl font-bold">Winner!</h2>
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