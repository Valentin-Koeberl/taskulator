<template>
  <div>
    <input v-model="description" placeholder="Enter TODO description">
    <button @click="createTodo">Add TODO</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const description = ref('');
const todos = ref([]);

const createTodo = () => {
  todos.value.push({ description: description.value, timestamp: new Date(), completed: false });
  description.value = '';
};
</script>

<style scoped>
div {
  font-family: Arial, sans-serif;
  margin: 10px;
}
input {
  padding: 5px;
}
button {
  padding: 5px 10px;
  background-color: #28a745;
  color: white;
  border: none;
  cursor: pointer;
}
button:hover {
  background-color: #218838;
}
</style>
