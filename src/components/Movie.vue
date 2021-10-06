<template>
  <div class="movie">
    <div class="poster">
      <img
        :src="`http://image.tmdb.org/t/p/w500/${movie.poster_path}`"
        alt=""
      />
    </div>
    <ul :class="{ show: movie.poster_path == null }">
      <li>
        {{ `Title: ${movie.title}` }}
      </li>
      <li>
        {{ `Original Title: ${movie.original_title}` }}
      </li>
      <li>
        <span> Language: </span>
        <span class="flag">
          <img
            :src="`https://www.unknown.nu/flags/images/${movie.original_language}-100`"
            :alt="movie.original_language"
          />
        </span>
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
  position: relative;
  height: 100%;
  display: flex;
  overflow: hidden;
  &:hover {
    ul {
      opacity: 1;
    }
  }
  .poster {
    position: relative;
    display: flex;
    width: 100%;
    height: 100%;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      object-position: center;
    }
  }
  ul {
    position: absolute;
    display: flex;
    flex-direction: column;
    padding: 1em;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    list-style: none;
    background-color: rgba(0, 0, 0, 0.8);
    color: white;
    font-size: 1.1em;
    font-family: monospace;
    font-weight: bold;
    opacity: 0;
    &.show {
      opacity: 1;
    }
    > li {
      padding: 0.2em 0;
      display: flex;
      align-items: center;
      .flag {
        display: flex;
        img {
          width: 1.5em;
          height: 1em;
        }
      }
    }
  }
}
</style>