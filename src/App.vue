<template>
  <div id="app">
    <BoolflixHeader @search="searchFilms" />
    <BoolflixMain :filmsArray="filmsFound"/>
  </div>
</template>

<script>
import BoolflixHeader from "./components/BoolflixHeader.vue";
import BoolflixMain from "./components/BoolflixMain.vue";

import axios from 'axios';

export default {
  name: "App",
  components: {
    BoolflixHeader,
    BoolflixMain,
  },
  data: function() {
    return {
      filmsFound: []
    }
  },

  methods: {
    searchFilms(inputKey) {
      axios
      .get('https://api.themoviedb.org/3/search/movie?', {
        params: {
          api_key: "71b7bde2de09a826a8388d622891aa6b",
          query: inputKey
          }
        }
      )
      .then((resp) => {
        this.filmsFound = resp.data.results;
        console.log(this.filmsFound);
      }
      );
    }
  }
};
</script>

<style lang="scss">
#app {
  width: 100%;
  height: calc(100vh);
}
</style>