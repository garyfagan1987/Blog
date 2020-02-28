<template>
    <img :src="path" :alt="alt" />
</template>

<script>
export default {
  name: 'Foo',
  props: ['alt', 'src'],
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
