<template>
  <div class="about">
    <Header />
    <Alert v-if="error" />
    <div v-if="loaded">
      <my-image v-if="article" as="background" :alt="article.name" :src="article.image.url" />
      <div class="container">
        <Breadcrumb :label="article.name" />
        <h1>{{article.name}}</h1>
        <sub-heading :timeToRead="article.content" :posted="article.date" />
        <markdown :source="article.content" />
        <Badge
          v-for="category in article.categories"
          :key="category"
          :label="category.name" />
      </div>
    </div>
    <div v-else-if="!loaded && !error">
      <Spinner />
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';
import Markdown from 'vue-markdown';

import Alert from '@/components/Alert.vue';
import Badge from '@/components/Badge.vue';
import Breadcrumb from '@/components/Breadcrumb.vue';
import Header from '@/components/Header.vue';
import MyImage from '@/components/Image.vue';
import Spinner from '@/components/Spinner.vue';
import SubHeading from '@/components/SubHeading.vue';

Vue.use(VueAxios, axios);

Vue.use(Markdown);

export default {
  name: 'Article',
  components: {
    Alert,
    Badge,
    Breadcrumb,
    Header,
    MyImage,
    Markdown,
    Spinner,
    SubHeading,
  },
  data() {
    return {
      article: {},
      error: false,
      loaded: false,
      timeToRead: '',
      posted: null,
    };
  },
  created() {
    this.fetchArticles();
  },
  methods: {
    fetchArticles() {
      const name = this.$route.params.pathMatch.replace(/-/g, ' ');
      axios.get(`${process.env.VUE_APP_API_ARTICLES_PATH}?name=${name}`).then((response) => {
        // eslint-disable-next-line prefer-destructuring
        this.article = response.data[0];
        this.loaded = true;
      }).catch(() => {
        this.error = true;
      });
    },
  },
};
</script>

<style scoped>
img {
  width: 100%;
  height: 400px;
  object-fit: cover;
}
</style>
