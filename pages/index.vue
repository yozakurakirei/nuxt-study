<template>
  <div class="home">
    <Hero />

    <!-- search -->
    <div class="container-search">
      <v-text-field 
        @keyup.enter="$fetch"
        outlined label="映画を検索する" 
        prepend-inner-icon="mdi-map-marker" 
        v-model.lazy="searchInput"
        class="search-input"></v-text-field>
      <v-btn @click="clearSearch" v-show="searchInput != ''" elevation="2" class="search-button">クリア</v-btn>
    </div>

    <!-- loading -->
    <Loading v-if="$fetchState.pending" />

    <!-- movie -->
    <v-container v-else class="movie-area">
      <v-row v-if="searchInput !== ''" id="movie-grid" class="movie-grid">
        <v-col class="movie" v-for="(movie, index) in searchedMovies" :key="index" cols="4">
          <NuxtLink class="button button-light" :to="{ name: 'movie-movieid', params: { movieid: movie.id } }">
          <div class="movie-img">
            <img :src="`https://image.tmdb.org/t/p/w300/${movie.poster_path}`" alt="映画ポスター">
            <p class="review">{{ movie.vote_average }}</p>
            <p class="overview">{{ movie.overview.slice(0, 100) }}
              <span v-if="movie.overview.length > 80">...</span>
            </p>
          </div>
          </NuxtLink>
          <div class="info">
            <p class="title">{{ movie.title.slice(0, 25) }}
              <span v-if="movie.title.length > 25">...</span>
            </p>
            <p class="release">リリース日:
              {{ new Date(movie.release_date).toLocaleString("ja-JP", {
                  month: "long",
                  day: "numeric",
                  year: "numeric",
                })
              }}
            </p>
          </div>
        </v-col>
      </v-row>

      <v-row v-else id="movie-grid" class="movie-grid">
        <v-col class="movie" v-for="(movie, index) in movies" :key="index" cols="4">
          <NuxtLink class="button button-light" :to="{ name: 'movie-movieid', params: { movieid: movie.id } }">
          <div class="movie-img">
            <img :src="`https://image.tmdb.org/t/p/w300/${movie.poster_path}`" alt="映画ポスター">
            <p class="review">{{ movie.vote_average }}</p>
            <p class="overview">{{ movie.overview.slice(0, 100) }}
              <span v-if="movie.overview.length > 80">...</span>
            </p>
          </div>
          </NuxtLink>
          <div class="info">
            <p class="title">{{ movie.title.slice(0, 25) }}
              <span v-if="movie.title.length > 25">...</span>
            </p>
            <p class="release">リリース日:
              {{ new Date(movie.release_date).toLocaleString("ja-JP", {
                  month: "long",
                  day: "numeric",
                  year: "numeric",
                })
              }}
            </p>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import Hero from "../components/Hero.vue"
import axios from "axios"

export default {
  name: "home",
  components: {
    Hero,
  },
  data() {
    return {
      movies: [],
      searchedMovies: [],
      searchInput: "",
    }
  },
  async fetch() {
    if(this.searchInput === "") {
      await this.getMovies()
      return
    }
    await this.searchMovies();
  },
  fetchDelay: 1000,
  methods: {
    async getMovies() {
      const data = axios.get(`https://api.themoviedb.org/3/movie/now_playing?api_key=4f0c49dbd551a0791e957317b1237dc1&language=en-US&page=1`)
      const result = await data
      result.data.results.forEach((movie) => {
        this.movies.push(movie)
      })
    },

    async searchMovies() {
      const data = axios.get(`https://api.themoviedb.org/3/search/movie?api_key=4f0c49dbd551a0791e957317b1237dc1&language=en-US&page=1&include_adult=false&query=${this.searchInput}`)
      const result = await data
      result.data.results.forEach((movie) => {
        this.searchedMovies.push(movie)
      })
      console.log(this.searchedMovies)
    },

    clearSearch() {
      this.searchInput = "",
      this.searchedMovies = []
    }
  }} 
</script>

<style lang="scss">
.home {
  .loading {
    padding-top: 120px;
    align-items: flex-start;
  }
}

.container-search {
  display: flex !important;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  .search-input {
    width: 80% !important;
  }
  .search-button {
    width: 100px !important;
  }
}

.movie-area {
  .movie {
    margin: 0 .5rem;
  }
}
</style>