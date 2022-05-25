<template>
  <section>
    <div class="card" v-if="film">
      <div class="card__poster">
        <img
          :src="`https://image.tmdb.org/t/p/w342${this.film.poster_path}`"
          alt=""
        />
      </div>
      <div class="card__info">
        <h2>{{ this.film.title.toUpperCase() }}</h2>
        <h3>{{ this.film.original_title }}</h3>
        <span v-if="this.languages.includes(this.film.original_language)">
          <img
            class="flag-icon"
            :src="require(`../assets/flags/${this.film.original_language}.png`)"
            alt=""
          />
        </span>
        <div class="no-flag-icon" v-else>
          {{ this.film.original_language.toUpperCase() }}
        </div>
        <div>
          <span v-for="n in 5" :key="n">
            <i
              :class="n <= voteStars(film.vote_average) ? 'fas' : 'far'"
              class="fa-star"
            ></i>
          </span>
        </div>
      </div>
    </div>

    <div class="card" v-if="serie">
      <div class="card__poster">
        <img
          :src="`https://image.tmdb.org/t/p/w342${this.serie.poster_path}`"
          alt=""
        />
      </div>
      <div class="card__info">
        <h2>{{ this.serie.name.toUpperCase() }}</h2>
        <h3>{{ this.serie.original_name }}</h3>
        <span v-if="this.languages.includes(this.serie.original_language)">
          <img
            class="flag-icon"
            :src="require(`../assets/flags/${this.serie.original_language}.png`)"
            alt=""
          />
        </span>
        <div class="no-flag-icon" v-else>
          {{ this.serie.original_language.toUpperCase() }}
        </div>
        <div>
          <span v-for="n in 5" :key="n">
            <i
              :class="n <= voteStars(serie.vote_average) ? 'fas' : 'far'"
              class="fa-star"
            ></i>
          </span>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "BoolflixCard",

  data() {
    return {
      languages: ["ch", "en", "es", "fr", "gr", "it", "jp", "pl"],
    };
  },

  props: {
    film: Object,
    serie: Object,
  },

  methods: {
    voteStars(vote) {
      return Math.ceil(vote / 2);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "~@fortawesome/fontawesome-free/css/all.min.css";
div {
  .card {
    border: 1px solid black;
    display: flex;
    background-color: rgb(40, 40, 40);
    background-image: url(../assets/k-logo.png);
    background-repeat: no-repeat;
    background-size: 100%;
    background-position: center;
    position: relative;
    cursor: pointer;
    margin-bottom: 1rem;

    &:hover .card__info {
      display: inline-block;
      position: absolute;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;

      h2 {
        font-size: 2.5rem;
      }

      h3 {
        font-size: 1.7rem;
      }

      span {
        font-size: 2rem;

        i {
          color: rgb(255, 248, 149);
        }
      }
    }

    &__poster {
      width: 342px;
      height: 500px;
      overflow: hidden;

      img {
        object-fit: cover;
      }
    }

    &__info {
      width: 342px;
      height: 500px;
      display: none;
      background-color: rgba($color: #000000, $alpha: 0.7);
      text-align: center;
    }

    .flag-icon {
      width: 4rem;
      margin: 2rem;
    }

    .no-flag-icon {
      display: inline-block;
      width: 4rem;
      height: 4rem;
      border-radius: 50%;
      background-color: rgb(212, 56, 56);
      line-height: 4rem;
      text-align: center;
      font-size: 1.3rem;
      font-weight: bold;
      text-align: center;
      margin: 2rem;
    }
  }
}
</style>