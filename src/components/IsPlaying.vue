<template>
  <div class="box">
    <BlockBack />
    <div class="mainGame">
    <h2>IsPlaying</h2>
    <button @click="toHome">ホームに戻る</button>
    <button @click="next">結果</button>
    </div>
  </div>
</template>

<script>
import BlockBack from "./_BlockBack.vue";
export default {
  components: {
    BlockBack,
  },
  methods: {
    next() {
      this.$emit("next");
    },
    toHome() {
      this.$emit("back");
    },
  },
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
  top: 20%;
  left: 0;
  right: 0;
}
</style>
