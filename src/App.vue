<template>
  <div id="app">
    <Header @getQuery="getQuery" />
    <main>
      <h2>This is the Main</h2>
      <Movies :query="query" />
    </main>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Movies from "./components/Movies.vue";

export default {
  name: "App",
  components: {
    Header,
    Movies,
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
