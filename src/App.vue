<template>
  <div id="app">
    <div v-if="loading" class="load">
      <BoolflixHeader @search="searchFilms" />
      <BoolflixStart />
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
import BoolflixStart from "./components/BoolflixStart.vue";

import axios from "axios";

export default {
  name: "App",
  components: {
    BoolflixHeader,
    BoolflixMain,
    BoolflixStart,
  },
  data: function () {
    return {
      resultsFound: [],
      inputFilmsFound: [],
      filmCast: [],
      searieCast: [],
      inputSeriesFound: [],
      loading: true,
      filmsId: [],
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
          axios
            .get(
              `https://api.themoviedb.org/3/movie/480/credits?api_key=71b7bde2de09a826a8388d622891aa6b`,
              {
                params: {
                  api_key: "71b7bde2de09a826a8388d622891aa6b",
                },
              }
            )
            .then((r) => {
              r.data.cast.forEach((actor, index) => {
                this.filmsId.push(resp.data.results[index].id);
                // console.log(this.filmsId);
              });
              this.filmsId.forEach((id, index) => {
                for (let i = 0; i < 5; i++) {
                  console.log(r);
                  
                }
              });
            });
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
  height: 100vh;
  background-color: black;
}
</style>