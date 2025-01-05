<template>
  <div class="todo-item">
    <slot name="description"></slot>
    <slot name="actions"></slot>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
};
</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 8px;
  margin-bottom: 10px;
  background-color: #fff;
  transition: all 0.3s ease;
}

.todo-item:hover {
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.1);
}
</style>
