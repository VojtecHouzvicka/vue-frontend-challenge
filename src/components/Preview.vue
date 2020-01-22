<template>
  <div class="preview">
    <h2>Weather Forecast for {{ city }}</h2>
  </div>
</template>

<script>
export default {
  name: 'Preview',
  props: {
    city: String,
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
