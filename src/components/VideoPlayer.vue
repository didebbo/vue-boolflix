<template>
  <div v-if="showPlayer" class="videoPlayer">
    <div class="position">
      <i class="fas fa-times-circle" @click="closePlayer"></i>
      <iframe :src="`https://www.youtube.com/embed/${trailer}`"> </iframe>
    </div>
  </div>
</template>

<script>
export default {
  name: "VideoPlayer",
  props: ["trailer"],
  data() {
    return {
      showPlayer: false,
    };
  },
  watch: {
    trailer() {
      this.showPlayer = true;
      // console.log(this.trailer);
    },
  },
  methods: {
    closePlayer() {
      this.showPlayer = false;
    },
  },
};
</script>

<style scoped lang="scss">
.videoPlayer {
  position: fixed;
  width: 100%;
  height: 100vh;
  top: 0;
  left: 0;
  // transform: translate(-50%, -50%);
  background-color: rgba(0, 0, 0, 0.4);
  z-index: 2;
  display: flex;
  justify-content: center;
  align-items: center;

  .position {
    position: relative;
    width: 560px;
    height: 315px;

    i {
      position: absolute;
      top: -0.5em;
      right: -0.5em;
      color: red;
      z-index: 3;
      font-size: 2em;
      cursor: pointer;
    }

    iframe {
      width: 100%;
      height: 100%;
      border: 0;
    }
  }
}
</style>