<template>
  <header>
      <div>
        logo
      </div>
      <div>
        <input @keyup.enter="$emit('search', inputKey)" type="text" v-model="inputKey">
        <button @click="$emit('search', inputKey)">Search</button>
      </div>
  </header>
</template>

<script>

export default {
  name: "BoolflixHeader",

  data: function() {
    return {
      myFilms: [],
      inputKey: "",
    }
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
    div {
        width: 250px;
        height: 70px;
        background-color: paleturquoise;
        line-height: 70px;
        text-align: center;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
</style>