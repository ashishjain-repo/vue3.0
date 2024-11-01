<script setup>

import { ref } from 'vue';

const name = ref('John Doe');
const status = ref('Active');
const tasks = ref(['Task One', 'Task Two', 'Task Three']);
const link = ref("https://google.com");

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending';
  }
  else if (status.value === 'pending') {
    status.value = 'inactive'
  }
  else {
    status.value = 'active'
  };
};


</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is Active</p>
  <p v-else-if="status === 'pending'">User is Pending</p>
  <p v-else>User is In-Active</p>

  <h3>Tasks: </h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
    <a v-bind:href="link">Click Link</a>
    <a :href="link">Click Link</a>
  </ul>

  <button v-on:click="toggleStatus">Change Status</button>
  <button @click="toggleStatus">Change Status</button>
</template>