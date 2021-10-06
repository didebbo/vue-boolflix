<template>
  <div class="series">
    <div class="fluid-container" v-if="series.length != 0">
      <div class="title">
        <h2>Series</h2>
      </div>
      <div class="row row-cols-1 row-cols-md-4 row-cols-lg-5">
        <div class="col" v-for="serie in series" :key="serie.id">
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
      series: [],
    };
  },
  watch: {
    query() {
      axios
        .get("https://api.themoviedb.org/3/search/tv", {
          params: {
            api_key: "af0ba66c25483bbc937edba39186698d",
            language: "it-IT",
            query: this.query,
          },
        })
        .then((res) => {
          // console.log(res.data.results);
          this.series = res.data.results;
        });
    },
  },
};
</script>

<style scoped lang="scss">
.series {
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