<template>
  <section>
    <h2>{{ this.film.title }}</h2>
    <h3>{{ this.film.original_title }}</h3>
    <country-flag :country="`${this.film.original_language}`"/>
    <p>{{ this.film.vote_average }}</p>
  </section>
</template>

<script>
import CountryFlag from 'vue-country-flag';

export default {
    name: "BoolflixCard",
    props: {
      film: Object
    },
    components: {
      CountryFlag
    }
}
</script>

<style lang="scss" scoped>
@import '~@fortawesome/fontawesome-free/css/all.min.css';
    section {
        width: 200px;
        height: 350px;
        background-color: plum;
        margin: 1rem;
    }
</style>