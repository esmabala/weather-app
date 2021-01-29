<template>
  <div class="searc-input">
    <b-form-input
      type="text"
      v-model.trim="city"
      @update="fetchWeather"
      debounce="500"
      placeholder="Search a place"
    ></b-form-input>
    <div class="spinner" v-if="loading">
      <b-spinner small></b-spinner>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "SearchInput",
  props: {},
  data() {
    return {
      city: "",
      loading: false,
      coordinate: null,
    };
  },
  methods: {
    fetchWeather() {
      this.loading = true;
      const key = "d61a4d226c5278bd3745169d74f83553";
      const parameters = {
        appid: key,
        units: "metric",
      };
      if (this.city) {
        parameters.q = this.city;
      } else {
        parameters.lon = this.coordinate.longitude;
        parameters.lat = this.coordinate.latitude;
      }

      axios
        .get("http://api.openweathermap.org/data/2.5/weather", {
          params: parameters,
        })
        .then(({ data }) => {
          console.log(data);
          this.$emit("fetch-weather", data);
        })
        .catch((error) => {
          console.log(error);
          this.$bvToast.toast(`Weather info is not found.`, {
            title: "Not Found",
            variant: "danger",
            autoHideDelay: 2000,
          });
        })
        .finally(() => {
          this.loading = false;
        });
    },
    fetchCurrentWeather() {},
    getLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition((position) => {
          this.coordinate = {
            latitude: position.coords.latitude,
            longitude: position.coords.longitude,
          };
          this.fetchWeather();
        });
      } else {
        this.$bvToast.toast(`Geolocation is not supported by this browser.`, {
          title: "Not Supported",
          variant: "danger",
          autoHideDelay: 2000,
        });
      }
    },
  },
  mounted() {
    this.getLocation();
  },
};
</script>

<style>
.searc-input {
  position: relative;
}
.spinner {
  position: absolute;
  top: 15%;
  right: 2%;
}
</style>