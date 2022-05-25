<template>
  <main>
    <div class="container">
      <h1>Movies</h1>
      <section>
        <BoolflixCard
          v-for="(film, i) in filmsFound"
          :key="i"
          :film="filmsFound[i]"
        />
      </section>

      <h1>Series</h1>
      <section>
        <BoolflixCard
          v-for="(series, i) in seriesFound"
          :key="i"
          :serie="seriesFound[i]"
        />
      </section>
    </div>
  </main>
</template>

<script>
import BoolflixCard from "./BoolflixCard.vue";

export default {
  name: "BoolflixMain",

  props: {
    filmsFound: Array,
    seriesFound: Array,
  },

  components: {
    BoolflixCard,
  },
};
</script>

<style lang="scss" scoped>
main {
  width: 100%;
  height: calc(100vh - 100px);
  background-color: black;
  overflow: auto;
  padding-top: 3rem;
  text-align: center;

  .container {
    width: 90%;
    margin: 0 auto;
    text-align: start;

    h1 {
      margin-bottom: 5rem;
      font-size: 3rem;
      font-weight: 100;
    }

    section {
      display: flex;
      flex-wrap: wrap;
      align-items: flex-start;
      justify-content: space-between;
    }
  }
}
</style>