<template>
  <div class="todo-list">
    <div v-if="todos.length === 0">
      <Message message="No open TODOs available." />
    </div>
    <ul>
      <li v-for="todo in openTodos" :key="todo.id">
        <TodoItem :todo="todo" @complete="completeTodo" />
      </li>
    </ul>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';
import Message from './Message.vue';

export default {
  name: 'TodoList',
  components: { TodoItem, Message },
  data() {
    return {
      todos: [],
    };
  },
  computed: {
    openTodos() {
      return this.todos.filter((todo) => !todo.completed);
    },
  },
  methods: {
    completeTodo(id) {
      const todo = this.todos.find((t) => t.id === id);
      if (todo) todo.completed = true;
    },
    addTodo(newTodo) {
      newTodo.id = Date.now();
      this.todos.push(newTodo);
    },
  },
};
</script>

<style scoped>
.todo-list ul {
  list-style-type: none;
  padding: 0;
}

.todo-list li {
  margin-bottom: 10px;
}
</style>
