<template>
  <div
    class="background"
    v-if="as === 'background'" :style="{backgroundImage: `url('${path}')`}"
  />
  <img v-else :src="path" :alt="alt" />
</template>

<script>
export default {
  name: 'Img',
  props: {
    alt: {
      type: String,
      required: true,
    },
    as: {
      default: 'image',
      type: String,
      required: false,
    },
    src: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      path: '',
    };
  },
  mounted() {
    this.path = `${process.env.VUE_APP_API_PATH}${this.src}`;
  },
};
</script>

<style scoped>
  .background {
    background-attachment: fixed;
    background-position: top;
    background-size: contain;
    height: 53vh;
    max-height: 415px;
    width: 100%;
  }
</style>
