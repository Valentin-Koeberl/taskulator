<template>
  <div>
    <div v-if="openTodos.length === 0">No open TODOs</div>
    <ul v-else>
      <li v-for="todo in openTodos" :key="todo.timestamp">
        <input type="checkbox" @change="markAsCompleted(todo)">
        {{ todo.description }} - {{ getTodoAge(todo) }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
    };
  },
  computed: {
    openTodos() {
      return this.todos.filter(todo => !todo.completed);
    },
  },
  methods: {
    getTodoAge(todo) {
      const now = new Date();
      const age = now - new Date(todo.timestamp);
      const days = Math.floor(age / (1000 * 60 * 60 * 24));
      const hours = Math.floor((age / (1000 * 60 * 60)) % 24);
      const minutes = Math.floor((age / (1000 * 60)) % 60);
      return `${days}d ${hours}h ${minutes}m`;
    },
    markAsCompleted(todo) {
      todo.completed = true;
    },
  },
  mounted() {
    setInterval(() => this.$forceUpdate(), 60000);
  },
};
</script>

<style scoped>
div {
  font-family: Arial, sans-serif;
  margin: 10px;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  margin: 5px 0;
  padding: 5px;
  background-color: #f8f9fa;
  border: 1px solid #dee2e6;
}
</style>
