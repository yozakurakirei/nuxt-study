<template>
  <v-app>
    <Header />

    <!-- main -->
    <v-main>
      <router-view />
    </v-main>

    <v-footer color="#00A85F" class="fotter" app>
      <Footer />
    </v-footer>
  </v-app>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
.fotter {
  color: #fff !important;
}
</style>