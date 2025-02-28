<script>
export default {
  data() {
    return {
      name: 'Vue Jobs',
      status: 'active', // active, pending, inactive
      tasks: ["Task 1", "Task 2", "Task 3"],
      link: 'https://cpage.co.tz',
      link2: 'https://google.com',
    }
  },

  methods: {
    toggleStatus() {
      if (this.status === 'active') {
        this.status = 'pending';
      } else if (this.status === 'pending') {
        this.status = 'inactive';
      } else {
        this.status = 'active';
      }
    }
  }
};
</script>

<template>
  <h1>{{ name }}</h1>

  <p v-if="status === 'active'">User is active!</p>
  <p v-else-if="status === 'pending'">User is pending!</p>
  <p v-else>User is inactive!</p>

  <h3>Tasks</h3>
  <ul>
    <li v-for="task in tasks" :key="task">
      {{ task }}
    </li>
  </ul>

  <a v-bind:href="link">Click for cPage</a>
  <a :href="link2">Click for Google</a>
  <br>
  <button v-on:click="toggleStatus">Change Status</button>
  <button @click="toggleStatus">Change Status 2</button>
</template>





<style scoped>
h1 {
  color: red;
}
</style>
