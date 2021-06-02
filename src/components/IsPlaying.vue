<template>
  <div class="box">
    <BlockBack />
    <div class="mainGame">
      <Display
        :point="point"
        @minus10="$emit('minus10')"
        @plus10="$emit('plus10')"
        @plus20="$emit('plus20')"
        @plus30="$emit('plus30')"
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
.mainGame {
  z-index: 1;
  position: absolute;
  top: 5%;
  left: 0;
  right: 0;
  height: 100%;
}
</style>
