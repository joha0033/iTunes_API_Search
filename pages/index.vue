<template>
  <section class="container">
    <h1>Search iTunes</h1>
    <br>
    <form @submit.prevent="submit">
      <input
      v-model="search"
      placeholder="Artist Name"
      autofocus/>
    </form>
  </section>
</template>

<script>


export default {
  components: {
    },
  data() {
    return{
      search: ''
    }
  },
  methods: {
    submit(event) {
      this.$router.push(`results/${this.search}`)
    }
  }
}
</script>

<style>
  *{
    text-align: center;
  }
  h1{
    padding: 5%;
  }
</style>
