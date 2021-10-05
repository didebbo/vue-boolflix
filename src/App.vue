<template>
  <div id="app">
    <Header @getQuery="getQuery" />
    <main>
      <Movies :movies="movies" />
    </main>
  </div>
</template>

<script>
import axios from "axios";
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
      movies: [],
      tvs: [],
    };
  },
  methods: {
    getQuery(query) {
      this.query = query;
      this.getMovies();
      this.getTvs();
    },
    getMovies() {
      axios
        .get("https://api.themoviedb.org/3/search/movie", {
          params: {
            api_key: "af0ba66c25483bbc937edba39186698d",
            language: "it-IT",
            query: this.query,
          },
        })
        .then((res) => {
          // console.log(res.data.results);
          this.movies = res.data.results;
        });
    },
    getTvs() {
      axios
        .get("https://api.themoviedb.org/3/search/tv", {
          params: {
            api_key: "af0ba66c25483bbc937edba39186698d",
            language: "it-IT",
            query: this.query,
          },
        })
        .then((res) => {
          console.log(res.data.results);
          // this.tvs = res.data.results;
        });
    },
  },
};
</script>

<style lang="scss">
</style>
