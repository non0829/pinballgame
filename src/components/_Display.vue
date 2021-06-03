<template>
  <div class="flex">
    <Game
      class="display"
      @minus10="$emit('minus10')"
      @plus10="$emit('plus10')"
      @plus20="$emit('plus20')"
      @plus30="$emit('plus30')"
      @plusRandom="$emit('plusRandom')"
    ></Game>
    <div class="side-menu">
      <p>{{ point }}</p>
    </div>
  </div>
</template>

<script>
import Game from "./__Game.vue";
export default {
  components: { Game },
  props: ["point"],
};
</script>

<style scoped>
.flex {
  display: flex;
  justify-content: center;
  /* flex-direction: column; */
  width: 625px;
  height: 90%;
  border: 10px solid rgba(0, 0, 0, 0.7);
  border-radius: 10px;
}
.display {
  width: 500px;
  background-color: whitesmoke;
}
.side-menu {
  color: aliceblue;
  background-color: rgba(0, 0, 0, 0.7);
  border-left: 3px solid rgba(0, 0, 0, 0.7);
  width: 125px;
}
</style>
