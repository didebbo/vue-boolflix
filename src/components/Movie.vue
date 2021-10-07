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
        <span> Vote Average: </span>
        <template v-for="(item, index) in 5">
          <i
            v-if="index <= Math.floor(movie.vote_average / 2)"
            class="fas fa-star"
            :key="index"
          ></i>
          <i v-else class="far fa-star" :key="index"></i>
        </template>
      </li>
      <li class="genres">{{ `Genres:${genres}` }}</li>
      <li class="cast">{{ `Cast:${cast}` }}</li>
      <li class="trailer" v-if="trailer">
        <button @click="playVideo">Trailer</button>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import Player from "../observable/Player";

export default {
  name: "Movie",
  props: ["movie"],
  data() {
    return {
      maxLengthCast: 5,
      cast: [],
      genres: [],
      trailer: null,
      Player,
    };
  },
  mounted() {
    this.getCast();
    this.getGenres();
    this.getVideo();
  },
  methods: {
    getCast() {
      axios
        .get(`https://api.themoviedb.org/3/movie/${this.movie.id}/credits`, {
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
        .get(`https://api.themoviedb.org/3/movie/${this.movie.id}`, {
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
    getVideo() {
      axios
        .get(`https://api.themoviedb.org/3/movie/${this.movie.id}/videos`, {
          params: {
            api_key: "af0ba66c25483bbc937edba39186698d",
            language: "it-IT",
          },
        })
        .then((res) => {
          if (res.data.results.length > 0) {
            this.trailer = res.data.results[0].key;
          }
        });
    },
    playVideo() {
      this.$emit("playVideo", this.trailer);
      this.Player.show = true;
    },
  },
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
      height: 20em;
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
      i {
        font-size: 0.8em;
      }
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
      font-size: 0.9em;
    }
    .trailer {
      display: flex;
      justify-content: center;
      margin-top: auto;
      button {
        padding: 0.2em 0.5em;
      }
    }
  }
}
</style>