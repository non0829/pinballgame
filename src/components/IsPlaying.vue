<template>
  <div class="box">
    <div class="finishText">
      <h1>Finish!!!</h1>
      <button>次へ</button>
    </div>
    <BlockBack />
    <div class="mainGame">
      <Display
        :point="point"
        @minus10="$emit('minus10')"
        @plus10="$emit('plus10')"
        @plus20="$emit('plus20')"
        @plus30="$emit('plus30')"
        @plusRandom="$emit('plusRandom')"
      />
    </div>
  </div>
</template>

<script>
import BlockBack from "./_BlockBack.vue";
import Display from "./_Display.vue";
export default {
  components: {
    BlockBack,
    Display,
  },
  props: ["point"],
};
</script>

<style scoped>
.box {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  position: relative;
  background-color: rgba(0, 0, 0, 0.2);
}
.finishText {
  position: absolute;
  top: 40%;
  left: 0;
  right: 0;
  z-index: 2;
}
.finishText h1 {
  font-size: 50px;
}
.finishText button {
  display: inline-block;
  width: 300px;
  margin-top: 30px;
  padding: 10px;
  background-color: seashell;
  font-size: 28px;
  border-radius: 5px;
  box-shadow: 0 3px 2px gray;
}
.finishText button:hover {
  opacity: 0.8;
}
.finishText button:active {
  box-shadow: none;
  transform: translateY(3px);
}
.mainGame {
  z-index: 1;
  position: absolute;
  top: 5%;
  left: 0;
  right: 0;
  height: 100%;
}
</style>
