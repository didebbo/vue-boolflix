<template>
  <ul class="movie">
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
      {{ `Language: ${movie.original_language}` }}
    </li>
    <li>
      {{ `Vote Average: ${movie.vote_average}` }}
    </li>
  </ul>
</template>

<script>
export default {
  name: "Movie",
  props: ["movie"],
};
</script>

<style>
</style>