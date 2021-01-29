<template>
  <div v-if="weather">
    <b-img :src="icon"></b-img>
    <div>Location:{{ weather.name }}</div>
    <div>Temperature:{{ temperature }}</div>
    <div>Feels Like:{{ feelsLike }}</div>
  </div>
  <div v-else>No weather info.</div>
</template>

<script>
export default {
  name: "WeatherDashboard",
  props: {
    weather: {
      type: Object,
      default: null,
    },
  },
  computed: {
    temperature() {
      return this.weather?.main?.temp + "°C";
    },
    feelsLike() {
      return this.weather?.main?.feels_like + "°C";
    },
    icon() {
      return `http://openweathermap.org/img/wn/${this.weather?.weather[0]?.icon}@4x.png`;
    },
  },
};
</script>

<style>
</style>