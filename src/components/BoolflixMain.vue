<template>
  <main>
      <div class="container">
        <BoolflixCard v-for="(film, index) in filmsArray" :key="index" :film="filmsArray[index]" />
      </div>
  </main>
</template>

<script>
import BoolflixCard from "./BoolflixCard.vue";

export default {
    name: "BoolflixMain",

    props: {
        filmsArray: Array
    },

    components: {
        BoolflixCard,
    },
}
</script>

<style lang="scss" scoped>
    main {
        width: 100%;
        height: calc(100vh - 100px);
        background-color: darkseagreen;
        overflow: auto;
        padding-top: 3rem;

        .container {
            width: 80%;
            margin: 0 auto;
            display: flex;
            flex-wrap: wrap;
            align-items: flex-start;
            justify-content: space-between;
        }
    }
</style>