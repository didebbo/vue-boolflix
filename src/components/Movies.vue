<template>
  <div class="movies">
    <div class="fluid-container" v-if="movies.length != 0">
      <div class="title">
        <h2>Movies</h2>
      </div>
      <div class="row row-cols-1 row-cols-md-2 row-cols-lg-4 row-cols-xl-5">
        <div class="col" v-for="movie in movies" :key="movie.id">
          <Movie :movie="movie" />
        </div>
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
  .fluid-container {
    .title {
      padding: 0.5em;
      color: lightgray;
      background-color: gray;
    }
    .row {
      > .col {
        padding: 1em;
      }
    }
  }
}
</style>