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
      <h1>{{ this.forecast.name }}</h1>
      <span class="temp">{{ this.forecast.main.temp }}°c</span>
    </div>
    <!-- <span>{{ time.date }}</span> -->
    <!-- <span>{{ time.time }}</span> -->
    <span> min: {{ this.forecast.main.temp_min }}°c</span>
    <span> max: {{ this.forecast.main.temp_max }}°c</span>
  </div>
</template>

<script>
// import axios from "axios";

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
      }
    };
  },
  //   created() {
  //     axios
  //       .get(
  //         `https://api.openweathermap.org/data/2.5/weather?q=paris,fr&appid=d83285f6c4a72b38447dd6961904b40e&units=metric`
  //       )
  //       .then(res => {
  //         this.this.forecast = res.data;
  //       });
  // axios
  //   .get("http://worldtimeapi.org/api/timezone/Europe/Paris")
  //   .then(res => (this.timeZone = res.data.datetime));
  //   },
  methods: {
    getDate() {
      let today = new Date();
      return (
        today.getDate() +
        " / " +
        (today.getMonth() + 1) +
        " / " +
        today.getFullYear()
      );
    },
    getTime() {
      let today = new Date();
      return today.getHours() + ":" + today.getMinutes();
    }
  }
};
</script>
