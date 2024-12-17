<template>
  <div class="todo-item">
    <span>{{ todo.description }}</span>
    <span>({{ age }})</span>
    <button @click="completeTodo">Mark as Completed</button>
  </div>
</template>

<script>
import { computed } from 'vue';

export default {
  name: 'TodoItem',
  props: ['todo'],
  emits: ['complete'],
  setup(props, { emit }) {
    const age = computed(() => {
      const now = new Date();
      const ageInMs = now - new Date(props.todo.timestamp);
      const days = Math.floor(ageInMs / (1000 * 60 * 60 * 24));
      const hours = Math.floor((ageInMs % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
      const minutes = Math.floor((ageInMs % (1000 * 60 * 60)) / (1000 * 60));
      return `${days}d ${hours}h ${minutes}m`;
    });

    const completeTodo = () => {
      emit('complete', props.todo.id);
    };

    return { age, completeTodo };
  },
};
</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
button {
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 5px 10px;
  cursor: pointer;
}
button:hover {
  background-color: #0056b3;
}
</style>
