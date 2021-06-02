<template>
  <div class="box">
    <BlockBack />
    <!-- <button @click="toHome" class="toHome">ホーム画面</button> -->
    <div class="mainGame">
      <Display />
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
  methods: {
    // next() {
    //   this.$emit("next");
    // },
    // toHome() {
    //   this.$emit("back");
    // },
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
  top: 5%;
  left: 0;
  right: 0;
  height: 100%;
}
/* .toHome {
  position: absolute;
  top: 30px;
  right: 30px;
  height: 40px;
  background-color: wheat;
  border-radius: 5px;
  box-shadow: 0 3px 2px black;
 
}
.toHome:hover {
  opacity: 0.8;
}
.toHome:active {
  box-shadow: none;
  transform: translateY(3px);
} */
</style>
