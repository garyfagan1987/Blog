<template>
  <div class="home">
    <Alert v-if="error" />
    <div v-if="loaded">
      <Card :article="article" v-for="article in articles" :key="article.name" />
      <Center v-if="articles.length > 0">
        <Button
          :click="getMoreArticles"
          :disabled="articles.length === total"
          label="Load more"
        />
      </Center>
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

import Alert from '@/components/Alert.vue';
import Button from '@/components/Button.vue';
import Card from '@/components/Card.vue';
import Center from '@/components/Center.vue';
import Spinner from '@/components/Spinner.vue';

Vue.use(VueAxios, axios);

const START = 0;
const PER_PAGE = 2;

export default {
  name: 'Articles',
  components: {
    Alert,
    Button,
    Card,
    Center,
    Spinner,
  },
  data() {
    return {
      articles: [],
      end: PER_PAGE,
      error: false,
      loaded: false,
      start: START,
      total: null,
    };
  },
  methods: {
    getArticles() {
      this.axios
        .get(
          `${process.env.VUE_APP_API_ARTICLES_PATH}?_start=${this.start}&_limit=${this.end}`,
        )
        .then((response) => {
          this.loaded = true;
          this.articles = this.articles.concat(response.data);
        })
        .catch(() => {
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
    this.axios
      .get(`${process.env.VUE_APP_API_ARTICLES_PATH}/count`)
      .then((response) => {
        this.total = response.data;
      })
      .catch(() => {
        this.error = true;
      });
  },
};
</script>
