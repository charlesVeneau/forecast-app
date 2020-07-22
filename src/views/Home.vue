<template>
  <div class="home">
    <div class="input-container">
      <input
        type="text"
        placeholder="Type a City"
        class="input"
        v-model="citySearchString"
        @change="getForecast"
      />
      <button class="searchButton" @click.prevent="getForecast">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="feather feather-search"
        >
          <circle cx="11" cy="11" r="7" />
          <line x1="21" y1="21" x2="16.65" y2="16.65" />
        </svg>
      </button>
    </div>
    <div class="cards">
      <Card v-if="forecast" :forecast="forecast" />
      <div v-else class="errorMsg">City not found!</div>
    </div>
  </div>
</template>

<script>
import Card from "@/components/Card.vue";
import axios from "axios";

export default {
  components: {
    Card
  },
  data() {
    return {
      citySearchString: "",
      forecast: null
    };
  },
  created() {
    axios
      .get(
        `https://api.openweathermap.org/data/2.5/weather?q=paris,fr&appid=${process.env.VUE_APP_OPENWEATHER}&units=metric`
      )
      .then(res => {
        this.forecast = res.data;
      });
  },
  methods: {
    getForecast() {
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.citySearchString}&appid=${process.env.VUE_APP_OPENWEATHER}&units=metric`
        )
        .then(res => {
          this.forecast = res.data;
        })
        .catch(e => console.log(e), (this.forecast = null));
    }
  }
};
</script>
