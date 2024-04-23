<template>
  <div
    class="bg-skyBlue text-black w-[50rem] text-2xl rounded-2xl p-4 flex flex-col gap-4"
  >
    <div v-if="scoreMessage">{{ scoreMessage }}</div>
    <div v-if="instructionMessage">{{ instructionMessage }}</div>
    <div v-if="highScoreMessage">{{ highScoreMessage }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      instructionMessage: "Click Go to test your reaction time!",
      scoreMessage: null,
      highScoreMessage: null,
    };
  },
  props: ["buttonType", "reactionTime", "highScoreTime"],
  updated() {
    if (this.buttonType === "Stop") {
      this.instructionMessage = "Pay attention. Click stop when color changes";
      this.scoreMessage = null;
      this.highScoreMessage = null;
    } else if (this.reactionTime && this.buttonType === "Go") {
      this.scoreMessage = `Your reaction time was ${this.reactionTime}`;
      this.instructionMessage = "Click Go to test your reaction time!";
      this.highScoreMessage = `Your High Score is: ${this.highScoreTime}`;
    } else if (this.reactionTime === undefined) {
      this.instructionMessage = `Too quick... Try again!`;
    }
  },
};
</script>

<style scoped>
</style>