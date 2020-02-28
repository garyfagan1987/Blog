<template>
  <button @click="click" :disabled="disabled">{{ label }}</button>
</template>

<script>
export default {
  props: ['click', 'disabled', 'label'],
  name: 'Button',
};
</script>

<style scoped>
button {
    background-color: var(--color-primary);
    border-radius: 30px;
    color: var(--color-white);
    cursor: pointer;
    font-family: inherit;
    font-weight: 600;
    font-size: inherit;
    min-width: 320px;
    outline: 0;
    padding: 20px;
}
button:hover {
    background-color: var(--color-primary-dark);
}
button:active {
    background-color: var(--color-primary-darker);
}
button:disabled {
  background-color: var(--color-grey);
  cursor: not-allowed;
}
</style>
