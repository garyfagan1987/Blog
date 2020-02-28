<template>
  <div class="home">
    <div class="hero">
      <div class="container">
        <div class="flex">
          <div>
            <img src="https://miro.medium.com/fit/c/150/150/2*2BjeiNs9eMzOBJSHQOE63w.png" />
          </div>
          <div>
            <h1>My blog, my thoughts, my ideas</h1>
            <p>Hi, I’m Gary, an enthusiastic front end web developer with over eight
              years of professional experience looking to work on challenging and
              exciting projects. Highly skilled in front end technologies with a strong
              focus on building clean user interfaces with great user experience.
              Passionate about shipping dry, bug-free clean code with the assistance
              of test-driven and behaviour driven development.</p>
          </div>
        </div>
      </div>
    </div>
    <div class="container">
      <Card
        :article="article"
        v-for="article in articles"
        :key="article.name"
      />
      <div>
        <Button :click="getMoreArticles" :disabled="articles.length === total" label="Load more" />
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';

import Button from '@/components/Button.vue';
import Card from '@/components/Card.vue';

Vue.use(VueAxios, axios);

const PER_PAGE = 5;

export default {
  name: 'Home',
  components: {
    Button,
    Card,
  },
  data() {
    return {
      articles: [],
      limit: PER_PAGE,
      total: null,
    };
  },
  methods: {
    getArticles(limit) {
      this.axios.get(`${process.env.VUE_APP_API_ARTICLES_PATH}?_start=0&_limit=${limit}`).then((response) => {
        this.articles = response.data;
      });
    },
    getMoreArticles() {
      this.limit += PER_PAGE;
      this.getArticles(this.limit);
    },
  },
  mounted() {
    this.getArticles(this.limit);
    this.axios.get(`${process.env.VUE_APP_API_ARTICLES_PATH}/count`).then((response) => {
      this.total = response.data;
    });
  },
};
</script>

<style scoped>
.hero {
  background-color: var(--color-primary);
  color: var(--color-white);
  border: 0;
  margin-bottom: 20px;
  padding: 30px 0;
}

.flex {
  display: flex;
}

.flex > div {
  padding: 20px;
}

img {
  border-radius: 50%;
}

@media only screen and (max-width: 900px) {
  .flex > div:first-child {
    display:none;
  }
}
</style>
