<template>
  <div class="series">
    <div class="fluid-container" v-if="series.length != 0">
      <div class="header">
        <h2>Series</h2>
        <select v-model="currentGenre">
          <option :value="null" selected>All</option>
          <option v-for="genre in genres" :key="genre.id" :value="genre.id">
            {{ genre.name }}
          </option>
        </select>
      </div>
      <div class="row row-cols-1 row-cols-md-2 row-cols-lg-4 row-cols-xl-5">
        <div class="col" v-for="serie in filteredSeries" :key="serie.id">
          <Serie :serie="serie" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Serie from "./Serie.vue";
export default {
  name: "Series",
  props: ["query"],
  components: {
    Serie,
  },
  data() {
    return {
      displaySeriesSection: false,
      series: [],
      genres: [],
      currentGenre: null,
    };
  },
  watch: {
    query() {
      this.getSeries(this.query);
    },
  },
  created() {
    this.getSeries();
  },
  methods: {
    getSeries(query) {
      const url =
        query != null && query != ""
          ? "https://api.themoviedb.org/3/search/tv"
          : "https://api.themoviedb.org/3/tv/popular";
      const params = {
        api_key: "af0ba66c25483bbc937edba39186698d",
        language: "it-IT",
      };
      if (query != null && query != "") params.query = query;
      axios.get(url, { params }).then((res) => {
        // console.log(res.data.results);
        this.series = res.data.results;
        this.getDisplaySeriesSection();
      });
    },
    getDisplaySeriesSection() {
      this.displaySeriesSection = this.series.length != 0;
      axios
        .get("https://api.themoviedb.org/3/genre/tv/list", {
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
    filteredSeries() {
      const filter = this.series.filter((serie) => {
        // console.log(this.currentGenre);
        if (this.currentGenre == null) return true;
        return serie.genre_ids.includes(this.currentGenre);
      });
      return filter;
    },
  },
};
</script>

<style scoped lang="scss">
.series {
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