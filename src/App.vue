<template>
  <div
    :class="[gameStop ? 'bg-darkGreen' : 'bg-blue']"
    class="w-screen h-screen bg-blue flex flex-col justify-center items-center gap-8"
  >
    <go-stop-button
      :buttonType="buttonType"
      @buttonHandler="buttonHandler"
    ></go-stop-button>
    <result-component
      :buttonType="buttonType"
      :reactionTime="reactionTime"
      :gameStop="gameStop"
      :userStopTime="userStartTime"
      :highScoreTime="highScoreTime"
    ></result-component>
    <result-popup
      v-if="showPopup"
      @hidePopup="() => (showPopup = false)"
      :reactionTime="reactionTime"
      :highScoreTime="highScoreTime"
      :isHighScore="reactionTimeInMS <= highScoreInMs"
    ></result-popup>
  </div>
</template>

<script>
import GoStopButton from "./components/GoStopButton";
import ResultComponent from "./components/ResultComponent.vue";
import ResultPopup from "./components/ResultPopup.vue";

export default {
  components: { GoStopButton, ResultComponent, ResultPopup },
  data() {
    return {
      buttonType: "Go",
      gameStop: false,
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
    randomNumber(max, min) {
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
        this.gameStop = false;
        this.gameStopTime = this.randomNumber(5000, 2000);
        this.currentTimeOut = setTimeout(() => {
          this.gameStop = true;
        }, this.gameStopTime);
      } else {
        this.userStopTime = Date.now() - this.userStartTime;

        if (this.gameStop === false) {
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
            console.log("NEW HIGH SCORE");
            this.highScoreInMs = timeDifference;
            this.highScoreTime = this.milliSecondsToTime(timeDifference);
          }
          this.showPopup = true;
        } else {
          this.reactionTime = undefined;
        }
        this.gameStop = false;
      }
    },
  },
  updated() {
    console.log({
      // gameStop: this.gameStop,
      // startTime: this.userStartTime,
      // UserStopTime: this.userStopTime,
      // GameStopTime: this.gameStopTime,
      reactionTime: this.reactionTimeInMS,
      highScoreTime: this.highScoreInMs,
      // buttonType: this.buttonType,
      // highScoreInMs: this.highScoreInMs,
    });
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