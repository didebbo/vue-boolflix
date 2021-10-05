<template>
  <div class="movies">
    <h2 v-if="movies.length != 0">Movies:</h2>
    <Movie v-for="(movie, index) in movies" :key="index" :movie="movie" />
  </div>
</template>

<script>
import Movie from "./Movie.vue";
export default {
  name: "Movies",
  props: ["movies"],
  components: {
    Movie,
  },
};
</script>

<style>
</style>