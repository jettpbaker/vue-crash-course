<script>
export default {
  data() {
    return {
      name: 'John Doe',
      status: 'active',
      tasks: ['task 1', 'task 2', 'task 3'],
      link: 'https://google.com',
    }
  },
  methods: {
    toggleStatus() {
      if (this.status === 'active') return (this.status = 'pending')
      if (this.status === 'pending') return (this.status = 'inactive')
      this.status = 'active'
    },
  },
}
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <a :href="link">Click for Google</a>
  <br />
  <button @click="toggleStatus">Change Status</button>
</template>
