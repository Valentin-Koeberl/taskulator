<template>
  <transition-group name="fade" tag="ul" class="todo-list fade">
    <li
        v-for="(todo, index) in todos"
        :key="todo.timestamp"
        class="todo-item"
    >
      <p class="todo-text">{{ todo.description }}</p>
      <span class="todo-time">{{ formatAge(todo.timestamp) }}</span>
      <button @click="$emit('remove-todo', index)">Complete</button>
    </li>
  </transition-group>

</template>

<script>
export default {
  name: 'TodoList',
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
  methods: {
    formatAge(timestamp) {
      const ageInMilliseconds = new Date() - new Date(timestamp);
      const minutes = Math.floor(ageInMilliseconds / 60000) % 60;
      const hours = Math.floor(ageInMilliseconds / 3600000) % 24;
      const days = Math.floor(ageInMilliseconds / 86400000);

      return `${days}d ${hours}h ${minutes}m ago`;
    },
  },
};
</script>

<style>
.todo-list {
  margin-top: 20px;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #616161;
}

.todo-text {
  flex: 1;
  white-space: normal;
  word-wrap: break-word;
  max-width: calc(20ch);
}

.todo-time {
  margin-left: 10px;
  font-size: 0.9rem;
  color: gray;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease, transform 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

.fade-enter-to,
.fade-leave-from {
  opacity: 1;
  transform: translateY(0);
}

</style>

