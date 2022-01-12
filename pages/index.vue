<template>
  <div class="home">
    <Hero />

    <!-- movie -->
    <div class="container movies">
      <div id="movie-grid" class="movie-grid">
        <div class="movie" v-for="(movie, index) in movies" :key="index">
          <div class="movie-img">
            <img :src="`https://image.tmdb.org/t/p/w300/${movie.poster_path}`" alt="映画ポスター">
          </div>
        </div>
      </div>
    </div>
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
      movies: []
    }
  },
  async fetch() {
    await this.getMovies()
  },
  methods: {
    async getMovies() {
      const data = axios.get(`https://api.themoviedb.org/3/movie/now_playing?api_key=4f0c49dbd551a0791e957317b1237dc1&language=en-US&page=1`)
      const result = await data
      result.data.results.forEach((movie) => {
        this.movies.push(movie)
      })
    }
  }
}
</script>

<style>

</style>