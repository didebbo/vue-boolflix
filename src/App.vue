<template>
  <div id="app">
    <Header @getQuery="getQuery" />
    <VideoPlayer />
    <main>
      <Movies :query="query" />
      <Series :query="query" />
    </main>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Movies from "./components/Movies.vue";
import Series from "./components/Series.vue";
import VideoPlayer from "./components/VideoPlayer.vue";

export default {
  name: "App",
  components: {
    Header,
    Movies,
    Series,
    VideoPlayer,
  },
  data() {
    return {
      query: "",
    };
  },
  methods: {
    getQuery(query) {
      this.query = query;
    },
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap-grid";

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #434343;
  font-family: sans-serif;
}

main {
  padding: 1em;
}
</style>
