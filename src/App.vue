<template>
  <div id="app">
    <BoolflixHeader />
    <BoolflixMain />
  </div>
</template>

<script>
import BoolflixHeader from "./components/BoolflixHeader.vue";
import BoolflixMain from "./components/BoolflixMain.vue";

export default {
  name: "App",
  components: {
    BoolflixHeader,
    BoolflixMain,
  },
};
</script>

<style lang="scss">
#app {
  width: 100%;
  height: calc(100vh);
}
</style>
