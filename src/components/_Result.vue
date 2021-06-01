<template>
  <div class="descriptionBox" v-if="result">
    <p>Result</p>
    <button @click="active">戻る</button>
  </div>
</template>

<script>
export default {
  props: ['result'],
  methods: {
    active() {
      this.$emit('back')
    }
  }
}
</script>

<style scoped>
.descriptionBox {
  position: absolute;
  top: 20%;
  right: 0;
  left: 0;
  width: 90%;
  height: 60vh;
  max-width: 800px;
  background-color: cornsilk;
  opacity: 1;
  transition: opacity linear;
  transition-duration: 0.5s;
  z-index: 3;
}
</style>

