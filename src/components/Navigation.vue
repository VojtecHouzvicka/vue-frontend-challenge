<template>
  <div class="navigation">
    <h1>Cities Forecast</h1>
    <small>Pick a city from the list to see weather forecast.</small>

    <p v-if="cities.length < 1">
      No cities found
    </p>

    <div v-else class="items">
      <NavigationItem v-for="city in cities"
                      :key="city.id"
                      :city="city"
                      :selected="city.id === selectedCityId"
                      @selectCity="selectCity(city.id)"
      />
    </div>
  </div>
</template>

<script>
import NavigationItem from './NavigationItem.vue';

export default {
  components: {
    NavigationItem,
  },
  name: 'Navigation',
  props: {
    cities: Array,
    selectedCityId: Number,
  },
  methods: {
    selectCity(cityId) {
      this.$emit('selectCity', cityId);
    },
  },
};
</script>

<style scoped>
h1 {
  margin: 16px 16px 8px 16px;
}
small {
  margin: 0 16px;
}
.navigation {
  display: flex;
  flex-direction: column;
  border-right: 2px solid grey;
}
.items {
  display: flex;
  flex-direction: column;
  overflow-y: auto;
  margin-top: 8px;
}
</style>
