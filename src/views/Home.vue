<template>
  <div class="home">
    <About />
    <div class="container">
      <Articles />
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';

import About from '@/components/containers/About.vue';
import Articles from '@/components/containers/Articles.vue';

Vue.use(VueAxios, axios);

export default {
  name: 'Home',
  components: {
    About,
    Articles,
  },
};
</script>
