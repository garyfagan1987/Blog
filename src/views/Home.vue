<template>
  <div class="home">
    <alert :error="error" />
    <about />
    <div class="container">
      <Card
        :article="article"
        v-for="article in articles"
        :key="article.name"
      />
      <div v-if="articles.length > 0">
        <Button :click="getMoreArticles" :disabled="articles.length === total" label="Load more" />
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';

import About from '@/components/containers/About.vue';
import Alert from '@/components/Alert.vue';
import Button from '@/components/Button.vue';
import Card from '@/components/Card.vue';

Vue.use(VueAxios, axios);

const START = 0;
const PER_PAGE = 2;

export default {
  name: 'Home',
  components: {
    About,
    Alert,
    Button,
    Card,
  },
  data() {
    return {
      articles: [],
      end: PER_PAGE,
      error: false,
      start: START,
      total: null,
    };
  },
  methods: {
    // todo, this should be the article list components job
    getArticles() {
      this.axios.get(`${process.env.VUE_APP_API_ARTICLES_PATH}?_start=${this.start}&_limit=${this.end}`).then((response) => {
        this.articles = this.articles.concat(response.data);
      }).catch(() => {
        this.error = true;
      });
    },
    getMoreArticles() {
      this.start += PER_PAGE;
      this.end = this.start + PER_PAGE;
      this.getArticles();
    },
  },
  mounted() {
    this.getArticles();
    this.axios.get(`${process.env.VUE_APP_API_ARTICLES_PATH}/count`).then((response) => {
      this.total = response.data;
    }).catch(() => {
      this.error = true;
    });
  },
};
</script>
