<template>
  <div id="app">
    <Navigation />
    <Preview city="Prague"/>
  </div>
</template>

<script>
import Navigation from './components/Navigation.vue';
import Preview from './components/Preview.vue';

export default {
  name: 'app',
  components: {
    Navigation,
    Preview,
  },
};
</script>

<style>
html, body {
  height: 100%;
  margin: 0;
  padding: 0;
}

#app {
  height: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  align-items: stretch;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
}
</style>
