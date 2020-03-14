<template>
    <div class="alert">
        <span>There was an error</span>
    </div>
</template>

<script>
export default {
  name: 'Alert',
  props: ['error'],
};
</script>

<style scoped>
.alert {
    align-items: center;
    background-color: var(--color-danger);
    color: var(--color-white);
    display: flex;
    justify-content: space-between;
    padding: 10px 20px;
    top: 20px;
    width: inherit;
}
</style>
