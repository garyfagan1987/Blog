<template>
    <div class="header">
        <div class="container">
            <h1>
                <router-link to="/">Gary Fagan</router-link>
            </h1>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Header',
};
</script>

<style scoped>
.header {
  background-color: var(--color-primary);
  padding: 10px 0;
}

.header a {
  color: var(--color-white);
}
</style>
