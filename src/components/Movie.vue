<template>
  <div class="movie">
    <img
      :src="`http://image.tmdb.org/t/p/w500/${movie.poster_path}`"
      :alt="movie.title"
    />
    <ul v-if="false" class="info">
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
  </div>
</template>

<script>
export default {
  name: "Movie",
  props: ["movie"],
};
</script>

<style scoped lang="scss">
.movie {
  // border: 0.2em solid orange;
  height: 100%;
  display: flex;
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
  }
}
</style>