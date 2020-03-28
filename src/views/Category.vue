<template>
  <div class="category">
    <Header />
    <Alert v-if="error" />
    <div v-if="loaded">
      <my-image v-if="category" as="background" :alt="category.name" :src="category.image.url" />
      <div class="container">
        <Breadcrumb :label="`Categories / ${category.name}`" />
        <h1>{{category.name}}</h1>
        <Card :article="article" v-for="article in articles" :key="article.name" />
        <Center v-if="articles.length > 0">
          <Button
            :click="fetchMoreArticles"
            :disabled="articles.length === total"
            label="Load more"
          />
        </Center>
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

import Alert from '@/components/Alert.vue';
import Breadcrumb from '@/components/Breadcrumb.vue';
import Button from '@/components/Button.vue';
import Card from '@/components/Card.vue';
import Center from '@/components/Center.vue';
import Header from '@/components/Header.vue';
import MyImage from '@/components/Image.vue';
import Spinner from '@/components/Spinner.vue';

Vue.use(VueAxios, axios);

const START = 0;
const PER_PAGE = 2;

export default {
  name: 'Category',
  components: {
    Alert,
    Breadcrumb,
    Button,
    Card,
    Center,
    Header,
    MyImage,
    Spinner,
  },
  data() {
    return {
      articles: [],
      category: {},
      end: PER_PAGE,
      error: false,
      loaded: false,
      start: START,
      total: null,
    };
  },
  methods: {
    fetchCategory(category) {
      const data = `{
        categories(where: { name: "${category}" }) {
          name
          image {
            url
          }
          articles(limit: ${this.end}, start: ${this.start}) {
            content
            date
            id
            name
            excerpt
            image {
              url
            }
          }
        }
      }`;
      axios.get(`${process.env.VUE_APP_GRAPHQL_API_PATH}${data}`).then((response) => {
        this.category = {
          name: response.data.data.categories[0].name,
          image: response.data.data.categories[0].image,
        };
        this.articles = this.articles.concat(response.data.data.categories[0].articles);
        this.loaded = true;
      }).catch(() => {
        this.error = true;
      });
    },
    fetchTotal(category) {
      const data = ` {
        categories(where: { name: "${category}" }) {
          articles {
            id
            name
          }
        }
      }`;
      axios.get(`${process.env.VUE_APP_GRAPHQL_API_PATH}${data}`).then((response) => {
        this.total = response.data.data.categories[0].articles.length;
      }).catch(() => {
        this.error = true;
      });
    },
    fetchMoreArticles() {
      this.start += PER_PAGE;
      this.end = this.start + PER_PAGE;
      this.fetchCategory(this.category.name);
    },
  },
  mounted() {
    const category = this.$route.params.pathMatch.replace(/-/g, ' ').replace(/\/$/, '');
    this.fetchCategory(category);
    this.fetchTotal(category);
  },
};
</script>
