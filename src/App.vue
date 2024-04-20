<template>
  <div id="container">
    <go-stop-button :buttonType="buttonType" @changeButton="changeButton"></go-stop-button>
    <result-component :buttonType="buttonType"></result-component>
  </div>
</template>

<script>
import GoStopButton from "./components/GoStopButton";
import ResultComponent from './components/ResultComponent.vue';

export default {
  components: { GoStopButton, ResultComponent },
  data() {
    return {
      buttonType: "Go",
    };
  },
  methods:{
    changeButton(){
      this.buttonType =  this.buttonType === 'Go' ? 'Stop' : 'Go';
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

#container{
  width: 100vw;
  height: 100vh;
  background-color: #2B87D1;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 2vw;
}
</style>


<!-- colors: {
  blue: "#2B87D1",
  green: "#68AE64",
  skyBlue: "#D9EDF7",
  darkGreen: "#008000",
  red: "#C86A67",
}, -->