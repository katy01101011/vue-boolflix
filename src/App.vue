<template>
  <div id="app">
    <div v-if="loading" class="load">
      <BoolflixHeader @search="searchFilms" />
      <div class="load__info">
        <div class="n-serie">
          <img class="n-logo" src="./assets/n-logo.png" alt="" />
          <span> S E R I E</span>
        </div>
        <img src="./assets/russian_logo.png" alt="" />
        <p>
          Nadia continua a morire e a rivivere il suo trentaseiesimo compleanno,
          bloccata in un loop temporale che non le lascia via di fuga davanti
          all'abisso della mortalità.
        </p>
        <div class="buttons">
          <button class="play-btn">
            <i class="fa-solid fa-play"></i> Riproduci
          </button>
          <button class="info-btn">
            <span class="info-icon">i</span>
            Altre info
          </button>
        </div>
      </div>
    </div>
    <div v-else>
      <BoolflixHeader @search="searchFilms" />
      <BoolflixMain
        :filmsFound="inputFilmsFound"
        :seriesFound="inputSeriesFound"
      />
    </div>
  </div>
</template>

<script>
import BoolflixHeader from "./components/BoolflixHeader.vue";
import BoolflixMain from "./components/BoolflixMain.vue";

import axios from "axios";

export default {
  name: "App",
  components: {
    BoolflixHeader,
    BoolflixMain,
  },
  data: function () {
    return {
      resultsFound: [],
      inputFilmsFound: [],
      inputSeriesFound: [],
      loading: true,
    };
  },

  methods: {
    searchFilms(inputKey) {
      axios
        .get("https://api.themoviedb.org/3/search/movie", {
          params: {
            api_key: "71b7bde2de09a826a8388d622891aa6b",
            query: inputKey,
          },
        })
        .then((resp) => {
          this.inputFilmsFound = resp.data.results;
        });
      axios
        .get("https://api.themoviedb.org/3/search/tv", {
          params: {
            api_key: "71b7bde2de09a826a8388d622891aa6b",
            query: inputKey,
          },
        })
        .then((resp) => {
          this.inputSeriesFound = resp.data.results;
          this.loading = false;
        });
    },
  },
};
</script>

<style lang="scss">
@import "./style/common.scss";
@import "~@fortawesome/fontawesome-free/css/all.min.css";

#app {
  width: 100%;
  height: calc(100vh);
  background-color: black;

  .load {
    width: 100%;
    height: 100vh;
    background-image: url(./assets/russian_doll.jpeg);
    background-repeat: no-repeat;
    background-size: cover;
    position: relative;

    &__info {
      max-width: 40vw;
      color: white;
      font-size: 2rem;
      padding-left: 4.6rem;
      position: absolute;
      left: 1rem;
      bottom: 24vh;

      .n-serie {
        display: flex;
        align-items: center;
        font-size: 1.4rem;

        .n-logo {
          height: 3rem;
          margin: 0.3rem;
          margin-right: 1rem;
        }
      }

      img {
        height: 7.5rem;
        margin-top: 3rem;
      }

      p {
        margin-top: 2rem;
        margin-bottom: 3rem;
      }

      .buttons {
        display: flex;
        align-items: center;

        button {
        padding: 1rem 2.8rem;
        font-size: 1.8rem;
        border: none;
        margin-right: 1.2rem;
        border-radius: 5px;
        display: flex;
        align-items: center;

        i {
          font-size: 2.5rem;
          margin-right: 0.8rem;
          color: black;
        }

        .info-icon {
          display: inline-block;
          width: 2.7rem;
          height: 2.7rem;
          line-height: 2.4rem;
          border-radius: 50%;
          border: 4px solid white;
          font-size: 1.8rem;
          margin-right: 0.9rem;
        }
      }
      }

      .play-btn {
        background-color: white;
        color: black;

        &:hover {
          background-color: rgba($color: #ffffff, $alpha: 0.85);
        }
      }

      .info-btn {
        background-color: rgba($color: #767676, $alpha: 0.7);
        color: white;

        &:hover {
          background-color: rgba($color: #767676, $alpha: 0.4);
        }
      }
    }
  }
}
</style>