<template>
  <div class="todo-form">
    <input v-model="description" type="text" placeholder="Enter a new task" @keyup.enter="addTodo" />
    <button @click="addTodo">Add Task</button>
  </div>
</template>

<script>
import { ref, emit } from 'vue';

export default {
  name: 'TodoForm',
  setup(_, { emit }) {
    const description = ref('');

    const addTodo = () => {
      if (description.value.trim()) {
        emit('add-todo', {
          description: description.value,
          timestamp: new Date(),
          completed: false,
        });
        description.value = '';
      }
    };

    return { description, addTodo };
  },
};
</script>

<style scoped>
.todo-form {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
  width: 100%;
  max-width: 1020px;
  margin-left: auto;
  margin-right: auto;
}

input {
  flex: 1;
  padding: 12px 15px;
  border: 1px solid #ccc;
  border-radius: 25px;
  font-size: 16px;
  outline: none;
}

input:focus {
  border-color: #28a745;
  box-shadow: 0 0 5px rgba(40, 167, 69, 0.5);
}

button {
  padding: 12px 20px;
  background-color: #28a745;
  color: #fff;
  border: none;
  border-radius: 25px;
  cursor: pointer;
  font-size: 16px;
  white-space: nowrap;
}

button:hover {
  background-color: #218838;
}

@media (max-width: 1020px) {
  .todo-form {
    max-width: 90%;
  }
}

@media (max-width: 600px) {
  .todo-form {
    flex-direction: column;
    gap: 15px;
  }

  input, button {
    width: 90%;
  }
}
</style>
