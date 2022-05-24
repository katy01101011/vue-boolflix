<template>
  <section>
    <div v-if="film">
      <img :src="`https://image.tmdb.org/t/p/w200${this.film.poster_path}`" alt="">
      <h2>{{ this.film.title }}</h2>
      <h3>{{ this.film.original_title }}</h3>
      <country-flag :country="`${this.film.original_language}`" />
      <p>{{ Math.round( this.film.vote_average / 2 ) }}</p>
    </div>

    <div v-if="serie">
      <img :src="`https://image.tmdb.org/t/p/w200${this.serie.poster_path}`" alt="">
      <h2>{{ this.serie.name }}</h2>
      <h3>{{ this.serie.original_title }}</h3>
      <country-flag :country="`${this.serie.original_language}`" />
      <p>{{ this.serie.vote_average }}</p>
    </div>
  </section>
</template>

<script>
import CountryFlag from "vue-country-flag";

export default {
  name: "BoolflixCard",
  props: {
    film: Object,
    serie: Object,
  },
  components: {
    CountryFlag,
  },
};
</script>

<style lang="scss" scoped>
@import "~@fortawesome/fontawesome-free/css/all.min.css";
div {
  div {
    border: 1px solid black;
    margin: 1rem;
  }
}
</style>