<template>
  <div>
    <component
      :is="currentComponent[currentNumber]"
      :point ='point'
      @next="addCurrentNumber"
      @back="backCurrentNumber"
      @minus10="minus10"
      @plus10="plus10"
      @plus20="plus20"
      @plus30="plus30"
    ></component>
  </div>
</template>

<script>
import Home from "./components/Home.vue";
import IsPlaying from "./components/IsPlaying.vue";
import Final from "./components/Final.vue";

export default {
  data() {
    return {
      currentComponent: ["Home", "IsPlaying", "Final"],
      currentNumber: 1,
      point: 0,
      currentPlusPoint: 0,
    };
  },
  components: {
    Home,
    IsPlaying,
    Final,
  },
  methods: {
    addCurrentNumber() {
      this.currentNumber++;
      if (this.currentNumber === 3) {
        this.currentNumber = 0;
      }
    },
    backCurrentNumber() {
      this.currentNumber--;
    },
    minus10() {
      this.currentPlusPoint = 10
      this.point -= this.currentPlusPoint
      console.log(this.point)
    },
    plus10() {
      this.currentPlusPoint = 10
      this.point += this.currentPlusPoint
      console.log(this.point)
    },
    plus20() {
      this.currentPlusPoint = 20
      this.point += this.currentPlusPoint
      console.log(this.point)
    },
    plus30() {
      this.currentPlusPoint = 30
      this.point += this.currentPlusPoint
      console.log(this.point)
    },
    plusRandom() {
      this.currentPlusPoint = Math.floor(Math.random() * 60) - 30
      this.point += this.currentPlusPoint
      console.log(this.point)
    }
  },
};
</script>

<style>
* {
  text-align: center;
  margin: 0 auto;
  box-sizing: border-box;
}
button {
  display: block;
  width: 20%;
  height: 15%;
}
</style>
