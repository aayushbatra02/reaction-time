<template>
  <div
    :class="[isGameStopped ? 'bg-darkGreen' : 'bg-blue']"
    class="w-screen h-screen bg-blue flex flex-col justify-center items-center gap-8"
  >
    <game-button
      :buttonLabel="buttonLabel"
      @gameButtonHandler="gameButtonHandler"
    ></game-button>
    <result-component
      :buttonLabel="buttonLabel"
      :reactionTime="reactionTime"
      :isGameStopped="isGameStopped"
      :userStopTime="userStartTime"
      :highScoreTime="highScoreTime"
    ></result-component>
  </div>
</template>

<script>
import moment from "moment";

import GameButton from "./components/GameButton";
import ResultComponent from "./components/ResultComponent.vue";

export default {
  components: { GameButton, ResultComponent },
  data() {
    return {
      buttonLabel: "Go",
      isGameStopped: false,
      userStartTime: 0,
      userStopTime: null,
      gameStopTime: 0,
      reactionTime: null,
      reactionTimeInMS: null,
      highScoreInMs: null,
      highScoreTime: null,
      currentTimeOut: null,
    };
  },
  methods: {
    generateRandomNumber(max, min) {
      return Math.floor(Math.random() * (max - min + 1) + min);
    },

    milliSecondsToTime(durationInMs) {
      const duration = moment.duration(durationInMs);
      const { hours, minutes, seconds, milliseconds } = duration._data;
      return `${hours}:${minutes}:${seconds}.${milliseconds}`;
    },

    precedingZeroHandler(time) {
      return time < 10 ? `0${time}` : time;
    },

    gameButtonHandler() {
      this.buttonLabel = this.buttonLabel === "Go" ? "Stop" : "Go";

      if (this.buttonLabel === "Stop") {
        this.userStartTime = Date.now();
        this.isGameStopped = false;
        this.gameStopTime = this.generateRandomNumber(5000, 2000);
        this.currentTimeOut = setTimeout(() => {
          this.isGameStopped = true;
        }, this.gameStopTime);
      } else {
        this.userStopTime = Date.now() - this.userStartTime;

        if (this.isGameStopped === false) {
          clearTimeout(this.currentTimeOut);
        }

        const timeDifference = this.userStopTime - this.gameStopTime;
        if (this.userStopTime > this.gameStopTime) {
          this.reactionTimeInMS = timeDifference;
          this.reactionTime = this.milliSecondsToTime(timeDifference);
          if (
            this.highScoreInMs === null ||
            this.highScoreInMs > timeDifference
          ) {
            this.highScoreInMs = timeDifference;
            this.highScoreTime = this.milliSecondsToTime(timeDifference);
          }
        } else {
          this.reactionTime = undefined;
        }
        this.isGameStopped = false;
      }
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>