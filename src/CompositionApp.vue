<script setup>
import { ref, onMounted } from 'vue'

const name = ref('John Doe')
const status = ref('active')
const tasks = ref(['task 1', 'task 2', 'task 3'])
const newTask = ref('')

const toggleStatus = () => {
  if (status.value === 'active') return (status.value = 'pending')
  if (status.value === 'pending') return (status.value = 'inactive')
  status.value = 'active'
}

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value)
    newTask.value = ''
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos')
    const data = await response.json()
    tasks.value = data.map((task) => task.title)
  } catch (err) {
    console.error('Error fetching tasks', err)
  }
})
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>

  <br />
  <button @click="toggleStatus">Change Status</button>
</template>
