<template>
  <div class="movie">
    <img :src="`http://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="" />
    <ul class="info">
      <!-- <li>
        {{ `ID: ${movie.id}` }}
      </li> -->
      <li>
        {{ `Titolo: ${movie.title}` }}
      </li>
      <li>
        {{ `Titolo Originale: ${movie.original_title}` }}
      </li>
      <li>
        <span> Language: </span>
        <span class="flag">
          <img
            :src="`https://flagcdn.com/16x12/${movie.original_language}.png`"
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
  // border: 0.2em solid orange;
  position: relative;
  height: 100%;
  display: flex;
  // overflow: hidden;
  &:hover {
    ul {
      opacity: 1;
    }
  }
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
    border: 0.1em solid transparent;
    background-color: gray;
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
    opacity: 0;
    list-style: none;
    background-color: rgba(0, 0, 0, 0.8);
    color: white;
    outline: 0.1em solid white;
    font-size: 1.1em;
    font-family: monospace;
    font-weight: bold;
    > li {
      padding: 0.2em 0;
      display: flex;
      align-items: center;
      // border: 0.2em solid red;
      .flag {
        display: flex;
        // border: 0.2em solid blue;
      }
    }
  }
}
</style>