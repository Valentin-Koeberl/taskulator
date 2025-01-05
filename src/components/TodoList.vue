<template>
  <transition-group name="fade" tag="div" class="todo-list">
    <div v-for="(todo, index) in todos" :key="todo.timestamp" class="todo-item">
      <p class="todo-text">{{ todo.description }}</p>
      <span class="todo-time">{{ formatAge(todo.timestamp) }}</span>
      <button @click="$emit('remove-todo', index)">Complete</button>
    </div>
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
  white-space: normal; /* Ermöglicht Zeilenumbrüche */
  word-wrap: break-word; /* Bricht den Text, wenn er die Breite überschreitet */
  max-width: calc(20ch); /* 20 Zeichen (ch ist die Breite eines '0') */
}

.todo-time {
  margin-left: 10px;
  font-size: 0.9rem;
  color: gray;
}

/* CSS-Transition für Fade-In/Fade-Out */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease-in-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>

