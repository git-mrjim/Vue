<script>
import { ref, onMounted } from 'vue';

  export default {
    setup() {
      const name = ref('John Doe');
      const status = ref(true)
      const tasks = ref(['Learn Vue', 'Learn React', 'Learn Angular']);
      const newTask = ref('');
      const url = 'https://google.com/';

      function toggleStatus() {
        status.value = !status.value;
      }

      function addTask() {
        if (newTask.value.trim() !== '') {
            tasks.value.push(newTask.value);
            newTask.value = '';
        }
      }

      function removeTask(index) {
        tasks.value.splice(index, 1);
      }

      onMounted(async () => {
          try {
              const response = await fetch('https://jsonplaceholder.typicode.com/todos');
              const data = await response.json();
              tasks.value = data.map(todo => todo.title);
          } catch (error) {
              console.error(error);
          }
      })

      return { name, status, tasks, newTask, url, toggleStatus, addTask, removeTask };
    }
  }
</script>

<template>
  <h1>Hello {{ name }}</h1>
  <p v-if="status">User is active</p>
  <p v-else="status">User is not active</p>

    <form @submit.prevent="addTask">
        <label for="addTask">Add new task</label>
        <input type="text" id="addTask" v-model="newTask">
        <button type="submit">Add</button> 
    </form>

  <h3>Tasks</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
        <span>{{ task }}</span>
        <button @click="removeTask(index)">X</button>
    </li>
  </ul>
  <a :href="url">Google</a>
  <button v-on:click="toggleStatus">Change Status</button>
</template>

<style>

</style>