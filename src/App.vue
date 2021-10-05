<template>
  <div id="app">
    <Header @getQuery="getQuery" />
    <main>
      <Movies :query="query" />
      <Tvs :query="query" />
    </main>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Movies from "./components/Movies.vue";
import Tvs from "./components/Tvs.vue";

export default {
  name: "App",
  components: {
    Header,
    Movies,
    Tvs,
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
</style>
