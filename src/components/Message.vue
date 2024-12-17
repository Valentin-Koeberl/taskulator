<template>
  <div class="message">{{ message }}</div>
</template>

<script>
export default {
  name: 'Message',
  props: ['message'],
};
</script>

<style scoped>
.message {
  text-align: center;
  font-size: 1.2rem;
  color: #888;
}
</style>
