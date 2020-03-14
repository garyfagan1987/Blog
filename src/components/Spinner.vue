<template>
    <div class="spinner" />
</template>

<script>
export default {
  name: 'Spinner',
};
</script>

<style scoped>
.spinner {
  animation: spin 1s linear infinite;
  border: 5px solid var(--color-white);
  border-radius: 50%;
  border-top: 5px solid var(--color-primary-darker);
  height: 30px;
  margin: 0 auto;
  width: 30px;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>
