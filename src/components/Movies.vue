<template>
  <div class="movies">
    <!-- <h2 v-if="movies.length != 0">Movies:</h2> -->
    <div class="row">
      <div class="col" v-for="movie in movies" :key="movie.id">
        <Movie :movie="movie" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Movie from "./Movie.vue";
export default {
  name: "Movies",
  props: ["query"],
  components: {
    Movie,
  },
  data() {
    return {
      movies: [],
    };
  },
  watch: {
    query() {
      axios
        .get("https://api.themoviedb.org/3/search/movie", {
          params: {
            api_key: "af0ba66c25483bbc937edba39186698d",
            language: "it-IT",
            query: this.query,
          },
        })
        .then((res) => {
          console.log(res.data.results);
          this.movies = res.data.results;
        });
    },
  },
};
</script>

<style scoped lang="scss">
.movies {
  display: flex;
  flex-direction: column;
  align-items: center;
  // border: 0.2em solid red;
  .row {
    display: flex;
    flex-wrap: wrap;
    > .col {
      // border: 0.2em solid blue;
      padding: 1em;
      width: (100% / 5);
    }
  }
}
</style>