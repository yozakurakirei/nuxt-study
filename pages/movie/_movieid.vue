<template>
  <Loading v-if="$fetchState.pending" />
  <div v-else>
    <h1>{{ this.movie.title }}</h1>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "single-movie",
  fetchDelay: 1000,
  data() {
    return {
      movie: "",
    }
  },
  async fetch() {
    await this.getSingleMovie()
  },
  methods: {
    async getSingleMovie() {
      const data = axios.get(`https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=4f0c49dbd551a0791e957317b1237dc1&language=en-US`)
      const result = await data
      this.movie = result.data
    }
  }
}
</script>

<style>

</style>