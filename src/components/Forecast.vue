<template>
  <div v-if="this.forecast" class="forecast">
    <p>Next 3 days in {{ city.name }}:</p>
    <table>
      <tr>
        <th>Date</th>
        <th>Conditions</th>
        <th>Temperature</th>
      </tr>
      <tr v-for="dailyForecast in forecast" :key="dailyForecast.date">
        <td><b>{{ dailyForecast.date }}</b></td>
        <td>{{ dailyForecast.weather }}</td>
        <td>{{ dailyForecast.temperature }} °C</td>
      </tr>
    </table>
  </div>
  <div v-else>Loading ...</div>
</template>

<script>
export default {
  name: 'Forecast',
  props: {
    city: Object,
  },
  mounted() {
    this.getForecastByCityId(this.city.id);
  },
  beforeUpdate() {
    this.getForecastByCityId(this.city.id);
  },
  data() {
    return {
      forecast: null,
      loading: false,
      currentCityId: null,
    };
  },
  methods: {
    getForecastByCityId(cityId) {
      if (this.currentCityId === cityId) {
        return;
      }

      this.loading = true;
      this.forecast = null;
      this.currentCityId = cityId;
      const appId = 'dceb26ef7cc4fc3d84ac692b3d85adec';
      const url = 'http://api.openweathermap.org/data/2.5/forecast';

      const xhr = new XMLHttpRequest();
      xhr.open('GET', `${url}?id=${cityId}&appId=${appId}`);
      xhr.onload = () => {
        if (xhr.status === 200) {
          this.forecast = this.parseWeatherData(xhr.response);
        }
        this.loading = false;
      };

      xhr.send();
    },
    parseWeatherData(data) {
      const daysOfForecast = 3;
      const dataPointsPerDay = 8;

      const dataParsed = JSON.parse(data).list.reduce(
        (accumulator, currentValue, currentIndex) => {
          if (currentIndex === 0 || (currentIndex + 1) % dataPointsPerDay === 0) {
            accumulator.push({
              date: currentValue.dt_txt.substring(0, 10),
              temperature: currentValue.main.temp_kf,
              weather: currentValue.weather[0].description,
            });
          }

          return accumulator;
        }, [],
      );

      return dataParsed.slice(1, daysOfForecast + 1);
    },
  },
};
</script>

<style scoped>
th, td {
  padding: 8px;
}
</style>
