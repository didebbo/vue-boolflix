<template>
  <div class="movies">
    <h3>This is the movies section</h3>
    <Movie />
  </div>
</template>

<script>
import Movie from "./Movie.vue";
export default {
  name: "Movies",
  props: ["query"],
  components: {
    Movie,
  },
  watch: {
    query() {
      console.log(this.query);
    },
  },
};
</script>

<style>
</style>