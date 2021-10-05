<template>
  <ul class="movie">
    <li>
      <img
        :src="`http://image.tmdb.org/t/p/w500/${movie.poster_path}`"
        :alt="movie.title"
      />
    </li>
    <li>
      {{ `ID: ${movie.id}` }}
    </li>
    <li>
      {{ `Title: ${movie.title}` }}
    </li>
    <li>
      {{ `Original Title: ${movie.original_title}` }}
    </li>
    <li>
      Language:
      <img
        :src="`https://flagcdn.com/16x12/${movie.original_language}.png`"
        :alt="movie.original_language"
      />
    </li>
    <li>
      Vote Average:
      <i
        v-for="(item, index) in Math.floor(movie.vote_average / 2)"
        :key="index"
        class="fas fa-star"
      ></i>
    </li>
  </ul>
</template>

<script>
export default {
  name: "Movie",
  props: ["movie"],
};
</script>

<style scoped lang="scss">
</style>