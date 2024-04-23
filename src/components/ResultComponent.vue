<template>
  <div
    class="bg-skyBlue text-black w-[50rem] text-2xl rounded-2xl p-4 flex flex-col gap-4"
  >
    <div v-if="scoreMessage">
      Your reaction time was <span v-if="hours">{{ hours }} hour </span>
      <span v-if="minutes">{{ minutes }} min </span> {{ seconds }} seconds
    </div>
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
      hours: 0,
      minutes: 0,
      seconds: 0,
    };
  },
  props: ["buttonType", "reactionTime", "highScoreTime"],
  methods: {
    getUnitsFromTime(time) {
      let timeUnits = time?.split(":");
      const [hr, min, sec] = timeUnits.map((unit) => parseFloat(unit));
      return { hr, min, sec };
    },
  },
  updated() {
    if (this.buttonType === "Stop") {
      this.instructionMessage = "Pay attention. Click stop when color changes";
      this.scoreMessage = null;
      this.highScoreMessage = null;
    } else if (this.reactionTime && this.buttonType === "Go") {
      const { hr, min, sec } = this.getUnitsFromTime(this.reactionTime);
      this.scoreMessage = true;
      this.hours = hr;
      this.minutes = min;
      this.seconds = sec;
      this.instructionMessage = "Click Go to test your reaction time!";
      this.highScoreMessage = `Your High Score is: ${this.highScoreTime}`;
    } else if (this.reactionTime === undefined) {
      this.instructionMessage = `Too quick... Try again!`;
    }
    if (this.reactionTime) {
      this.getUnitsFromTime(this.reactionTime);
    }
  },
};
</script>

<style scoped>
</style>