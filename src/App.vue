<template>
  <div id="app">
    <Navigation
      :cities="cities"
      :selected-city-id="selectedCity ? selectedCity.id : null"
      @selectCity="selectCity"
    />
    <Preview :city="selectedCity"/>
  </div>
</template>

<script>
import Navigation from './components/Navigation.vue';
import Preview from './components/Preview.vue';
import cities from './assets/cities.json';

export default {
  name: 'app',
  components: {
    Navigation,
    Preview,
  },
  methods: {
    selectCity(cityId) {
      if (this.selectedCity && this.selectedCity.id === cityId) {
        return;
      }

      this.selectedCity = this.getCityById(cityId);
    },
    getCityById(cityId) {
      let city = null;
      let i = 0;

      for (i; i < this.cities.length; i += 1) {
        if (this.cities[i].id === cityId) {
          city = this.cities[i];
          break;
        }
      }

      return city;
    },
  },
  data() {
    return {
      selectedCity: null,
      cities,
    };
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
* {
  transition: background-color 400ms linear;
}
</style>
