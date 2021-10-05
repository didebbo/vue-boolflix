<template>
  <div id="app">
    <Header />
    <main>
      <h2>This is the Main</h2>
      <Movies />
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
};
</script>

<style lang="scss">
</style>
