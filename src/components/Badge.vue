<template>
  <router-link class="badge" :to="`/category/${label}/`">{{ label }}</router-link>
</template>

<script>
export default {
  name: 'Badge',
  props: ['label'],
};
</script>

<style scoped>
.badge {
  background-color: var(--color-grey-light);
  border-radius: 5px;
  color: inherit;
  font-size: inherit;
  padding: 5px 10px;
}
</style>
