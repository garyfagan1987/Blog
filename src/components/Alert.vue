<template>
    <div class="alert" v-if="show">
        <span>There was an error</span>
        <button @click="handleDismiss">&times;</button>
    </div>
</template>

<script>
export default {
  name: 'Alert',
  props: ['error'],
  data() {
    return {
      show: null,
    };
  },
  methods: {
    handleDismiss() {
      this.show = false;
    },
  },
  watch: {
    error: function error(value) {
      this.show = value;
    },
  },
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
    position: fixed;
    top: 20px;
    width: inherit;
}
.alert button {
    background-color: transparent;
    border: 0;
    color: var(--color-white);
    cursor: pointer;
    font-size: 3rem;
}
</style>
