<template>
  <hero :content="content" :error="error" :loaded="loaded" />
</template>

<script>
import axios from 'axios';

import Hero from '@/components/Hero.vue';

export default {
  name: 'About',
  components: {
    Hero,
  },
  data() {
    return {
      content: {},
      error: false,
      loaded: false,
    };
  },
  created() {
    this.fetchContent();
  },
  methods: {
    fetchContent() {
      axios
        .get(process.env.VUE_APP_API_ABOUT_PATH)
        .then((response) => {
          this.content = response.data;
          this.loaded = true;
        })
        .catch(() => {
          this.error = true;
        });
    },
  },
};
</script>
