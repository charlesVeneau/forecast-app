<template>
  <div class="card">
    <img
      class="logo"
      :src="
        'http://openweathermap.org/img/wn/' +
          this.forecast.weather[0].icon +
          '@2x.png'
      "
      alt="logo"
    />
    <div class="mainInfo">
      <h1>{{ this.forecast.name }}, {{ this.forecast.sys.country }}</h1>
      <span class="temp">{{ Math.round(this.forecast.main.temp) }}°c</span>
    </div>
    <p class="description">{{ time.date }} | {{ time.time }}</p>
    <p class="description">{{ this.forecast.weather[0].description }}</p>
    <!-- <span>{{ time.date }}</span> -->
    <!-- <span>{{ time.time }}</span> -->
    <p class="extraInfo">
      min: {{ Math.round(this.forecast.main.temp_min) }}°c max:
      {{ Math.round(this.forecast.main.temp_max) }}°c
      <button class="extendForecast" @click="this.toggleForecast">+</button>
    </p>
    <transition name="slideY-fade">
      <ul v-if="showHourly" class="hourlyData--list">
        <li
          v-for="(hour, index) in hourlyForecast"
          :key="index"
          class="hourlyData--item"
        >
          <img
            class="item--logo"
            :src="
              'http://openweathermap.org/img/wn/' +
                hour.weather[0].icon +
                '.png'
            "
            alt="logo"
          />
          <p class="item--data">{{ Math.round(hour.temp) }}°c</p>
          <p class="item--data">{{ new Date(hour.dt * 1000).getHours() }}h</p>
        </li>
      </ul>
    </transition>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: {
    forecast: Object
  },
  data() {
    return {
      //   this.forecast: null,
      //   timeZone: null,
      time: {
        date: this.getDate(),
        time: this.getTime()
      },
      hourlyForecast: [],
      isLoading: false,
      showHourly: false
    };
  },
  methods: {
    getDate() {
      let today = new Date();
      return (
        today.getDate() +
        "/" +
        (today.getMonth() + 1) +
        "/" +
        today.getFullYear()
      );
    },
    getTime() {
      let time = new Date(this.forecast.dt * 1000);
      return `${time.getHours()}h`;
    },
    toggleForecast() {
      this.showHourly = !this.showHourly;
    }
  },
  created() {
    axios
      .get(
        `https://api.openweathermap.org/data/2.5/onecall?lat=${this.forecast.coord.lat}&lon=${this.forecast.coord.lon}&,fr&appid=${process.env.VUE_APP_OPENWEATHER}&units=metric&lang=fr&exclude=current,minutely,daily`
      )
      .then(res => {
        let i = 1;
        while (i < 6) {
          this.hourlyForecast.push(res.data.hourly[i]);
          i++;
        }
      });
  }
};
</script>

<style>

</style>
