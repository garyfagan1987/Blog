<template>
  <div class="center">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'Center',
};
</script>

<style scoped>
.center {
  display: flex;
  justify-content: center;
}
</style>
