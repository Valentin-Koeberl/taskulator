<template>
  <div id="app">
    <h1>Taskulator</h1>
    <br>
    <TodoForm @add-todo="addTodo" />
    <TodoList ref="list" />
  </div>
</template>

<script>
import TodoForm from './components/TodoForm.vue';
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: { TodoForm, TodoList },
  methods: {
    addTodo(todo) {
      this.$refs.list.addTodo(todo);
    },
  },
};
</script>

<style>
#app {
  max-width: 2000px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}
</style>
