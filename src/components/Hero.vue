<template>
  <div class="hero">
    <div class="container">
      <alert v-if="error" />
      <div v-if="loaded">
        <div class="flex">
          <div>
            <my-image v-if="content.image.url" :src="content.image.url" :alt="content.title" />
          </div>
          <div>
            <h1>{{ content.title }}</h1>
            <p>{{ content.description }}</p>
          </div>
        </div>
      </div>
      <div v-else-if="!loaded && !error">
        <spinner />
      </div>
    </div>
  </div>
</template>

<script>
import Alert from '@/components/Alert.vue';
import MyImage from '@/components/Image.vue';
import Spinner from '@/components/Spinner.vue';

export default {
  name: 'Hero',
  props: ['content', 'loaded', 'error'],
  components: {
    Alert,
    MyImage,
    Spinner,
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
  height: 100%;
  object-fit: cover;
  width: 200px;
}

@media only screen and (max-width: 900px) {
  .flex > div:first-child {
    display: none;
  }
}
</style>
