<template>
  <table>
    <tbody>
      <tr v-for="customer in data.data" :key="customer.id">
        <th>{{ customer.name }}</th>
        <th>{{ customer.email }}</th>
        <th>{{ customer.address }}</th>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  async asyncData({ app }) {
    const data = await app.$axios.$get("http://localhost:8000/api/customers")
    return { data }
  }
}
</script>

<style>

</style>