<template>
  <div class="movies">
    <h2 v-if="movies.length != 0">Movies:</h2>
    <Item v-for="(movie, index) in movies" :key="index" :movie="movie" />
  </div>
</template>

<script>
import Item from "./Item.vue";
export default {
  name: "Movies",
  props: ["movies"],
  components: {
    Item,
  },
};
</script>

<style>
</style>