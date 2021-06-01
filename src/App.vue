<template>
  <div>
    <component
      :is="currentComponent[currentNumber]"
      @next="addCurrentNumber"
      @back="backCurrentNumber"
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
