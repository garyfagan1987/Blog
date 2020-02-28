<template>
  <div class="flex">
    <router-link :to="linkPath">
      <foo v-if="article.image.url" :src="article.image.url" :alt="article.name" />
    </router-link>
    <div>
      <h2>
        <router-link :to="linkPath">{{ article.name }}</router-link>
      </h2>
      <sub-heading :posted="article.date" :timeToRead="article.content" />
      <p>{{ article.excerpt }}</p>
      <router-link :to="linkPath">Read more</router-link>
    </div>
  </div>
</template>

<script>
import Foo from '@/components/Image.vue';
import SubHeading from '@/components/SubHeading.vue';

export default {
  name: 'Card',
  components: {
    Foo,
    SubHeading,
  },
  props: {
    article: {
      type: Object,
      required: true,
    },
  },
  computed: {
    linkPath() {
      return `/article/${this.article.name.replace(/\s+/g, '-')}`;
    },
  },
};
</script>

<style scoped>
.flex {
  background-color: var(--color-white);
  border: 1px solid var(--color-grey);
  display: flex;
  margin-bottom: 20px;
}

@media only screen and (max-width: 900px) {
  .flex {
    flex-direction: column;
  }
}

.flex > div {
  padding: 20px;
}

h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

img {
  height: 100%;
  object-fit: cover;
  width: 200px;
}

@media only screen and (max-width: 900px) {
  img {
    height: 100px;
    width: 100%;
  }
}
</style>
