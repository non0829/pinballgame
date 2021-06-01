<template>
  <div class="box">
    <h1 class="boxChild">崩せ！ブロックの壁</h1>
    <transition tag="template" name="fade">
      <div
        class="flex boxChild"
        :class="{ actionBlock: description }"
        v-if="!description && !result"
      >
        <button @click="start">ゲームスタート</button>
        <button @click="changeDescription">説明</button>
        <button @click="changeResult">今までの記録</button>
      </div>
    </transition>
    <transition tag="template" name="fade">
      <description @back="changeDescription" :description="description"></description>
    </transition>
    <transition tag="template" name="fade">
      <result @back="changeResult" :result="result"></result>
    </transition>
    <BlockBack />
  </div>
</template>

<script>
import BlockBack from "./_BlockBack.vue";
import description from "./_Description.vue";
import result from "./_Result.vue";
export default {
  components: {
    BlockBack,
    description,
    result
  },
  data() {
    return {
      description: false,
      result: false,
    };
  },
  methods: {
    changeDescription() {
      this.description = !this.description;
    },
    changeResult() {
      this.result = !this.result;
    },
    start() {
      this.$emit('next')
    }
  },
};
</script>

<style scoped>
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.7s;
}

.box {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  position: relative;
  background-color: rgba(0, 0, 0, 0.2);
}
.boxChild {
  position: absolute;
  z-index: 1;
}
h1,
button {
  display: inline-block;
  width: 500px;
  background-color: rgba(255, 255, 255, 0.6);
  border-radius: 5px;
  padding: 5px;
  border: 5px solid rgb(98, 119, 119);
  margin-top: 30px;
  font-size: 40px;
  top: 20%;
  left: 0;
  right: 0;
}
.boxChild:nth-child(2) {
  max-width: 760px;
  width: 80%;
  top: 60%;
  left: 0;
  right: 0;
}
.flex {
  display: flex;
  flex-direction: initial;
  flex-wrap: wrap;
  flex-shrink: 0;
}
button {
  font-size: 20px;
  opacity: 1;
  margin: 0 auto 20px;
  width: 300px;
  transition: opacity linear;
  transition-duration: 5s;
}
button:hover {
  cursor: pointer;
  opacity: 0.8;
}
button:active {
  box-shadow: none;
  transform: translateY(3px);
}
.actionBlock {
  opacity: 0;
  user-select: none;
}
</style>
