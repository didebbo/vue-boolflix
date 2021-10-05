<template>
  <ul class="tv">
    <li>
      <img
        :src="`http://image.tmdb.org/t/p/w500/${tv.poster_path}`"
        :alt="tv.name"
      />
    </li>
    <li>
      {{ `ID: ${tv.id}` }}
    </li>
    <li>
      {{ `Title: ${tv.name}` }}
    </li>
    <li>
      {{ `Original Title: ${tv.original_name}` }}
    </li>
    <li>
      Language:
      <img
        :src="`https://flagcdn.com/16x12/${tv.original_language}.png`"
        :alt="tv.original_language"
      />
    </li>
    <li>
      Vote Average:
      <i
        v-for="(item, index) in Math.floor(tv.vote_average / 2)"
        :key="index"
        class="fas fa-star"
      ></i>
    </li>
  </ul>
</template>

<script>
export default {
  name: "Tv",
  props: ["tv"],
};
</script>

<style>
</style>