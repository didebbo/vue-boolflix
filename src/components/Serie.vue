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
      <li class="genres">{{ `Genres:${genres}` }}</li>
      <li class="cast">{{ `Cast:${cast}` }}</li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Serie",
  props: ["serie"],
  data() {
    return {
      maxLengthCast: 5,
      cast: [],
      genres: [],
    };
  },
  mounted() {
    this.getCast();
    this.getGenres();
  },
  methods: {
    getCast() {
      axios
        .get(`https://api.themoviedb.org/3/tv/${this.serie.id}/credits`, {
          params: {
            api_key: "af0ba66c25483bbc937edba39186698d",
            language: "it-IT",
          },
        })
        .then((res) => {
          for (
            let i = 0;
            i < this.maxLengthCast && i < res.data.cast.length;
            i++
          ) {
            // console.log(res.data.cast[i].name);
            this.cast.push(" " + res.data.cast[i].name);
          }
        });
    },
    getGenres() {
      axios
        .get(`https://api.themoviedb.org/3/tv/${this.serie.id}`, {
          params: {
            api_key: "af0ba66c25483bbc937edba39186698d",
            language: "it-IT",
          },
        })
        .then((res) => {
          for (let i = 0; i < res.data.genres.length; i++) {
            // console.log(res.data.genres[i].name);
            this.genres.push(" " + res.data.genres[i].name);
          }
        });
    },
  },
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
    .genres,
    .cast {
      padding: 1em 0;
      font-size: 0.8em;
    }
  }
}
</style>