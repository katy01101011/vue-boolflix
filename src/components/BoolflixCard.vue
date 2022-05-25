<template>
  <section>
    <div class="card" v-if="film">
      <img
        :src="`https://image.tmdb.org/t/p/w200${this.film.poster_path}`"
        alt=""
      />
      <h2>{{ this.film.title }}</h2>
      <h3>{{ this.film.original_title }}</h3>
      <span v-if="this.languages.includes(this.film.original_language)">
        <img
          class="flag-icon"
          :src="require(`../assets/flags/${this.film.original_language}.png`)"
          alt=""
        />
      </span>
      <span class="no-flag-icon" v-else>
        {{ this.film.original_language.toUpperCase() }}
      </span>
      <!-- <country-flag :country="`${this.film.original_language}`" /> -->
      <div>
        <i
          v-for="star in stars(this.film.vote_average)"
          :key="star"
          class="fa-solid fa-star"
        ></i>
      </div>
    </div>

    <!-- <div class="card" v-if="serie">
      <img :src="`https://image.tmdb.org/t/p/w200${this.serie.poster_path}`" alt="">
      <h2>{{ this.serie.name }}</h2>
      <h3>{{ this.serie.original_title }}</h3>
      <country-flag :country="`${this.serie.original_language}`" />
      <div>
        <i v-for="star in stars(this.serie.vote_average)" :key="star" class="fa-solid fa-star"></i>
      </div>
    </div> -->
  </section>
</template>

<script>
// import CountryFlag from "vue-country-flag";

export default {
  name: "BoolflixCard",

  data() {
    return {
      languages: ["ch", "en", "es", "fr", "gr", "jp", "pl"],
    };
  },

  props: {
    film: Object,
    serie: Object,
  },

  methods: {
    stars(vote) {
      return Math.ceil(vote / 2);
    },
  },

  components: {
    // CountryFlag,
  },
};
</script>

<style lang="scss" scoped>
@import "~@fortawesome/fontawesome-free/css/all.min.css";
div {
  .card {
    width: 200px;
    border: 1px solid black;
    margin-right: 0.1rem;

    .flag-icon {
      width: 2.5rem;
    }

    .no-flag-icon {
      display: inline-block;
      width: 2.5rem;
      height: 2.5rem;
      border-radius: 50%;
      background-color: rgb(212, 56, 56);
      line-height: 2.5rem;
      text-align: center;
      font-size: 1.3rem;
      font-weight: bold;
    }
  }
}
</style>