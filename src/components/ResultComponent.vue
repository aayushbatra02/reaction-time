<template>
  <div id="result">
    <div>{{ message }}</div>
    <div id="score">
      <div>Your High Score</div>
      <div>No highscore yet.</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "Click Go to test your reaction time!",
    };
  },
  props: ["buttonType"],
  updated() {
    this.message =
      this.buttonType === "Go"
        ? "Click Go to test your reaction time!"
        : "Pay attention. Click stop when the color changes.";

  },
};
</script>

<style scoped>
#result {
  background-color: #d9edf7;
  color: black;
  border: none;
  font-size: 1.5rem;
  width: 50rem;
  height: 10rem;
  border-radius: 1rem;
  padding: 1rem;
}
</style>