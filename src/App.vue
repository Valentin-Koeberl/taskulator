<template>
  <div class="app">
    <h1>Taskulator</h1>
    <TodoForm @add-todo="addTodo" />
    <TodoList :todos="todos" @toggle-todo="toggleTodo" @remove-todo="removeTodo" />
  </div>
</template>

<script>
import { ref, onMounted, watch } from 'vue';
import TodoForm from './components/TodoForm.vue';
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: { TodoForm, TodoList },
  mounted() {
    document.title = 'Tasktulator - Dein Todo Manager'; // Setzt den Titel, wenn die Komponente gemountet wird
  },
  setup() {
    // TODO-Liste als reaktive Referenz
    const todos = ref([]);

    // LocalStorage: TODOs laden
    onMounted(() => {
      const savedTodos = localStorage.getItem('todos');
      if (savedTodos) {
        todos.value = JSON.parse(savedTodos);
      }
    });

    // LocalStorage: TODOs speichern, wenn sie sich ändern
    watch(
        todos,
        (newTodos) => {
          localStorage.setItem('todos', JSON.stringify(newTodos));
        },
        {deep: true}
    );

    // TODO hinzufügen
    const addTodo = (todo) => {
      todos.value.push(todo);
    };

    // TODO-Status toggeln (optional für zukünftige Features)
    const toggleTodo = (index) => {
      todos.value[index].completed = !todos.value[index].completed;
    };

    // TODO entfernen
    const removeTodo = (index) => {
      todos.value.splice(index, 1);
    };

    return {todos, addTodo, toggleTodo, removeTodo};
  },
};
</script>

<style>
body {
  margin: 0;
  font-family: 'Arial', sans-serif;
  background: linear-gradient(135deg, #f3f4f6, rgba(0, 83, 248, 0.2));
  color: #221e1e;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 10px;
}

.container {
  width: 100%;
  max-width: 900px;
  background: #ffffff;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
}

h1 {
  text-align: center;
  font-size: 6rem;
  margin-bottom: 20px;
  color: #192331;
}

form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

textarea {
  width: 100%;
  padding: 10px;
  border: 1px solid #cbd5e0;
  border-radius: 8px;
  font-size: 1rem;
  resize: none;
  outline: none;
  transition: border 0.3s ease-in-out;
}

textarea:focus {
  border: 1px solid #4a90e2;
}

button {
  padding: 10px 15px;
  border: none;
  background: #4a90e2;
  color: #fff;
  font-size: 1rem;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
}

button:hover {
  background: #357ab8;
}

.todo-list {
  margin-top: 20px;
  list-style: none;
  padding: 0;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #e2e8f0;
  transition: background 0.3s ease;
}

.todo-item:hover {
  background: #f7fafc;
}

.todo-text {
  font-size: 1rem;
  flex: 1;
}

.todo-time {
  margin-left: 10px;
  font-size: 0.9rem;
  color: #718096;
}

.todo-item button {
  background: #31da18;
  color: #fff;
  padding: 5px 10px;
  font-size: 0.9rem;
  border-radius: 6px;
}

.todo-item button:hover {
  background: #23ac0e;
}

@media (max-width: 600px) {
  .container {
    padding: 15px;
  }
}

</style>
