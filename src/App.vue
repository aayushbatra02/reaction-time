<template>
  <div
    :class="[isGameStopped ? 'bg-darkGreen' : 'bg-blue']"
    class="w-screen h-screen bg-blue flex flex-col justify-center items-center gap-8"
  >
    <game-button
      :buttonType="buttonType"
      @buttonHandler="buttonHandler"
    ></game-button>
    <result-component
      :buttonType="buttonType"
      :reactionTime="reactionTime"
      :isGameStopped="isGameStopped"
      :userStopTime="userStartTime"
      :highScoreTime="highScoreTime"
    ></result-component>
    <result-popup
      v-if="showPopup"
      @hidePopup="hidePopup"
      :reactionTime="reactionTime"
      :highScoreTime="highScoreTime"
      :isHighScore="isHighScore"
    ></result-popup>
  </div>
</template>

<script>
import GameButton from "./components/GameButton";
import ResultComponent from "./components/ResultComponent.vue";
import ResultPopup from "./components/ResultPopup.vue";

export default {
  components: { GameButton, ResultComponent, ResultPopup },
  data() {
    return {
      buttonType: "Go",
      isGameStopped: false,
      userStartTime: 0,
      userStopTime: null,
      gameStopTime: 0,
      reactionTime: null,
      reactionTimeInMS:null,
      highScoreInMs: null,
      highScoreTime: null,
      currentTimeOut: null,
      showPopup: false,
    };
  },
  methods: {
    generateRandomNumber(max, min) {
      return Math.floor(Math.random() * (max - min + 1) + min);
    },

    milliSecondsToTime(durationInMs) {
      let hours = Math.floor(durationInMs / (1000 * 60 * 60));
      hours = this.precedingZeroHandler(hours);
      durationInMs %= 1000 * 60 * 60;
      let minutes = Math.floor(durationInMs / (1000 * 60));
      minutes = this.precedingZeroHandler(minutes);
      durationInMs %= 1000 * 60;
      let seconds = Math.floor(durationInMs / 1000);
      seconds = this.precedingZeroHandler(seconds);
      let milliseconds = durationInMs % 1000;
      return `${hours}:${minutes}:${seconds}.${milliseconds}`;
    },

    precedingZeroHandler(time) {
      return time < 10 ? `0${time}` : time;
    },

    buttonHandler() {
      this.buttonType = this.buttonType === "Go" ? "Stop" : "Go";

      if (this.buttonType === "Stop") {
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
          this.reactionTimeInMS = timeDifference
          this.reactionTime = this.milliSecondsToTime(timeDifference);
          if (
            this.highScoreInMs === null ||
            this.highScoreInMs > timeDifference
          ) {
            this.highScoreInMs = timeDifference;
            this.highScoreTime = this.milliSecondsToTime(timeDifference);
          }
          this.showPopup = true;
        } else {
          this.reactionTime = undefined;
        }
        this.isGameStopped = false;
      }
    },
    hidePopup(){
      this.showPopup = false
    }
  },
  computed:{
    isHighScore(){
      return this.reactionTimeInMS <= this.highScoreInMs
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>