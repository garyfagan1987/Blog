<template>
  <div class="about">
    <foo :alt="article.name" :src="article.image.url" />
    <div class="container">
      <breadcrumb :label="article.name" />
      <h1>{{article.name}}</h1>
      <sub-heading :timeToRead="article.content" :posted="article.date" />
      <markdown :source="article.content" />
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';
import Markdown from 'vue-markdown';

import Breadcrumb from '@/components/Breadcrumb.vue';
import Foo from '@/components/Image.vue';
import SubHeading from '@/components/SubHeading.vue';

Vue.use(VueAxios, axios);

Vue.use(Markdown);

export default {
  name: 'Article',
  components: {
    Breadcrumb,
    Foo,
    Markdown,
    SubHeading,
  },
  data() {
    return {
      article: {},
      timeToRead: '',
      posted: null,
    };
  },
  created() {
    this.fetchArticles();
  },
  methods: {
    fetchArticles() {
      axios.get(process.env.VUE_APP_API_ARTICLES_PATH).then((response) => {
        const name = this.$route.params.pathMatch.replace(/-/g, ' ');
        this.article = response.data.find((a) => a.name === name);
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

<style>
pre {
  background-color: var(--color-grey-light);
  overflow-y: scroll;
  padding: 20px;
}
</style>
