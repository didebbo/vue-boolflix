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
        <span> Vote Average: </span>
        <template v-for="(item, index) in 5">
          <i
            v-if="index <= Math.floor(serie.vote_average / 2)"
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
  name: "Serie",
  props: ["serie"],
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
    getVideo() {
      axios
        .get(`https://api.themoviedb.org/3/tv/${this.serie.id}/videos`, {
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
      font-size: 0.8em;
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