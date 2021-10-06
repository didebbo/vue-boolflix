<template>
  <div class="movies">
    <div class="fluid-container" v-if="displayMoviesSection">
      <div class="header">
        <h2>Movies</h2>
        <select v-model="currentGenre">
          <option :value="null" selected>All</option>
          <option v-for="genre in genres" :key="genre.id" :value="genre.id">
            {{ genre.name }}
          </option>
        </select>
      </div>
      <div class="row row-cols-1 row-cols-md-2 row-cols-lg-4 row-cols-xl-5">
        <div class="col" v-for="movie in filteredMovies" :key="movie.id">
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
      displayMoviesSection: false,
      movies: [],
      genres: [],
      currentGenre: null,
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
          // console.log(res.data.results);
          this.movies = res.data.results;
          this.getDisplayMoviesSection();
        });
    },
  },
  methods: {
    getDisplayMoviesSection() {
      this.displayMoviesSection = this.movies.length != 0;
      axios
        .get("https://api.themoviedb.org/3/genre/movie/list", {
          params: {
            api_key: "af0ba66c25483bbc937edba39186698d",
            language: "it-IT",
          },
        })
        .then((res) => {
          // console.log(res.data.genres);
          this.genres = res.data.genres;
        });
    },
  },
  computed: {
    filteredMovies() {
      const filter = this.movies.filter((movie) => {
        // console.log(this.currentGenre);
        if (this.currentGenre == null) return true;
        return movie.genre_ids.includes(this.currentGenre);
      });
      return filter;
    },
  },
};
</script>

<style scoped lang="scss">
.movies {
  .fluid-container {
    .header {
      display: flex;
      justify-content: space-between;
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