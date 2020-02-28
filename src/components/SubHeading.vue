<template>
  <small class="time">
      {{date}} - {{time}}
  </small>
</template>

<script>
import readingTime from 'reading-time';
import dayjs from 'dayjs';

export default {
  props: ['posted', 'timeToRead'],
  name: 'SubHeading',
  data() {
    return {
      time: readingTime(this.timeToRead).text,
      date: dayjs(this.posted).format('MMM DD, YYYY'),
    };
  },
};
</script>

<style scoped>
.time {
  color: var(--color-grey-dark)
}
</style>
