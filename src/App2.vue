<script>
  export default {
    data() {
      return {
        name: 'Jimwell Chen',
        status: true,
        tasks: ['Learn Vue', 'Learn React', 'Learn Angular'],
        url: 'https://google.com/'
      }
    },
    methods: {
      toggleStatus() {
        this.status = !this.status;
      }
    }
  }
</script>

<template>
  <h1>Hello {{ name }}</h1>
  <p v-if="status">User is active</p>
  <p v-else="status">User is not active</p>
  <h3>Tasks</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <a :href="url">Google</a>
  <button v-on:click="toggleStatus">Change Status</button>
</template>

<style>

</style>
