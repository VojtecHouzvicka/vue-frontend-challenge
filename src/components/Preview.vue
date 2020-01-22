<template>
  <div class="preview">
    <h2 v-if="city">Weather Forecast for {{ city.name }}, {{ city.country }}</h2>
  </div>
</template>

<script>
export default {
  name: 'Preview',
  props: {
    city: Object,
  },
};
</script>

<style scoped>
  .preview {
    flex-grow: 1;
    padding: 16px;
  }
  h2 {
    margin: 8px 0;
  }
</style>
