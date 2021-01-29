<template>
  <div id="app">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-lg-6 col-md-8 col-sm-12">
          <h1>Weather App</h1>
          <SearchInput @fetch-weather="handleFetchWeather"></SearchInput>
          <WeatherDashboard :weather="weather"></WeatherDashboard>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SearchInput from "./components/SearchInput";
import WeatherDashboard from "./components/WeatherDashboard";

export default {
  name: "App",
  components: { SearchInput, WeatherDashboard },
  data() {
    return {
      weather: null,
    };
  },
  methods: {
    handleFetchWeather(weather) {
      this.weather = weather;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
