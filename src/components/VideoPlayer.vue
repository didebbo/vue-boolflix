<template>
  <div v-if="Player.show" class="videoPlayer">
    <div class="outside" @click="closePlayer"></div>
    <div class="position">
      <i class="fas fa-times-circle" @click="closePlayer"></i>
      <iframe :src="`https://www.youtube.com/embed/${trailer}`"> </iframe>
    </div>
  </div>
</template>

<script>
import Player from "../observable/Player";

export default {
  name: "VideoPlayer",
  props: ["trailer"],
  data() {
    return {
      Player,
    };
  },
  methods: {
    closePlayer() {
      this.Player.show = false;
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
  z-index: 2;
  display: flex;
  justify-content: center;
  align-items: center;

  .outside {
    position: fixed;
    width: 100%;
    height: 100vh;
    top: 0;
    left: 0;
    background-color: rgba(0, 0, 0, 0.4);
  }

  .position {
    position: relative;
    width: 50vw;
    height: 50vh;

    i {
      position: absolute;
      top: -0.5em;
      right: -0.5em;
      color: red;
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

@media screen and (orientation: portrait) {
  .videoPlayer {
    .position {
      width: 80vw;
      height: 80vh;
    }
  }
}
</style>