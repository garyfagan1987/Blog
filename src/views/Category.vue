<template>
  <div class="category">
    <Alert v-if="error" />
    <div v-if="loaded">
      <div class="container">
        <Breadcrumb :label="category.name" />
        <h1>{{category.name}}</h1>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';

import Alert from '@/components/Alert.vue';
import Breadcrumb from '@/components/Breadcrumb.vue';

Vue.use(VueAxios, axios);

export default {
  name: 'Category',
  components: {
    Alert,
    Breadcrumb,
  },
  data() {
    return {
      category: {},
      error: false,
      loaded: false,
    };
  },
  created() {
    this.fetchCategory();
  },
  methods: {
    fetchCategory() {
      const category = this.$route.params.pathMatch.replace(/-/g, ' ');
      axios.get(`${process.env.VUE_APP_API_PATH}/categories?name=${category}`).then((response) => {
        // eslint-disable-next-line prefer-destructuring
        this.category = response.data[0];
        this.loaded = true;
      }).catch(() => {
        this.error = true;
      });
    },
  },
};
</script>
