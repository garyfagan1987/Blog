<template>
  <small class="time">
      {{posted}} - {{timeToRead}}
  </small>
</template>

<script>
export default {
  props: ['posted', 'timeToRead'],
  name: 'SubHeading',
};
</script>

<style scoped>
.time {
  color: var(--color-grey-dark)
}
</style>
