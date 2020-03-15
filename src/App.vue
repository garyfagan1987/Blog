<template>
  <div id="app">
    <router-view/>
    <Footer />
  </div>
</template>

<script>
import Footer from '@/components/Footer.vue';

export default {
  name: 'App',
  components: {
    Footer,
  },
  watch: {
    $route: function route() {
      if (this.$route.name.toLowerCase() === 'home') {
        document.title = 'Blog';
      } else {
        const name = this.$route.params.pathMatch.replace(/-/g, ' ');
        document.title = name;
      }
    },
  },
};
</script>

<style>
:root {
  --color: 153, 47%;
  --l: 49%;
  --color-danger: #D81C1C;
  --color-grey: #BBB;
  --color-grey-dark: #777;
  --color-grey-light: #EEE;
  --color-primary: hsl(var(--color), var(--l));
  --color-primary-dark: hsl(var(--color),calc(var(--l) - 5%));
  --color-primary-darker: hsl(var(--color),calc(var(--l) - 10%));
  --color-white: #FFF;
  font-size: 62.5%;
}

html, body {
  min-height: 100%;
}

body {
  margin: 0;
}

#app {
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-size: 1.6rem;
  height: -webkit-fill-available;
  justify-content: space-between;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
}

.container {
  margin: 0 auto;
  width: 900px;
}

@media only screen and (max-width: 900px) {
  .container {
    box-sizing: border-box;
    padding: 0 20px;
    width: 100%;
  }
}

a {
  color: #42b983;
  text-decoration: none;
}

h1, h2, h3, h4, h5, h6 {
  margin: 0;
}

pre {
  background-color: var(--color-grey-light);
  overflow-y: scroll;
  padding: 20px;
}
</style>
