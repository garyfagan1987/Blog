<template>
  <div class="breadcrumb">
    <router-link to="/">Home</router-link> / {{label}}
  </div>
</template>

<script>
export default {
  props: ['label'],
  name: 'Breadcrumb',
};
</script>

<style scoped>
  .breadcrumb {
    background-color: var(--color-grey-light);
    margin: 15px 0;
    padding: 10px;
  }
</style>
