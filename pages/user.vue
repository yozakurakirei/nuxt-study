<template>
  <table>
    <tbody>
      <tr v-for="user in data.users" :key="user.id">
        <th>{{ user.name }}</th>
        <th>{{ user.email }}</th>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  async asyncData ({ app }) {
    const data = await app.$axios.$get(`http://localhost:8000/api/users`)
    return { data }
  }
}
</script>

<style>

</style>