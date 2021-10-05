<template>
  <div class="tvs">
    <h2 v-if="tvs.length != 0">TVs:</h2>
    <Tv v-for="(tv, index) in tvs" :key="index" :tv="tv" />
  </div>
</template>

<script>
import Tv from "./Tv.vue";
export default {
  name: "Tvs",
  props: ["tvs"],
  components: {
    Tv,
  },
};
</script>

<style>
</style>