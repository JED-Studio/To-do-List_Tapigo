<template>
  <div id="app">
    <h1>Список задач</h1>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        <input type="checkbox" v-model="task.done" />
        {{ task.title }}
      </li>
    </ul>
  </div>
</template>

<script>
import { ref, onMounted, watch } from 'vue'
import tasksData from './tasks/tasks.json'

export default {
  setup() {
    const tasks = ref([])

    const loadTasks = () => {
      tasks.value = JSON.parse(localStorage.getItem('tasks')) || tasksData
    }

    onMounted(() => {
      loadTasks()
    })

    watch(
      tasks,
      (newTasks) => {
        localStorage.setItem('tasks', JSON.stringify(newTasks))
      },
      { deep: true },
    )

    return {
      tasks,
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

ul {
  list-style-type: none;
  padding: 0;
}
</style>
