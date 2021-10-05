<template>
  <div class="tvs">
    <h2 v-if="tvs.length != 0">TVs:</h2>
    <Tv v-for="(tv, index) in tvs" :key="index" :tv="tv" />
  </div>
</template>

<script>
import axios from "axios";
import Tv from "./Tv.vue";
export default {
  name: "Tvs",
  props: ["query"],
  components: {
    Tv,
  },
  data() {
    return {
      tvs: [],
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
          this.tvs = res.data.results;
        });
    },
  },
};
</script>

<style>
</style>