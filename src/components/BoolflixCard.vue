<template>
  <section>
    <div class="card" v-if="film">
      <div class="card__poster" v-if="this.film.poster_path">
        <img
          :src="`https://image.tmdb.org/t/p/w342${this.film.poster_path}`"
          alt=""
        />
      </div>
      <div v-else class="card__poster no-img">
        <h2>{{ this.film.title.toUpperCase() }}</h2>
      </div>
      <div class="card__info">
        <div class="card__info__bottom">
          <h2>{{ this.film.title.toUpperCase() }}</h2>
          <h3>{{ this.film.original_title }}</h3>
          <div>
            <span v-for="n in 5" :key="n">
              <i
                :class="n <= voteStars(film.vote_average) ? 'fas' : 'far'"
                class="fa-star"
              ></i>
            </span>
          </div>
          <span v-if="this.languages.includes(this.film.original_language)">
            <img
              class="flag-icon"
              :src="
                require(`../assets/flags/${this.film.original_language}.png`)
              "
              alt=""
            />
          </span>
          <div class="no-flag-icon" v-else>
            {{ this.film.original_language.toUpperCase() }}
          </div>
          <p>{{ this.filmCast.cast }}</p>
        </div>
      </div>
    </div>

    <div class="card" v-if="serie">
      <div class="card__poster" v-if="this.serie.poster_path">
        <img
          :src="`https://image.tmdb.org/t/p/w342${this.serie.poster_path}`"
          alt=""
        />
      </div>
      <div v-else class="card__poster no-img">
        <h2>{{ this.serie.name.toUpperCase() }}</h2>
      </div>
      <div class="card__info">
        <div class="card__info__bottom">
          <h2>{{ this.serie.name.toUpperCase() }}</h2>
          <h3>{{ this.serie.original_name }}</h3>
          <div>
            <span v-for="n in 5" :key="n">
              <i
                :class="n <= voteStars(serie.vote_average) ? 'fas' : 'far'"
                class="fa-star"
              ></i>
            </span>
          </div>
          <span v-if="this.languages.includes(this.serie.original_language)">
            <img
              class="flag-icon"
              :src="
                require(`../assets/flags/${this.serie.original_language}.png`)
              "
              alt=""
            />
          </span>
          <div class="no-flag-icon" v-else>
            {{ this.serie.original_language.toUpperCase() }}
          </div>
        </div>
      </div>
    </div>

    <!-- <div class="card" v-if="serie">
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
            :src="
              require(`../assets/flags/${this.serie.original_language}.png`)
            "
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
    </div> -->
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
    filmCast: Array,
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
        font-size: 1.6rem;
      }

      h3 {
        font-size: 1.2rem;
        margin-bottom: 1rem;
      }

      span {
        font-size: 1.5rem;

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

    .no-img {
      text-align: center;
      padding-top: 1.1rem;
      font-size: 1.7rem;
    }

    &__info {
      width: 342px;
      height: 500px;
      display: none;
      position: relative;

      &__bottom {
        width: 100%;
        height: 45%;
        background-color: #1d1d1d;
        position: absolute;
        bottom: 0;
        left: 0;
        padding: 1.5rem 2rem;
        text-align: start;
        overflow: scroll;
      }
    }

    .flag-icon {
      width: 2rem;
      margin-top: 1rem;
    }

    .no-flag-icon {
      display: inline-block;
      width: 2rem;
      height: 2rem;
      border-radius: 50%;
      background-color: rgb(212, 56, 56);
      line-height: 2rem;
      text-align: center;
      font-size: 1.3rem;
      font-weight: bold;
      text-align: center;
      margin-top: 1rem;
    }
  }
}
</style>