<template>
  <div
    class="bg-skyBlue text-black w-[50rem] h-[10rem] text-2xl rounded-2xl p-4"
  >
    <div>{{ scoreMessage }}</div>
    <div>{{ instructionMessage }}</div>
    <div>{{ highScoreMessage }}</div>
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
      this.scoreMessage = `Your Current Score is: ${this.reactionTime}`;
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