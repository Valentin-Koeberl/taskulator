<template>
  <div class="todo-form">
    <textarea
        v-model="description"
        @keyup.enter="handleSubmit"
        ref="inputRef"
        placeholder="Enter a new TODO (max 50 characters)"
    ></textarea>
    <button @click="handleSubmit">Add Task</button>
    <p v-if="warningMessage" class="warning">{{ warningMessage }}</p>
  </div>
</template>

<script>
import { ref, watch, onMounted } from 'vue';

export default {
  name: 'TodoForm',
  emits: ['add-todo'],
  setup(_, { emit }) {
    const description = ref('');
    const warningMessage = ref('');
    const inputRef = ref(null);

    watch(description, (newValue) => {
      if (newValue.length > 50) {
        warningMessage.value = 'Character limit exceeded! Max 50 characters allowed.';
      } else {
        warningMessage.value = '';
      }
    });

    const handleSubmit = () => {
      if (description.value.trim() && description.value.length <= 50) {
        emit('add-todo', {
          description: description.value,
          timestamp: new Date().toISOString(),
          completed: false,
        });
        description.value = ''; // Eingabefeld leeren
      }
    };

    // Fokussiert das Textfeld, wenn die Komponente geladen wird
    onMounted(() => {
      inputRef.value.focus();
    });

    return {description, warningMessage, handleSubmit, inputRef};
  },
};
</script>

<style>
.todo-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

textarea {
  width: 100%;
  padding: 10px;
  font-size: 1rem;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.warning {
  color: red;
  font-size: 0.9rem;
}
</style>
