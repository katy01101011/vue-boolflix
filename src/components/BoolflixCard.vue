<template>
  <section>
    <div class="card" v-if="film">
      <img :src="`https://image.tmdb.org/t/p/w200${this.film.poster_path}`" alt="">
      <h2>{{ this.film.title }}</h2>
      <h3>{{ this.film.original_title }}</h3>
      
      <country-flag :country="`${this.film.original_language}`" />
      <div>
        <i v-for="star in stars(this.film.vote_average)" :key="star" class="fa-solid fa-star"></i>
      </div>
      
    </div>


    <div class="card" v-if="serie">
      <img :src="`https://image.tmdb.org/t/p/w200${this.serie.poster_path}`" alt="">
      <h2>{{ this.serie.name }}</h2>
      <h3>{{ this.serie.original_title }}</h3>
      <country-flag :country="`${this.serie.original_language}`" />
      <div>
        <i v-for="star in stars(this.serie.vote_average)" :key="star" class="fa-solid fa-star"></i>
      </div>
      <p>{{ this.seriesStars }}</p>
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

  methods: {
    stars(vote) {
      return Math.ceil(vote / 2);
    }
  },

  components: {
    CountryFlag,
  },
};
</script>

<style lang="scss" scoped>
@import "~@fortawesome/fontawesome-free/css/all.min.css";
div {
  .card {
    width: 200px;
    border: 1px solid black;
    margin: 1rem;
  }
}
</style>