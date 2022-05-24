<template>
  <div id="app">
    <BoolflixHeader @search="searchFilms" />
    <BoolflixMain :filmsArray="filmsFound" />
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
      resultsFound: [
        {
          filmsFound: "",
        },
        {
          seriesFound: "",
        },
      ],
      filmsApi: [
        "https://api.themoviedb.org/3/search/movie?",
        "https://api.themoviedb.org/3/search/tv?",
      ],
    };
  },

  methods: {
    searchFilms(inputKey) {
      for (let i = 0; i < this.filmsApi.length; i++) {
        axios
          .get(`${this.filmsApi[i]}`, {
            params: {
              api_key: "71b7bde2de09a826a8388d622891aa6b",
              query: inputKey,
            },
          })
          .then((resp) => {
            this.resultsFound[i] = resp.data.results;

            for (let i = 0; i < this.filmsApi.length; i++) {
              console.log(this.resultsFound[i]);
            }
          }
        );
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  width: 100%;
  height: calc(100vh);
}
</style>