<template>
  <header>
      header
      <BoolflixSearch />
  </header>
</template>

<script>
import BoolflixSearch from "./BoolflixSearch.vue"
export default {
    name: "BoolflixHeader",
    components: {
    BoolflixSearch,
  },
}
</script>

<style lang="scss" scoped>
    header {
        width: 100%;
        height: 100px;
        background-color: pink;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
</style>