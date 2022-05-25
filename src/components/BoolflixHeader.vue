<template>
  <header>
    <div class="menu">
      <img src="../assets/boolflix.png" alt="" />
      <div class="links">
        <ul>
          <li>
            <a class="active" href=""> Home </a>
          </li>
          <li v-for="(link, i) in headerLinks" :key="i">
            <a href=""> {{ link.text }} </a>
          </li>
        </ul>
      </div>
    </div>
    <div class="search">
      <div
        class="search-input-container"
        v-if="this.isClicked"
      >
        <i @click="clicked()" class="fa-solid fa-magnifying-glass"></i>
        <input
          class="search__input"
          @keyup.enter="$emit('search', inputKey)"
          type="text"
          v-model="inputKey"
          placeholder="Cerca un titolo"
        />
      </div>
      <button
        v-if="this.isClicked === false"
        class="search__click"
        @click="
          $emit('search', inputKey);
          clicked();
        "
      >
        <i class="fa-solid fa-magnifying-glass"></i>
      </button>
    </div>
  </header>
</template>

<script>
export default {
  name: "BoolflixHeader",

  methods: {
    clicked: function () {
      this.isClicked = !this.isClicked;
    },
  },

  data: function () {
    return {
      isClicked: false,
      myFilms: [],
      inputKey: "",
      headerLinks: [
        {
          text: "SerieTV",
          url: "#",
        },
        {
          text: "Film",
          url: "#",
        },
        {
          text: "Nuovi e popolari",
          url: "#",
        },
        {
          text: "La mia lista",
          url: "#",
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
header {
  width: 100%;
  height: 100px;
  padding-left: 5rem;
  padding-right: 5rem;
  background: linear-gradient(
    0deg,
    rgba(0, 0, 0, 0) 0%,
    rgba(0, 0, 0, .87) 100%
  );
  display: flex;
  justify-content: space-between;
  align-items: center;

  .menu {
    width: 250px;
    height: 70px;
    line-height: 70px;
    text-align: center;
    display: flex;
    justify-content: space-between;
    align-items: center;

    .links {
      display: flex;

      ul {
        width: 700px;
        display: flex;
        line-height: 1.5rem;

        li {
          margin-right: 2rem;
          display: flex;
          color: white;

          .active {
            color: white;
          }
        }
      }
    }

    img {
      height: 55px;
      margin-right: 4rem;
    }
  }

  .search {
    &__click {
      padding: 1rem;
      font-size: 1.8rem;
      background-color: transparent;
      border: none;
      color: white;
      cursor: pointer;
    }

    .search-input-container {
      width: 400px;
      height: 50px;
      background-color: black;
      cursor: pointer;
      border: 1px solid white;
      display: flex;
      justify-content: space-between;
      align-items: center;

      i {
        color: white;
        font-size: 1.8rem;
        padding-left: 1.2rem;
        padding-right: 1rem;
      }

      input {
        height: 100%;
        width: 85%;
        background-color: black;
        border: none;
        color: white;
        font-size: 1.5rem;
        padding: 1.4rem;

        &:focus {
          outline: none;
          border: none;
        }
      }
    }
  }
}
</style>