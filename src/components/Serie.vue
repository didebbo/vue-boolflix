<template>
  <div class="serie">
    <div class="poster">
      <img
        :src="`http://image.tmdb.org/t/p/w500/${serie.poster_path}`"
        alt=""
      />
    </div>
    <ul :class="{ show: serie.poster_path == null }">
      <li>
        {{ `Title: ${serie.name}` }}
      </li>
      <li>
        {{ `Original Title: ${serie.original_name}` }}
      </li>
      <li>
        <span> Language: </span>
        <span class="flag">
          <img
            :src="`https://www.unknown.nu/flags/images/${serie.original_language}-100`"
            :alt="serie.original_language"
          />
        </span>
      </li>
      <li>
        Vote Average:
        <i
          v-for="(item, index) in Math.floor(serie.vote_average / 2)"
          :key="index"
          class="fas fa-star"
        ></i>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Serie",
  props: ["serie"],
};
</script>

<style scoped lang="scss">
.serie {
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